# Examen 3 - Sistemas Distribuidos

## Integrantes
- Juan David Bolaños - A00077464
- Andrés Zapata - A00077512

## 0. Sobre el proyecto

Este proyecto consta de un aplicativo Python que levanta un API Rest (que usa el estándar OpenAPI) con servicios que permiten responder a peticiones HTTP GET, POST, y DELETE y también de FrontEnds (Para enviar peticiones y testear la salud de los componentes) manufacturados en el Framework de Javascript Vue. Todo lo anterior separado y distribuido dentro de contenedores de Docker mediante Docker Compose.

La siguiente tabla muestra cada servicio en su respectivo contenedor, junto a la dirección y puerto, para este proyecto los puertos fueron especificados al momento del desliegue, mientras que las direcciones IP fueron brindadas automáticamente por Docker Compose.

Servidor | Descripción | Dirección IP | Puerto mapeado
-------- | ----------- | ------------ | --------------
Flask App  | Back end (API) | 172.18.0.2 | 5050
Vue App | Front end | 172.18.0.3 | 6060 | 
Health App | Monitor | 172.18.0.4  | 7070 |

Para poder desplegar los micro servicios es necesario ejecutar el siguiente comando:

~~~
    sudo docker compose-up -d
    sudo docker compose-up ps
~~~

Los anteriores comandos son los encargados de realizar el aprovisionamiento de los servicios y su respectivo despliegue. Al ejecutarlos debe aparecer lo siguiente para garantizar que la aplicación se ejecutó con éxito.

[Alt text](images/compose_ps.png?raw=true "Docker Compose PS")

Para acceder a los servicios se debe ingresar a las siguiente rutas:

* BACK END: http://172.18.0.2:5050/ui/
* FRONT END: http://172.18.0.3/
* MONITOR: http://172.18.0.4/

La siguiente captura muestra el back end en ejecución mediante una interaz provista por swagger, desde aquí se pueden realizar peticiones HTTP al API.

[Alt text](images/flask_app.png?raw=true "Docker Compose PS")


## 1. Despliegue mediante Docker Compose

Para esto, se requiere tener previamente instalado Docker y Docker-compose, los cuales permiten el aprovisionamiento de los contenedores donde se leventarán los diferentes módulos que conforman la aplicación, así como su respectivo despliegue. Para esto, es necesario unicamente configurar un archivo llamado *docker-compose.yml* en el cual se definen los servicios que serán desplegados, es decir, los contenedores que se crearán, para cada servicio se debe definir su imagen, su nombre, los puertos por el cual podrá ser accesible y sus dependencias a otros servicios. 

En este archivo se definen los tres servicios que conforman la aplicación, estos son el servidor flask que contiene el back end mediante una API, el servidor front que permite realizar peticiones HTTP al servidor mediante una interfaz web y un segundo servidor web que hará el trabajo de un monitor de salud de los demás servicios. Más adelante se especifíca en detalle cada servicio. El *docker-compose.yml* puede verse a continuación.

[Alt text](images/compose.png?raw=true "Docker Compose")


## 2. Aprovisionamiento mediante Docker




sudo docker build -t flask_img .
sudo docker run -v -d -p 5050:5050 --name flask_app flask_img
sudo docker ps -a
sudo docker kill flask_app
sudo docker rm flask_app
sudo docker rmi flask_img

sudo docker compose-up -d
sudo docker exec -ti vue_app hostname -i
sudo docker exec -ti health_app hostname -i

https://mherman.org/blog/dockerizing-a-vue-app/
