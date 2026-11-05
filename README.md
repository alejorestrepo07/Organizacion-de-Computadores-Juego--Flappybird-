# Flappy Bird (Jack) - Hito 1: Tablero y Objetos Gráficos

**Asignatura:** Organización de Computadores
**Institución:** Universidad EAFIT
**Autor:** Alejandro Restrepo Osorio

## Descripción General
Este proyecto consiste en el desarrollo de un clon del videojuego de estilo retro Flappy Bird, implementado íntegramente en el lenguaje de programación orientado a objetos Jack. El software está diseñado para ser ejecutado en la máquina virtual de la arquitectura Hack, correspondiente a la plataforma Nand2Tetris. 

Esta entrega corresponde al **Hito 1 (Tercer Parcial)**, enfocándose en la estructuración modular de las clases, la correcta gestión de la memoria, y el renderizado estático y dinámico del tablero junto con los objetos gráficos iniciales.

## Arquitectura de Clases
El proyecto aplica principios de programación orientada a objetos (POO), distribuyendo las responsabilidades en los siguientes módulos para garantizar un bajo acoplamiento:
* **`Main.jack`**: Punto de entrada de la aplicación. Se encarga de inicializar el entorno de juego (instanciando `Board`) y de iniciar el ciclo de ejecución, asegurando además la liberación de recursos al finalizar.
* **`Board.jack`**: Clase controladora del escenario. Administra el bucle principal de juego (Game Loop), la instanciación de las entidades (jugador y obstáculos) y la temporización (sincronización de cuadros por segundo mediante `Sys.wait`).
* **`Pipe.jack`**: Representa los obstáculos. Incluye la lógica matemática para la generación de alturas mediante un algoritmo congruencial lineal que simula pseudoaleatoriedad. Emplea técnicas de renderizado diferencial (Delta Rendering) para actualizar la posición en pantalla mitigando el parpadeo (flickering).
* **`Bird.jack`**: Representa el objeto gráfico del jugador (sprite inicial). Contiene los métodos para su renderizado geométrico espacial e incluye la estructura de borrado que será utilizada en la etapa de movimiento y física de colisiones.

## Gestión de Memoria y Optimización
Dado que la plataforma Hack posee recursos limitados, el proyecto implementa un estricto control de memoria:
* **Asignación:** Uso eficiente de constructores para reservar el espacio exclusivo de las entidades.
* **Liberación:** Cada clase incorpora un método `dispose()` que ejecuta `Memory.deAlloc(this)` para destruir los objetos gráficos y las estructuras de datos (como el `Array` de tuberías) una vez finaliza el ciclo, previniendo fugas de memoria (Memory Leaks).

## Instrucciones de Compilación
Para traducir el código fuente a bytecode (`.vm`), proceda con las siguientes instrucciones:
1. Abra una terminal de línea de comandos apuntando al directorio raíz del proyecto (`FlappyBird`).
2. Ejecute el compilador de Jack (`JackCompiler`) indicando el directorio actual:
   ```bash
   JackCompiler.bat .