# Introducción a SMTP y Postfix

El protocolo SMTP (Simple Mail Transfer Protocol) es el estándar para el envío de correos electrónicos en Internet. Define cómo los servidores de correo electrónico intercambian mensajes y permite la transmisión confiable de correo electrónico.

## ¿Qué es SMTP?
SMTP es un protocolo de nivel de aplicación basado en texto que permite la comunicación entre servidores de correo para el envío y recepción de mensajes. Fue desarrollado en los años 80 y se encuentra definido en la especificación RFC 5321.

### Características principales de SMTP
- **Protocolo basado en texto:** Los comandos y respuestas se transmiten en texto plano.
- **Modelo cliente-servidor:** Un cliente SMTP inicia la comunicación con un servidor SMTP.
- **Reenvío y entrega:** SMTP solo gestiona la transmisión del correo, dejando el almacenamiento a otros protocolos como POP3 o IMAP.
- **Seguridad y autenticación:** Se pueden usar extensiones como STARTTLS para cifrar las comunicaciones.

### Puertos utilizados por SMTP
SMTP utiliza diferentes puertos dependiendo de la función y nivel de seguridad requerido:
- **Puerto 25:** Usado para la comunicación entre servidores de correo (MTA a MTA). Generalmente bloqueado por los proveedores de Internet para evitar el envío de spam desde clientes finales.
- **Puerto 587:** Utilizado para el envío de correos desde clientes (MUA a MTA) con autenticación y cifrado STARTTLS.
- **Puerto 465:** Antiguamente reservado para SMTP sobre SSL/TLS. Actualmente se recomienda el uso del puerto 587 con STARTTLS en lugar de este.

### Principales comandos SMTP
| Comando | Descripción |
|---------|-------------|
| HELO/EHLO | Identifica el cliente al servidor |
| MAIL FROM | Especifica el remitente del correo |
| RCPT TO | Define el destinatario del correo |
| DATA | Inicia el cuerpo del mensaje |
| QUIT | Termina la sesión |

### Flujo de un correo SMTP
1. El cliente abre una conexión con el servidor SMTP en el puerto 25, 587 o 465.
2. Se identifica con `EHLO` o `HELO`.
3. Especifica el remitente del mensaje con `MAIL FROM`.
4. Especifica uno o más destinatarios con `RCPT TO`.
5. Envía el cuerpo del mensaje con `DATA`.
6. Finaliza la sesión con `QUIT`.

## ¿Qué es Postfix?
Postfix es un agente de transferencia de correo (MTA) ampliamente utilizado en servidores Linux. Su objetivo es enrutar y entregar correo electrónico de manera eficiente y segura, proporcionando herramientas de configuración avanzadas y seguridad reforzada.

## ¿Por qué usar Postfix?
- **Fiabilidad:** Postfix es conocido por su estabilidad y rendimiento.
- **Seguridad:** Soporta autenticación y cifrado TLS para proteger los correos electrónicos.
- **Flexibilidad:** Se puede integrar con múltiples bases de datos y sistemas de autenticación.
- **Facilidad de configuración:** Comparado con otros MTAs, Postfix tiene una configuración más sencilla y bien documentada.

Esta guía cubrirá la instalación, configuración básica y avanzada, así como medidas de seguridad recomendadas para un servidor de correo basado en Postfix.
