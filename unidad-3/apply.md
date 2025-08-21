# Unidad 3


## 🛠 Fase: Apply

### Diagnóstico del problema
El primer error se encuentra en el inicio al definir al personaje y reservar memoria en el heap con ``estadisticas = new int[3];`` y eventualmente no liberar esta memoria en ningún momento, esto es algo que se repitió mucho en las anteriores actividades y es la advertencia de siempre liberar la memoria con un ``delete[]`` de lo contrario termina pasando lo de este ejemplo. Aquí ocurre entonces que al crearse el objeto heroe en ``simularEncuentro`` se guarda en el stack y sus estadisticas se guardan en el heap pero el problema es que al salir de aqui este junto con el copiaHeroe que tambien utiliza el ``new int[3]`` se destruyen ambos por estar en el stack, y el espacio de memoria nunca se libera, esto causa que si se aplica cada vez que se cree un personaje y simulen encuentros se vaya acomulando memoria sin liberar y a la que ya no es posible acceder creando asi una fuga.

El segundo error se encuentra al momento de asignarle a copiaHeroe estadísticas ya que al crearse como se hace (``Personaje copiaHeroe = heroe;``) sus estadisticas apuntan al mismo array que el heroe, ammbos viven en el stack y aputan al mismo punto en el heap por lo que al editar las estadisticas de uno se afecta al otro a la vez, y si se liberara la memoria de alguno esto llevaria a que se liberara una segunda vez lo cual podria causar errores.

### Solución y refactorización
````c++
#include <iostream>
#include <string>
#include <array>

class Personaje {
public:
    std::string nombre;
    std::array<int,3> estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas = {vida, ataque, defensa}; 
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};
void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
````
Aquí cambie el int[3] original con new que causaba el error con la memoria a un array normal en stack, podría haber hecho un destructor pero el problema es que esto seguia ocasionando el problema de que al simular un encuentro la copia del heroe tomaba este mismo array en el heap como referencia y esto no supe como solucionarlo, asi que me pareció mejor directamente cambiar la naturaleza de las estadisticas. Quizas algo que podría mejorar esto sería que la copia tambien tenga su propio array en heap que cree y destruya individualmente cada vez que se llama, pero esto alargaria demasiado el código y resultaría peor para un programa que esta buscando reducir su uso innecesario de memoria además que esto requeriría que se pase la información del original a el actual leyendo lo guardado en la dirección de memoria.
