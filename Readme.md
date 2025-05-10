# WordPress Docker Setup

This project sets up a local **WordPress development environment** using Docker. It's perfect for developers or beginners who want to explore WordPress without installing PHP, MySQL, or Apache manually.

✅ Includes:
- WordPress
- MySQL
- phpMyAdmin
- Follow: [Wordpress Docker Hub](https://hub.docker.com/_/wordpress)
---

## 🧰 Prerequisites

Before you begin, make sure you have:

- ✅ [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop) installed and running
- ✅ Docker Compose (bundled with Docker Desktop)
- ✅ Basic terminal knowledge

---

## 📁 Folder Structure

```bash
.
|__ docker/php.ini      # Customize the PHP configuration
├── docker-compose.yml  # Docker configuration
├── wordpress/          # WordPress files will be stored here
└── .env                # Environment variables (you will copy this from .env.example)
```

# 🚀 Setup Instructions

1. Clone the repository
```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

2. Create a .env file in the root of your project and add the following:
```bash
cp .env.example .env
```
Edit .env with your credentials:

```bash
MYSQL_ROOT_PASSWORD=rootpass
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
```

3. Start Docker containers
```bash
# Optional: Stop and clean old containers if needed
docker compose down

# Start the stack
docker compose up -d
```
This will:

- 🐬 Start MySQL database

- 🌐 Launch WordPress at http://localhost:8000

- 🛠️ Launch phpMyAdmin at http://localhost:8080

## 🧠 How WordPress Is Installed Automatically

In docker-compose.yml, you’ll see:

```yaml
volumes:
  - ./wordpress:/var/www/html
```

Here’s what happens:

- If `./wordpress` doesn’t exist, Docker creates it.
- The official WordPress image then copies WordPress files into `/var/www/html`.
- Because it's mounted to your local `./wordpress`, the files appear on your computer too.
- The official `wordpress:latest` image is built on top of an official `PHP image`, which means `PHP` is already installed.


## 🐞 Viewing Logs (For Debugging)
```bash
# Check the status of all running containers:
docker-compose ps  

# View logs from all containers
docker compose logs -f

# View logs for WordPress app
docker compose logs -f wordpress_app

# View logs for MySQL
docker compose logs -f db

# Verify PHP inside the container
docker exec -it wordpress_app bash
php -v

## View PHP error logs:
docker exec -it wordpress_app cat bash
tail -f php-errors.log
```

## ⚠️ Common Issues
❌ POST Content-Length exceeds limit
Solution: Increase PHP's upload_max_filesize and post_max_size in a php.ini, .htaccess, or Dockerfile.

**How to fix**

Adjust any PHP configuration at `docker/php.ini`

## ❌ phpMyAdmin session error
Clear your browser cookies

Ensure PHP session folder is writable (if using custom PHP setup)

## 🎨 Want to Customize?
- Add custom WordPress themes to `./wordpress/wp-content/themes`

- Add plugins to `./wordpress/wp-content/plugins`


## 🔒 Production?
This setup is for development only. For production:

- Use HTTPS (with Nginx or Traefik)
- Use production-grade database
- Optimize images and performance

Let me know if you want a production-ready version! 🙌

## 📄 License
MIT — use freely and contribute back if you improve it!