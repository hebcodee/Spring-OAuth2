# Spring OAuth2

Sistema de login utilizando **OAuth 2** e **Spring Boot Security 6**, com suporte a autenticação via **GitHub** e **Google**.

## Tecnologias

- **Java 21**
- **Spring Boot 4.0**
- **Spring Security** (OAuth2 Client)
- **Spring Web MVC**

## Funcionalidades

- Login com **GitHub** (OAuth2)
- Login com **Google** (OAuth2)

## Estrutura do projeto

```
src/main/java/org/example/springoauth2/
├── SpringOAuth2Application.java    # Classe principal
├── config/
│   └── SecurityConfig.java        # Configuração de segurança e OAuth2
└── controller/
    └── HomeController.java        # Endpoints da aplicação
```

## Pré-requisitos

- **JDK 21**
- **Maven 3.6+** (ou use o wrapper incluído: `./mvnw` / `mvnw.cmd`)

## Configuração

### 1. Credenciais OAuth2

É necessário configurar as credenciais dos provedores (GitHub e/ou Google) via variáveis de ambiente:

| Variável               | Descrição                            |
| ---------------------- | ------------------------------------ |
| `GITHUB_CLIENT_ID`     | Client ID do app OAuth no GitHub     |
| `GITHUB_CLIENT_SECRET` | Client Secret do app OAuth no GitHub |
| `GOOGLE_CLIENT_ID`     | Client ID do app OAuth no Google     |
| `GOOGLE_CLIENT_SECRET` | Client Secret do app OAuth no Google |

**GitHub:** [Settings → Developer settings → OAuth Apps](https://github.com/settings/developers)  
**Google:** [Google Cloud Console → APIs & Services → Credentials](https://console.cloud.google.com/apis/credentials)

Para desenvolvimento local, você pode criar um arquivo `.env` (e não versioná-lo) ou exportar as variáveis no terminal antes de rodar a aplicação.

### 2. application.properties

As credenciais são lidas do `application.properties`, que já está configurado para usar as variáveis de ambiente acima. O arquivo também define:

- `spring.application.name=Spring-OAuth2`
- `logging.level.org.springframework.security=TRACE` (útil para debug)

## Como executar

### Com Maven instalado

```bash
mvn spring-boot:run
```

### Executando o JAR

```bash
./mvnw package
java -jar target/Spring-OAuth2-0.0.1-SNAPSHOT.jar
```

A aplicação sobe por padrão em **http://localhost:8080**.

## Endpoints

| Rota           | Acesso      | Descrição                      |
| -------------- | ----------- | ------------------------------ |
| `GET /`        | Público     | Página inicial                 |
| `GET /secured` | Autenticado | Página protegida (exige login) |

Ao acessar uma rota protegida sem estar logado, você será redirecionado para o fluxo de login (OAuth2 ou formulário).
