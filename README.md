# ArangoDB Container
## Comenzando 🚀
Descargar el archivo docker-compose.yaml y guardarlo en $HOME/username (se puede guardar en otra ubicación). Los datos JSON guardarlos en la carpeta de su preferencia.

### Pre-requisitos 📋
Instalar Docker, sustituir $Username por su nombre de usuario.
```
curl -sSL https://get.docker.com | sh
sudo apt-get update && sudo apt-get install -y docker-ce docker-compose
sudo usermod -a -G docker $Username
```
### Instalación 🔧

En la terminal ubicandose en $Home/username o el PATH de la ubicación del archivo docker-compose.yaml ejecutar lo siguiente:
```
docker-compose up -d
```
El contenedor se debe descargar e iniciar correctamente. Si presentas problemas verifica tu instalación de Docker y que hayas agregado tu usuario al grupo Docker.

## EAbrir la interfaz de ArangoDB ⚙️

En su navegador entrar a http://127.0.0.1:8529/ debe mostrarse la interfaz correctamente
