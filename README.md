# Config-repo

Spring Cloud Configuration repo for the following projects:
- [Catalog-Service](https://github.com/asgarov1/catalog-service)

### Add to the project:
- create a SpringCloudConfig server - like [here](https://github.com/asgarov1/polar-config-server)
- in the project where you want to use the properties add following the following to `application.yml`
```
spring:
  application:
    name: catalog-service
  config:
    import: "optional:configserver:"
  cloud:
    config:
      uri: http://localhost:8888 # host:port where your configserver is running
```

### To update properties after push in runtime:
- add `Spring Boot Actuator` dependency and expose the refresh endpoint:
```
management:
  endpoints:
    web:
      exposure:
        include: refresh
```
- send POST to the refresh endpoint:
`curl -X POST localhost:9001/actuator/refresh`

9001 being the port where the application is running