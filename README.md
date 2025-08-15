# n8n-oracle
Dockerfile that runs n8n with oracle instant-client driver installed.

## Generate new build

1. Clone the repository
```bash
git clone https://github.com/JulianoBazzi/n8n-oracle.git
cd n8n-oracle
```

2. Build new version
```bash
docker build --platform=linux/amd64 -t julibazzi/n8n-oracle:latest .
```

3. Push version
```bash
docker push julibazzi/n8n-oracle:latest
```

## Easypanel - Volume
```bash
n8n-data
/home/node/.n8n
```
```bash
n8n-workflows
/home/node/.n8n/workflows
```
```bash
n8n-credentials
/home/node/.n8n/credentials
```

## Easypanel - Environment Variables
WEBHOOK_URL=https://seu-dominio.com
N8N_HOST=seu-dominio.com
N8N_PROTOCOL=https
