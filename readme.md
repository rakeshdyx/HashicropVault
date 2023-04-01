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
2. Test the server status using `vault status` command.

### Setup GCP Secret Engine

1. Enable the google cloud secret engine using below command.
```
vault secrets enable gcp
```
2. Run `vault secrets list` to check if gcp seceret vault has created. O/P looks like below.
```
$ vault secrets list
Path          Type         Accessor              Description
----          ----         --------              -----------
cubbyhole/    cubbyhole    cubbyhole_d25198a5    per-token private secret storage
gcp/          gcp          gcp_219aa2d8          n/a
identity/     identity     identity_d99aadfe     identity store
secret/       kv           kv_d893e4fa           key/value secret storage
sys/          system       system_96ba5c20       system endpoints used for control, policy and debugging
```
3. Create a Service Account with required permission. Here I have taken mandetory roles to a create token.
```
ServiceAccountAdmin
ServiceAccountKeyAdmin
ServiceAccountTokenCreator
``` 
4. Create a Service Account key and download the json file.
5. Go to the vault server and copy the SA key to ur working directory.
6. Now configure the secrets engine with account credential using command below.

```
vault write gcp/config credentials=@sa-key.json
```

Reference URL -  https://developer.hashicorp.com/vault/docs/secrets/gcp

### Configure 