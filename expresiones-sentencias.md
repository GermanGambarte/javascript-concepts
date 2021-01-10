Los leguajes de programación tienen una sintaxis, es decir un grupo de reglas que definen cómo podemos conbinar distintos símbolos para producir intrucciones válidas y así crear un programa que la computadora entienda.

Una computadora no puede entender un programa si no cumple con la sintaxis del lenguaje que estemos usando. En JAVASCRIPT existen dos estructuras sintácticas para escribir programas: las EXPRESIONES y las SENTENCIAS.

## Expresiones

Las EXPRESIONES nos sirven para producir nuevos valores. Estas son basicamente una unidad de código que produce en valor. Además, algunas expresiones pueden tener efectos secundarios

Las que no, simplemente pueden ser remplazadas por el por el valor que producen
```
10 + 10
// ↪ 20
```
Podemos pensar las expresiones en JavaScript como las palabras o pequeñas frases del español. Supongamos que tenemos que asiganarle un valor a una variable. ¿Qué expresiones usariamos?

Empecemos por la más basica: **expresiones primarias**, se considera como tal a cualquier palabra pequeña que por sí sola produzca una valor, un ejemplo de esto son los valores primitivos
```
let unaVariable;
unaVariable = 'texto';
unaVariable = 123;
unaVariable = true;
unaVariable = false;
unaVariable = null;
unaVariable = undefined;
unaVariable = Symbol('foo');
unaVariable = 9007199254740992n;
```
Son las más basicas de todas, ya que al ser evaluadas producen el mismo valor que tienen. Tambien podemos usar ciertas palabras reservadas del lenguaje como ***this*** o el nombre de otra variable. Estas tambien son consideradas como **expresiones primarias**
```
let unaVariable;
unaVariable = this;
unaVariable = otraVariable;
```
### Objetos y Arrays

Otras expresiones mas complejas que los valores primitivos son los objetos y los arrays.

En cada posición del array debe ir un valor o algo que produzca un valor, es decir una expresión
```
const arr = [10, 20, 15 * 2];
```
Y los mismo ocurre con los objetos, estos tiene claves y valores. Las claves generalmente son strings que no necesitan comillas a no ser que contengan espacios y los valores son expresiones
```
const usuario = {
    nombre: 'Germán',
    apellido: 'Gambarte',
    'usuario de twitter': '@gerchugambarte'
};
```
Lo que hay que tener en cuenta es que en JavaScript a diferencia de los valores primitivos, los objetos, arrays y las funciones, son evaluadas como referencia, esta es la posicion en memoria donde se encuentran almacenados esos objetos. Pero son transparentes para nosotros, no las podemos ver.

Si creamos dos objetos con las mismas propiedades y valores, estos van a guardarse en posiciones de memoria distintas y si los comparamos no vas a ser iguales, porque lo que JavaScript va a evaluar son las referencias.
```
const german1 = { nombre: 'Germán' };
const german2 = { nombre: 'Germán' };

german1 === german2
// ↪ false
```

### Expresion de Función

Lo mismo sucede con las funciones, esto me lleva a hablar del siguiente tipo de expresion, la **expresión de función**.

Así como teniamos los strings, los números o los objetos, en JavaScript tambien podemos usar las funciones como valores
```
let unaVariable;
unaVariable = function saludar() {
    console.log('Hola!');
}
```
Cuando escribimos una función en un lugar del código donde se espera un valor, estamos escribiendo lo que se conoce como **expresión de función** (function expression).

Podemos asiganar una función como variable o podemos pasarla como parametro cuando invocamos a otra función
```
const func = function saludar() {
    console.log('Hola!');
}

numeros.filter(function filtrarPares(numero) {
    return numero % 2 === 0;
});
```
Cuando una función como valor no es necesario que le demos un nombre, puede ser una función anonima
```
const func = function saludar() {
    console.log('Hola!');
}

numeros.filter(function(numero) {
    return numero % 2 === 0;
});
```
O podriamos escribirla como una **arrow function** y seguiria siendo una expresión de función
```
const func = function saludar() {
    console.log('Hola!');
}

numeros.filter(numero => numero % 2 === 0);
```
Algo diferente seria escribir una función de la siguiente manera
```
function saludar() {
    console.log('Hola!');
}

numeros.filter(numero => numero % 2 === 0);
```
Pero ya vamos a llegar a eso.

### Propiedades de los objetos

Tambien podemos usar alguna propiedad de un objeto como expresión, escribiendo el nombre del objeto luego un punto y el nombre de la propiedad o remplazando el punto por corchetes que contengan el nombre de la propiedad entre comillas
```
let unaVariable;
const miObjeto = { nombre: 'Germán' };

unaVariable = miObjeto.nombre;
// ↪ 'Germán'

unaVariable = miObjeto['nombre'];
// ↪ 'Germán'
```
Y para los array es lo mismo, pero con expresiones numericas que indican la posicion de los valores que contienen, teniedo en cuenta que las posiciones se empiezan a contar desde el **0**
```
let unaVariable;
const miArray = [29, 43, 98];

unaVariable = miArray[0]
// ↪ 29
```
Si hablamos de producir un valor una expresion que no puede olvidarse es la invocación de una función. En JavaScript cuando invocamos a una función, siempre obtendremos algún valor de retorno

Si tenemos una función que no tiene un **return** en su cuerpo, por defecto va a retornar **undefined**
```
let unaVariable;

function saludar() {
    console.log('Hola!');
}

unaVariable = saludar();
// ↪ undefined
```
En cambio si tenemos un **return** dentro del cuerpo de la función obtendremos el valor que le expresemos cuando la invoquemos
```
let unaVariable;

function sumar(n1, n2) {
    return n1 + n2;
}

unaVariable = sumar();
// ↪ 30
```
Y si una función retorna un objeto un array u otra función, basicamente algo que no sea un valor primitivo, lo que nos va a devolver es la referencia para acceder a ese objeto, array o función 
```
let unaVariable;
function crearUsuario(nombre) {
    return {
        nombre: nombre.toUpperCase()
    };
}

unaVariable = crearUsuario('Germán')
unaVariable = crearUsuario('Germán')
unaVariable = crearUsuario('Germán')
```
Por cada una de esas invocaciones estamos recibiendo una refencia distinta.

### Invocacion de Función

Invocar a una función es de los ejemplos mas claros que tenemos para producir valores, pero hay que tener cuidado porque alguna funciones ademas de retornar un valor tienen efecos secundarios.

Por ejemplo al invocar a la función **setTimeout()** 
```
setTimeout(function () {
    console.log('Esto se va a ejecutar más tarde');
},2000)
```
Obtendremos una identificador para cancelar el timer si quisieramos
```
const timerId = setTimeout(function () {
    console.log('Esto se va a ejecutar más tarde');
},2000)
```
Aunque lo que nos interesa principalmente es que se produzaca su efecto secundario, en este caso, postergar la ejecucios de esta función cierta cantidad de milisegundos más tarde.

Otro ejemplo podria se si creamos un elemento **h1** y le ponemos algo de texto como su contenido
```
const titulo = document.createElement('h1');
titulo.innerHTML = 'Mi título'
```
Al invocar un **appendChild()**, obtenemos como resultado el mismo elemento que pasamos por parametro.
```
const titulo = document.createElement('h1');
titulo.innerHTML = 'Mi título'
const element = document.body.appendChild(titulo)
// ↪ <h1>Mi título</h1>
```
Siendo que estamos más interesados en que se produzca su efecto secundario que es que ese elemento se agregue al cuerpo de de nuestro documento, para que podamos verlo en la pantalla.
```
const titulo = document.createElement('h1');
titulo.innerHTML = 'Mi título'
document.body.appendChild(titulo)
```

### Constructor
Cuando creamos un objeto con un constructor tambien estamos produciendo un nuevo valor
```
let unaVariable = new Date(2021,01,09);
```
Crear un objeto es similar a invocar una función solo que anteponemos la palabra **new** y si el constructor no lleva parametros, podemos prescindir de los parentesis
```
let unaVariable = new Date;
```
### Operadores
Los operadores nos permiten generar nuevos valores, apartir de una o mas expresiones.

Una operación entre dos números genera como valor el resultado de esa operacion
```
let resultado = 10 + 20;
// ↪ 30
```
Pero no solo existen las operaciones numéricas, si una variable tiene un valor booleano, podemos generar el opuesto con el operador de negación
```
let activo = false;

let activo = !activo;
// ↪ true
```
De todas formas la gran mayoria de operadores neceitan dos expresiones. Si a una variable le asignamos una comparación, en ella se guardará el resultado que esta misma produzca
```
let activo = usuario.nombre !== 'Invitado!;
// ↪ true
```
Y podemos lograr lo mismo con comparaciones numericas
```
let tieneEnvioGratis = producto.precio >= 1000;
```
Cuando asiganamos valor a una variable tambien estamos usando un operador, el de asignación (=) y este tambien nos produce un valor, el que le estamos asignando
```
let unaVariable = 20;
```
Generalmente no usamos el operador de asignación por el valor que produce, sino que lo usamos para que se produzca el efecto secundario que tiene, para que una variable tome un nuevo valor. Pero no estamos aca para hablar de operadores, asi que como conclusión decimos que los operadores son expresiones debido a que nos permiten producir nuevos valores.

### Nuevas expresiones
En versiones recientes del lenguaje se sumaron algunas expresiones nuevas:
- la expresion de función asincrona (async function)
- la invocación de una función asincrona (await)
- los generadores (function*)

Cada una de ellas se merece su propia explicación, por ahora solo nos quedaremos con el conocimiento de que existen.

## Sentencias
Si dijimos que las expresiones son como las palabras en nuestro idioma, las sentencias serian las oraciones
Las SENTENCIAS son las acciones que hacen avanzar la lógica de nuestro programa.

