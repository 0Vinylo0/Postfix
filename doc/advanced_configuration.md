# Configuración Avanzada de Postfix

En esta sección, abordaremos configuraciones avanzadas para mejorar la seguridad y el rendimiento de Postfix.

## 1. Configuración de Autenticación y Cifrado TLS

Para asegurar la transmisión de correos electrónicos, es recomendable habilitar la autenticación SMTP y el cifrado TLS.

### 1.1. Habilitar la autenticación SASL
Edita el archivo de configuración principal:
```bash
sudo nano /etc/postfix/main.cf
```

Añade o modifica las siguientes líneas:
```ini
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_tls_security_level = may
smtpd_tls_cert_file = /etc/ssl/certs/mailserver.pem
smtpd_tls_key_file = /etc/ssl/private/mailserver.key
```

Reinicia Postfix para aplicar los cambios:
```bash
sudo systemctl restart postfix
```

## 2. Configuración de Relay con Autenticación
Si deseas utilizar un relay para enviar correos a través de un servidor externo, agrega en `/etc/postfix/main.cf`:
```ini
relayhost = [smtp.ejemplo.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_tls_security_level = encrypt
```

Crea el archivo `/etc/postfix/sasl_passwd` y añade las credenciales del relay:
```plaintext
[smtp.ejemplo.com]:587 usuario:contraseña
```

Guarda los cambios y protege el archivo:
```bash
sudo chmod 600 /etc/postfix/sasl_passwd
sudo postmap /etc/postfix/sasl_passwd
```

Reinicia Postfix:
```bash
sudo systemctl restart postfix
```

## 3. Configuración de Restricciones y Seguridad
Para evitar el abuso del servidor SMTP, se pueden definir restricciones adicionales en `/etc/postfix/main.cf`:
```ini
smtpd_helo_required = yes
smtpd_helo_restrictions = reject_invalid_hostname, reject_non_fqdn_hostname
smtpd_recipient_restrictions = reject_unauth_destination
smtpd_sender_restrictions = reject_unknown_sender_domain
```

Reinicia Postfix:
```bash
sudo systemctl restart postfix
```

Con estas configuraciones avanzadas, Postfix será más seguro y confiable. En la siguiente sección, veremos cómo implementar listas negras y filtrado de spam.
