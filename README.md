# Taller6-AREP

# LABORATORIO MODULARIZACIÓN CON VIRTUALIZACIÓN: DOCKER Y A AWS

1. El servicio MongoDB es una instancia de MongoDB corriendo en un container de docker en una máquina virtual de EC2
2. LogService es un servicio REST que recibe una cadena, la almacena en la base de datos y responde en un objeto JSON con las 10 ultimas cadenas almacenadas en la base de datos y la fecha en que fueron almacenadas.
3. La aplicación web APP-LB-RoundRobin está compuesta por un cliente web y al menos un servicio REST. El cliente web tiene un campo y un botón y cada vez que el usuario envía un mensaje, este se lo envía al servicio REST y actualiza la pantalla con la información que este le regresa en formato JSON. El servicio REST recibe la cadena e implementa un algoritmo de balanceo de cargas de Round Robin, delegando el procesamiento del mensaje y el retorno de la respuesta a cada una de las tres instancias del servicio LogService.

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/ff3bfd10-35ba-43c3-9a8e-c0f687e2efda)
	

### Instalación

Para descargar el proyecto ejecute:  

  ```
  git clone https://github.com/CrisRod8/Taller6-AREP.git
  ```

## Documentación
Para generar la documentación se debe ejecutar en la ubicación de los respectivos servicios:  

  ```
  mvn javadoc:javadoc
  ```

Esta quedará en la carpeta target/site/apidocs de cada servicio:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/32c8068e-0b64-43df-8453-5738c082a6f8)  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/e079be12-31ff-4c2f-adc1-10e5e3fa52c2)  

## DESARROLLO  

Creamos los archivos Dockerfile para la creación de imagenes y contenedores.  

Logroundrobin:  

  ```
  docker build --tag roundrobin-java .
  ```

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/a60c04b7-33fd-443c-89dd-30ae94f1129d)

Logservice:  

  ```
  docker build --tag logservices .
  ```

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/6e691e8f-f285-4993-bd98-3fec60e9d8ce)  

Imagen en docker desktop:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/7070269b-9013-4601-b637-2300fde5eeef)  

Se crea el archivo docker-file.compose y ejecutamos:

  ```
  docker-compose up -d
  ```

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/b4685f64-a013-475a-813a-af2a9405ce03)

Verificamos en Docker los contenedores creados:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/951670db-5518-4ba4-9cee-a56e1437a758)  

Entramos a la página:  

  ```
  http://localhost:35000/index.html
  ```

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/8592f66d-aabd-4161-a42a-05f3af607342)

### AWS:

Para que funcione en AWS debemos subir las imagenes a repositorios de Docker hub.

Vinculamos las imagenes:  

  ```
  docker tag roundrobin-java cristianrodri/logroundrobin
  ```
  ```
  docker tag logservices cristianrodri/logservice
  ```

Lo subimos a los respectivos respositorios:  

  ```
  docker push cristianrodri/logroundrobin
  ```
  ```
  docker push cristianrodri/logservice
  ```

Modificamos el docker compose:

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/98eb7fc0-95dc-43df-8985-c2b04bb05f4d)  

Entramos a AWS y lanzamos la instancia:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/286ba6fe-52db-434a-b63f-8e3b6f5f9784)  

Configuramos los puertos:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/63c05a6e-8c77-4596-9e52-b5838b4e52b5)  

Hacemos la conexion con la máquina:

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/bf6dd9ea-c2dc-4123-8676-88085d8e41f9)  

Descargamos Docker, git y Docker-compose:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/1df21606-7847-4d09-aeaa-a95b820ede0d)  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/7cca09d7-b2b4-4cf7-beec-171a052bfbf2)  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/11ea1a30-16c3-4197-b9a7-3393c208c6c1)  

Clonamos nuestro repositorio de github y ejecutamos el docker-compose:  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/a671887b-e445-4cae-a7d3-3c16bbeb989a)  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/25429484-d84c-40d7-8884-0da7501c1d26)  

Finalmente entramos a la siguiente pagina: http://ec2-107-23-51-58.compute-1.amazonaws.com:35000  

![image](https://github.com/CrisRod8/Taller6-AREP/assets/111186898/fa03ef54-e86f-466a-8ebe-99c5d7a620e5)  

Video de ejecución:  

https://youtu.be/-iHoAQJOO7Y

