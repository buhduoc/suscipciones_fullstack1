# Suscripciones Fullstack - AWS ECS

Proyecto desarrollado en Spring Boot y desplegado en Amazon Web Services utilizando Docker, Amazon ECS (EC2), Amazon ECR, Application Load Balancer, Prometheus, Grafana y GitHub Actions para CI/CD.

---

## Tecnologías utilizadas

- Java 21
- Spring Boot
- Spring Actuator
- Maven
- Docker
- PostgreSQL
- Amazon EC2
- Amazon ECS (EC2 Launch Type)
- Amazon ECR
- Application Load Balancer (ALB)
- Prometheus
- Grafana
- GitHub Actions

---

## Arquitectura

```
GitHub
   │
   │ Push
   ▼
GitHub Actions
   │
   │ Build Docker
   ▼
Amazon ECR
   │
   │ Pull Image
   ▼
Amazon ECS (EC2)
   │
   ▼
Application Load Balancer
   │
   ▼
Spring Boot
   │
   ├── /actuator/health
   └── /actuator/prometheus

Prometheus
      │
      ▼
Grafana Dashboard
```

---

## Funcionalidades

- Gestión de Suscripciones
- API REST con Spring Boot
- Monitoreo mediante Spring Actuator
- Métricas Prometheus
- Dashboard Grafana
- Despliegue automático con GitHub Actions
- Balanceo de carga mediante Application Load Balancer

---

## Docker

Construir imagen

```bash
docker build -t wuh-app .
```

Ejecutar

```bash
docker run -p 8080:8080 wuh-app
```

---

## Docker Compose

Levantar ambiente completo

```bash
docker compose up -d
```

Servicios incluidos

- Spring Boot
- PostgreSQL
- Prometheus
- Grafana
- Loki
- Promtail

---

## AWS

Infraestructura implementada

- Amazon ECS (EC2)
- Amazon EC2
- Amazon ECR
- Application Load Balancer
- Target Group
- Security Groups

---

## CI/CD

Cada push realizado a la rama **main** ejecuta automáticamente:

1. Compilar proyecto
2. Construir imagen Docker
3. Publicar imagen en Amazon ECR
4. Actualizar el servicio ECS
5. Realizar un nuevo despliegue automáticamente

Workflow ubicado en:

```
.github/workflows/ci.yml
```

---

## Monitoreo

Spring Boot expone:

```
/actuator/health
```

```
/actuator/prometheus
```

Prometheus obtiene las métricas desde el Application Load Balancer.

Grafana utiliza Prometheus como Data Source.

Dashboard incluye:

- Estado del servicio
- Hora de inicio
- Tiempo activo
- Uso de CPU
- Uso de Memoria JVM
- Requests por segundo
- Latencia promedio
- Threads JVM
- Respuestas HTTP

---

## Prometheus

Archivo de configuración

```
prometheus.yml
```

Target monitoreado

```
http://wuh-alb-1772784568.us-east-1.elb.amazonaws.com/actuator/prometheus
```

---

## Grafana

Datasource

```
Prometheus
```

Dashboard personalizado para monitorear:

- AWS ECS
- Spring Boot
- JVM
- HTTP Requests

---

## GitHub Actions

Pipeline automático

```
Push
↓
Build Docker
↓
Push Amazon ECR
↓
Deploy ECS
```

---

## Ejecución Local

Clonar repositorio

```bash
git clone https://github.com/buhduoc/suscipciones_fullstack1.git
```

Entrar al proyecto

```bash
cd suscipciones_fullstack1
```

Levantar servicios

```bash
docker compose up -d
```

Aplicación

```
http://localhost:8080
```

Grafana

```
http://localhost:3000
```

Prometheus

```
http://localhost:9090
```

---

## Autor

Nicolás Oyarzo

Ingeniería en Informática

Duoc UC
