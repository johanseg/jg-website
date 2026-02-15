# Deploy Astro to Hostinger KVM2 (Auto Deploy with GitHub Actions)

This project is a static Astro site. The recommended flow is:

1. Build on GitHub Actions.
2. Upload `dist/` to your VPS with SSH + `rsync`.
3. Serve files with Nginx.

This avoids opening a public webhook port and avoids polling with cron.

## 1) Prepare the VPS

```bash
ssh root@YOUR_VPS_IP
apt update
apt install -y nginx rsync certbot python3-certbot-nginx
```

Create a deploy directory:

```bash
mkdir -p /var/www/johangarcia
chown -R www-data:www-data /var/www/johangarcia
```

## 2) Configure Nginx

Create `/etc/nginx/sites-available/johangarcia`:

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;

    root /var/www/johangarcia;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

Enable it:

```bash
ln -s /etc/nginx/sites-available/johangarcia /etc/nginx/sites-enabled/johangarcia
nginx -t
systemctl reload nginx
```

## 3) Add SSL

```bash
certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

## 4) Create an SSH key for GitHub Actions

On your local machine:

```bash
ssh-keygen -t ed25519 -C "github-actions-deploy" -f ~/.ssh/hostinger_actions
```

Add the public key to VPS:

```bash
ssh-copy-id -i ~/.ssh/hostinger_actions.pub root@YOUR_VPS_IP
```

Copy the private key content:

```bash
cat ~/.ssh/hostinger_actions
```

## 5) Configure GitHub Secrets

In your GitHub repo: **Settings -> Secrets and variables -> Actions -> New repository secret**

- `VPS_HOST`: your VPS IP or DNS
- `VPS_USER`: SSH user (for example `root`)
- `VPS_PORT`: SSH port (optional, defaults to `22`)
- `VPS_SSH_KEY`: private key from `~/.ssh/hostinger_actions`
- `DEPLOY_PATH`: `/var/www/johangarcia`
- `RELOAD_COMMAND`: optional, for example `systemctl reload nginx`

## 6) Deploy

The workflow in `.github/workflows/deploy-hostinger.yml` runs on:

- push to `main`
- manual trigger (`workflow_dispatch`)

After deploy, Nginx serves the updated static files from `/var/www/johangarcia`.

## Notes

- If you use a non-root deploy user, ensure it can write to `DEPLOY_PATH`.
- Keep `VPS_SSH_KEY` in GitHub Secrets only.
- For static Astro sites, no Node process manager (`pm2`) is needed in production.
