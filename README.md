# API Gateway

Refer to the department-service for:
- Register to service registry (Eureka)
- Use externalized configuration (Spring Cloud Config Server)
- Distributed tracing (Zipkin)


## API Gateway

### Import dependencies

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

### Configure routes

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: employee-service
          uri: lb://employee-service
          predicates:
            - Path="/employees/**"
        - id: department-service
          uri: lb://department-service
          predicates:
            - Path="/departments/**"
```

## API Testing

### Test department service through API gateway

Request:
```bash
# access department-service directly
http GET :8060/departments/with-employees

# access department-service through API gateway
http GET :8060/departments/with-employees
```

## References

- <https://cloud.spring.io/spring-cloud-gateway/reference/html/>
- <https://cloud.spring.io/spring-cloud-gateway/reference/html/#the-path-route-predicate-factory>