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

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
