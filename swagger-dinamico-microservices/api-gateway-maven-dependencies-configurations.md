# Dependências Maven para Swagger

## Api-Gateway - Webflux

O API Gateway disponibiliza uma interface Swagger dinâmica, composta a partir dos microsserviços registrados no Eureka.

### Spring Boot versão 3.X.X

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-starter-webflux-ui</artifactId>
	<version>2.9.0</version>
</dependency>
```

### Spring Boot versão 4.0.X

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-starter-webflux-ui</artifactId>
	<version>3.1.0</version>
</dependency>
```

### application.properties

Acrescentar após a última linha no `applicatio.properties`
```properties
# SWAGGER dinamico
springdoc.swagger-ui.disable-swagger-default-url=true
springdoc.swagger-ui.operationsSorter=method
springdoc.swagger-ui.tagsSorter=alpha
```

### DynamicSwaggerConfig - Classe de Configuração

Criar o package `config` e criar a classe a seguir.

```java
import org.springdoc.core.properties.AbstractSwaggerUiConfigProperties.SwaggerUrl;
import org.springdoc.core.properties.SwaggerUiConfigProperties;
import org.springframework.cloud.client.discovery.DiscoveryClient;
import org.springframework.context.event.EventListener;
import org.springframework.boot.context.event.ApplicationReadyEvent;
import org.springframework.scheduling.annotation.EnableScheduling;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

import java.util.LinkedHashSet;
import java.util.Set;
import java.util.stream.Collectors;

@Component
@EnableScheduling
public class DynamicSwaggerConfig {

    private final DiscoveryClient discoveryClient;
    private final SwaggerUiConfigProperties swaggerUiConfigProperties;

    public DynamicSwaggerConfig(
            DiscoveryClient discoveryClient,
            SwaggerUiConfigProperties swaggerUiConfigProperties) {

        this.discoveryClient = discoveryClient;
        this.swaggerUiConfigProperties = swaggerUiConfigProperties;
    }

    @EventListener(ApplicationReadyEvent.class)
    public void carregarAoIniciar() {
        atualizarUrls();
    }

    @Scheduled(initialDelay = 10000, fixedDelay = 10000)
    public void atualizarUrls() {

        Set<SwaggerUrl> urls = discoveryClient.getServices()
                .stream()
                .filter(service ->
                        !service.equalsIgnoreCase("api-gateway"))
                .sorted()
                .map(service -> new SwaggerUrl(
                        service,
                        "/" + service + "/v3/api-docs",
                        service
                ))
                .collect(Collectors.toCollection(LinkedHashSet::new));

        swaggerUiConfigProperties.setUrl(null);
        swaggerUiConfigProperties.setUrls(urls);
    }
}
```

### Como acessar Swagger - ui

No navegador digite o endereço:
```http
http://localhost:8082/swagger-ui/index.html
```