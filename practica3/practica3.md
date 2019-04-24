# Práctica 3: Balanceo de carga
    Autores: David Joaquín González-Venegas Guerra-Librero y Marina Hurtado Rosales
    Correos: davidvenegasfb@correo.ugr.es; marinahurtado@correo.ugr.es
En esta tercera práctica se configurará una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.
El problema a solucionar es la sobrecarga de los servidores. Se puede balancear
cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web, balancearemos los servidores HTTP que tenemos configurados.
 De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.
 El objetivo es obtener la siguiente red de máquinas:
 
<center>![img](https://github.com/Feiniel/SWAP/blob/master/practica3/imagenes/graficoGranjaWweb.PNG)</center>

De esta manera en esta práctica se realizarán las siguientes tareas:
- Configurar una máquina e instalar **nginx** como balanceador de carga.
- Configurar una máquina e instalar **haproxy** como balanceador de carga.
- Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.


--------------------------------------------------------------------------------------------------------------------
## Instalación y configuración de nginx como balanceador de carga

## Instalación y configuración de haproxy como balanceador de carga

## Sometimiento de la granja web a una alta carga con Apache Benchmark
