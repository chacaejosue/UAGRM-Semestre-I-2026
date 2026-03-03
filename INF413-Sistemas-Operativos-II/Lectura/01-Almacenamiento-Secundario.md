# Almacenamiento Secundario

## 📦 Dispositivos de Almacenamiento

Los **discos duros** (HDD) son el elemento principal de la memoria secundaria de un ordenador.

### Diferencias entre Memoria Principal y Secundaria

| Característica | Memoria Principal | Memoria Secundaria |
|-----------|-------------------|-------------------|
| **Volatilidad** | Volátil | No volátil |
| **Velocidad** | Muy rápida | Menos rápida |
| **Capacidad** | Reducida | Gran capacidad |

---

## 🔧 Estructura Física de un Disco Duro

### Componentes Principales

1. **Unidad de lectura y escritura**: Cabezales magnéticos
2. **Disco**: Conjunto de componentes electrónicos y mecánicos para almacenamiento y recuperación

### Organización del Disco

- **Platos**: Pila de discos que almacenan información magnéticamente
- **Superficies magnéticas**: Cada plato tiene 2 superficies (superior e inferior)
- **Elementos magnetizables**: Millones de pequeños elementos capaces de magnetización positiva o negativa

---

## ⚙️ Funcionamiento de la Unidad

### Mecanismo de Operación

- **Cabezales**: Cada superficie magnética tiene asignado un cabezal de lectura/escritura
  - $\text{Cant. Cabezales} = \text{Cant. Platos} \times 2$

- **Desplazamiento**: El conjunto de cabezales se desplaza linealmente mediante un brazo mecánico desde el exterior hasta el interior de la pila

- **Rotación**: Los discos giran a **velocidad constante** sin parar (a diferencia de discos flexibles o CD, donde la velocidad varía según la distancia al centro)

### Operación de Lectura o Escritura

1. Desplazar los cabezales hasta la ubicación donde comienzan los datos
2. Esperar a que el primer dato que gira con los platos llegue a la posición de los cabezales
3. Leer el dato con el cabezal correspondiente

---

## 📍 Estructura Física: Pistas, Cilindros y Sectores

### Conceptos Clave

- **Cara**: Cada superficie magnética
  - $\text{Cant. Caras} = \text{Cant. Cabezales}$

- **Pista**: Anillo concéntrico en cada cara

- **Cilindro**: El mismo anillo en todos los discos de la pila

- **Sector**: División de cada pista (unidad mínima: **512 bytes**)
  - Una pista generalmente contiene entre 100 y 300 sectores

### Cálculo de Sectores

$$\text{Total de Sectores} = \text{Caras} \times \text{Pistas/Cara} \times \text{Sectores/Pista}$$

### Identificación Única de Sectores

Cada sector queda unívocamente determinado por:
- **Cabeza** (cabezal)
- **Cilindro**
- **Sector**

---

## 💾 Ejemplo Práctico: Disco Seagate ST33221A

**Especificaciones:**
- Cilindros: 6,253
- Cabezas: 16
- Sectores: 63
- Bytes por sector: 512

**Cálculos:**

$$\text{Total de Sectores} = 6,253 \times 16 \times 63 = 6,303,024 \text{ sectores}$$

$$\text{Capacidad} = 6,303,024 \times 512 \text{ bytes} = 3,227,148,288 \text{ bytes} \approx 3 \text{ GB}$$

### Numeración

- **Cabezas y cilindros**: Comienzan desde 0
- **Sectores**: Comienzan desde 1
- **Primer sector del disco**: Cabeza 0, Cilindro 0, Sector 1

---

## ⏱️ Tiempo de Acceso a los Datos

El tiempo de acceso se compone de tres componentes:

### Componentes del Tiempo de Acceso

1. **Tiempo de búsqueda**: Desplazamiento del brazo desde la posición actual hasta el cilindro deseado
   - *Este es el mayor de los tres (~10 veces más que los otros)*

2. **Tiempo de latencia**: Espera a que el sector deseado llegue bajo los cabezales

3. **Tiempo de transmisión**: Lectura/escritura de un bloque de datos en sectores contiguos

---

## 🏗️ Estructura Lógica del Disco Duro

El disco duro se divide en tres áreas:

1. **Sector de arranque** (Master Boot Record)
2. **Espacio particionado**
3. **Espacio sin particionar**

### 1. Sector de Arranque (MBR)

- **Ubicación**: Primer sector del disco (Cabeza 0, Cilindro 0, Sector 1)
- **Contenido**:
  - Tabla de particiones
  - Programa Master Boot (inicialización)
- **Función**: Leer la tabla de particiones y ceder el control al sector de arranque de la partición activa

> **Nota**: Si no existe partición activa, muestra un mensaje de error

### 2. Espacio Particionado

Espacio del disco asignado a alguna partición y accesible del sistema.

### 3. Espacio Sin Particionar

Espacio no accesible del disco que aún no ha sido asignado a ninguna partición.

---

## 🔀 Particiones

### Conceptos Básicos

- **Unidades físicas**: Cada disco duro es una unidad física distinta
- **Unidades lógicas**: Los S.O. trabajan con unidades lógicas
- **Partición**: Cada unidad lógica constituye una partición dentro de una unidad física

### Mínimo de Particiones

- **Mínimo 1**: Debe existir al menos 1 partición con la totalidad del espacio físico

### Razones para Crear Múltiples Particiones

1. **Razones organizativas**: Múltiples usuarios
2. **Instalación de múltiples sistemas operativos**
3. **Razones de eficiencia**: Mejor tener varias FAT pequeñas que pocas grandes

### Diferencia entre Particiones y Directorios

| Aspecto | Particiones | Directorios |
|---------|-------------|-------------|
| **Tamaño** | Fijo | Variable |
| **Ubicación** | Cilindros contiguos | Dispersa en la partición |
| **Sistema de archivos** | Puede diferir entre particiones | Mismo para toda la partición |
| **Seguridad** | Mayor (contigüidad) | Menor |

---

## 📊 Particiones Primarias y Lógicas

### Características

- **Primarias**: Pueden ser hasta 4 máximo en un disco duro
- **Lógicas**: Se definen dentro de una partición extendida
- **Partición extendida**: Tipo especial de partición primaria para definir particiones lógicas sin límite

### Tabla de Particiones

- Ubicada en el primer sector del disco (MBR)
- Contiene 4 entradas máximo
- Una debe estar marcada como **partición activa** (aquella que recibe el control en el arranque)

### Partición Extendida

- **Máximo**: 1 por disco duro
- **Ubicación en tabla**: Ocupa una de las 4 entradas de la tabla de particiones
- **Particiones lógicas**: Sin límite de cantidad dentro de la extendida
- **Espacio**: Puede estar completamente ocupado o tener espacio libre

### Mecanismo de Particiones Lógicas

1. Tabla MBR contiene una entrada con partición extendida
2. Esta entrada apunta a una nueva tabla de particiones
3. La nueva tabla utiliza sus dos primeras entradas:
   - Primera: Partición lógica 1
   - Segunda: Apuntador a la siguiente tabla similar

### Limitaciones y Consideraciones

| Aspecto | Primarias | Lógicas |
|---------|-----------|---------|
| **Generan unidades lógicas** | ✅ Sí | ✅ Sí |
| **Se pueden activar** | ✅ Sí | ❌ No |
| **Acceso desde otros S.O.** | ⚠️ Depende del S.O. | ✅ Más accesible |

### Recomendaciones de Instalación

> **Importante**: Los sistemas operativos deben instalarse en particiones primarias (de lo contrario no podrían arrancar)

**Mejores prácticas:**
- Instalar S.O. en particiones primarias
- Crear particiones lógicas para datos sin S.O.

**Ventajas de usar particiones lógicas para datos:**
- No se malgastan entradas de la tabla de particiones
- Evitan problemas de acceso desde otros sistemas operativos

---

## 🏢 Estructura Lógica de Particiones

La estructura lógica de una partición depende del **sistema de archivos** utilizado.

---

## 🚀 Secuencia de Arranque del Sistema

### Pasos del Proceso de Arranque

1. **Programa ROM de arranque**: Se carga cuando se enciende el ordenador
   - Pequeño programa almacenado en ROM

2. **Chequeo de hardware**: Realiza una verificación breve de los componentes

3. **Intento de arranque**: Intenta arrancar desde la primera unidad física indicada en la secuencia de arranque

4. **Reintentos**: Si falla, repite con la siguiente unidad de la lista hasta encontrar una unidad arrancable

5. **Secuencia de arranque configurable**: Se define en la configuración del ordenador (Setup, CMOS o BIOS)

6. **Master Boot**: El programa ROM cede el control a su programa de inicialización (Master Boot)

7. **Búsqueda de partición activa**: Master Boot busca en la tabla de particiones la partición activa

8. **Carga del S.O.**: Cede el control al sector de arranque de la partición activa, que procede al arranque del sistema operativo

---

**Fin del documento**
