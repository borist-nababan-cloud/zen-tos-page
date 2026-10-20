# Deploying zen-tos-page to Coolify

This guide explains how to deploy `zen-tos-page` to your Coolify instance under the domain **`https://tos.zenfamilyspa.id`**.

---

## 1. Prerequisites (DNS Record)
Before or right after creating the application in Coolify, ensure your DNS provider (e.g., Cloudflare, DigitalOcean DNS) points the subdomain to your Coolify VPS IP:
* **Type**: `A`
* **Name**: `tos` (or `tos.zenfamilyspa.id`)
* **Target / IP**: Your Coolify VPS IP Address
* **Proxy status**: DNS only or Proxied (if using Cloudflare, standard DNS only / gray cloud is recommended for initial SSL cert generation).

---

## 2. Coolify Application Setup

1. **Log in** to your Coolify dashboard.
2. Navigate to your **Project** and select your environment (e.g., `Production`).
3. Click **"+ New"** $\to$ **"Application"**.
4. Select **"Public Repository"** (or connect via GitHub App):
   * **Repository URL**: `https://github.com/borist-nababan-cloud/zen-tos-page.git`
   * **Branch**: `main`
   * Click **Check Repository**.

---

## 3. Configuration in Coolify

Coolify will inspect the repository and see the `Dockerfile` and `nginx.conf`:

* **Build Pack**: Ensure it is set to **`Dockerfile`**.
* **Base Directory**: `/` (default root).
* **Ports Exposes**: `80` (Matches the Nginx port exposed in the Dockerfile).
* **Domains**: 
  ```text
  https://tos.zenfamilyspa.id
  ```
  *(Coolify & Traefik will automatically generate a free Let's Encrypt SSL/TLS certificate).*
* **Health Check Path**: `/healthz` (Pre-configured in `nginx.conf`).
* **Environment Variables**: **None needed** (The site is 100% lightweight static HTML/CSS/JS served directly through Nginx).

---

## 4. Deploy

1. Click **Deploy** at the top right.
2. Watch the deployment log. Since it uses pre-compiled static files with `nginx:alpine`, build time is typically under **10 seconds**.
3. Once the status turns to **"Running (Healthy)"**, test the deployment:
   * **Main Legal Hub**: `https://tos.zenfamilyspa.id`
   * **Direct Privacy Policy**: `https://tos.zenfamilyspa.id/privacy-policy.html` (or `/privacy-policy`)
   * **Direct Terms of Service**: `https://tos.zenfamilyspa.id/terms-of-service.html` (or `/terms-of-service`)
   * **Healthcheck**: `https://tos.zenfamilyspa.id/healthz`
