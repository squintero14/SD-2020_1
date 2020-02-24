# Taller 01

## Car Lewis Álvarez Cossio - A00310516
## Andrés Felipe Aguirre Aguilar - 
## Juan Sebastián Quintero Yoshioka - A00310448

## Infraestructura como código
## Objetivos:
- Comprender las motivaciones de la automatización de infraestructura.
- Realizar de forma autónoma el aprovisionamiento automático de infraestructura.
- Diagnosticar y ejecutar de forma autónoma las acciones necesarias para lograr infraestructuras estables.

## Escenario 02 (sesión en clase)

Con el fin de probar una aplicación web, se requieren montar dos servidores con CentOS 8.1: en al primero se ejecutará el servidor web NGINX y en el segundo un servidor de PostgreSQL

## Pre Requisitos

- VirtualBox
- Vagrant
- Ansible

## Actividades

1. Con acompañamiento del profesor elabore la creación y provisionamiento de la máquina virtual para la base de datos.

Nota: para realizar este escenario se decidió utilizar Ubuntu.

Con el acompañamiento del profesor e investgiando, se creó y aprovisionó la máquina virtual para la base de datos. Para ello, es necesario crear los siguientes archivos:

![Archivos](/taller01/imagenes/Archivos.png)

- Dentro del archivo playbooks/server.yml se realizará el aprovisionamiento de la máquina virtual.
- En el archivo ansible.cfg iría lo siguiente:
  <code> [defaults] </code> <br>
  <code> hostfile = hosts </code> <br>
  <code> host_key_checking = False </code>
- En el archivo hosts se especifica una lista o grupo de listas de los hosts en los cuales Ansible realizará el aprovisionamiento.

2. Realice la conexión via SSH a la máquina virtual (con acompañamiento del profesor)
3. Destruya y reconstruya la máquina virtual de la BD (con acompañamiento del profesor).
4. A partir del conocimiento anterior cree y provisione la máquina virtual para el servidor web, recuerde que el servidor web sea acessible desde la máquina local.

Dificultades encontradas en el proceso.
Escriba en máximo 3 párrafos por qué esta forma de crear ambiente de pruebas puede ser apropiado (o inapropiado) para desplegar réplicas de este ambiente.
