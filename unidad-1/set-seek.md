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
