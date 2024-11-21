# Securing Actuator Endpoints 

<details>
  <summary>Setup Keycloak</summary>

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

![keycloak-console](https://github.com/user-attachments/assets/be64d4c2-0c07-4a8b-a071-13edd8368a5f)
 
#### Setup a Realm

Log in to Keycloak Admin Console: https://62.138.26.145:8443/ 

Create a new realm (e.g., actuator-secure).

![keycloak-console](https://github.com/user-attachments/assets/5b9daa63-7d80-41c5-8b89-fd86f66fbb45)

![realm-create](https://github.com/user-attachments/assets/ae392cab-72b9-42ce-bd29-b4482ca77941)

![realm-create-3](https://github.com/user-attachments/assets/d286706a-9b6a-4327-bb8e-576417ea103f)


#### Setup a Client

Navigate to Clients and click Create. 

- Client ID: service-a-client 
- Client Protocol: openid-connect 
- Access Type: confidential \
  
Save and generate a client secret from the Credentials tab. Save this value for later.



</details>
