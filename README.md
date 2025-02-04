# docker compose for local

---
---
---

# For Vault _________________
## Setup Instructions
### 1. Clone the Repository
```sh
git clone https://github.com/yourusername/golang-vault-service.git
cd golang-vault-service
```

### 2. Set Up Vault Using Docker
Create a `docker-compose.yml` file to run Vault locally.

```yaml
version: '3.7'

services:
  vault:
    image: hashicorp/vault:latest
    container_name: vault-dev
    restart: always
    ports:
      - "8200:8200"
    environment:
      VAULT_DEV_ROOT_TOKEN_ID: root
      VAULT_ADDR: http://127.0.0.1:8200
    cap_add:
      - IPC_LOCK
    command: server -dev
```

Run the following command to start Vault:
```sh
docker-compose up -d
```

Check if Vault is running:
```sh
docker ps
```

### 3. Initialize and Store Secrets in Vault

Run the following commands inside the Vault container:
```sh
docker exec -it vault-dev vault login root
vault secrets enable -path=secret kv
vault kv put secret/myapp username=admin password=supersecret
vault kv get secret/myapp
```

---
---
---