# PRACTICA-6


Se procede a explicar la composición del documento yaml para la  construcción de un entorno servidor-cliente  DNS BIND9-Alpine.
El proceso se llevará a cabo para cada uno de los contenedores y de los campos asociados a cada uno de ellos 

## BIND9

-**IMAGE**:se usa la imagen _ubuntu/bind9_ vinculado al DNS BIND9

-**CONTAINER_NAME**:se le asigna el nombre al contenedor con el fin de su identificación 

-**PORTS**:se realiza un mapeo del puerto 54 del host con el puerto 54 del contenedor, tanto para los protocolos TCP y UDP

-**NETWORKS**:lleva a cabo la conexión del contenedor bind9 a la red bind9

-**VOLUMES**:los volúmenes son soluciones de permanencia para la tecnología de contenedores. Son una extensión del almacenamiento de los contenedores en el propio anfitrión.La concreción de los volúmenes a especificar son :_

		- _ ./conf:/home/daniel/compose/conf _: monta el directorio ./conf dentro del contenedor en la ruta /home/daniel/compose/conf .Aqui estaran almacenados los archivos de configuración del servidor BIND9
		
		- ./zonas:/home/jose/compose/zonas: monta el directorio ./zonas perteneciente al host en /home/daniel/compose/zonas del contenedor.Aquí estarán almacenados los datos de zona del servicio DNS 

-**RESTART**: Se establece los requisitos de actuación en caso de detención del contenedor. Se concreta el campo con _always_, habilitando el reinicio automático .


## CLIENTE 

-**CONTAINER_NAME**:identificamos el contenedor con el nombre cliente.

-**IMAGE**: Se utiliza la imagen _alpine:latest_ (distribución de Linux)

-**tty**:hace referencia al terminal de comunicación 

-**dns**:se concreta la IP asociada al servicio de DNS , en este caso el encargado de ello es el contenedor bind9.

-**networks**:permite la conexión del _cliente_ a la red _bind9_, consolidando la conexión entre los dos contenedores definidos.



## SECCIÓN DE RED


-**NETWORKS BIND**: Se define la red _bind9_ con la configuración puente.Se delimita el nombre de la red .



## UTILIZACIÓN DEL COMANDO DIG



El comando _dig_ es una herramienta empleada para la realización de consultas al sistema de nomnbres de dominio (DNS).Su propósito  principal es obtener información sobre nombres de dominio, direcciones 	IP, registros DNS y otros datos relacionados .

En primer lugar para acceder al entorno  del contenedor utilizamos el comando .

		
		`docker exec -it  nombre.contenedor`


Una vez dentro del contenedor,llevamos a cabo la actualización de repositorios y la instalación de la herramienta _dig_.Como la distribución de Linux empleada para el contenedor cliente es _Alpine_ , se hace uso del comando _apk_.


		`apk update`
		
		`apk add bind-tools`
		


Finalmente realizamos la consulta DNS  a través de la sintaxis. 


		`dig@IP`
		
		
		 			
			






