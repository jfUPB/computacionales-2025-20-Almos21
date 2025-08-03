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
#### ¿Cómo se traduce esto a C++?
``` c++
Memoria[SCREEN] = -1;;
CONTADOR = 0;
int tmp;
while(1)
{
tmp= KBD;
if(tmp == 100){
//DERECHA
}
else if (tmp == 105){
//IZQUIERDA
}
}
Memoria[CONTADOR+SCREEN]=0;
CONTADOR = CONTADOR +1;
Memoria[CONTADOR+SCREEN] = -1

```
### Actividad 04
Un for como este:
````c++
//Adds 1+...+100.
int sum=0;
for(int i = 1; i <=100; i++){
   sum+= i;
}
````
puede ser convertido en un while facilmente, ya que despues de todo es un ciclo que va verificando si una variable cumple una condición e ir sumandole a esta, esto podria hacerse así:
````c++
 int i=1;
 int sum=0;

 while(i <=100){
    sum+= i;
    i++;
 }
````
esto es igual a el primer código mostrado en la guía, por ende el código ensamblador resultante debe ser el mismo:
````asm
 @i 
 M=1
 @sum 
 M=0 
 (LOOP)
 @i
 D=M 
 @100
 D=D-A 
 @END
 D;JGT 
 @i
 D=M 
 @sum
 M=D+M 
 @i
 M=M+1 
 @LOOP
 0;JMP
 (END)
 @END
 0;JMP 
````
Este es el mismo código del for inicial, es posible observar como era posible convertir el for en while entendiendo la lógica de este, y como se replica la misma lógica de ir sumando valores a una variable y verificando si esta cumple con una condición asignada constantemente y mientras esto no se cumpla se reinicie el ciclo.

### Actividad 05
En esta actividad hay que pasar el código de c++ a uno en lenguaje ensamblador entendiendo el uso de los punteros y como replicar su función, para el primero este fue mi resultado:
(Original)
````c++
int a = 10;
int* p;
p = &a;
*p = 20;
````
(Ensamblador)
````asm
@10
D=A
@i
M=D
D=A
@sum
M=D
@20
D=A
@sum
A=M
M=D
````
Ahora el segundo código, en este la intención es establecer dos variables y un apuntador, y que el puntero tome la posición de memoria de a y despues b tenga asignado el valor de la variable a la que apunta p, en el código de ensamblador lo hice definiendo primero b y guardando el valor 5 en su espacio de memoria designado, esto para que fuera más sencillo el proceso y a estuviera antes que la instancia del puntero en el código:
(Original)
````c++
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
````
(Ensamblador)
```` asm
@5
D=A
@sum
M=D
@10
D=A
@i
M=D
D=A
@ptr
M=D
A=M
D=M
@sum
M=D
````
