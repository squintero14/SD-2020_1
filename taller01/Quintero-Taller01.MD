# Taller 01

# Juan Sebastián Quintero Yoshioka - A00310448

## Infraestructura como código
## Objetivos:
- Comprender las motivaciones de la automatización de infraestructura.
- Realizar de forma autónoma el aprovisionamiento automático de infraestructura.
- Diagnosticar y ejecutar de forma autónoma las acciones necesarias para lograr infraestructuras estables.

## Escenario 01 (Sesión en clase)

Con el fin de probar una aplicación web, se requiere montar un servidor con CentOS 8.1, donde se ejecute el servidor web NGINX.

## Pre Requisitos

- VirtualBox

## Actividades

 1. Descargue la imagen ISO de CentOS.
 
 El proyecto CentOS es un esfuerzo de software libre impulsado por la comunidad centrado en entregar un ecosistema robusto de código abierto alrededor de una plataforma Linux. Es una plataforma consistente y manejable que se adapta a una amplia variedad de implementaciones. Para algunas comunidades de código abierto, es una base sólida y predecible sobre la cual construir. [1]
 
 En este taller, se descarga la ISO versión 7 de CentOS Linux, disponible en: https://wiki.centos.org/Download
 
 
 2. Cree una máquina virtual en virtualbox e Instale CentOS en ella. (Instalación estándar de centOS)
 
 3. Acceda a la máquina CentOS e instale NGINX.
 
 4. Configure en VirtualBox una red solo anfitrión que le permita acceder a Nginx desde la máquina local.
 

### Dificultades encontradas en el proceso

### ¿Es apropiado o no para desplegar réplicas en un ambiente de pruebas?




[1] CentOS Project. Retrieved 2 February 2020, from https://www.centos.org/
