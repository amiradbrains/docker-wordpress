# WordPress Docker Development Environment

Beginner-friendly local WordPress setup using Docker.

This setup includes:

* WordPress
* MySQL
* phpMyAdmin
* MailHog (Email Testing)

---

# Requirements

Install:

* Docker
* Docker Compose

## Ubuntu / Debian Installation

```bash
sudo apt update

sudo apt install docker.io docker compose -y
```

Enable Docker:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

Check installation:

```bash
docker --version
docker compose --version
```

---

# Project Structure

```text
project-folder/
│
├── docker-compose.yml
├── wp-content/
├── wp-config.php
└── other wordpress files...
```

---

# Start Project

Open terminal inside project folder:

```bash
docker compose up -d --build
```

---

# Stop Project

```bash
docker compose down
```

Remove containers + database:

```bash
docker compose down -v
```

---

# Access URLs

## WordPress

```text
http://localhost:8080
```

## phpMyAdmin

```text
http://localhost:8081
```

## MailHog

```text
http://localhost:8025
```

---

# Database Credentials

| Setting  | Value     |
| -------- | --------- |
| Database | wordpress |
| Username | wordpress |
| Password | wordpress |
| Host     | db        |

---

# phpMyAdmin Login

| Setting  | Value    |
| -------- | -------- |
| Server   | db       |
| Username | root     |
| Password | password |

---

# MailHog Setup for WordPress SMTP

Install plugin:

* WP Mail SMTP

Go to:

```text
WordPress Dashboard
→ WP Mail SMTP
→ Settings
```

Use these settings:

| Setting        | Value      |
| -------------- | ---------- |
| Mailer         | Other SMTP |
| SMTP Host      | mailhog    |
| SMTP Port      | 1025       |
| Encryption     | None       |
| Authentication | OFF        |

Save settings.

Send test email.

View emails:

```text
http://localhost:8025
```

---

# Useful Docker Commands

## Check Running Containers

```bash
docker ps
```

## View Logs

```bash
docker compose logs
```

Specific service logs:

```bash
docker compose logs wordpress
docker compose logs db
```

---

# Common Issues

## Error Establishing Database Connection

Check:

```yaml
WORDPRESS_DB_PASSWORD: wordpress
```

Must match:

```yaml
MYSQL_PASSWORD: wordpress
```

Then rebuild:

```bash
docker compose down -v
docker compose up -d
```

---

## Port Already In Use

Change ports:

```yaml
ports:
  - "8090:80"
```

Then access:

```text
http://localhost:8090
```

---

# Container Architecture

```text
Browser
   ↓
WordPress Container
(Apache + PHP + WordPress)
   ↓
MySQL Container
```

The official WordPress Docker image already includes:

* Apache
* PHP
* WordPress

So no separate PHP container is required.

---

# Verify PHP Inside Container

```bash
docker exec -it <wordpress-container-name> bash
```

Then:

```bash
php -v
apache2 -v
```

---

# Restart Containers

```bash
docker compose restart
```

---

# Update Containers

```bash
docker compose pull
docker compose up -d
```
