<h1 align="center">OpenCode en Docker</h1>
<h3>Cómo instalar OpenCode en Docker: La IA que programa por ti. Integración con Api NVIDIA Container Gemini Gratis 🐳🚀</h3>
<p align="center">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/OpenCode-8080FF?style=for-the-badge" alt="OpenCode">
  <img src="https://img.shields.io/badge/ARM64-Soporte-orange?style=for-the-badge" alt="ARM64">
  <img src="https://img.shields.io/badge/NVIDIA-GPU-green?style=for-the-badge&logo=nvidia&logoColor=white" alt="NVIDIA">
</p>

<p align="center">
  <strong>Despliegue de OpenCode en Docker con soporte ARM64 (Raspberry Pi) y conexión a NVIDIA.</strong>
</p>

---

## 📋  Tabla de Contenidos

- [Visión General](#-visión-general)
- [Características](#-características)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación Rápida](#-instalación-rápida)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Seguridad](#-seguridad)
- [Solución de Problemas](#-solución-de-problemas)
- [Enlaces Útiles](#-enlaces-útiles)

---

## 🎯  Visión General

Este proyecto proporciona una configuración Dockerizada para ejecutar **OpenCode**, un asistente de desarrollo impulsado por IA de código abierto. La configuración está optimizada para arquit
ecturas **ARM64** (Raspberry Pi 4/5, Apple Silicon) yendo más allá al permitir la conexión con las APIs de **NVIDIA** para potenciar la inferencia de modelos de lenguaje de forma gratuita.

---

## ⭐  Características

- 🏗️  **Arquitectura Multi-Plataforma**: Soporte nativo para **ARM64** y x86_64.
- 🧠  **Integración NVIDIA**: Conexión con NVIDIA NIM usando modelos como Nemotron sin coste.
- 🔒  **Autenticación Opcional**: Configuración sencilla de usuario y contraseña para el servidor web.
- 📂  **Persistencia de Datos**: Volúmenes para conservar la configuración, el historial y el espacio de trabajo.
- ⚙️  **Configuración Flexible**: Control total del entorno mediante archivo ".env".
- 🚀  **Lista para Usar**: Un solo comando para levantar el servicio con Docker Compose.

---

## 🛠️  Requisitos Previos

- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- **(Opcional, pero recomendado)** Una cuenta en NVIDIA AI para obtener la API Key gratuita.

---

## 🚀  Instalación Rápida

1.  **Clona este repositorio e ingresa al directorio:**

    ```bash
    git clone <URL_DEL_REPOSITORIO>
    cd opencode
    ```

2.  **Prepara el archivo de configuración:**

    Copia el archivo de ejemplo ".env" y llena los valores necesarios.

    ```bash
    cp .env.example .env
    nano .env
    ```

3.  **Inicia el contenedor:**

    ```bash
    docker compose up -d
    ```

4.  (Después del primer arranque, llena los datos de login de opencode con un: **docker logs opencode** y configura el modelo)

5.  **Accede a la aplicación:**

    Abre tu navegador en: `http://localhost:4096`

---

## ⚙️  Configuración

La configuración se gestiona a través del archivo ".env`` y el ``compose.yml`. A continuación se detallan las variables más importantes:

### Puerto del Servidor Web

| Variable | Descripción | Valor por Defecto |
| :--- | :--- | :--- |
| `OPENCODE_PORT` | Puerto expuesto en el host | `4096` |

### Autenticación del Servidor (Opcional) ✨

Si quieres proteger el acceso a la interfaz web, descomenta y configura estas variables tanto en .env como en compose.yml:

| Variable | Descripción | Ejemplo |
| :--- | :--- | :--- |
| `OPENCODE_SERVER_USERNAME` | Usuario para acceso HTTP | `opencode` |
| `OPENCODE_SERVER_PASSWORD` | Contraseña para acceso HTTP | `password` |

> 🔒  **Recomendación:** Activar esto si tu instancia es accesible desde internet o una red no segura.

### Proveedor NVIDIA (API Key)

Para usar los modelos gratuitos de NVIDIA, registra tu cuenta y genera una API Key en [build.nvidia.com](https://build.nvidia.com). Substitute tu clave real:

```dotenv
NVIDIA_API_KEY=TU-API-KEY
```

> 🚀  Modelos como Nemotron son potentes, gratuitos y perfectos para tareas de programación.

---

## 📂  Estructura del Proyecto

opencode/

├── compose.yml              # Definición de servicios Docker (OpenCode y GPU)

├── .env.example             # Plantilla de variables de entorno

├── .env                     # Variables de entorno reales (ignorado en git)

├── README.md                # Este archivo

├── workspace/               # Tu espacio de trabajo

├── data/ #Datos persistentes de la aplicación y modelos locales

└── config/ #Configuraciones del contenedor OpenCode


---

## 🔐  Seguridad

-   **API Keys:** Asegúrate de que el archivo `.env` nunca se suba a tu repositorio. Ya está incluido en el `.gitignore` (si lo creas).
-   **Autenticación:** Considera siempre habilitar `OPENCODE_SERVER_USERNAME` y `OPENCODE_SERVER_PASSWORD` si tu instancia está expuesta.
-   **Actualizaciones:** Mantén la imagen actualizada ejecutando:
    ```bash
    docker compose pull && docker compose up -d
    ```

---

## 🛠️  Solución de Problemas

### Error de conexión con NVIDIA

Si OpenCode no puede conectarse a los modelos, verifica que tu `NVIDIA_API_KEY` sea válida y esté correctamente copiada de tu cuenta de [build.nvidia.com](https://build.nvidia.com).

### Permisos en Raspberry Pi

Si experimentas problemas de escritura en los volúmenes, puedes necesitar ajustar los permisos del directorio local:

```bash
sudo chown -R $USER:$USER workspace/ data/ config/
sudo chmod a+rwx workspace/ data/ config/
```

### Verificar logs del contenedor

```bash
docker compose logs -f opencode
```

---

## 🔗  Enlaces Útiles

-   **DockerHub (Imagen):** [smanx/opencode](https://hub.docker.com/r/smanx/opencode)
-   **OpenCode GitHub:** [github.com/opencode](https://github.com/opencode) (o su repositorio principal)
-   **NVIDIA NIM:** [build.nvidia.com](https://build.nvidia.com)
-   **Docker Docs:** [docker.com/get-started](https://www.docker.com/get-started)

---

<p align="center">Hecho con ❤️ y OpenCode  para la comunidad de desarrolladores ARM64</p>
