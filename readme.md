# XAMPP Clone - Docker Edition

A lightweight Docker-based alternative to XAMPP, providing MariaDB and phpMyAdmin services for local development.

## 🚀 Features

- **MariaDB 10.11**: Fast and reliable MySQL-compatible database
- **phpMyAdmin**: Web-based database administration interface
- **Docker Compose**: Easy setup and management
- **Persistent Data**: Database data survives container restarts
- **Secure Configuration**: Environment-based credentials management

## 📋 Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your system
- [Docker Compose](https://docs.docker.com/compose/install/) installed

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/hilalahmad0101/xampp-clone.git
cd xampp-clone
```

### 2. Environment Configuration

Create a `.env` file in the project root to secure your credentials:

```bash
cp .env.example .env
```

Edit the `.env` file with your preferred credentials:

```env
# Database Configuration
MYSQL_ROOT_PASSWORD=your_secure_root_password_here
MYSQL_DATABASE=your_database_name
MYSQL_USER=your_username
MYSQL_PASSWORD=your_secure_password_here

# phpMyAdmin Configuration
PMA_HOST=mysql
```

### 3. Start the Services

```bash
docker-compose up -d
```

This will start both MariaDB and phpMyAdmin in the background.

## 🌐 Access Your Services

| Service | URL | Default Credentials |
|---------|-----|-------------------|
| **phpMyAdmin** | http://localhost:8082 | Username: `root`<br>Password: (from .env file) |
| **MariaDB** | localhost:3306 | Host: `localhost`<br>Port: `3306`<br>Username: `root` or your custom user<br>Password: (from .env file) |

## 🎯 Usage Examples

### Connecting from PHP Applications

```php
<?php
$host = 'localhost';
$port = '3306';
$dbname = 'your_database_name'; // from .env
$username = 'your_username';    // from .env
$password = 'your_password';    // from .env

try {
    $pdo = new PDO("mysql:host=$host;port=$port;dbname=$dbname", $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully!";
} catch(PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

### Connecting from Command Line

```bash
mysql -h localhost -P 3306 -u your_username -p
```

## 🔧 Management Commands

### Start Services
```bash
docker-compose up -d
```

### Stop Services
```bash
docker-compose down
```

### View Logs
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs mysql
docker-compose logs phpmyadmin
```

### Restart Services
```bash
docker-compose restart
```

### Update Images
```bash
docker-compose pull
docker-compose up -d
```

## 📁 Project Structure

```
xampp-clone/
├── docker-compose.yml      # Main Docker Compose configuration
├── .env.example           # Environment variables template
├── .env                   # Your environment variables (create this)
├── .gitignore            # Git ignore file
└── README.md             # This file
```

## 🔒 Security Best Practices

1. **Never commit `.env` file** - It's already in `.gitignore`
2. **Use strong passwords** - Generate secure passwords for production
3. **Change default ports** if needed for additional security
4. **Regular updates** - Keep Docker images updated

## 🐛 Troubleshooting

### Port Already in Use
If ports 3306 or 8082 are already in use, modify the ports in `docker-compose.yml`:

```yaml
ports:
  - "3307:3306"  # Changed from 3306:3306
  # or
  - "8083:80"    # Changed from 8082:80
```

### Database Connection Issues
1. Ensure containers are running: `docker-compose ps`
2. Check logs: `docker-compose logs mysql`
3. Verify credentials in `.env` file

### Data Persistence
Database data is stored in Docker volume `mariadb_data`. To reset:

```bash
docker-compose down -v  # Warning: This deletes all data!
```

## 📊 Default Configuration

- **MariaDB Version**: 10.11
- **Default Database**: As specified in `.env`
- **MariaDB Port**: 3306
- **phpMyAdmin Port**: 8082
- **Data Volume**: `mariadb_data`

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

## 🆘 Support

If you encounter any issues:

1. Check the [Issues](https://github.com/hilalahmad0101/xampp-clone/issues) page
2. Create a new issue with detailed information
3. Include logs and system information

---

**Made with ❤️ for the developer community**

*This project aims to provide a simple, Docker-based alternative to traditional XAMPP installations.*