# Secured Actuator

## Exposing Only Essential Endpoints
Restrict Actuator endpoint exposure to only necessary endpoints, such as health and info, which can be safely exposed for monitoring purposes.
```bash
management.endpoints.web.exposure.include=health,info
```
By limiting the number of exposed endpoints, you reduce the application’s attack surface while still providing necessary health and status information.

## Securing Sensitive Endpoints
Use Spring Security to restrict access to sensitive Actuator endpoints, allowing only authenticated users (or specific roles) to access them.
```bash
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/actuator/health", "/actuator/info").permitAll()  // Expose basic endpoints
            .requestMatchers("/actuator/**").hasRole("ADMIN")  // Restrict other Actuator endpoints
        )
        .httpBasic();  // Use HTTP Basic auth, or configure as needed
    return http.build();
}
```
 Restricting access to only specific roles ensures that only authorized personnel can access sensitive operational data or administrative actions, adding a layer of protection.

## Environment-Specific Configurations
Configure exposure and security settings based on the environment. For example, limit exposure in production while allowing broader access in development.

application-prod.properties:
  ```bash
management.endpoints.web.exposure.include=health,info
```

application-dev.properties:
```bash
management.endpoints.web.exposure.include=*
```
Different environments (dev, test, prod) have varying security requirements. Limiting exposure in production while allowing more flexibility in development aligns with good security practices without compromising developer productivity
