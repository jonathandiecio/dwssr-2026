# Reporte de Práctica: S01T04 Dev Containers y Entorno de Desarrollo

**Alumno:** Jonathan Diego Ignacio  
**Asignatura:** Desarrollo Web / Entornos Dev  
**Fecha:** 8 de septiembre de 2026  
**Repositorio GitHub:** https://github.com/jonathandiecio/dwssr-2026  

---

## 1. Introducción
En este reporte se documenta el proceso de configuración del entorno de desarrollo local y en la nube utilizado durante la Semana 01. Se detalla la preparación del subsistema Linux mediante WSL2, la configuración global de Git, el despliegue de contenedores de desarrollo (Dev Containers) con servicios como Node.js y MongoDB, y la vinculación final del repositorio de la materia a GitHub.

---

## 2. Preparación y Ajuste de WSL (Windows Subsystem for Linux 2)
Para contar con un entorno ejecutable Linux nativo sobre Windows sin la sobrecarga de una máquina virtual tradicional, se habilitaron las características requeridas desde PowerShell con privilegios de administrador:

* **Habilitación de WSL y la plataforma de máquina virtual:**
  `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
  `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
* **Configuración de WSL 2 e instalación de la distribución Ubuntu:**
  `wsl --set-default-version 2`
  `wsl --install -d Ubuntu`
* **Inicialización de usuario:** Se completó la creación del usuario UNIX y la contraseña de administración dentro del subsistema Ubuntu.

---

## 3. Instalación, Configuración y Primeros Comandos de Git
Se configuraron las credenciales globales del sistema de control de versiones y el editor por defecto mediante la terminal:

* **Establecer nombre de usuario y correo global:**
  `git config --global user.name "Jonathan Diecio"`
  `git config --global user.email "ignaciojonathandiego41@gmail.com"`
* **Configurar VS Code como editor por defecto:**
  `git config --global core.editor "code --wait"`

---

## 4. Configuración y Uso de Dev Containers (Codespaces / Docker)
Se estructuró el entorno virtual dentro de la carpeta `.devcontainer/` para garantizar un entorno estandarizado entre desarrolladores:

1. **Definición de archivos base:**
   * `devcontainer.json`: Especifica extensiones de VS Code y servicios.
   * `Dockerfile`: Define la imagen base de Linux/Node (`mcr.microsoft.com/devcontainers/javascript-node:24-bookworm`) e instala las herramientas CLI de MongoDB (`mongosh`).
2. **Prueba de conexión a servicios:**
   * Se inició la sesión de terminal interactiva dentro del contenedor y se ejecutó la CLI de MongoDB para verificar el servicio:
     `mongosh`
   * **Resultado de ejecución:**
     `test> show dbs`
     `admin   40.00 KiB`
     `config  60.00 KiB`
     `local   72.00 KiB`

---

## 5. Creación y Publicación del Repositorio
Se creó la estructura del proyecto localmente y se sincronizó con la plataforma remota GitHub mediante GitHub CLI (`gh`):

`git init`
`git add .`
`git commit -m "feat: initial commit with devcontainers setup"`
`git branch -M main`
`gh repo create dwssr-2026 --public --source=. --remote=origin --push`
