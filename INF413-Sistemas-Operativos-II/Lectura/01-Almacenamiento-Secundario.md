Dispositivos de Almacenamiento
 Los discos duros forman el 
principal elemento de la 
memoria secundaria de 
un ordenado
 Diferencias:
 Memoria
principal: volátil, 
muyrápida pero de 
capacidad reducida
 Memoria
secundaria: no 
volátil, menos rápida y de 
gran capacidad

Estructura Fisica de un H.D.
• La unidadde 
lectura y 
escritura
• El disco.
Conjunto de componentes electrónicos y 
mecánicos que hacen posible el 
almacenamiento y recuperación de los datos 
en el disco 
❑ En realidad, una pila de discos, llamados platos, 
que almacenan información magnéticamente
• Cada uno de los platos tiene dos superficies 
magnéticas: la superior y la inferior 
• Estas superficies magnéticas están formadas por 
millones de pequeños elementos capaces de ser 
magnetizados positiva o negativamente

Funcionamiento..(Unidad)
• cada superficie magnética tiene asignado uno de los 
cabezales de lectura/escritura de la unidad (cant. 
Cabezales = cant platos x 2)
• El conjunto de cabezales se puede desplazar 
linealmente desde el exterior hasta el interior de la pila 
de platos mediante un brazo mecánico que los 
transporta
• Por último, para que los cabezales tengan acceso a la 
totalidad de los datos, es necesario que la pila de discos 
gire (Veloc. Constante y sin parar, distinto a los Discos 
flexibles. En CD no es velo. Constante por que depende 
de la distancia respecto al centro)

Funcionamiento
Operacion de Lectura o Escritura:
1.
Desplazar los cabezales hasta el lugar donde
empiezan los datos
2.
3.
Esperar a que el primer dato, que gira con los 
platos, llegue al lugar donde están los cabezales; 
y, finalmente, leer el dato con el cabezal
correspondiente

Estructura Fisica (pistas,cilindro,sectores)
 Cadasuperficie es llamada cara.
 Cant. Caras = cant. Cabezales
 CadaCara se dividide en anillos concentricos
llamados pistas.
 cilindro es el mismo anillo en todos los discos de la 
pila.
 cada pista se divide en sectores

• Los sectores son las unidades mínimas de información que puede leer o 
escribir (512 bytes)
• Cada pista por lo general tiene entre 100 y 300 sectores.
nº sectores = nº caras * nº pistas/cara * nº 
sectores/pista
• Cada sector queda unívocamente determinado si conocemos los siguientes
valores: cabeza, cilindro y sector

Ejercicio
 Por ejemplo, el disco duro ST33221A de Seagate 
tiene las siguientes especificaciones: 
cilindros = 6.253, cabezas = 16 y sectores = 63. 
por
tanto
, 
Cant. Total 
Si 
cada
disco 
sector 
duro
será
Sectores
almacena
= 6.253*16*63 = 6.303.024
512 bytes de 
de:
información
, la 
capacidad
máxima
de 
este
6.303.024 
sectores
* 512 bytes/sector = 3.227.148.228 bytes ~ 
3 GB.
• Las cabezas y cilindros comienzan a numerarse desde el 0 
y los sectores desde el 1

• En consecuencia, el primer sector de un disco duro será el 
correspondiente a la cabeza 0, cilindro 0 y sector 1

Tiempo de Acceso a los Datos
• El t.a.d. esta definido por el tiempo de búsqueda, el 
tiempo de latencia y el retardo rotacional.
• Tiempo de búsqueda: tiempo que tarda el 
desplazamiento del brazo desde la posición actual 
hasta el cilindro deseado.
• Tiempo de Latencia: tiempo que tarda en quedar bajo 
las cabezas el sector donde se leera-escribira.
• Tiempo de Transmisión: tiempo que tarda en leer
escribir un bloque de datos en sectores contiguos.
El mayor de estos es el tiempo de búsqueda. 
(10 veces mayor a los otros tiempos).

Estructura Lógica
 El sector de arranque (Master Boot Record)
 Espacio particionado
 Espacio sin particionar

1. Sector de Arranque
 Esel primer sector de todo disco duro (cabeza 0, 
cilindro 0, sector 1). 
 En él se almacena la tabla de particiones y un 
pequeño programa master de inicialización, 
llamado también Master Boot. 
 Este programa es el encargado de leer la tabla de 
particiones y ceder el control al sector de 
arranque de la partición activa. Si no existiese
partición activa, mostraría un mensaje de error

2. Espacio Particionado
Espacio del disco que ha sido asignado a alguna
partición
3.Espacio no particionado,
Espacio no accesible del disco ya que todavía no ha 
sido asignado a ninguna partición

Ejemplo:
Un sector de arranque que contenga una tabla de 
particiones con una sola partición, y que esta partición
ocupe la totalidad del espacio restante del disco

Particiones
 Cada disco duro constituye una unidad física distinta
 Los S.O trabajan con Unidades Logicas.
 Dentro de una U. Fisica hay varias U. Logicas.
 Cada U. Logica constituye una particion.

Diferenciaentre Particionesy Directorios
TamañoFijo
Ocupanun grupode 
cilindroscontiguosdel 
disco duro(mayor 
seguridad);
Cadaparticióndel 
disco duropuede
tenerun sistemade 
archivos(sistema
operativo) distinto

Tamaño Variable
Suelen tener su 
información 
desperdigada por toda 
la partición
todos los directorios 
de la partición tienen 
el sistema de archivos 
de la partición


Particiones
 Minimo 1 particion con la totalidad del Espacio fisico.
RAZONES  PARA CREAR MAS DE 
1 PARTICION
1. Razones organizativas
. Mas de 1 usuario.
2. Instalación de más de un sistema operativo
3. Razones de eficiencia
pocas grandes.
. Mejor varias FAT pequeñas que 
 
 Particiones Primarias y logicas
 Las particiones pueden ser de dos tipos: 
primarias o lógicas. Las particiones lógicas se 
definen dentro de una partición primaria especial 
denominada partición extendida
 En un HD sólo pueden existir 4 particiones
primarias (incluida la partición extendida, si
existe).
 Las particiones existentes deben inscribirse en 
una tabla de particiones de 4 entradas situada en 
el primer sector de todo disco duro
 De estas cuatro pueden estar utilizadas o no 
dependiendo de la situacion.

Particiones Primarias y Lógicas
 Es necesario que en la tabla de particiones figure una de ellas
como partición activa (es aquella a la que el programa de 
inicialización (Master Boot) cede el control al arrancar )
 Conclusiones:
 Para que un disco duro sea utilizable debe tener al menos una
partición primaria
 Además para que un disco duro sea arrancable debe tener activada
una de las particiones y un S.O.

Particion Extendida
 Maximo 1
 Esta partición ocupa, al igual que el resto de las 
particiones primarias, una de las cuatro entradas 
posibles de la tabla de particiones
 Dentro de una partición extendida se pueden 
definir particiones lógicas sin límite
 El espacio de la partición extendida puede estar 
ocupado en su totalidad por particiones lógicas o 
bien, tener espacio libre sin particionar

Mecanismo para crear Particiones Lógicas
 En la tabla de particiones del Master Boot Record debe existir
una entrada con una partición extendida (la cual no tiene
sentido activar) 
 Esta entrada apunta a una nueva tabla de particiones similar a 
la ya estudiada, de la que sólo se utilizan sus dos primeras
entradas.
 Unaesla particion logica 1 y la segunda es un apuntador a la 
sig. Tabla similiar a la anterior.

Part. Primarias – Part. Lógicas
 Ambas generan las correspondientes unidades lógicas del 
ordenador
 Sólo las particiones primarias se pueden activar
 Algunos S.O. no pueden acceder a particiones primarias 
distintas a la suya
CONSIDERACION
 Los sistemas operativos deben instalarse en particiones 
primarias, ya que de otra manera no podrían arrancar
 El resto de particiones que no contengan un sistema 
operativo, es más conveniente crearlas como particiones 
lógicas. Por dos razones:
 no se malgastan entradas de la tabla de particiones 
del disco duro
 evitan problemas para acceder a estos datos desde 
los sistemas operativos instalados

Estructura lógica de las Particiones
 Dependiendo del sistema de archivos utilizado en 
cada partición, su estructura lógica será distinta

Secuencia de Arranque
1.
Todos disponen de un pequeño programa 
almacenado en la ROM  encargado de tomar el 
control cuando se enciende.
2. Lo primero que hace el programa de arranque es 
un breve chequeo de los componentes hardware
3. Si todo está en orden, intenta el arranque desde la 
primera unidad física indicada en la secuencia de 
arranque
4. Si el intento es fallido, repite la operación con la 
segunda unidad de la lista y así hasta que 
encuentre una unidad arrancable
5. Esta secuencia de arranque se define en el 
programa de configuración del ordenador 
(también llamado Setup, CMOS o BIOS). 

6. el programa de arranque de la ROM cederá el 
control a su programa de inicialización (Master 
Boot).
7. Este programa buscará en la tabla de particiones la 
partición activa y le cederá el control a su sector de 
arranque
8. El programa contenido en el sector de arranque de 
la partición activa procederá al arranque del 
sistema operativ