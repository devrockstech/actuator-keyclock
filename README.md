# Securing Actuator Endpoints 

## Setup Keycloak

### Generate Certificates

```bash
openssl req -newkey rsa:2048 -nodes \
  -keyout server.key.pem -x509 -days 3650 -out server.crt.pem
```

### Run KeyCloak Instace (Docker)

```
docker run  \
    -e KEYCLOAK_ADMIN=admin   \
    -e KEYCLOAK_ADMIN_PASSWORD=password   \
    -e KC_HTTPS_CERTIFICATE_FILE=/opt/keycloak/conf/server.crt.pem   \
    -e KC_HTTPS_CERTIFICATE_KEY_FILE=/opt/keycloak/conf/server.key.pem   \
    -v $PWD/server.crt.pem:/opt/keycloak/conf/server.crt.pem   \
    -v $PWD/server.key.pem:/opt/keycloak/conf/server.key.pem   \
    -p 8443:8443   quay.io/keycloak/keycloak:latest   start-dev
```
