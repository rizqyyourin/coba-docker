# 🚀 Laravel Sail Deployment Guide

## Stack
- **Framework**: Laravel 12
- **Database**: SQLite (file-based, portable)
- **Docker**: Laravel Sail (built-in Docker)
- **PHP**: 8.5

---

## Local Development

### Setup Awal (Sekali Doang)

```bash
# 1. Clone project
git clone <repo-url>
cd <project>

# 2. Install dependencies
composer install

# 3. Copy environment file
cp .env.example .env

# 4. Generate app key
./vendor/bin/sail artisan key:generate

# 5. Build and start containers
./vendor/bin/sail up -d

# 6. Run migrations
./vendor/bin/sail artisan migrate

# Done! Buka http://localhost:8000
```

### Commands Sehari-hari

```bash
# Start containers
./vendor/bin/sail up -d

# Stop containers
./vendor/bin/sail down

# View logs
./vendor/bin/sail logs -f

# Run Artisan commands
./vendor/bin/sail artisan <command>

# Run Tinker (PHP REPL)
./vendor/bin/sail tinker
```

### Optional: Setup Alias

Tambahkan di `~/.bashrc` atau `~/.zshrc`:

```bash
alias sail='./vendor/bin/sail'
```

Kemudian tinggal:

```bash
sail up -d
sail artisan migrate
sail down
```

---

## VPS/Server Deployment

### Requirements
- Docker & Docker Compose installed
- Port 80 or custom port available
- Minimum 1GB RAM

### Deployment Steps

```bash
# 1. Clone project
git clone <repo-url>
cd <project>

# 2. Copy .env (or create manually)
cp .env.example .env

# 3. Edit .env (set APP_URL, APP_KEY, etc)
nano .env

# 4. Generate app key (if not already in .env)
./vendor/bin/sail artisan key:generate

# 5. Start containers (first time will build)
./vendor/bin/sail up -d

# 6. Run migrations
./vendor/bin/sail artisan migrate --force

# Done! Visit your domain
```

### .env Configuration for Production

```ini
APP_NAME=YourAppName
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com
APP_PORT=80

DB_CONNECTION=sqlite

LOG_CHANNEL=stack
LOG_LEVEL=error
```

### Useful VPS Commands

```bash
# Check status
docker ps

# View logs
./vendor/bin/sail logs -f

# Restart containers
./vendor/bin/sail restart

# Stop containers
./vendor/bin/sail down

# Backup SQLite database
cp database/database.sqlite database/database.sqlite.backup

# Restore from backup
cp database/database.sqlite.backup database/database.sqlite
```

---

## Database Management

### SQLite Database
- Automatically created at `database/database.sqlite`
- Portable - just copy the file for backup/migration
- No external service needed

### Backup

```bash
# Local
cp database/database.sqlite database/database.sqlite.backup

# VPS - Transfer via SFTP
# Download database/database.sqlite to your computer
```

### Restore

```bash
# Overwrite with backup
cp database/database.sqlite.backup database/database.sqlite

# Run migrations if needed
./vendor/bin/sail artisan migrate
```

---

## Troubleshooting

### Port Already In Use
Edit `.env` and change `APP_PORT`:
```ini
APP_PORT=8001
```

### Container Won't Start
```bash
# Check logs
./vendor/bin/sail logs

# Rebuild
./vendor/bin/sail build --no-cache
./vendor/bin/sail up -d
```

### Permission Issues
```bash
# Run from container as root
docker exec -u root coba-docker-laravel.test-1 chown -R sail:sail /var/www/html
```

### Database Locked
```bash
# SQLite files sometimes lock - just restart
./vendor/bin/sail restart
```

---

## File Structure

Important files committed to git:

```
project/
├── compose.yaml              # Docker Compose config ✅ COMMIT
├── .env.example              # Environment template ✅ COMMIT
├── app/
├── database/
│   └── migrations/           ✅ COMMIT
│   └── database.sqlite       ❌ DON'T COMMIT (auto-created)
├── vendor/                   ❌ DON'T COMMIT (in .gitignore)
└── ... (other Laravel files)
```

---

## Tips

1. **Always commit `composer.lock`** - Ensures same version in production
2. **Use `--force` flag** when running migrations on production
3. **Backup SQLite file regularly** - Simple copy to cloud storage
4. **Monitor disk space** - SQLite files can grow with logs/uploads
5. **Use environment variables** - Keep secrets in .env, not in code

---

## Support

- [Laravel Sail Documentation](https://laravel.com/docs/sail)
- [Laravel Documentation](https://laravel.com/docs)
- [Docker Documentation](https://docs.docker.com/)
