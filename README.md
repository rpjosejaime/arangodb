# ArangoDB Container
## Comenzando 🚀
Descargar el archivo docker-compose.yaml y guardarlo en $HOME/username o (se puede guardar en otra ubicación). Los datos JSON guardarlos en la carpeta de su elección. 

***Nota*** Puedes cambiar el password por el de tu preferencia

```
version: '3'
services:
  arangodb_db_container:
    container_name: arangodb
    image: arangodb:latest
    environment:
      ARANGO_ROOT_PASSWORD: password
    ports:
      - 127.0.0.1:8529:8529
    volumes:
      - ./arangodb/arangodb_data_container:/var/lib/arangodb3
      - ./arangodb/arangodb_apps_data_container:/var/lib/arangodb3-apps
    restart: always
```

### Pre-requisitos 📋
Instalar Docker, sustituir $Username por su nombre de usuario.
```
curl -sSL https://get.docker.com | sh
sudo apt-get update && sudo apt-get install -y docker-ce docker-compose
sudo usermod -a -G docker $Username
```
### Instalación 🔧

En la terminal ubicandose en $Home/username o en la ruta del archivo docker-compose.yaml ejecutar lo siguiente:
```
docker-compose up -d
```
El contenedor se debe descargar e iniciar correctamente. Si presentas problemas verifica tu instalación de Docker y que hayas agregado tu usuario al grupo Docker.

### Abrir la interfaz de ArangoDB ⚙️

En su navegador entrar a http://127.0.0.1:8529/ debe mostrarse la interfaz correctamente.

### Redirección al puerto 80 con subdominio en NGINX 🔧
Al estar expuesto en un servidor real, es necesario asignarle un dominio/subdominio para no poner la ip, de misma manera para no abrir más puertos en el Firewall.
Para este caso se creo un nuevo archivo de configuración de Nginx ***(sites-available)***, recordar al final hacer en enlace simbolico a ***sites-enabled***. El nombre del subdominio es libre de tu elección.

Ejemplo de archivo:

```
server {
	listen 80;

	# Add index.php to the list if you are using PHP
	#index index.html index.htm index.nginx-debian.html;

	server_name arango.tudominio.com;

        location / {
            allow all;
            proxy_pass http://127.0.0.1:8529;
            #proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            #proxy_set_header X-Forwarded-Host $host:$server_port;
            #proxy_set_header X-Forwarded-Proto $scheme;
        }

}
```

## Conexión segura (HTTPS) con Let’s Encrypt 🔧
Al punto anterior ***ArangoDB*** funciona perfectamente, único detalle la comunicación entre cliente-servidor no está cifrada, esto puede provocar que alguien espíe ***(Sniffer)*** nuestra red/dispositivos y vea lo que enviamos o recibimos como lo puede ser nuestras credenciales de acceso o los datos que se envíen a las ***API's*** que creamos.

Para solucionarlo basta con usar Cerbot para generar los certificados

```
$ sudo certbot --nginx -d arango.tudominio.com 
```
Esto ejecuta certbot con el conector --nginx, usando -d para especificar los nombres sobre los cuales queremos que el certificado sea válido.

---

## Comprobación de puertos 📋
Verificar el estado del firewall
```
sudo ufw status
```
Solo debe permitir los puertos que realmente necesita que esten abiertos al exterior.
Para eliminar una regla puede usar:
```
sudo ufw status numbered
```
Se enumeraran las reglas. Para eliminar una basta con poner el número de la regla que quiere quitar.
Ejemplo:
```
sudo ufw delete 4
```
Con esto queda configurado nuestro ArangoDB con la seguridad básica.

⌨️ con ❤️ por [Jaime Rodríguez](https:resumen.rpjosejaime.com) 😊

