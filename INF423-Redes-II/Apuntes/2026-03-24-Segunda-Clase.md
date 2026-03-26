
📡 DHCP (Dynamic Host Configuration Protocol)

DHCP es un protocolo de nivel de aplicación que permite asignar automáticamente direcciones IP y otros parámetros de red a los dispositivos (clientes).

Se convirtió en un estándar porque facilita la administración de redes sin necesidad de configurar manualmente cada equipo.

⚙️ Funcionamiento básico

DHCP trabaja bajo un modelo de:

Servidor DHCP → Asigna direcciones IP
Cliente DHCP → Solicita una dirección IP

👉 Todo servicio DHCP necesita estos dos roles.

✅ Beneficios del protocolo DHCP
✔️ Asignación automática de direcciones IP
✔️ Evita errores de configuración manual
✔️ Reduce el tiempo de administración de red
✔️ Permite reutilizar direcciones IP (mediante concesiones)
✔️ Facilita la conexión de nuevos dispositivos
✔️ Centraliza la gestión de la red
✔️ Evita conflictos de IP duplicadas
📄 Servicio de asignación

DHCP funciona mediante concesiones (leases), que son contratos temporales de uso de una IP.

🔹 Tipos de servicio
Generación de concesión
Se asigna una nueva IP a un cliente que no tiene servicio.
Renovación de concesión
Un cliente que ya tiene IP solicita extender su contrato.
🔄 Proceso de generación de concesión (4 pasos)

Este proceso también se conoce como DORA:

DHCP Discover (Descubrimiento)
El cliente inicia y busca servidores DHCP (mensaje de difusión).
DHCP Offer (Oferta)
El servidor responde ofreciendo una dirección IP.
DHCP Request (Solicitud)
El cliente solicita usar la IP ofrecida.
DHCP Acknowledgment (Confirmación)
El servidor confirma y asigna la IP oficialmente.
❓ ¿Cómo se comunica el cliente si no tiene IP?

El cliente utiliza mensajes de difusión (broadcast) para comunicarse en la red y encontrar un servidor DHCP.

🔁 Proceso de renovación de concesión
El cliente solicita renovar su IP
El servidor acepta y extiende el tiempo de uso

👉 Este proceso puede ser automático antes de que expire la concesión.

🖥️ Instalación del servicio DHCP (Paso a paso)
🔹 Requisitos iniciales
Tener permisos de administrador
Configurar una IP fija en el servidor
🔹 Configuración de red previa
Ir a Centro de redes y recursos compartidos
Entrar a Propiedades de red
Seleccionar la tarjeta Ethernet
Asignar una IP manual (ejemplo: 192.168.1.X)
🔹 Verificación de conexión
Abrir CMD

Ejecutar:

ipconfig

→ Verifica IP y estado de conexión

Probar conexión con:

ping 192.168.1.X
Probar entre máquina virtual y máquina real:
Desde la VM → hacer ping a la real
Desde la real → hacer ping a la VM
⚠️ Problemas comunes
Firewall activado puede bloquear conexión
👉 Solución:
Ir a Panel de control → Sistema y seguridad → Firewall
Activar/desactivar según prueba (privada y pública)
🔹 Instalación del rol DHCP (Windows Server)
Abrir Administrador del servidor
Seleccionar:
“Agregar roles y características”
Elegir:
Instalación basada en roles o características
Seleccionar el servidor
Marcar:
✅ Servidor DHCP
Aceptar agregar características adicionales
Continuar con Siguiente
Dar clic en Instalar
🔹 Configuración del DHCP
Ir a:
Herramientas → DHCP
Expandir:
DHCP → IPv4
Crear nuevo ámbito:
Click derecho → Nuevo ámbito
Configuración del ámbito:
Nombre del ámbito
Rango de direcciones IP (misma red)
Máscara de subred
Exclusiones (opcional)
Tiempo de concesión
Configuración opcional (puede hacerse después)
Finalizar y activar:
Click derecho en el ámbito → Activar

💻 Comandos importantes
🔹 Ver información completa
ipconfig /all .- 
Muestra a detalle las configuraciones
Muestra:

Dirección IP
Servidor DHCP
Fecha de expiración de concesión

🔹 Liberar IP
ipconfig /release
Suelta la concesion 
El cliente suelta la IP
La tarjeta queda sin dirección

🔹 Renovar IP
ipconfig /renew
Solicita una nueva IP al servidor DHCP, busca un nuevo contrato

 🛠️ Administración del DHCP (Herramientas)

Una vez instalado el servicio DHCP, podemos administrar y visualizar información desde:

👉 Herramientas → DHCP

Luego seguimos esta ruta:

DHCP → IPv4 → (tu ámbito configurado)
📦 Conjunto de direcciones (Address Pool)

Aquí puedes ver:

🔹 Direcciones distribuidas → IPs que el servidor puede asignar
🔹 Direcciones excluidas → IPs que NO se asignarán

👉 Las exclusiones se usan cuando quieres reservar manualmente ciertas IP (por ejemplo para servidores o impresoras).

📄 Concesiones de direcciones (Address Leases)

Aquí puedes ver:

✔️ Los dispositivos que tienen IP asignada
✔️ El “contrato” activo (concesión)
✔️ Tiempo de expiración

👉 Desde aquí puedes:

❌ Eliminar una concesión
→ El cliente perderá su IP
→ Tendrá que solicitar una nueva
📌 Reservas (Reservations)

Las reservas permiten que un dispositivo siempre tenga la misma dirección IP.

👉 Es útil para:

Impresoras
Servidores
Equipos importantes
⚠️ Requisitos para hacer una reserva

Para crear una reserva debes cumplir:

✔️ La IP debe estar dentro del rango del ámbito (direcciones distribuidas)
✔️ Necesitas identificar el dispositivo
🧾 Datos necesarios para una reserva

Para crear una reserva necesitas:

🔹 Dirección IP que se va a asignar
🔹 Dirección MAC (dirección física del equipo)
🔹 Nombre de la reserva (opcional pero recomendado)
🔍 ¿Cómo obtener la dirección MAC?

Desde el cliente:

Abrir CMD
Escribir:
ipconfig /all
Buscar:
👉 Dirección física (Physical Address)

Ese es el dato que necesitas para la reserva.

🧠 Ejemplo práctico

Si tienes:

IP: 192.168.1.50
MAC: 00-1A-2B-3C-4D-5E

👉 Esa IP siempre será asignada a ese dispositivo.

