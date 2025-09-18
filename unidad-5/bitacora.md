# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**
### Parte 1: 
#### ¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.
Encapsulamiento es un método usado para proteger los atributos de una clase, ya que no es recomendado permitir el acceso directo a estos, por ende se encapsulan para que las demás clases puedan acceder a sus datos a travez de manera segura.
#### ¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.
La herencia es usada para hacer que una clase herede atributos de una clase padre, esta es usada preferiblemente en ocasiones donde varias clases compartan atributos similares, haciendo útil que una clase padre herede estos atributos a varias hijas. Un programador decidiría usarla ante debido a que es algo que ayuda mucho al rendimiento y el orden a la hora de programar, no necesita instanciar en cada clase los mismos atributos cuando puede heredarlos y establecerlos como base.
#### ¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.
El polimorfismo es algo que permite que un mismo atributo sea interpretado y utilizado de maneras distintas entre clases, un código polimórfico es aquel que se vale de esto y constantemente esta redefiniendeo sus atributos y métodos.
### Parte 2
#### Encapsulamiento
-Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.
```` c++
public string Nombre
    {
        get { return nombre; }
        protected set { nombre = value; }
    }
````
En esta línea de código se crea un encapsulamiento de la variable Nombre en el que se obtiene el valor de nombre y después se define a partir de un value, pero de una manera en la que no se accede directamente a la variable original.

-¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
La idea es acceder y editar el valor de nombre desde otra propiedad que sea pública, esto evita que se acceda directamente a la propiedad original, por esto Nombre es public mientras que nombre no lo es
#### Herencia
-¿Cómo se evidencia la herencia en la clase Circulo?
```` c++
public class Circulo : Figura
````
Al crear la clase Circulo se especifica que hereda de la clase abstracta Figura con estos dos puntos, esto evidencia que es una clase hija y que hereda los atributos y métodos de la clase padre llamada Figura.

-Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?
Almacena también el atributo nombre junto con su encapsulamiento y el método Dibujar, que después es redefinido con un override dentro de círculo, también evita el tener que reescribir nombre en su constructor ya que lo hereda de la clase Figura.
#### Polimorfismo
-Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”?
Creo que "por debajo" esta redefiniendo constantemente las propiedades de la función dibujar dependiendo de la clase que lea.
### Parte 3
- Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?
Al crear un objeto este y sus atributos se almacena de manera diferente dependiendo de como se cree, esto en base a lo que habiamos visto anteriormente, si se crea en el stack como algo temporal dentro de otra función o se guarda con las variables estáticas y globales si se crea asi o en el heap si es creado con un new.
- Polimorfismo:¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo?
Supongo que lo hace a partir del texto que lee en el espacio de la memoria designado a las funciones, identifica que le indica al momento de realizar la función dependiendo del tipo de Figura que tenga.
-Encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase?
Supongo que lo realiza identificando en las instucciones que variables estan designadas de que manera y al momento de ejecutar comandos verifica que la variable llamada si sea accesible desde el punto donde fue pedida y de su tipo.
## 2.  **La pregunta inicial**
Revisando mi diagnosticó puedo encontrar como el concepto en el que más flaqueo es el polimorfismo, ví como más adelante en la bitácora se habla del vtable y que esta relacionado de alguna manera con el polimorfismo así que he decidido que mi pregunta va a ir encaminada a preguntarme como es que se interpreta el polimorfismo al interior del programa en su momento de ejecución y que es lo que tiene que ver este "vtable"
### ¿Cómo implementa C++ el polimorfismo en tiempo de ejecución y qué papel juega la vtable en esto?
## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).
### Actividad 02
Primero que nada en ofApp.h se establecen las bases de las partículas que aparecen en el programa y como actuan de diferente dependiendo de que tipo de partícula sean, aqui se evidencia el primer uso de herencia, encontrado en la clase ``Particula`` que será la más importante, esta establece sus atributos, después se establece la clase ``RisingParticle`` esta tiene otros atributos extra pero hereda su mayoría de Partícula, pero aqui es donde pasa algo que me interesa debido a que decidí enfocarme en polimorfísmo, esto es el update que utiliza el override para establecer su propia versión de este, lo mismo pasa con el draw, aunque aún no se como lo hace por debajo entiendo que es lo que hace que puedo esperar que las demás clases utilicen esto para poder definir sus capacidades, también cambia los estados de algunos métodos.

Ahora se crea otra clase base que hereda de particle y que heredará a las diferentes clases de explosiones, esta es llamada ``ExplosionParticle`` de esta surgen las diferentes formas de explosión, todas definen su propias maneras de funcionar en el update y draw usando polimorfísmo y dibujando sus formas con conceptos matemáticos que permitan crearlas. El ofApp.cpp se encarga de manejar todo esto creando partículas entre los tres tipos de manera random, asignando hacia donde van, su tamaño, su velocidad, etc. permitiendo que se destruyan y establece que para crearlas se puede usar clic para crear de manera individual o la barra espaciadora para crear muchas a la vez, y la s para el screenshoot.

<img width="1920" height="1051" alt="screenshot_1224" src="https://github.com/user-attachments/assets/8a2068b8-2f89-4447-8d05-0663c6af7009" />
<img width="1920" height="1051" alt="screenshot_1534" src="https://github.com/user-attachments/assets/52791962-4130-4bc3-81b7-bcb3a2c614f2" />
<img width="1920" height="1051" alt="screenshot_1638" src="https://github.com/user-attachments/assets/7044d6d4-9047-4121-91dc-52f5a7f1ebb9" />
### Actividad 03
En memoria espero encontrar los espacios designados de las funciones y vectores, solo que no tengo muy bien entendido como se ve esto realmente, espero encontrar una especie de lista de funciones que den instrucciones para el programa saber que hacer y como interpretarlo.


## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
