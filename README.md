# Desplegar dos servicos con docker swarm
## Explicación de como hacer el trabajo:
### Primero hay que crear los dockerfile de los servidores apache y node, y crear los servidores de cada uno:

Con los siguientes comandos se crean las imagenes para ambos servidores

```sh
docker build -t image_apache ./apache-datos
```
```sh
docker build -t image_node ./node-datos
```
### Luego se crea un archivo .yml para configurar los servicios:

- Se crea el archivo docker-compose.yml
- se configura las rutas, imagenes y volumenes que van a usar cada servicio

### Luego hay que configura la conexión de la base de datos:

- Para conectar el servicio de la base de datos a los demas servicios, se configuro el host de cada servicio con el nombre del servicio que contendrá a la base de datos, en este caso se llama "mysql_bal"

### Luego hay que crear los servicios con Docker Swarm:
- Para crear los servicios hay que pasarle las imagenes creadas de cada servidor a los servicios que correrán dichas imagenes
- Para desplegar los servicios se utiliza el siguiente comando: 
```sh
docker stack deploy -c docker-compose.yml services
``` 
Donde docker-compose.yml es el archivo .yml con la configuracion para el despliegue y services es el nombre de los servicios.

### Luego hay que acceder a los servicios y verificar si todo funciona:
- Para acceder al servicio de apache hay que situarse en:
```
http://localhost:8080
```
- Para acceder al servicio de node hay que situarse en:
```
http://localhost:8090
```