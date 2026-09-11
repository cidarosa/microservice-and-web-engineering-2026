# Dependências Maven nos Microsserviços para Swagger

## Microsserviços

### Spring Boot versão 3.X.X

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
	<version>2.9.0</version>
</dependency>
```

### Spring Boot versão 4.0.X

```xml
<dependency>
	<groupId>org.springdoc</groupId>
	<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
	<version>3.1.0</version>
</dependency>
```

### OpenApiConfig - Classe de Configuração

Classe de configuração para o exemplo do Microsserviço de Pedidos.

Substitua as informações de acordo com o seu microsserviço.

Para os microsserviços, na classe de configuração, em  `new Server().url("/ms-pedidos")` substitua pelo nome do microsserviços registrado no `application.properties`.

Criar o package `config` e a classe a seguir:

```java
import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import io.swagger.v3.oas.models.servers.Server;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.util.List;

@Configuration
public class OpenApiConfig {

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("Microsserviço de Pedidos")
                        .description("API responsável pelo gerenciamento de pedidos")
                        .version("v1"))

                .servers(List.of(
                        new Server().url("/ms-pedidos")
                ));
    }
}
```

### Como acessar Swagger - ui

No navegador digite o endereço:
```http
http://localhost:8082/swagger-ui/index.html
```