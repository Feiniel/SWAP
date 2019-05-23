
# Práctica 5: Replicación de bases de datos MySQL
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es

El objetivo de esta práctica es configurar todos los aspectos relativos a la seguridad de la granja web ya creada.
Hay que llevar a cabo las siguientes tareas:
- Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe copiar al resto de máquinas servidoras y al balanceador de carga. Se debe configurar nginx adecuadamente para aceptar y balancear correctamente tanto el tráfico HTTP como el HTTPS.
- Configurar las reglas del cortafuegos con IPTABLES en uno de los servidores web finales para asegurarlo, permitiendo el acceso por los puertos de HTTP y HTTPS a dicho servidor. Como se indica, esta configuración se hará en una de las máquinas servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las reglas del cortafuegos que se ejecute en el arranque del sistema.

-------------------------------------------------------------------------------------

## Crear un tar con ficheros locales y copiarlos en un equipo remoto

Vamos a crear un tar.gz con un directorio de un equipo y dejarlo en otro mediante ssh, mediante el comando:
>tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/0.0.png">
</p>

## Crear una BD e insertar datos

Vamos a crear una BD en MySQL e insertar algunos datos. Así tendremos datos con los cuales hacer las copias de seguridad:

Entramos en la interfaz de la línea de comandos de MySQL con:
>mysql -uroot -p

Creamos la base de datos contactos con:
>create database contactos;

Declaramaos que vamos a usar dicha tabla con:
>use contactos;

Creamos la tabla datos con:
>create table datos(nombre varchar(100),tlf int);

Mostramos todas las tabla con:
>show tables;

Insertamos una linea de datos en nuestra tabla con:
>insert into datos(nombre,tlf) values ("pepe",95834987);

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/0.png">
</p>

Aquí podemos ver como como podemos hacer consultas sql como:
>select * from datos;

O que nos diga los tipos de datos de la tabla:
>describe datos;

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/1.png">
</p>


## Replicar una BD MySQL con mysqldump

Vamos a usar mysqldump para generar copias de seguridad de BD.

Podemos ver todas las opciones disponibles con el comando:
>mysqldump --help

En primer lugar debemos de tener en cuenta que los datos pueden estar actualizándose constantemente en el servidor de BD principal. En este caso, antes de hacer la copia de seguridad en el archivo .SQL debemos evitar que se acceda a la BD para cambiar nada. Para ello haremos:

>FLUSH TABLES WITH READ LOCK;

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/2.png">
</p>

Ahora ya podemos usar mysqldump para guardar los datos.

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/3.png">
</p>

Si hacemos un vim de contactos.sql veremos:

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/4.png">
</p>

Y desbloqueamos por último las tablas:

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/5.png">
</p>

Ahora vamos a la máquina 2 para copiar el archivo .SQL con todos los datos salvados desde la máquina principal con el comando:
>scp 192.168.1.100/tmp/ejemplodb.sql /tmp/

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/7.png">
</p>

y habremos copiado desde la máquina principal (1) a la máquina secundaria (2) los
datos que hay almacenados en la BD.

Con el archivo de copia de seguridad en el esclavo ya podemos importar la BD completa en el MySQL. Para ello, en un primer paso creamos la BD, con el comando:
>CREATE DATABASE ‘contactos’;

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/6.png">
</p>

En un segundo paso restauramos los datos contenidos en la BD (se crearán las
tablas en el proceso), con el comando:

>mysql -u root -p contactos < /tmp/contactos.sql

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/8.png">
</p>

## 5.4 Replicación de BD mediante una configuración maestro-esclavo

Lo primero que debemos hacer es la configuración de mysql del maestro, para lo que vamos a editar /etc/mysql/my.cnf con varias configuraciones tal y como vemos con:
>vim /etc/mysql/my.cnf

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/7.png">
</p>

Y reiniciamos el servicio con:
>/etc/init.d/mysql restart

<p align="center">
    <img src="https://github.com/davidvenegasfb/SWAP/blob/master/practica5/8.png">
</p>
