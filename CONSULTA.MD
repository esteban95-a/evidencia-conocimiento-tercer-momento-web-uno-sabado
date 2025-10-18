# Cuestionario: Asincronismo y Consumo de APIs en JavaScript

*A continuación, responde cada una de las siguientes preguntas. Recuerda hacer un commit por cada pregunta principal que completes.*

### Pregunta 1: El Call Stack

* **1.1.** ¿Qué es el **Call Stack** en JavaScript? Explícalo con una analogía del mundo real que facilite su comprensión.
* **1.2.** ¿Qué significa el famoso error `Maximum call stack size exceeded` y cómo podrías provocarlo intencionalmente con un pequeño y simple fragmento de código? (Incluye el código de ejemplo).

**[ESPACIO PARA TU RESPUESTA 1]**
1.1 El Call Stack (pila de llamadas) es una estructura de datos tipo pila (LIFO: Last In, First Out) que utiliza el motor de JavaScript para registrar el orden en el que se ejecutan las funciones.

Cada vez que se invoca una función, esta se coloca (“empuja”) en la parte superior del stack.
Cuando la función termina su ejecución, se retira (“saca”) del stack.
De esta manera, el intérprete sabe en qué punto del programa debe continuar una vez que una función finaliza.
analogia de una cafeteria :
Un cliente pide un café latte, así que comienzas a prepararlo (lo colocas en la pila de tareas).

En medio de eso, otro cliente pide un capuchino, y decides atenderlo primero (lo pones encima de la pila).

Cuando terminas el capuchino, lo entregas (lo sacas del stack) y retomas el café latte.
1.2 Este error ocurre cuando el Call Stack se llena más allá de su capacidad.
Cada llamada de función ocupa un espacio en la pila, y si una función se llama a sí misma indefinidamente (recursión infinita) sin una condición de salida, la pila nunca se vacía.
Cuando esto sucede, el motor de JavaScript lanza el error:
function repetitiva() {
  repetitiva();
}
repetitiva();
---

### Pregunta 2: Los Callbacks

* **2.1.** ¿Qué es un **"callback"** en JavaScript? Explica con tus propias palabras para qué se utilizaban principalmente en el contexto asíncrono.
* **2.2.** Investiga en internet sobre el término **"Callback Hell"** o **"Pyramid of Doom"**. Pega un ejemplo de código que lo ilustre y explica por qué esa estructura es problemática para la legibilidad y el mantenimiento del código a largo plazo.

**[ESPACIO PARA TU RESPUESTA 2]**
2.1 Un callback es una función que se pasa como argumento a otra función, y que se ejecuta después de que la función principal haya terminado su tarea.
se utilizaban para :
Leer archivos desde el disco.
Consultar datos en una API.
Esperar una respuesta del servidor.
2.2
obtenerUsuario(1, function (usuario) {
  obtenerPosts(usuario.id, function (posts) {
    obtenerComentarios(posts[0].id, function (comentarios) {
      guardarEnBD(comentarios, function (resultado) {
        console.log("Datos guardados correctamente:", resultado);
      }, function (error) {
        console.error("Error al guardar en BD:", error);
      });
    }, function (error) {
      console.error("Error al obtener comentarios:", error);
    });
  }, function (error) {
    console.error("Error al obtener posts:", error);
  });
});
La indentación excesiva hace que el código sea difícil de seguir visualmente,Agregar, cambiar o eliminar una llamada asíncrona puede romper el flujo,Cada nivel requiere su propio bloque de manejo de errores,Las funciones quedan dependientes unas de otras en un mismo bloque.

---

### Pregunta 3: El Mundo de las APIs 

* **3.1.** ¿Qué es una **API** ? Explícalo de forma sencilla, como si se lo estuvieras explicando a alguien que no es programador.
* **3.2.** ¿Qué es una **API REST**? Describe brevemente sus características principales o principios.
* **3.3.** ¿Qué es un **Endpoint**? En el contexto de la API de Rick and Morty (`https://rickandmortyapi.com/api/character/2`), ¿qué parte de la URL representa el endpoint y qué información específica esperarías obtener de él?
* **3.4.** ¿Para qué sirve una herramienta como **Postman** o **Thunder Client** (la extensión de VS Code)? Describe su función principal en el desarrollo de software.
* **3.5. Códigos de Estado HTTP:** Investiga y explica qué representa cada una de las siguientes familias de códigos de estado. Para cada familia, menciona al menos un ejemplo de código específico y lo que significa. 🆕
    * **Codigos (100-199):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (200-299):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (300-399):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (400-499):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (500-599):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?

**[ESPACIO PARA TU RESPUESTA 3]**
3.1 Una API (Application Programming Interface) es un conjunto de reglas y herramientas que permiten que dos programas se comuniquen entre sí.Una API es como un mesero en un restaurante.
Tú (el cliente) haces un pedido (una solicitud), el mesero (la API) lleva tu pedido a la cocina (el servidor), y luego te trae de vuelta lo que pediste (la respuesta).
3.2tipo de API que sigue un conjunto de principios y reglas para permitir la comunicación entre cliente y servidor a través de protocolo HTTP, el mismo que usan las páginas web.

Características principales de una API REST:

Usa métodos HTTP estándar:

GET → Obtener información

POST → Crear un nuevo recurso

PUT → Actualizar un recurso existente

DELETE → Eliminar un recurso

Es stateless (sin estado):
Cada solicitud contiene toda la información necesaria. El servidor no recuerda lo que el cliente hizo antes.

Usa URLs claras y organizadas:
Cada dirección web identifica un recurso, por ejemplo:
https://api.ejemplo.com/usuarios/5 → representa el usuario con ID 5.

Devuelve datos en formato estándar:
Generalmente JSON, fácil de leer por humanos y procesar por máquinas.

3.3 Un endpoint es una dirección específica (URL) dentro de una API donde se puede acceder o manipular un recurso concreto.
https://rickandmortyapi.com/	Dominio principal (el servidor donde vive la API)
/api/character/	Ruta base del recurso (endpoint general para personajes)
2	Identificador del personaje específico.
 este seria el endpoint     /api/character/2 
3.4 Herramientas como Postman o Thunder Client son programas que sirven para probar, analizar y documentar APIs.

Permiten al desarrollador enviar solicitudes HTTP (GET, POST, PUT, DELETE) y ver las respuestas del servidor sin necesidad de crear código.funciones:Probar endpoints de una API.

Enviar datos (JSON, formularios, etc.).

Revisar respuestas y códigos de estado HTTP.

Simular diferentes escenarios (errores, autenticaciones, etc.).

Documentar y compartir pruebas entre equipo
3.5
| Familia | Tipo de respuesta  | Ejemplo                   | Significado                              |
| ------- | ------------------ | ------------------------- | ---------------------------------------- |
| 100–199 | Informativa        | 100 Continue              | El servidor está recibiendo la solicitud |
| 200–299 | Éxito              | 200 OK                    | Solicitud completada correctamente       |
| 300–399 | Redirección        | 301 Moved Permanently     | El recurso cambió de ubicación           |
| 400–499 | Error del cliente  | 404 Not Found             | El recurso no existe                     |
| 500–599 | Error del servidor | 500 Internal Server Error | Fallo interno del servidor               |

---

### Pregunta 4: Las Promesas (La solución elegante)

* **4.1.** ¿Qué es una **Promesa (`Promise`)** en JavaScript? Describe detalladamente sus tres estados posibles: `pending`, `fulfilled` y `rejected`.
* **4.2.** ¿Cómo resuelven las promesas el problema del "Callback Hell"? Explica el papel que juegan los métodos `.then()`, `.catch()` y `.finally()` en el manejo de una promesa.

**[ESPACIO PARA TU RESPUESTA 4]**
--
### Pregunta 5: Async/Await (Azúcar sintáctico)

* **5.1.** ¿Qué son las palabras clave **`async`** y **`await`**? ¿Qué problema vienen a solucionar o mejorar en comparación con el uso de `.then()` y `.catch()`?
* **5.2.** A menudo se dice que `async/await` es "azúcar sintáctico" sobre las Promesas. ¿Qué significa esta afirmación? Explícalo con tus palabras.
* **5.3.** Tomando como base el código que creaste para la pregunta 4.3, reescríbelo utilizando la sintaxis `async/await` y un bloque `try...catch` para manejar tanto el caso de éxito como el de error.

**[ESPACIO PARA TU RESPUESTA 5]**