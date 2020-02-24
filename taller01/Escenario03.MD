# Taller 01

## Car Lewis Álvarez Cossio - A00310516
## Andrés Felipe Aguirre Aguilar - 
## Juan Sebastián Quintero Yoshioka - A00310448

## Infraestructura como código
## Objetivos:
- Comprender las motivaciones de la automatización de infraestructura.
- Realizar de forma autónoma el aprovisionamiento automático de infraestructura.
- Diagnosticar y ejecutar de forma autónoma las acciones necesarias para lograr infraestructuras estables.

## Escenario 03 (Para hacer en casa y entregar en 15 días)

En este escenario se hará uso de lo aprendido anteriormente para implementar una aplicación web que haga uso de una base de datos, el sistema debe permitir insertar y listar datos de una tabla en la base de datos. La aplicación debe ser desplegada en un servidor web y la base de datos en un servidor aparte.

## Pre Requisitos

- VirtualBox
- Vagrant
- Ansible

## Actividades

1. Primero, porcedemos a crear en local la aplicación. 

Para la base de datos, decidimos utilizar MongoDB, que es una base de datos no relacional orientada a documentos. Esto quiere decir que en lugar de guardar los datos en registros, guarda los datos en documentos. Estos documentos son almacenados en BSON, que es una representación binaria de JSON [1] 

Para la aplicación web, se desea utilizar Node JS, el cual es un entorno de ejecución para JavaScript construido con el motor de JavaScript V8 de Chrome. [2]

Para realizar la aplicación, nos basamos en el siguiente video: https://youtu.be/3J925fRl_UE

2. Ahora procedemos a realizar la configuración y aprovisionamiento de la máquina virtual con Vagrant y Ansible respectivamente.

 a. Primero, en la carpeta raiz ejecutamos el comando <code> ssh-keygen </code> para generar un par de llaves pública y privada para poder, posteriormente, realizar SSH desde una máquina a otra:
 
  ![ssh-keygen](/taller01/imagenes/ssh-keygen.png)
  
  Esto nos creará los siguientes archivos:
  
  ![Archivos al ejecutar ssh-keygen](/taller01/imagenes/Archivosssh.png)
  
  b. Luego, realizamos la configuración de la máquina virtual tanto del servidor web como de la base de datos, esto se debe guardar en un archivo Vagrantfile:
  
  ![Vagrantfile](/taller01/imagenes/Vagrantfile.png)
  
  c. Se debe especificar el inventario de los hosts:
  
  ![Inventarios hosts](/taller01/imagenes/InventarioHosts.png)
  
  d. EL archivo de configuración de Ansible:
  
  ![Ansible cfg](/taller01/imagenes/ansiblecfg.png)
  
  e. Por último, se debe realizar el aprovisionamiento de ambas máquinas virtuales:
  
  Aprovisionamiento máquina virtual de la base de datos:
  
  ![Database Ansible](/taller01/imagenes/DatabaseAnsible.png)
  
  - Primero, se instala mongodb.
  - Luego, se copia el archivo de configuración de la base de datos, esto es necesario para especificar que se pueda acceder desde máquinas remotas a la base de datos.
  - Las siguientes dos tareas se realizan para crear y dar permisos a la carpeta donde se guardarán los datos.
  - Se puede reiniciar el servidor o bien, detener el servicio de mongodb y volverlo a ejecutar.
  
  Aprovisionamiento máquina virtual del servidor web:
  
  ![Webserver Ansible](/taller01/imagenes/WebserverAnsible.png)
  
  - En las primeras tres tareas se instala Node JS.
  - Luego, se instala Git y se copia el repositorio donde se encuentra la aplicación web.
  - Por último, se ejecuta la aplicación mediante el gestor de paquetes npm.
  
  f. Se ejecuta el comando <code> vagrant up </code>
  
  ![Vagrant UP](/taller01/imagenes/vagrantup.png)
  
  Al final, veremos el puerto por el que está escuchando el servidor web y mensaje de conexión exitosa a la base de datos:
  
  ![Estado](/taller01/imagenes/estado.png)
  
  
 g. Para verificar el funcionaiento, entramos en el navegador a la siguiente dirección: <code> 192.168.56.2:3000 </code>, nos aparecerá lo siguiente:
 
 ![App web inicial](/taller01/imagenes/AppWebInicial.png)
 
 Ejemplo de insersión:
 
 ![Ejemplo](/taller01/imagenes/EjemploNodeJS.png)
 
 Por último, verificamos que se pueda realizar SSH a un servidor desde otro servidor:
 
 ![SSH ServerB](/taller01/imagenes/sshServerB.png)
  
[1] https://www.genbeta.com/desarrollo/mongodb-que-es-como-funciona-y-cuando-podemos-usarlo-o-no <br>
[2] https://nodejs.org/es/
