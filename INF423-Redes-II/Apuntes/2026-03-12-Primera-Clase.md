# Capa de Transporte

Las aplicaciones generan datos, que son enviados a la red y viajan por cada una de las capas.

## Funciones
- **Primera función**: Actuar como intermediario entre las aplicaciones y la red, enviando los datos. Las aplicaciones utilizan la capa de transporte.
- **Segunda función**: Encargarse de procesos como el control de flujo y congestión.
- **Última función**: Asegurarse de que el mensaje llegue a su destino sin errores.

Al encargarse del servicio de transporte, hay dos opciones principales para enviar los datos:
1. **TCP** (Transmission Control Protocol)
2. **UDP** (User Datagram Protocol)

Estos se diferencian en la calidad del servicio.

### ¿Cómo se define la calidad en redes?
- **Equilibrar costo-beneficio**:
  - **Costo**: Cantidad de datos (overhead).
  - **Beneficio**: Certeza de que los datos lleguen correctamente, con total exito.

De estas opciones, una ofrece más calidad que la otra:
- Opción con calidad: Requiere más recursos, pero garantiza fiabilidad.
- Opción sin calidad: Envío rápido, pero sin garantías.

**TCP = Calidad (fiable)**; **UDP = No calidad (rápido)**.

## Primera Diferencia entre TCP y UDP

- **Protocolos orientados a conexión** → TCP:
  1. Establecer conexión entre origen y destino (handshake de tres vías).
  2. Supervisar la conexión en todo momento.
  3. Cerrar la conexión al finalizar.
  
  **Ejemplo**: Llamadas normales de WhatsApp (requieren conexión estable).

- **Protocolos no orientados a conexión** → UDP:
  - Envío directo de mensajes sin establecer conexión.
  
  **Ejemplo**: Mensajes de texto tradicionales (SMS).

### Ventajas y Desventajas
- **TCP**:
  - Ventajas: Entrega fiable, ordenada y sin errores; control de flujo y congestión.
  - Desventajas: Mayor overhead, más lento.
- **UDP**:
  - Ventajas: Rápido, bajo overhead, ideal para tiempo real.
  - Desventajas: No garantiza entrega ni orden.

### Usos Comunes
- **TCP**: Navegación web (HTTP/HTTPS), FTP, SMTP.
- **UDP**: Streaming (video/audio), juegos, DNS.

## Puertos

Es un número de identificación (16 bits, de 0 a 65535). Las aplicaciones tienen un número de puerto, como 80 (origen) - 80 (destino), clave para recibir y enviar datos.

Además, las aplicaciones necesitan un **socket**, que es la combinación de DIRECCIÓN IP + NÚMERO DE PUERTO.

**Ejemplo**: 192.168.0.15:21 (5 números en total; sockets se usan para establecer conexiones).

### Rangos de Puertos
- **Bien conocidos (0-1023)**: Reservados (ej. 80: HTTP, 443: HTTPS).
- **Registrados (1024-49151)**: Aplicaciones específicas.
- **Dinámicos (49152-65535)**: Asignados por el SO.

## ID de Conexión

Número único formado por socket origen + socket destino:
 IP.PUERTO_ORIGEN + IP.PUERTO_DESTINO (10 números en total, 10 numeros forman la cadena de conexion ).

Un equipo puede tener múltiples conexiones simultáneas. Para manejar esto sin confusión, se usan multiplexación y desmultiplexación.

## 1. Multiplexación

Proceso donde la capa de transporte combina datos de múltiples aplicaciones en un flujo único hacia la red, identificando cada uno por puertos.

### Gráfico de Multiplexación
```
+-------------+     +-------------+     +-----------------+
| Aplicación  | --> | Aplicación  | --> | Capa de         |
| 1 (Puerto   |     | 2 (Puerto   |     | Transporte      |
| 80)         |     | 443)        |     |                 |
+-------------+     +-------------+     | Combina datos   |
                                        | en un flujo     |
+-------------+     +-------------+     | único --> Red   |
| Aplicación  | --> | Aplicación  | --> +-----------------+
| 3 (Puerto   |     | 4 (Puerto   |
| 22)         |     | 53)         |
+-------------+     +-------------+
```

Esto permite compartir el canal de red eficientemente.

## 2. Desmultiplexación

Proceso inverso: la capa de transporte recibe el flujo de la red y lo distribuye a la aplicación correcta usando puertos.

### Gráfico de Desmultiplexación
```
Red --> +-----------------+     +-------------+
        | Capa de         | --> | Aplicación  |
        | Transporte      |     | 1 (Puerto   |
        |                 |     | 80)         |
        | Distribuye      |     +-------------+
        | datos por       |
        | puertos         |     +-------------+
        +-----------------+ --> | Aplicación  |
                                | 2 (Puerto   |
                                | 443)        |
                                +-------------+
                                +-------------+
                                | Aplicación  |
                                | 3 (Puerto   |
                                | 22)         |
                                +-------------+
```

Ejemplo: Un paquete llega con puerto destino 80, se dirige a la aplicación web.

## Otros Aspectos de la Capa de Transporte

### Control de Flujo
Evita que el emisor sobrecargue al receptor. En TCP, usa ventana deslizante.

### Control de Congestión
Gestiona congestión en la red (ej. algoritmo de Tahoe en TCP).

### Comparación con Otras Capas
- **Capa de Red**: Enrutamiento entre hosts.
- **Capa de Transporte**: Comunicación entre procesos.

### Errores y Recuperación
- TCP: Reenvía paquetes perdidos.
- UDP: No hay recuperación; depende de la aplicación.

Esta versión mejora la estructura, corrige errores gramaticales y añade gráficos detallados para mayor claridad.

