# idp_client
- This is a sample idp client - mostly from [dex/example-app](https://github.com/dexidp/dex/blob/master/examples/example-app/main.go)

## Examples
### Vault IDP
```bash
res=$(vault read -format=json identity/oidc/client/{{ .client_id }} | jq)
client_id=$(echo ${res} | jq  '.data.client_id' -r)
client_secret=$(echo ${res} | jq  '.data.client_secret' -r)
echo "client_id: ${client_id}"
echo "client_secret: ${client_secret}"
echo res:
echo ${res} | jq

# this is the build of https://github.com/dexidp/dex/tree/master/examples/example-app
issuer=${VAULT_ADDR}/v1/identity/oidc/provider/{{ .provider }}
~/tmp/dex/examples/oidc-client \
  --issuer=${issuer} \
  --client-id=${client_id} \
  --client-secret=${client_secret}
```
