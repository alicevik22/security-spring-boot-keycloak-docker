# Security with Spring Boot, Keycloak and Docker

<b>Author:</b> <a href="https://github.com/spring-boot-react-nextjs" target="_blank">spring-boot-react-nextjs</a><br>
<b>Created:</b> 2023-12-04<br>
<b>Last updated:</b> 2023-12-09
<br><br>
This repository serves as a demonstration on how to create a robust and scalable security application with modern technologies.<br>
Within this repository, the following technologies are applied:
- Spring Boot [![](https://img.shields.io/badge/version-3.2.0-blue)]()
- Keycloak [![](https://img.shields.io/badge/version-23.0.1-blue)]()
- Docker
<br><br>

![01-spring-boot-icon](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/01-spring-boot-icon.png)  ![02-docker-icon](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/02-docker-icon.png)  ![03-keycloak-icon](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/03-keycloak-icon.png)

## 1 Installation Prerequisites

- <a href="https://maven.apache.org/download.cgi" target="_blank">Maven</a>
- <a href="https://adoptium.net" target="_blank">Java 21</a> or higher
- <a href="https://www.docker.com/products/docker-desktop/" target="_blank">Docker Desktop</a>
- IDE (of your choice)
<br>

## 2 Project Installation

- Clone the repository:

```bash
git clone https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker.git
```

- Build the project using Maven:

```bash
mvn clean install
```

- Run the <strong>Spring Boot</strong> application:

```bash
mvn spring-boot:run
```

## 3 User Credentials

To login to Keycloak via ```http://localhost:8080```, use the following credentials:

**Username:** ```admin```<br>
**Password:** ```admin```<br>

<i><b>NOTE:</b> These credentials can be changed within the ```.env``` file.</i><br><br>

The following users are loaded into Keycloak automatically.<br>
The credentials are loaded according the ```src/main/resources/data/keycloak/import/realm-import.json``` file.

**Username:** ```user-admin```<br>
**Password:** ```test```<br>
**Role:** ```client_admin```


**Username:** ```user-moderator```<br>
**Password:** ```test```<br>
**Role:** ```client_moderator```

**Username:** ```user-user```<br>
**Password:** ```test```<br>
**Role:** ```client_user```
<br>

## 4 API Endpoints

To avoid as much manual work as possible, a Postman collection is provided for you to import within your Postman installation.<br>
This file can be found in ```src/main/resources/data/postman/import/collection-import.json```

![04-postman-collection](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/04-postman-collection.jpg)

### 4.1 Keycloak Request Token Endpoint

[![](https://img.shields.io/badge/HTTP-POST-yellow)]()

**Description:** Post user credentials via the <b>Keycloak request token endpoint</b><br>
**Endpoint URL:** ```http://localhost:8080/realms/security-realm/protocol/openid-connect/token```

![05-postman-test-keycloak-request-token-endpoint](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/05-postman-test-keycloak-request-token-endpoint.jpg)
<br>

### 4.2 Controller Endpoints

[![](https://img.shields.io/badge/HTTP-GET-green)]()

**Description:** Get the message from the <b>unsecured controller demo endpoint</b><br>
**Endpoint URL:** ```http://localhost:8081/api/v1/demo```

![06-postman-test-unsecured-controller-demo-endpoint](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/06-postman-test-unsecured-controller-demo-endpoint.jpg)
<br><br>

<i><b>NOTE:</b> Following endpoints are secured.<br>
Copy the provided token, from the <b>Keycloak Request Token Endpoint</b> into your GET request<br>
(tab ```Authorization```, type ```Bearer```), as per provided example (Postman images) below.</i>
<br><br>

[![](https://img.shields.io/badge/HTTP-GET-green)]()

**Description:** Get the message from the <b>secured controller admin endpoint</b><br>
**Endpoint URL:** ```http://localhost:8081/api/v1/admin``` <br>
**Access restricted:** Users with role ```client_admin``` only

![07-postman-test-secured-controller-admin-endpoint](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/07-postman-test-secured-controller-admin-endpoint.jpg)
<br><br>

[![](https://img.shields.io/badge/HTTP-GET-green)]()

**Description:** Get the message from the <b>secured controller moderator endpoint</b><br>
**Endpoint URL:** ```http://localhost:8081/api/v1/moderator``` <br>
**Access restricted:** Users with role ```client_moderator``` only

![08-postman-test-secured-controller-moderator-endpoint](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/08-postman-test-secured-controller-moderator-endpoint.jpg)
<br><br>

[![](https://img.shields.io/badge/HTTP-GET-green)]()

**Description:** Get the message from the <b>secured controller user endpoint</b><br>
**Endpoint URL:** ```http://localhost:8081/api/v1/user``` <br>
**Access restricted:** Users with role ```client_user``` only

![09-postman-test-secured-controller-user-endpoint](https://github.com/spring-boot-react-nextjs/security-spring-boot-keycloak-docker/blob/main/images/09-postman-test-secured-controller-user-endpoint.jpg)
