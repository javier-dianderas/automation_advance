# Proyectos de automatización n8n

En este repositorio se muestran distintos ejemplos de automatizaciones en n8n.

## Instalación de cloudflared

1. Instalar Cloudflare via winget con el siguiente comando en powershell: winget install --id Cloudflare.cloudflared.
2. Iniciar sesión con una cuenta gratuita creada en Cloudflare con el siguiente comando: cloudflared tunnel login.
3. Solicitar una url pública con el siguiente comando: cloudflared tunnel --url http://localhost:5678.
4. Copiar la url pública generada en la consola de comandos. Por ejemplo: https://beautifully-interpretation-geography-trinity.trycloudflare.com/.

## Instalación de n8n

Existen muchas formas de instalar n8n, a continuación mostraremos la instalación mediante una instancia de docker desktop.

1. Descargar Docker Desktop para Windows en el siguiente enlace: https://docs.docker.com/desktop/setup/install/windows-install/.
2. Instalar Docker Desktop con la configuración por defecto.
3. Crear la carpeta n8n en cual quier ruta del sistema, por ejemplo D:\docker y dentro de ella crear las carpetas n8n_data y n8n_files.
4. Dentro de la carpeta n8n crear el archivo docker-compose.yml con el siguiente contenido (modificando WEBHOOK_URL con la url pública generada por cloudflared):

services:
n8n:
image: docker.n8n.io/n8nio/n8n
container_name: n8n

    ports:
      - "5678:5678"

    environment:
      - N8N_HOST=localhost
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - TZ=America/Lima
      - WEBHOOK_URL=https://beautifully-interpretation-geography-trinity.trycloudflare.com/

    volumes:
      - ./n8n_data:/home/node/.n8n
      - ./n8n_files:/home/node/.n8n-files

    restart: unless-stopped

5. Abrir powershell y navegar a la ruta D:\docker\n8n. Luego ejecutar el comando: docker compose up -d.
6. Navegar a la url pública generada por cloudflared: https://beautifully-interpretation-geography-trinity.trycloudflare.com/.
7. Crear una cuenta e iniciar sesión en n8n.

## Instalación de checkpoint1_javier_dianderas.json

1. Crear un nuevo workflow en n8n.
2. Copiar el contenido del archivo checkpoint1_javier_dianderas.json en el diseñador del workflow.
3. Ajustar las credenciales de las cuentas de Gmail y Google Sheets para correr el ejemplo.
4. Ejecutar el workflow
