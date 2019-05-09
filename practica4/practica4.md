# Práctica 4: Asegurar la granja web
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es
El objetivo de esta práctica es configurar todos los aspectos relativos a la seguridad de la granja web ya creada.
Hay que llevar a cabo las siguientes tareas:
- Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe copiar al resto de máquinas servidoras y al balanceador de carga. Se debe configurar nginx adecuadamente para aceptar y balancear correctamente tanto el tráfico HTTP como el HTTPS.
- Configurar las reglas del cortafuegos con IPTABLES en uno de los servidores web finales para asegurarlo, permitiendo el acceso por los puertos de HTTP y HTTPS a dicho servidor. Como se indica, esta configuración se hará en una de las máquinas servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las reglas del cortafuegos que se ejecute en el arranque del sistema.

-------------------------------------------------------------------------------------

## Instalar un certificado SSL autofirmado para configurar el acceso por HTTPS

Vamos a generar un certificado SSL autofirmado en la máquina 1, la cual tiene Ubuntu Server instalado. Para ello lo primero que hacemos es activar el módulo SSL de Apache:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c1.PNG">
    
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c2.PNG">
</p>

Pasamos a generar los certificados. En este paso se nos pide una serie de datos para configurar el dominio:

<p align="center">
   <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c3.PNG">
</p>

Una vez hecho esto, editamos el archivo de configuración del sitio default-ssl con el siguiente comando:

```
$ vi /etc/apache2/sites-available/default-ssl.conf
```
Modificamos el archivo agregando estas lineas debajo de donde pone SSLEngine on:

```
SSLCertificateFile /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/3.png">
</p>

Activamos el sitio default-ssl y reiniciamos apache:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/4.png">
</p>

Con esto funcionaría HTTPS en la máquina 1, sin embargo, como queremos que la granja al completo nos permita usar el HTTPS, debemos configurar el segundo servidor (M2) y el balanceador para que también acepte este tráfico (puerto 443).
Para configurar HTTPS en el segundo servidor simplemente copiaremos la pareja de archivos (el .crt y el .key) que hemos generado en M1 en la carpeta /etc/apache2/ssl (la cual tenemos que crear) de la máquina M2. 


Para hacer esto, copiaremos la pareja de archivos (el .crt y el .key) a todas las máquinas de la granja web. No vamos a generar nuevos certificados, sino que copiaremos los archivos apache.crt y apache.key que generamos en el primer servidor en el paso anterior en el otro servidor y el balanceador. Para ello hemos usado 

![img](https://github.com/davidvenegasfb/SWAP/blob/master/practica4/imagenes/5.png)

En el segundo servidor debemos activar el sitio default-ssl y reiniciar apache (como
hicimos en el primer servidor). 

![img](https://github.com/davidvenegasfb/SWAP/blob/master/practica4/imagenes/6.png)

En el balanceador pondremos la ruta a la carpeta donde hayamos copiado el apache.crt y el apache.key. Después, en el balanceador nginx debemos añadir lo siguiente al archivo /etc/nginx/conf.d/default.conf y reiniciarlo:

![img](https://github.com/davidvenegasfb/SWAP/blob/master/practica4/imagenes/7.png)

## Configuración del cortafuegos

Creamos un script con las órdenes para una configuración básica de un servidor web y lo ejecutamos:

![img](https://github.com/davidvenegasfb/SWAP/blob/master/practica4/imagenes/8.png)

