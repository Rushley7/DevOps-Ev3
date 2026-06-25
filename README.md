# DevOps Ev3 - Innovatech Chile

## Descripción
Proyecto de orquestación y automatización en AWS ECS con pipeline CI/CD usando GitHub Actions.

## Arquitectura
-**Frontend**: React + Nginx, desplegado en ECS Fargate
-**Backend Ventas**: Spring Boot, puerto 8080, conectado a RDS MySQL
-**Backend Despachos**: Spring Boot, puerto 8081, conectado a RDS MySQL
-**Base de datos**: Amazon RDS MySQL (rushley-db)
- **Load Balancer**: Application Load Balancer (rushley-alb)
- **Orquestación**: AWS ECS Fargate (rushley-cluster)
- **Registro de imágenes**: Amazon ECR
- **CI/CD**: GitHub Actions

## URL pública
http://rushley-alb-1011781161.us-east-1.elb.amazonaws.com

## Endpoints
- Frontend: http://rushley-alb-1011781161.us-east-1.elb.amazonaws.com/
- Ventas API: http://rushley-alb-1011781161.us-east-1.elb.amazonaws.com/api/v1/ventas
- Despachos API: http://rushley-alb-1011781161.us-east-1.elb.amazonaws.com/api/v1/despachos

## Servicios ECS
- rushley-front-service
- rushley-ventas-service
- rushley-despachos-service

## Pipeline CI/CD
El pipeline se activa automáticamente con cada push a main:
1. Build de imagen Docker
2. Push a Amazon ECR
3. Deploy automático en ECS

## Autoscaling
Configurado con Target Tracking al 50% de CPU, mínimo 1 tarea, máximo 3.