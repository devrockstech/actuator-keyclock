# Misconfigured Actuator Endpoints

## Exposing All Endpoints in Production
```bash
management.endpoints.web.exposure.include=*
```
Exposing all Actuator endpoints publicly can be a serious security risk. \
Actuator endpoints like ```/actuator/env, /actuator/beans, and /actuator/mappings ``` provide sensitive information about the application’s environment, beans, and configurations, which could be exploited.

## Disabling Security on Actuator Endpoints
Setting up your security configuration to allow unrestricted access to all Actuator endpoints:
```bash
http
    .authorizeHttpRequests((requests) -> requests
        .requestMatchers("/actuator/**").permitAll()
    );
```

Allowing unrestricted access to all Actuator endpoints bypasses security, making it easier for unauthorized users to gather sensitive information or trigger admin-level actions (like shutdown).


## Embedding Sensitive Information in Public Endpoints
Exposing the ```/actuator/metrics``` endpoint without restriction
```bash
management.endpoints.web.exposure.include=metrics
```
Metrics can reveal performance-related data (like heap memory and active thread counts) that might be used for reconnaissance in attack scenarios. Exposing this endpoint without proper security controls can compromise application integrity
