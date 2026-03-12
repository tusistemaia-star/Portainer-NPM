# Portainer y Nginx Proxy Manager (Docker Compose)

Este repositorio contiene la configuración en `docker-compose.yml` para desplegar fácilmente **Portainer** (gestión visual de Docker) y **Nginx Proxy Manager** (gestión de proxies inversos y certificados SSL gratuitos con Let's Encrypt) en un servidor VPS usando Docker.

## 📋 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado en tu servidor (VPS):

- **Docker:** Motor de contenedores.
- **Docker Compose:** Herramienta para definir y ejecutar aplicaciones Docker multi-contenedor.

## 🚀 Instalación y Despliegue

1. Clona este repositorio en tu servidor:

   ```bash
   git clone https://github.com/tusistemaia-star/Portainer-Nginx-Proxy-Manager.git
   ```

2. Accede al directorio del proyecto clonado:

   ```bash
   cd Portainer-Nginx-Proxy-Manager
   ```

3. Levanta los servicios en segundo plano usando Docker Compose:

   ```bash
   docker compose up -d
   ```

## ⚙️ Acceso a los Servicios

Una vez que los contenedores estén corriendo, podrás acceder a los paneles de administración utilizando la dirección IP de tu VPS y los puertos correspondientes:

### 1. Portainer (Panel de Administración de Docker)

- **URL de acceso:** `https://<IP_DE_TU_VPS>:9443`
  - *Nota: Accede siempre mediante `https://`. La primera vez tu navegador te mostrará una advertencia de seguridad (certificado auto-firmado), debes ignorarla y proceder.*
- **Configuración Inicial:** En el primer acceso, se te pedirá que crees un usuario administrador y establezcas una contraseña segura para tu entorno de gestion de Docker.

### 2. Nginx Proxy Manager (Gestión de Dominios y SSL)

- **URL de acceso:** `http://<IP_DE_TU_VPS>:81`
- **Configuración Inicial:** Inicia sesión con las credenciales por defecto. Te pedirá que cambies estos datos inmediatamente:
  - **Email (por defecto):** `admin@example.com`
  - **Contraseña (por defecto):** `changeme`

## 📦 Puertos Abiertos en el Servidor

Para que estos servicios funcionen correctamente, tu VPS y/o firewall deben tener los siguientes puertos abiertos:

| Puerto | Protocolo | Descripción |
|---|---|---|
| **80** | TCP | Tráfico HTTP público (Nginx Proxy Manager) |
| **443** | TCP | Tráfico HTTPS público (Nginx Proxy Manager) |
| **81** | TCP | Panel de administración de Nginx Proxy Manager |
| **8000** | TCP | Puerto Edge y comunicaciones de agente de Portainer |
| **9443** | TCP | Interfaz web segura (HTTPS) de Portainer |

## 📦 Persistencia de Datos

Este archivo define volúmenes de Docker para asegurar que no pierdes tus configuraciones si los contenedores se reinician o, se detienen o se eliminan:

- `portainer_data`: Almacena la base de datos y configuración de usuarios de Portainer.
- `npm_data`: Almacena las configuraciones y bases de datos SQLite integradas de Nginx Proxy Manager.
- `npm_letsencrypt`: Almacena los certificados SSL gratuitos generados automáticamente por Let's Encrypt para tus dominios.
