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
 This should open up the admin console of keycloak

 #### Setup a Realm

Log in to Keycloak Admin Console: http://localhost:8080/admin. \
Create a new realm (e.g., actuator-secure).

#### Setup a Client

Navigate to Clients and click Create. 

- Client ID: service-a-client 
- Client Protocol: openid-connect 
- Access Type: confidential \
  
Save and generate a client secret from the Credentials tab. Save this value for later.

