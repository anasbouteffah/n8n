# n8n Docker Setup

This repository contains everything you need to run n8n (a powerful workflow automation tool) using Docker and Docker Compose.

## 📋 Prerequisites

Before you start, make sure you have the following installed on your system:

- [Docker](https://docs.docker.com/get-docker/) (version 20.10 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 2.0 or higher)

## 🚀 Quick Start

1. **Clone this repository**
   ```bash
   git clone https://github.com/anasbouteffah/n8n
   cd n8n-docker-setup
   ```

2. **Start n8n**
   ```bash
   docker-compose up -d
   ```

3. **Access n8n**
   Open your browser and go to: http://localhost:5678

4. **Login credentials**
   - Username: `admin`
   - Password: `supersecure`

## 📁 Project Structure

```
.
├── docker-compose.yml    # Docker Compose configuration
├── README.md            # This file
└── n8n-data/           # n8n data directory (created automatically)
```

## ⚙️ Configuration

### Environment Variables

The following environment variables are configured in the `docker-compose.yml`:

| Variable | Value | Description |
|----------|-------|-------------|
| `N8N_BASIC_AUTH_ACTIVE` | `true` | Enables basic authentication |
| `N8N_BASIC_AUTH_USER` | `admin` | Username for n8n login |
| `N8N_BASIC_AUTH_PASSWORD` | `supersecure` | Password for n8n login |
| `N8N_ENCRYPTION_KEY` | `3a7f12948ea4abc8e4890c6c74b1d039` | Encryption key for credentials |
| `TZ` | `Etc/UTC` | Timezone setting |

### Ports

- **5678**: n8n web interface port (mapped to host port 5678)

### Volumes

- `./n8n-data:/home/node/.n8n`: Persists n8n data, workflows, and credentials

## 🔒 Security Recommendations

⚠️ **Important**: Before using in production, please:

1. **Change the default password**:
   ```yaml
   - N8N_BASIC_AUTH_PASSWORD=your_secure_password_here
   ```

2. **Generate a new encryption key**:
   ```bash
   openssl rand -hex 32
   ```
   Replace the `N8N_ENCRYPTION_KEY` value with the generated key.

3. **Consider using environment files**:
   Create a `.env` file for sensitive variables:
   ```env
   N8N_BASIC_AUTH_PASSWORD=your_secure_password
   N8N_ENCRYPTION_KEY=your_generated_key
   ```

## 🛠️ Useful Commands

### Start n8n
```bash
docker-compose up -d
```

### Stop n8n
```bash
docker-compose down
```

### View logs
```bash
docker-compose logs -f n8n
```

### Update n8n
```bash
docker-compose pull
docker-compose up -d
```

### Backup data
```bash
tar -czf n8n-backup-$(date +%Y%m%d).tar.gz n8n-data/
```

### Restore data
```bash
tar -xzf n8n-backup-YYYYMMDD.tar.gz
```

## 📊 Monitoring

To check if n8n is running properly:

```bash
# Check container status
docker-compose ps

# Check container health
docker-compose logs n8n
```

## 🔧 Troubleshooting

### Common Issues

1. **Port 5678 already in use**
   - Change the port mapping in `docker-compose.yml`:
     ```yaml
     ports:
       - "8080:5678"  # Use port 8080 instead
     ```

2. **Permission issues with volumes**
   ```bash
   sudo chown -R 1000:1000 n8n-data/
   ```

3. **Cannot access n8n**
   - Ensure Docker is running
   - Check if the container is running: `docker-compose ps`
   - Verify firewall settings

### Getting Help

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [n8n GitHub Repository](https://github.com/n8n-io/n8n)

## 📝 License

This setup configuration is provided as-is. n8n itself is licensed under the [Sustainable Use License](https://github.com/n8n-io/n8n/blob/master/LICENSE.md).

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

---

**Happy Automating! 🎉**

