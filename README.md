# 1024-config

This repo is used by 1024. I uploaded one of the `application.yml` file of service to test the Spring Cloud Config.

Spring Cloud Config provides server-side and client-side support for externalized configuration in a distributed system.

In order to apply this feature in mircroservice project, following steps are required:

1. Upload `application.yml` of each service with git.
2. Discard `application.yml` within the service.
3. Write `application.yml` for Config service. E.g.:
    ```xml
    spring:
      application:
      name: tensquare‐config
    cloud:
      config:
        server:
          git:
            uri: https://github.com/xiaokeliu666/1024-config.git
    server:
      port: 12000
    ```
4. Use `bootstrap.yml` for the bootstrap phase of an application context. E.g.:
    ```xml
    spring:
      cloud:
        config:
          name: base
          profile: dev
          label: master
          uri: http://127.0.0.1:12000
    ```
In this way, we can manage all the configurations by editting over github.
