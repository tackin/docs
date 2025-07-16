---
sidebar_position: 1
id: docker-compose-base
title: Docker Compose
description: '🌟 Full-blown featureset including web office.'
---

# OpenCloud with Docker Compose

Install a internet facing OpenCloud with SSL certification with Docker Compose.

This installation documentation is for **Ubuntu and Debian** systems. The software can also be installed on other Linux distributions, but the commands and package managers may differ.

## **Prerequisites**

- **Four domains** pointing to your server:
  - `cloud.YOUR.DOMAIN` → OpenCloud frontend
  - `collabora.YOUR.DOMAIN` → Collabora Online Server
  - `wopiserver.YOUR.DOMAIN` → WOPI server for document editing
  - `traefik.YOUR.DOMAIN` → Traefik dashboard

  Alternatively, you can use a wildcard domain (`*.YOUR.DOMAIN`)

- A **hosted server** (e.g., Hetzner, AWS, or your own VPS) with Linux and SSH access

---

## 1. Connect to Your Server

Log into your server via SSH:

```bash
ssh root@YOUR.SERVER.IP
```

## 2. Install Docker

Update your system and install Docker.

First, perform an update and upgrade:

```bash
apt update && apt upgrade -y
```

Install Docker following the [official Docker guide](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

Once Docker is installed, enable and start the service:

```bash
systemctl enable docker && systemctl start docker
```

## 3. Clone the OpenCloud Repository

Download the necessary configuration files:

```bash
git clone https://github.com/opencloud-eu/opencloud-compose.git
```

## 4. Configure the .env File for Staging Certificates

Before requesting real SSL certificates, test the setup with Let's Encrypt’s staging environment.

Navigate to the OpenCloud configuration folder:

```bash
cd opencloud-compose
```

Create environment file:

```bash
cp .env.example .env
```

> **Note:** The repository includes .env.example as a template with default settings and documentation. Your actual .env file is excluded from version control (via .gitignore) to prevent accidentally committing sensitive information like passwords and domain-specific settings.
> <br/>

Edit the `.env` file with the editor of your choice:

In our example we use nano

```bash
nano .env
```

Modify these settings:

### ✅ Disable insecure mode

```bash
# INSECURE=true
```

### ✅ Set your domain names

```bash
TRAEFIK_DOMAIN=traefik.YOUR.DOMAIN
OC_DOMAIN=cloud.YOUR.DOMAIN
COLLABORA_DOMAIN=collabora.YOUR.DOMAIN
WOPISERVER_DOMAIN=wopiserver.YOUR.DOMAIN
```

### ✅ Set your admin password

```bash
ADMIN_PASSWORD=YourSecurePassword
```

### ✅ Set your email for SSL certification

```bash
TRAEFIK_ACME_MAIL=your@email.com
```

### ✅ Use Let's Encrypt staging certificates (for testing)

```bash
TRAEFIK_ACME_CASERVER=https://acme-staging-v02.api.letsencrypt.org/directory
```

### ✅ Set your deployment options

For Example without Collabora:

```bash
COMPOSE_FILE=docker-compose.yml:traefik/opencloud.yml
```

Save and exit.

### 🚨 Production Setup Consideration

:::caution Production Setup Recommended

By default, OpenCloud stores configuration and data inside internal Docker volumes.  
This works fine for local development or quick evaluations — **but is not suitable for production environments**.

:::

#### 📦 Mount Persistent Volumes

In production, you should mount persistent local directories for configuration and data to ensure:

- Data durability
- Easier backups and recovery
- Full control over storage location and permissions

Update your `.env` file with custom paths:

```env
OC_CONFIG_DIR=/your/local/path/opencloud/config
OC_DATA_DIR=/your/local/path/opencloud/data
```

:::tip Folder Permissions

Ensure these folders exist and are owned by user and group 1000:1000, which the Docker containers use by default:

```bash
sudo mkdir -p /your/local/path/opencloud/{config,data}
sudo chown -R 1000:1000 /your/local/path/opencloud
```

:::

If these variables are left unset, Docker will use internal volumes, which **do not persist** if the containers are removed — not recommended for real-world use.

:::caution Security Warning

The user with UID 1000 on your host system will have full access to these mounted directories. This means that any local user account with this ID can read, modify, or delete OpenCloud config and data files.

This can pose a security risk in shared or multi-user environments. Make sure to implement proper user and permission management and consider isolating access to these directories.

:::

## 5. Start OpenCloud

Launch OpenCloud using Docker Compose:

```bash
docker compose up -d
```

This will start all required services in the background.

## 6. Verify SSL Certification

In your web browser, visit:

```bash
https://cloud.YOUR.DOMAIN
```

You should see a security warning because the staging certificate is not fully trusted.
Same should appear with the other domains you are using.

Example with Chrome browser:

<img src={require("./../../img/docker-compose/certificate-details.png").default} alt="Certificate Details" width="500"/>

✅ Check the certificate details to confirm it’s from Let's Encrypt Staging.

<img src={require("./../../img/docker-compose/certificate-viewer.png").default} alt="Certificate Details" width="500"/>
<img src={require("./../../img/docker-compose/subordinate-ca's.png").default} alt="Certificate Details" width="500"/>

## 7. Apply a Real SSL Certificate

Once the staging certificate works, switch to a production certificate.

### Steps

#### 1️⃣ Stop Docker Compose

```bash
docker compose down
```

#### 2️⃣ Remove old staging certificates

```bash
rm -r certs
```

(If you changed volume names, adjust accordingly.)

#### 3️⃣ Disable staging mode in `.env`

```bash
nano .env
```

Comment the staging server:

```bash
# TRAEFIK_ACME_CASERVER=https://acme-staging-v02.api.letsencrypt.org/directory
```

#### 4️⃣ Restart OpenCloud with a real SSL certificate

```bash
docker compose up -d
```

✅ Now, visiting `https://cloud.YOUR.DOMAIN` should show a secure connection with a valid SSL certificate.

<img src={require("./../../img/docker-compose/status-secure.png").default} alt="Certificate Details" width="1920"/>

## 8. Log into OpenCloud

Open a browser and visit:

```bash
https://cloud.YOUR.DOMAIN
```

Login with:

**Username:** `admin`

**Password:** (your password)

<img src={require("./../../img/docker-compose/login.png").default} alt="Admin general" width="1920"/>

## Troubleshooting

If you encounter any issues, check the [Common Issues & Help](./../../../resources/common-issues.md)
