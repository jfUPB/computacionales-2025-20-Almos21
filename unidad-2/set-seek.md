# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01
Para iniciar se busca cual es la dirección de memoria a la que @SCREEN se refiere, siendo esta: 16384, aquí empieza el mapa de memoria mencionado que representa la pantalla y pinta los pixeles dependiendo de sus bits, para pintar solo el primer pixel convertimos en 1 el primer bit para asi pintar el primer pixel de la pantalla, encontramos que el número que en binario se traduce a 0000000000000001 es el 1
```asm
@SCREEN
M=1
```
#### ¿Cómo se traduce esto a C++?
Ahora lo pasamos a c++ esto para poder entender como puede esto ser pasado a un lenguaje de alto nivel, aquí podemos relacionarlo a como en C++ asignamos un valor a esta variable, solo que aquí hay que encontrar como logar que el compilador asigne esta variable a la dirección 16384
```c++
screen = 1; //forzar al compilador para que asigne la variable screen a la dirección 16384
```
### Actividad 02
Para esto todos los bit deben estar en 1, al pasar esto a decimal encontramos que para encender todos estos es necesario asignar el número -1 a esta dirección de memoria, haciendolo de la siguiente forma:
```asm
@SCREEN
M=-1
```
#### ¿Cómo se traduce esto a C++?
```c++
screen = -1; //forzar al compilador para que asigne la variable screen a la dirección 16384
```

### Actividad 03
```asm
@SCREEN
M=-1
@CONTADOR
M=0


// la letra d tiene código 100 y la i tiene código 105
(LEER)
@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ

@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)

//BORRO POSICIÓN ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP


(IZQUIERDA)

//BORRO POSICIÓN ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP
```
