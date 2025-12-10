<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

---

# 🚀 Laravel 12 with Docker Sail + SQLite

Complete Laravel setup with **Docker Sail** for local development and **production-ready** deployment.

## 📊 Tech Stack

- **Framework**: Laravel 12
- **PHP**: 8.5
- **Database**: SQLite (portable, file-based)
- **Docker**: Laravel Sail (built-in)
- **Web Server**: Nginx
- **Port**: 5000 (customizable)

---

## ⚡ Quick Start (5 Minutes)

### **1. Clone Repository**
```bash
git clone https://github.com/rizqyyourin/coba-docker.git
cd coba-docker
```

### **2. Install Dependencies**
```bash
composer install
```

### **3. Setup Environment**
```bash
cp .env.example .env
./vendor/bin/sail artisan key:generate
```

### **4. Start Sail**
```bash
./vendor/bin/sail up -d
```

### **5. Run Migrations**
```bash
./vendor/bin/sail artisan migrate
```

### **6. Access Application**
```
🌍 http://localhost:5000
```

Done! ✅

---

## 📚 Detailed Setup Guide

### **Prerequisites**
- Docker & Docker Compose installed
- Composer installed
- Git installed

### **Installation Steps**

#### **1. Clone & Navigate**
```bash
git clone https://github.com/rizqyyourin/coba-docker.git
cd coba-docker
```

#### **2. Install Composer Dependencies**
```bash
composer install
```

#### **3. Copy Environment File**
```bash
cp .env.example .env
```

#### **4. Generate Application Key**
```bash
./vendor/bin/sail artisan key:generate
```

#### **5. Build & Start Containers**
```bash
# Start containers in background
./vendor/bin/sail up -d

# Or view logs in realtime
./vendor/bin/sail up
```

#### **6. Run Database Migrations**
```bash
./vendor/bin/sail artisan migrate
```

#### **7. Verify Application**
```bash
# Check if running
./vendor/bin/sail ps

# Test in browser
http://localhost:5000
```

---

## 🎮 Daily Development Commands

### **Container Management**
```bash
# Start containers
./vendor/bin/sail up -d

# Stop containers
./vendor/bin/sail down

# Restart containers
./vendor/bin/sail restart

# View logs
./vendor/bin/sail logs -f

# Check container status
./vendor/bin/sail ps
```

### **Artisan Commands**
```bash
# Run migrations
./vendor/bin/sail artisan migrate

# Create model with migration
./vendor/bin/sail artisan make:model Post -m

# Create controller
./vendor/bin/sail artisan make:controller PostController

# Interactive PHP shell
./vendor/bin/sail tinker

# View all routes
./vendor/bin/sail artisan route:list

# Reset database
./vendor/bin/sail artisan migrate:fresh
```

### **Package Management**
```bash
# Install composer package
./vendor/bin/sail composer require package/name

# Install npm packages
./vendor/bin/sail npm install

# Run development assets
./vendor/bin/sail npm run dev

# Build for production
./vendor/bin/sail npm run build
```

---

## 🌍 Deployment to VPS/Server

For detailed deployment guide, see [DEPLOYMENT.md](./DEPLOYMENT.md)

### **Quick VPS Setup**
```bash
# SSH to your VPS
ssh user@your-vps.com

# Clone repository
git clone https://github.com/rizqyyourin/coba-docker.git
cd coba-docker

# Install dependencies
composer install

# Setup environment
cp .env.example .env
nano .env  # Edit as needed

# Generate key
./vendor/bin/sail artisan key:generate

# Start application
./vendor/bin/sail up -d

# Run migrations
./vendor/bin/sail artisan migrate --force

# Done!
```

---

## ⚙️ Configuration

### **Port Configuration**

Default port is **5000**. To change:

**Edit `compose.yaml`:**
```yaml
ports:
    - '${APP_PORT:-5000}:80'  # Change 5000 to your port
```

**Edit `.env`:**
```ini
APP_PORT=5000
APP_URL=http://localhost:5000
```

**Restart:**
```bash
./vendor/bin/sail down && ./vendor/bin/sail up -d
```

### **Database Configuration**

SQLite is the default. Database file is at `database/database.sqlite` (auto-created).

To use MySQL instead, edit `compose.yaml` and `.env` - see DEPLOYMENT.md for examples.

---

## 🐛 Troubleshooting

### **Port Already In Use**
```bash
# Change port in .env and compose.yaml
# Then restart
./vendor/bin/sail restart
```

### **Container Won't Start**
```bash
# Check logs
./vendor/bin/sail logs

# Rebuild (no cache)
./vendor/bin/sail build --no-cache
./vendor/bin/sail up -d
```

### **Permission Denied**
```bash
# Fix permissions (if needed)
docker exec -u root container-name chown -R sail:sail /var/www/html
```

### **Out of Memory**
```bash
# Increase Docker resources
# Docker Desktop → Settings → Resources → Memory (increase to 4GB+)
```

---

## 📦 Optional: Setup Command Alias

To avoid typing `./vendor/bin/sail` each time:

**Add to `~/.bashrc` or `~/.zshrc`:**
```bash
alias sail='./vendor/bin/sail'
```

**Then reload:**
```bash
source ~/.bashrc
```

**Now you can:**
```bash
sail up -d
sail artisan migrate
sail tinker
```

---

## 📋 Project Structure

```
coba-docker/
├── app/                  # Application code
├── database/
│   ├── migrations/      # Database migrations ✅ commit
│   └── database.sqlite  # SQLite file (auto-created) ❌ gitignore
├── resources/           # Views, CSS, JS
├── routes/              # Route definitions
├── tests/               # Test files
├── compose.yaml         # Docker config ✅ commit
├── .env.example         # Environment template ✅ commit
├── .env                 # Environment (local) ❌ gitignore
├── composer.json        # PHP packages ✅ commit
├── composer.lock        # Lock file ✅ commit
└── DEPLOYMENT.md        # Deployment guide
```

---

## 📚 Resources

- [Laravel Documentation](https://laravel.com/docs)
- [Laravel Sail Documentation](https://laravel.com/docs/sail)
- [Docker Documentation](https://docs.docker.com/)
- [Deployment Guide](./DEPLOYMENT.md)

---

## 📝 Git Workflow

```bash
# Start feature
git checkout -b feature/new-feature

# Code & commit
git add .
git commit -m "feat: add new feature"

# Push to GitHub
git push origin feature/new-feature

# Create Pull Request on GitHub
```

---

## ✅ Checklist for Success

- [ ] Docker & Docker Compose installed
- [ ] Project cloned from GitHub
- [ ] `composer install` completed
- [ ] `.env` file created & configured
- [ ] `sail up -d` is running
- [ ] `sail artisan migrate` successful
- [ ] Application accessible in browser
- [ ] Database connected

---

## 📞 Support & Questions

- Check [DEPLOYMENT.md](./DEPLOYMENT.md) for deployment details
- Review Laravel docs: https://laravel.com/docs
- Check container logs: `./vendor/bin/sail logs -f`

---

## 📄 License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
