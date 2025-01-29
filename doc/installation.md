# Instalación de Postfix

En esta sección, veremos cómo instalar y configurar Postfix en un sistema Linux. Se proporcionarán instrucciones para Debian/Ubuntu y CentOS/RHEL.

## 1. Instalación en Debian/Ubuntu

Para instalar Postfix en sistemas basados en Debian o Ubuntu, sigue estos pasos:

### 1.1. Actualizar el sistema
```bash
sudo apt update && sudo apt upgrade -y
```

### 1.2. Instalar Postfix
```bash
sudo apt install postfix -y
```

Durante la instalación, se mostrará un menú de configuración. Selecciona:
- **Tipo de configuración:** Sitio de Internet
- **Nombre del sistema de correo:** `correo.ejemplo.com` (reemplaza con tu dominio)

## 2. Instalación en CentOS/RHEL

Para instalar Postfix en CentOS o RHEL, sigue estos pasos:

### 2.1. Actualizar el sistema
```bash
sudo yum update -y
```

### 2.2. Instalar Postfix
```bash
sudo yum install postfix -y
```

### 2.3. Habilitar y arrancar Postfix
```bash
sudo systemctl enable postfix
sudo systemctl start postfix
```

## 3. Verificación de Instalación
Para verificar que Postfix está instalado y en ejecución, usa:
```bash
systemctl status postfix
```

Si el servicio está activo y en ejecución, la instalación se ha completado correctamente.

En la siguiente sección, veremos cómo configurar Postfix para enviar y recibir correos electrónicos.
