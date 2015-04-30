**Práctica 4:** Comprobar el rendimiento de servidores web
==================

- Realizado por:
	+ Juan Antonio Velasco Gómez
	+ Miguel Sánchez Maldonado

    
    
Nuestro objetivo será analizar el rendimiento de servidores, es decir de nuestra granja web, pero usaremos
programas de línea de comandos que sobrecarguen lo menos posible las máqunas que estamos usando.

Usaremos *Apache Benchmark* y *Siege*

Como hay diferentes números de procesos en cada instante y la red dependiendo del momento puede estar más o menos 
cargada, haremos varias ejecciones y los resultados en media.
    
1. Rendimiento de servidores con **Apache Benchmark**
------------------

Para el rendimiento de un servidor web desde una terminal ejecutamos 

	ab -n 1000 -c 10 http://www.example.com/test.html
    
Con esta orden hemos indicado al Benchmark solicitar la pagina http://www.example.com/test.html 1000 veces concurrentemente de 10 en 10.
Aunque esto no muestra el uso de un usuario habitualmente porque estamos pidiendo el mismo recurso repetidamente.

Nosotros vamos a crear una página web y la colocamos en el directorio del espacio web de los servidores finales

	<html>
	<head>
	<title>prueba</title>
	</head>
	<body>
	Archivo con el que vamos a realizar la prueba
	</body>
	</html>
    
La URL es <http://maquina.com/prueba.html>
Y ahora veamos el rendimiento:
:solicitamos 1000 veces la página concurrentemente de 5 en 5
 
	ab -n 1000 -c 5 http://www.maquina.com/prueba.html
    
![Captura 1](images/)

2. Rendimiento de servidores con **Siege**
------------------

Una utilidad mediente linea de comando , una de las diferencias Siege con Benchmark será que podemos realizar test aa URLs diferentes.

    Opcion | Resultado 
    -- | -- 
    /siege -b -t60S -v URL | Ejecutamos los test sin pausas y comprobamos rendimiento general 
    /siege -t60S -v URL | Un segundo de pausa entre las diferentes peticione 
    -t60S | Para indicar el tiempo exacto de ejecucion en este caso 60 segundo 
     
![Captura 2](images/)


