# Configuración Básica de Postfix

Después de instalar Postfix, es importante configurarlo correctamente para que pueda enviar y recibir correos electrónicos de manera eficiente y segura.

## 1. Configuración Inicial

El archivo principal de configuración de Postfix es `/etc/postfix/main.cf`. Para editarlo, usa:
```bash
sudo nano /etc/postfix/main.cf
```

Asegúrate de que las siguientes líneas estén configuradas correctamente:
```ini
myhostname = correo.ejemplo.com
mydomain = ejemplo.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8
relayhost =
smtpd_banner = $myhostname ESMTP
```  
Reemplaza `correo.ejemplo.com` y `ejemplo.com` con tu dominio real.

### Explicación de cada línea:
- **`myhostname = correo.ejemplo.com`** → Define el nombre de host del servidor de correo. Debe coincidir con el nombre de dominio completo (FQDN) del servidor.
- **`mydomain = ejemplo.com`** → Especifica el dominio principal del servidor.
- **`myorigin = $mydomain`** → Define el dominio que se utilizará como remitente en los correos salientes. Generalmente es el mismo que `mydomain`.
- **`inet_interfaces = all`** → Indica en qué interfaces de red escuchará Postfix. `all` permite conexiones desde cualquier interfaz de red disponible.
- **`inet_protocols = ipv4`** → Especifica qué protocolos de red utilizará Postfix. `ipv4` indica que solo usará direcciones IPv4.
- **`mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain`** → Lista de dominios para los cuales Postfix aceptará correos entrantes.
- **`mynetworks = 127.0.0.0/8`** → Define qué redes pueden enviar correo sin autenticación. Por defecto, solo la red local (127.0.0.1).
- **`relayhost =`** → Especifica un servidor de retransmisión para enviar correos salientes. Si se deja vacío, el correo se enviará directamente.
- **`smtpd_banner = $myhostname ESMTP`** → Configura el mensaje de bienvenida que mostrará el servidor al iniciar una sesión SMTP.

## 2. Configuración de Usuarios

Cada usuario en el sistema puede enviar correos electrónicos. Para listar los usuarios del sistema:
```bash
cat /etc/passwd | cut -d: -f1
```

Para agregar un nuevo usuario que pueda enviar correos:
```bash
sudo adduser usuario_email
```

## 3. Reiniciar el Servicio Postfix

Cada vez que realices cambios en la configuración, debes reiniciar Postfix:
```bash
sudo systemctl restart postfix
```

## 4. Prueba de Envío de Correo
Para probar el envío de un correo electrónico, usa el siguiente comando:
```bash
echo "Esto es una prueba" | mail -s "Asunto de prueba" usuario@dominio.com
```

Si el correo no llega, revisa los logs para diagnosticar el problema:
```bash
tail -f /var/log/mail.log
```

En la siguiente sección, veremos cómo configurar Postfix con autenticación y cifrado TLS para mayor seguridad.
