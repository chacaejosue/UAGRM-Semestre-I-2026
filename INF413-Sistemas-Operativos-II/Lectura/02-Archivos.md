# 📁 Archivos y Sistemas de Archivos

## 🎯 Introducción

Todas las aplicaciones necesitan almacenar y recuperar información de forma persistente y segura.

### Problemas Identificados

1. **Espacio pequeño en Memoria Principal**: Capacidad limitada
2. **Memoria volátil**: Los datos se pierden al apagar
3. **Compartir información**: Múltiples procesos necesitan acceder a los mismos datos

### Requisitos para la Solución

- Almacenar **gran cantidad de información**
- **Persistencia** de datos tras terminación de procesos
- **Acceso concurrente** de múltiples procesos

### Solución: Sistema de Archivos

- Almacenamiento en dispositivos magnéticos (discos duros u otros) en unidades llamadas **archivos**
- Información **persistente**
- **Gestión centralizada** por parte del sistema operativo

> **Sistema de Archivos**: Parte del SO encargada de administrar archivos, su estructura, nombres, acceso, protección e implementación.

---

## 📝 1. Nombres de Archivo

### Concepto

- Los archivos tienen asignado un **nombre único** a través del cual los usuarios se refieren a ellos
- Cuando un proceso crea un archivo, le asigna un nombre que **persiste incluso después de que termina el proceso**
- Las reglas de nomenclatura varían según el SO

### Características Principales

| Aspecto | Características |
|--------|-----------------|
| **Longitud** | 8 a 255 caracteres (según SO) |
| **Mayúsculas** | Algunos SO las distinguen, otros no |
| **Símbolos** | Permitidos o restringidos según SO |

### Convenciones de Nombres por SO

| Sistema | Reglas |
|---------|--------|
| **MS-DOS** | Máximo 8 caracteres + extensión de 3. No distingue mayúsculas |
| **UNIX** | Máximo 256 caracteres. Distingue mayúsculas/minúsculas. Múltiples extensiones permitidas (ej: `image.tar.Z`) |
| **Windows NT** | Máximo 256 caracteres. No distingue mayúsculas/minúsculas. Múltiples extensiones permitidas |

---

## 📋 2. Estructura de Archivos

Los archivos pueden tener diferentes estructuras internas:

| Estructura | Descripción |
|-----------|-------------|
| **Sin estructura** | Sucesión de bytes sin formato específico |
| **Registros de longitud fija** | Datos organizados en registros de tamaño constante |
| **Registros de longitud variable** | Datos con estructura variable |

---

## 🗂️ 3. Tipos de Archivos

### En Sistemas UNIX

1. **Archivos Regulares o Normales**
   - Generalmente **ASCII** o **binarios**
   - El más común

2. **Directorios**
   - Archivos de sistema que mantienen la estructura del sistema de archivos

3. **Archivos Especiales de Caracteres**
   - Relacionados con operaciones de entrada/salida de dispositivos basados en caracteres

4. **Archivos Especiales de Bloques**
   - Usados para acceder a discos

### I. Archivos Normales

#### ASCII
- Líneas de texto que terminan con retorno de carro, salto de línea o ambos
- **Se pueden mostrar e imprimir** tal como son
- **Se pueden editar** con cualquier editor de texto

#### Binarios
- **No son comprensibles** si se muestran directamente (aparecen como "basura")
- Tienen **estructura interna específica** conocida solo por el programa que los usa
- Ejemplos: ejecutables, DLL, BMP, etc.

---

## 🔄 4. Acceso a Archivos

### Evolución del Acceso

**Inicialmente**: Acceso secuencial (cintas magnéticas)
- Los datos se leían en orden

**Con discos**: Acceso aleatorio
- Posibilidad de leer bytes o registros sin orden
- Esencial para bases de datos

### Métodos de Especificar Posición de Lectura

1. **READ con posición**: Cada operación READ especifica dónde comenzar a leer en el archivo
2. **SEEK + READ secuencial**: Operación especial **SEEK** establece la posición inicial, luego lectura secuencial

### Distinción Histórica

- **SO de Mainframe**: Definían el tipo de acceso al crear el archivo (secuencial vs. aleatorio)
- **SO Modernos**: No hacen distinción - todos los archivos son aleatorios

---

## 📌 5. Atributos de Archivos

Todo archivo posee atributos además de nombre y datos. Estos varían según el SO.

### Tabla de Atributos

| Atributo | Significado |
|----------|-------------|
| **Protección** | Quién puede acceder al archivo y cómo |
| **Contraseña** | Clave necesaria para acceso |
| **Creador** | ID de la persona que creó el archivo |
| **Dueño** | Propietario actual del archivo |
| **Indicador Read-Only** | 0: lectura/escritura; 1: solo lectura |
| **Indicador Oculto** | 0: normal; 1: no mostrar en listados |
| **Indicador Sistema** | 0: normal; 1: archivo de sistema |
| **Indicador Archivado** | 0: ya respaldado; 1: debe respaldarse |
| **Indicador ASCII/Binario** | 0: ASCII; 1: binario |
| **Indicador Acceso Aleatorio** | 0: solo secuencial; 1: aleatorio |
| **Indicador Temporal** | 0: normal; 1: borrar al terminar proceso |
| **Indicador Bloqueo** | 0: sin bloqueo; ≠0: bloqueado |
| **Longitud de Registro** | Número de bytes en un registro |
| **Posición de Clave** | Distancia a la clave dentro del registro |
| **Longitud de Clave** | Número de bytes en el campo clave |
| **Hora de Creación** | Fecha y hora de creación |
| **Hora de Último Acceso** | Última vez que se accedió |
| **Hora de Último Cambio** | Última vez que se modificó |
| **Tamaño Actual** | Número de bytes en el archivo |
| **Tamaño Máximo** | Máximo de bytes que puede alcanzar |

---

## ⚙️ 6. Operaciones con Archivos

### Operaciones Fundamentales

| Operación | Descripción |
|-----------|-------------|
| **Create** | Crear archivo sin datos iniciales |
| **Delete** | Borrar archivo para liberar espacio en disco |
| **Open** | Abrir archivo. El SO obtiene atributos y direcciones de disco, los coloca en memoria para acceso rápido |
| **Close** | Cerrar archivo para liberar espacio en tablas de memoria principal |
| **Read** | Leer datos desde posición actual. Especificar cantidad de bytes y buffer destino |
| **Write** | Escribir datos en posición actual (aumenta tamaño o sobrescribe) |
| **Append** | Forma restringida de write: solo agrega al final del archivo |
| **Seek** | En archivos aleatorios: establecer posición del apuntador de archivo |
| **Get Attributes** | Obtener atributos (útil para herramientas como make) |
| **Set Attributes** | Establecer o modificar atributos del archivo |
| **Rename** | Cambiar nombre del archivo |

---

## 📂 II. Directorios

Los sistemas de archivos con grandes volúmenes de información requieren mecanismos para estructurar y organizar los datos.

### II.1 Sistemas de Directorios de un Solo Nivel

**Características:**
- Un único directorio raíz contiene todos los archivos
- Solo funciona para sistemas monousuarios

**Ejemplo:**
```
Directorio Raíz: [A] [B] [C]
```

**Ventajas:**
- Simplicidad
- Rápida búsqueda

**Desventajas:**
- ❌ Múltiples usuarios pueden usar el mismo nombre para sus archivos → Conflictos de nombres

---

### II.2 Sistemas de Directorios de Dos Niveles

**Solución:** Agregar un nivel para cada usuario

**Estructura:**
```
Directorio Raíz
├── Usuario A: [AA] [B]
├── Usuario B: 
└── Usuario C: [CCC]
```

**Mejoras:**
- ✅ No hay conflictos con nombres de archivos entre usuarios
- Requiere **sistema de Login** para identificar al usuario

**Ejemplo:**
```
Open("x")           → Busca en directorio del usuario actual
Open("lrodas/x")    → Busca en directorio del usuario "lrodas"
```

---

### II.3 Sistema de Directorios Jerárquicos

**Problema anterior:** No satisface usuarios con gran número de archivos

**Solución:** Crear una **jerarquía general (árbol de directorios)**

**Ventajas:**
- ✅ Usuarios pueden agrupar archivos de forma lógica
- ✅ Escalable para grandes volúmenes
- ✅ Estructura intuitiva

**Estructura:**
```
Directorio Raíz
├── /usuarios
│   ├── /user1
│   │   ├── /documentos
│   │   └── /correo
│   └── /user2
├── /sistemas
└── /datos
```

---

### II.4 Nombres de Ruta

Para el sistema jerárquico se necesita un mecanismo para especificar ubicaciones de archivos.

#### Dos métodos principales:

**1. Nombre de Ruta Absoluta**
- Camino completo desde el directorio raíz hasta el archivo
- Ejemplos:
  - **Unix/Linux**: `/usr/ast/correo`
  - **Windows**: `C:\Users\Documents\archivo.txt`

**2. Nombre de Ruta Relativa**
- Se usa el concepto de **directorio de trabajo** (directorio actual)
- Ejemplo: Si el directorio actual es `/usr/ast/`:
  - Ruta absoluta: `/usr/ast/correo`
  - Ruta relativa: `correo`

#### Características Importantes:

- **Cada proceso** tiene su propio directorio de trabajo
  - No afecta a otros procesos

- **Entradas especiales** en cada directorio:
  - `.` → Directorio actual
  - `..` → Directorio padre

#### Buenas Prácticas:
- Los procedimientos de biblioteca casi nunca cambian el directorio de trabajo
- Si lo hacen, siempre lo restauran al terminar

---

## 🗄️ Sistema de Archivos

### Concepto Fundamental

Para mejorar la eficiencia, la transferencia de información entre memoria y discos se realiza en unidades denominadas **bloques**.

### Características:

- **Bloque**: Formado por uno o varios sectores de disco
- **Tamaño de sector**: Típicamente **512 bytes**
- **Tamaño de bloque**: Variable según SO (generalmente múltiplo de sectores)

### Dos Problemas de Diseño:

1. **Definir** cómo el sistema de archivos aparece al usuario
   - Estructura lógica visible
   - Interfaz de usuario

2. **Implementar** algoritmos y estructuras de datos para mapear el sistema lógico en dispositivos físicos
   - Gestión de bloques
   - Mapeo físico en disco

### Niveles de Control

```
┌─────────────────────────────────┐
│   Aplicaciones de Usuario       │
├─────────────────────────────────┤
│   Sistema de Archivos Lógico    │
├─────────────────────────────────┤
│  Control E/S                    │
│  - Manejadores de dispositivo   │
│    (Device Drivers)             │
│  - Manejadores de interrupciones│
│    (Interrupt Handlers)         │
├─────────────────────────────────┤
│   Dispositivos Físicos          │
│   (Discos magnéticos)           │
└─────────────────────────────────┘
```

El **nivel de control de entrada/salida** se compone de:
- **Device Drivers**: Manejadores de dispositivo
- **Interrupt Handlers**: Manejadores de interrupciones

---

**Fin del documento**
