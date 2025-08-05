# Unidad 2


## 🛠 Fase: Apply

### Actividad 06

#### Primera prueba
La primera prueba concistió en hacer un bucle que fuera llenando los arreglos aprovechandose de contadores y un puntero que vaya cambiando la dirección de memoria a la que apunta para llenar allí el siguiente número, este loop aún es "infinito" y solo era para poder entender como llenar el arreglo, lo siguiente sería definir el tamaño del arreglo definiendo hasta que punto llenar la memoria
```asm
@CONTADOR
M=0
@17
D=A
@POSICION
M=D
(LOOP)
@CONTADOR
M=M+1
D=M
@POSICION
M=M+1
A=M
M=D
@LOOP
0;JMP
@END
0;JMP
```
#### Segunda prueba
Para esta segunda lo que hice fue terminar de definir el loop para que únicamente llegara hasta llenar las direcciones de memoria hasta que su contenido sea 10 en la última, esto aprovechandome del ````JGT```` y en general lo que vimos las clases pasadas de como definir un while en ensamblador.
```asm
@CONTADOR
M=0
@17
D=A
@POSICION
M=D
(LOOP)
@CONTADOR
M=M+1
D=M
@POSICION
M=M+1
A=M
M=D
@9
D=D-A 
@END
D;JGT
@LOOP
0;JMP
@END
0;JMP
```
