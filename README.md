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
      - 8529:8529
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

## Abrir la interfaz de ArangoDB ⚙️

En su navegador entrar a http://127.0.0.1:8529/ debe mostrarse la interfaz correctamente.

***Nota*** La importación de datos se hará en clase.

---
⌨️ con ❤️ por [Jaime Rodríguez](https://github.com/rpjosejaime) 😊

