# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
#### Ciclo fetch-decode-execute
``` asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```

#### ¿Qué sucede?
Las instrucciones van guardando datos en las variables PC, A y D, en PC hay un contador que aumenta en cada instrucción e indica cual es la siguiente instrucción ejecutada en la ROM, las instrucciones van asignando valores a A y a D y finalmente se guarda un dato en la memoria RAM

#### ¿Qué valor se almacena en la dirección de memoria 16?                          
El número 3

#### ¿Por qué crees que es ese valor?
Este valor es almacenado en la dirección de memoria 16 cuando se llega a la instrucción número 5 que indica que en la dirección de memoria (que toma leyendo el valor de A) se asigna el valor de D (que en ese instante era 3)


#### ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
Al inicio la CPU lee el número guardado en PC que indica cual es la siguiente instrucción a ejecutar, después lee los datos en esta instrucción y los ejecuta, haciendo lo que se indique como asignar valores, guardar datos en la memoria, etc.

#### ¿Qué cambios observas en el contenido de la memoria y los registros?
En el espacio número 16 de la memoria se almacena el número 3, esto por las razónes explicadas más arriba.

#### Experimento
``` asm
@5
D=A
D=D+A
@20
M=D
@END
(END)
0;JMP
```

#### ¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?
Los datos de la ram se ven afectados por los de la ROM pero la RAM no afecta a la ROM, además hasta ahora no parece haber manera destro del código de modificar los datos de la ROM, estos están ahi es para ser leidos.

### Actividad 2
Nuevo código
``` asm
@SCREEN
D=A
@i
M=D
(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
@i
M=M-1
A=M
M=0
@READKEYBOARD
0;JMP

(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@16
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
```
#### Identifica una instrucción que use la ALU y explica qué hace.
ALU es la unidad encargada de realizar los calculos y comparaciones en un proceso, en este caso por ejemplo hay una en la línea 23 con "D=D-A" ya que aquí hay una operación de resta, esta línea se encarga de asignarle a D el resultado de esta resta.

#### ¿Para qué sirve el registro PC?
Es el que indica que instrucción será la siguiente que ser realizada, modificar esta variable es lo que posibilita el generar ciclos o condicionales, permitiendo viajar a diferentes instrucciones a lo largo del código.

#### ¿Cuál es la diferencia entre @i y @READKEYBOARD?
En el código @i indica una posición en la RAM donde se guardará o el número 16318 (@screen) o 24576 (@KBD) los cuales cambian dependiendo de si se presiona o no una tecla, además es desde 16318 hacia abajo que cambian los datos guardados a -1 al momento de ser apretada la tecla. En @READKEYBOARD se almacena el número de instrucción donde se almacena el código de la tecla pulsada, este es el que despues da valor a D y determina si el ciclo continua o a travez de los condicionales dirige a otra parte de las instrucciones.

#### Describe qué se necesita para leer el teclado y mostrar información en la pantalla.
Además de permitir usar el teclado de forma manual en el codigo se necesitan instrucciones como @SCREEN y @KBD.

#### Identifica un bucle en el programa y explica su funcionamiento.
Desde la línea 4 hasta la 13 hay un ciclo que se perpetua mientras al pasar por la línea 7 D sea igual a 0, este valor depende de si se presiona o nó una tecla, ya que la hacerlo se guarda el código de la tecla en @KBD y este se asigna a D donde se pasa a otras instrucciones.

#### Identifica una condición en el programa y explica su funcionamiento.
Continuando con lo anterior, hasta que no se cumpla la condición de que D sea diferente a 0 el bucle continua, cambiar esto es lo que permite que el programa continue y se ejecute.
