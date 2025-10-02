# Bitácora de aprendizaje de la unidad 6

## Actividad 01
### 1
Las teclas que permiten interactuar con la aplicación son N, A, S y R, N hace que las partículas estén en un estado normal, donde estan flotando alrededor de la pantalla, después A hace que el mouse funcione como atractor, S hace que se congelen las partículas en la posición en la que se encontraban, R hace que el mouse repela las partículas causando que se alejen poco a poco de la posición de este.
### 2
Se comportan igual respecto a lo mencionado anteriormente, lo que cambia es su color y tamaño, siendo de las más pequeñas a las más grandes las estrellas, después las estrellas fugaces y por ultimo los planetas respectivamente.
### 3
Estado inicial

<img width="1010" height="764" alt="image" src="https://github.com/user-attachments/assets/ae0e2a35-392d-4a0d-af32-c2cab7e9b49c" />

Después de apretar S

<img width="1007" height="742" alt="image" src="https://github.com/user-attachments/assets/30530e87-fa7f-4a16-b309-f009c089340c" />

Después de apretar A

<img width="1014" height="757" alt="image" src="https://github.com/user-attachments/assets/a4ac637d-86e8-43f6-9a79-6edb2c9cab21" />

Después de apretar R

<img width="1015" height="757" alt="image" src="https://github.com/user-attachments/assets/2eca6665-2923-4142-9787-6c1e1f6a35b8" />

Después de apretar N

<img width="1017" height="758" alt="image" src="https://github.com/user-attachments/assets/21decbd1-6c81-4f94-9e70-33a4ce72b5c3" />

### 4
Por lo que puedo suponer quizas va cambiando de alguna manera entre los estados que tiene probablemente desencadenado en base a las acciones que se tomen.

## Actividad 02
### 1
El propósito de utilizar el patrón observer en un proyecto es el de evitar que una clase esté revisando constantemente algún objeto o método para poder cambiar de estado, el hecho de que se le avise directamente y solo tenga que erperar a este mensaje para cambiar su estado mejora por mucho el rendimiento y facilidad de una aplicación y es mucho más cómodo y fácil.
### 2
<img width="1595" height="844" alt="image" src="https://github.com/user-attachments/assets/9cff95ca-13ff-44a8-8e01-e53e64ea4c0b" />

### 3
<img width="1158" height="662" alt="image" src="https://github.com/user-attachments/assets/3c94203f-c1fa-45ee-b6e5-8a5d501db0d7" />

### 4
El hecho de utilizar un observer facilita de una manera gigantesca las cosas, empezando por el hecho de que de otra manera un update debería ir mirando a cada partícula estando atento de que hacen y decidiendo por ellas que hacer en los diferentes casos, esto incrementaria mucho el acoplamiento debido a la gran dependencia entre las clases, cambiar cualquier lógica invidual de las partículas afectaría a ofApp, usar observadores elimina esto, ya que su función pasa a ser la de simplemente una clase que esta atenta a recibir una notificación y avisar a las demás para que individualmente cambien sus estados frente a esto. Esto facilita crear nuevas partículas de manera fácil sin tener un ofApp demasiado extenso y dificil de manejar, solo es necesario modificar el onNotify de la partícula.

Otra ventaja de tener esto así es que esto permite al código ser reutilizable, e otra manera el ofApp sería único para este caso, mientras que como está permite reutilizar el programa de notificaciones hecho.

## Actividad 03
### 1
El utilizar este método soluciona que al momento de crear objetos repetitiva y desordenada que obligaría a cambair muchas partes inidivuales y pequeñas del código si se quiere crear un nuevo tipo de objeto, modificando cada vez que se creen los tipos de objetos, otro porblema es el gran acoplamiento de el método normal de crear objetos, ya que la clase que crea puede acceder a todos los datos de como crear el otro objeto, esto no debería ser asi y usar este método lo evita.

### 2
La primera ventaja existente es que de no usar este método sería el hecho de dejarle a ofApp::setup la creación completa de las partículas permitiendole acceder a todos sus detalles, esto no es algo deseado, mientras que al usar el ParticleFactory se evita esto ya que la función de ofApp::setup sería solo pedir que estas se crean, sin enterarse de lo demás. Ahora, otra ventaja que tiene este método es el de permitir un código más limpio y el de que al momento de crear una nueva partícula solo sea necesario editar la Factory, no el ofApp, este no debería saber que hacen estas partículas, esto tambien fácilita mucho la edición de esto en este tipo de proyectos, y si se trabajara de una manera más grande evita que las personas se tengan que encargar, enterar o preocupar por como se crear estas, solo tienen que pedir que estas se creen y los encargados de la Factory se ocupen de esto.

### 3
si quisiera crear este nuevo tipo de partícula lo editaría directamente en el Factory, donde edito como quiero que sea creada y sus características, mientras que en el ofApp debería solo decidir cuantas crear y pedirlas, esto debido a los edxplicado anteriormente, ya que es justo este el punto de este método, evitar editar individualmente cada creación del objeto, solo es necesario pedirlo a la Factory y esta se encargará de esto, es allí donde debe ser definido como quiere ser creado. Los pasos serían simplemente crear otro else if para este tipo de partícula y definir sus características y en el ofApp establecer otra seccion del texto parecida a las demás que cree una cantidad de estas.

### 4
El hecho de que este método sea estático facilita su uso al no tener que instanciarlo y es útil en un caso como este donde nuestra lógica de creación es estática, pero en cuanto a desventajas está que evita el poder tener más fabricas con sus propias configuraciones distintas con sus parámetros y lógica propios. Un método de instancia puede arreglar esto permitiendo tener varias con configuraciones distintas, facilitando asi el poder hacer esto, lo malo es que deberia crear un objeto de este tipo cada q se quiera usar, al final depende de lo que se busque ya que para nuestro caso el actual siento es más útil y sencillo.

## Actividad 04
## 1
El uso de state evita que los objetos esten constantemente revisandose a si mismos para entender en que estado se encuentras y dependiendo de este que acciones realizar, mientras que de esta manera el como actuan es delegado a un objeto de estado, esto es super útil en casos donde queremos que el objeto cambie de estados de manera dinámica y fácil, además de tener varios objetos distientos que compartan ciertos estados que tenemos claramente definidos, utilizar estos además de facilitar todo reduce en gran cantidad el código necesario.

## 2
<img width="738" height="757" alt="image" src="https://github.com/user-attachments/assets/75f90122-11e4-4d57-9317-ff56ed4ca518" />

(Este cambio de estados lo explico mejor con las pruebas en la actividad 01)

## 3
En general la ventaja de usar estados es justamente el como están separados indivitualmente y pueden ser utilizados de manera más sencilla, en este caso donde lo comparamos con un gran if dentro del update podemos ver estas ventajas de manera más sencilla, el hecho de utilizar los estados significa que cada uno tiene su propio comportamiento creando una alta cohesión, utilizar un gran bloque junto de código bajaria demasiado esta, mezclando lógicas entre estos estados, haciendo que una sola parte haga muchas cosas no relacionadas entre sí.

En cuanto a extensibilidad pasa algo parecido que con las demás cosas vistas, estos métodos permiten que solo necesario editar unas pequeñas partes del código donde se defina la partícula y que en este caso implemente el state, evitando asi que hacer en el update un else if larguisimo y de maner individual por partícula y estado. En cuanto a el cumplimiento del prinicipo de abierto/cerrado, este indica que en un programa las clases deberian estar cerradas a modificaciones pero abiertas a extenciones, o sea que deberia ser posible agregarle funciones y partes extra sin modificar el código fuente original, el uso de estados permite esto, en este ejemplo en específico se pueden utilizar para agregar cosas a Particle sin modificarla, de lo contrario con un else/if sería obligatorio modificarla.

## 4
La lógica que implementan estos métodos es la de permitir que un estado se inicialice o se limpie permitiendo la transcición al siguiente, onEnter permite que se inicialicen las condiciones del estado mientras que onExit limpia y restaura el objeto para el siguiente estado. Los ejemplos de como podrían usarse en nuestro ejemplo seria por ejemplo hacer que la partícula este en estado Attract cambie de color para indicar el cambio de estado, esto con onEnter, mientras que con onExit se podría hacer que al salir del estado Stop se reinicie la velocidad para evitar que tenga reciduos o alteraciones en esta.

## Autoevaluación:
### Actividad 01
Nota: 1/1
En esta actividad logré identificar las bases del programa, proporcionar evidencias y hacer hipótesis al respecto que me permitieron despues ir identificando como los temas se relacionaban a este programa y como funcionaban




