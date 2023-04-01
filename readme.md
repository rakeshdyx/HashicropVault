# Hashicrop Vault

### Pre Requisite 

1. Create a Compute Engine in GCP.
2. Make sure to take OS of Ubuntu with version 20.4
3. Assign a service account and add a pub key for the terminal access.

### Vault instllation reference URL
https://developer.hashicorp.com/vault/downloads

### Post Installation steps 

1. Execute command `vault -h` to test the installation status.
2. Start the server with command `vault server -dev`.
3. Once vault server start, you will get Unsealed Key and Root token like below.

```
Unseal Key: VNLLZBbz8XXXXXXXXXXXXXXXXXXXXXXXXXXX
Root Token: hvs.xxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### Export Environment Variables
1. Execute below commnds.

```
export VAULT_ADDR="http://127.0.0.1:8200"
export VAULT_TOKEN="hvs.BsbRBk6DSmJwBgBSjvd4ShK4"
```

### Setup GCP Secret Engine

1. Enable the google cloud secret engine using below command.
```
vault secrets enable gcp
```

Reference URL -  https://developer.hashicorp.com/vault/docs/secrets/gcp

### Configure 