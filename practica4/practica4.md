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
</p>
<p align="center">
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
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c4.PNG">
</p>

Activamos el sitio default-ssl y reiniciamos apache:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c5.PNG">
</p>

Con esto funcionaría HTTPS en la máquina 1, sin embargo, como queremos poder usarlo en la granja al completo, debemos configurar el segundo servidor (M2) y el balanceador para que también acepte este tráfico (puerto 443).

### Acceso por HTTPS a M2
Para configurar HTTPS en el segundo servidor simplemente copiaremos la pareja de archivos (el .crt y el .key) que hemos generado en M1 en la carpeta /etc/apache2/ssl (la cual tenemos que crear) de la máquina M2. Para poder copiarlos en M2 primero hemos copiado la carpeta *ssl* en la carpeta *home*, y la hemos sincronizado con rsync. Posteriormente la hemos movido a donde corresponde.

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c6.PNG">
</p>
<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c7.PNG">
</p>

Una vez hecho esto, modificamos el archivo */etc/apache2/sites-available/default-ssl.conf* de la misma forma que hemos hecho con la máquina M1. Por último, debemos activar el sitio default-ssl y reiniciar apache (como hicimos en el primer servidor). 

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c8.PNG">
</p>

Una vez hecho esto comprobamos que funciona en ambas máquinas servidoras haciendo una petición a cada una desde la máquina M4:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c9.PNG">
</p>

### Acceso al balanceador (nginx) por HTTPS
 
Lo primero que hay que hacer, al igual que en el apartado anterior, es copiar los archivos de certificación en la máquina balanceadora. En este caso los situaremos en la carpeta */etc/ssl/*.

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c10.PNG">
</p>

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c11.PNG">
</p>

Después, en el balanceador nginx debemos añadir lo siguiente al archivo /etc/nginx/conf.d/default.conf y reiniciarlo:

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c12.PNG">
</p>

Una vez reiniciado, comprobamos que funciona haciéndole peticiones desde la máquina M4

<p align="center">
    <img src="https://github.com/Feiniel/SWAP/blob/master/practica4/imagenes/c13.PNG">
</p>

## Configuración del cortafuegos

Hemos configurado el cortafuegos con IPTABLES en la máquina M1, con dirección IP 192.168.1.100. Para hacer esto hemos creado un script el cual se tiene que ejecutar en el arranque del sistema. El script es el siguiente:

```
# (1) Eliminar todas las reglas (configuración limpia)
iptables -F
iptables -X
iptables -Z
iptables -t nat -F

# (2) Política por defecto: denegar todo el tráfico
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (3) Permitir cualquier acceso desde localhost (interface lo)
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# (4) Abrir el puerto 22 para permitir el acceso por SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT

# (5) Abrir los puertos HTTP (80) de servidor web
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 80 -j ACCEPT

# (6) Abrir los puertos HTTPS (443) de servidor web
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 443 -j ACCEPT
```

