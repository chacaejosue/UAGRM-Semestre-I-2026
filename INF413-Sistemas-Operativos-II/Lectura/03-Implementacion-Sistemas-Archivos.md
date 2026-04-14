# 🛠 Implementación de Sistemas de Archivos

## 📌 Contenido
1. Organización del sistema de archivos
2. Implementación de archivos
3. Implementación de directorios
4. Archivos compartidos
5. Administración de espacio en discos

---
(esto forma parte de los apuntes, quiero que combines ambas cosas, como una especie de unión, colocando lo que en mis apuntes están con lo que hemos hecho aquí en este documento, que ha sido scado directamente de un documento pdf.
esta sección es de posibles preguntas que nos dictó el docente 
Cuál es la prime tarea que va a realizar el sistema de archivos cuando se le asigne una unidad? 
1 Dividir todo espacio de la particion en bloques pequeños de igual tamaño. Se le conoce como bloques
Cuál es el objetivo?
- Mejorar la eficiendcia de la transferencia de informacion entre memoria y disco
De qué tamaño los bloques? 
mínimo 1 por lo general más de 1 sector del disco duro
Qué tamaño tenía un sector del disco duro? 
512 bytes

Para el sistema de archivos su unidad mínima es 1 bloque, para el disco duro es 1 sector.
Cuántoss bloques habrían o resultarían en una particion?
- No se puede calcular, está en función al espacio de la particion y del taamaño del bloque definido por el Sistema de archivos

2 Darle una forma
bloque de arranque, superbloque, adm espacio libre, nodo1, dir raiz
*hacerlo en forma de diagrama*
este paso se le conoce como formatear, dar formato, formatear no es borrar, su efecto causa que se borren los datos
3 Llevar el control de qué bloques se le han asignado a qué archivos
Administracion de archivos, esta es la tarea más importante
esta tercer tarea la vamos a estudiar en clases

Metodos de asignacion, es el espacio quese les va a dar a qué archivo
contigua, asigna bloques contiguos, juntos, bloques libres

ventaja, solo necesita 2 datos, el numero del bloque del primer bloque y cuantos bloques ocupa
implementacion sencilla

tabla
archivo empieza tamaño
a         1        4
b         5        3
c         6        5   

excelente desempeño de lectura
excelente velicidad de acceso porque todo está junto
desventaja
fragmentacion intercalacion de espacios ocupados y libres y esos libres no se pueden usar a veces, porque el espacio libre disponible no es suficiente para esa tarea de esa aplicacion
solamente este metodo se podria implementar para dvd/cd, en otras unidades no

asignacion por lista enlazada
consiste en que cada bloque viene a ser como un nodo
*diagrama de un nodo que dentro tenga un dato y tenga el enlace*
|dato|  | enlace----

cada bloque se convierte en un nodo, su primer byte se separa para el enlace, para apuntar a otro bloque los bloqes tienen un id unico

no es necesario que los bloques estén juntos, solo se necesita 1 solo dato, en qué bloque inicia

ventajas
aqui ya s epuee usar un bloque libre
no se desperdicia espacio
 no necesita 2 datos, solo necesita 1
 desventajas
 lo malo es que no hay accceso aleatorio para acceder al bloque n hay que leer los anteriores n-1
 la cantidad de datos almacenados ya no es potencia de 2
 
 2 ^n-1 operacion para que el procesador lo resuenva 2^n, si le dieramos esto le duplicamos el trabajo al procesador)
## 1. 🗂 Organización del Sistema de Archivos

- Cada partición define su propio **sistema de archivos (S.A.)**
- El S.A. especifica cómo está organizada la partición física

### 🌐 Estructura básica de un S.A.

```
Particiones
├─ MBR
└─ Bloque de arranque / Superbloque
   ├─ Administración de espacio libre
   ├─ Nodos-i
   ├─ Directorio raíz
   └─ Archivos y directorios
```

#### Componentes clave

- **Superbloque**:
  - Parámetros clave (número mágico, conteo de bloques, etc.)
  - Se carga en memoria al arrancar el sistema

- **Administración de bloques libres**:
  - Mapas de bits o listas enlazadas

- **Nodos-i (i-nodes)**:
  - Arreglo con una estructura por archivo que almacena atributos y direcciones de bloques

- **Directorio raíz**:
  - Contiene entrada de nivel más alto del S.A.

---

## 2. 📁 Implementación de Archivos

### 🔑 Control de bloques asignados
Para almacenar un archivo, el sistema debe saber qué bloques del disco están asignados al archivo. Existen varios métodos.

### a) Asignación contigua

- Se asignan bloques consecutivos a cada archivo.
- Ejemplo: un archivo de 50 KB obtiene 50 bloques contiguos de 1 KB.

**Ventajas**
- Implementación sencilla (solo se necesitan dos números: dirección inicial y número de bloques)
- Excelente rendimiento de lectura (todo puede leerse en una sola operación)

**Desventaja**
- Fragmentación con el tiempo

> 🟢 Uso típico: medios de sólo lectura como CD-ROM o DVD.

### b) Asignación por lista enlazada

- Cada bloque apunta al siguiente usando su primera palabra.
- El directorio guarda la dirección del primer bloque.

**Ventajas**
- Se pueden usar todos los bloques del disco
- No se desperdicia espacio por fragmentación

**Desventajas**
- Acceso aleatorio lento (para llegar al bloque *n* hay que leer los *n‑1* anteriores)
- El espacio de datos útil disminuye por el apuntador en cada bloque

### c) Asignación por lista enlazada con tabla en memoria

- El apuntador se almacena en una tabla en memoria en lugar de dentro del bloque.

**Desventajas**
- La tabla completa debe residir en memoria.
- Ejemplo: disco de 20 GB con bloques de 1 KB → 20 millones de entradas → 60‑80 MB de RAM.

### d) Nodos-i (índice)

- Cada archivo tiene un **nodo-i** que contiene atributos y direcciones de bloques.
- Permite localizar rápidamente todos los bloques de un archivo.

**Ventajas**
- El nodo-i solo se carga en memoria cuando el archivo está abierto.
- Si hay *k* archivos abiertos y cada nodo ocupa *n* bytes, la memoria usada es *k × n* bytes.

**Desventaja**
- Si el archivo crece más allá de las direcciones directas del nodo-i, se necesita una solución adicional.
  - Solución común: reservar la última entrada para apuntar a un bloque que contenga más direcciones (bloque indirecto).

---

## 3. 📂 Implementación de Directorios

- La ruta de directorios es necesaria para abrir un archivo.
- El directorio debe contener la información para localizar bloques en el disco.
- Su función principal: **asociar nombre de archivo con los datos necesarios para ubicarlo**.

### ¿Dónde guardar los atributos?

- En la entrada del directorio
- O en el nodo-i del archivo

---

## 4. 🔗 Archivos Compartidos

*(El contenido original no detalló esta sección, se puede desarrollar si se dispone de más información.)*

---

## 5. 💽 Administración de Espacio en Disco

### Estrategias de almacenamiento

1. **Asignar _n_ bytes consecutivos**
   - Problema: si el archivo crece puede ser necesario moverlo (desplazamiento costoso).

2. **Bloques de tamaño fijo** (opción usada por la mayoría de SO modernos)
   - El archivo se divide en bloques no necesariamente adyacentes.

### 🧠 Tamaño del bloque

- Unidad de asignación muy grande → desperdicio por fragmentación interna
- Unidad muy pequeña → muchos bloques por archivo, más operaciones de E/S
- Ideal: equilibrio entre búsqueda, demora rotacional y transferencia

### 🔎 Registro de bloques libres

- **Lista enlazada**: cada bloque libre contiene punteros a otros bloques libres.
- **Mapa de bits**: un bit por bloque; 1 = libre, 0 = ocupado (o viceversa).
  - Requiere suficiente memoria para almacenar el mapa completo.

---

## 🛡️ Fiabilidad del S.A.

### Protección y respaldo

- Realizar respaldos regulares para proteger los datos
- Pérdidas pueden ocurrir por hardware, software o eventos externos

### Manejo de bloques defectuosos

- **Solución de software**:
  - Crear un archivo que liste los bloques defectuosos
  - Eliminar esos bloques de la lista de libres
  - No permitir lectura/escritura de bloques defectuosos

---

## 🔄 Consistencia del S.A.

- El S.A. se lee, modifica y escribe de vuelta. Un fallo en medio puede causar inconsistencia.
- Bloques críticos:
  - Nodos-i
  - Directorios
  - Lista de bloques libres

### Herramientas de verificación

- Utilitarios que verifican consistencia al arrancar o a pedido
- Pueden operar a nivel de bloques o archivos
- Utilizan dos tablas:
  - Tabla de bloques en uso
  - Tabla de bloques libres

### Ejemplos de inconsistencias

| Problema | Síntomas | Solución |
|----------|----------|----------|
| Bloque no aparece en ninguna tabla | "Bloque faltante" | Añadirlo a la lista de libres |
| Bloque duplicado en tabla de libres | Ocurre en listas enlazadas | Depurar la tabla de libres |
| Bloque duplicado en tabla de usados | Puede pertenecer a dos archivos o dos veces al mismo | Copiar contenido a bloque libre, actualizar tablas, notificar al usuario |
| Bloque en ambas tablas (libre y usado) | Inconsistencia grave | Eliminarlo de la tabla de libres |

---

## 🚀 Desempeño del S.A.

- Discos son mucho más lentos que la memoria (ms vs ns)
- **Objetivo**: reducir accesos a disco

### 🧱 Bloque caché / buffer

- Colección de bloques lógicos almacenados en memoria
- Permite ocultar la latencia de disco (
*del francés* "cacher": ocultar)

---

**Fin del documento**
