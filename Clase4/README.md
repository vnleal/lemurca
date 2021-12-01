# JavaScript: Datos y bibliotecas

### Clase 4 → 30-11-2021

- - - - - - - 

#### Presentación

**En JavaScript podemos crear toda variables con una palabra reservada, que puede ser `var`, `let` o `const`**. Para entender la diferencia entre las opciones, conviene consultar el artículo [*Var, let y const. ¿Donde, cuando y por qué?*](https://medium.com/@tatymolys/var-let-y-const-donde-cuando-y-por-qu%C3%A9-d4a0ee66883b) 

Imaginemos las variables creadas como cajas marcadas. Por ejemplo, `var a` crea una caja marcada con una `a`. En cada caja podemos meter datos que pueden variar en la ejecución del programa completo (por eso `var`), sólo en un contexto (`let`) o pueden quedarse constantes, sin variar (`const`).

A esta caja creada con `var`, `let` o `const` le podemos asignar valores de distintos tipos: 

```
//número entero
var a = 18261884;

//número de punto flotante
var b = 24.15267252;

//booleano
var c = true;

//cadena de caracteres
var d = "Lisa the Vegetarian";

//arreglo
var e = ["Marge Simpson", "Homer Simpson", "Bart Simpson", "Lisa Simpson", "Maggie Simpson"];

//objeto
var f = {
    mom: "Luann Van Houten",
    dad: "Kirk Van Houten",
    child: "Milhouse Van Houten"
};

//objeto con arreglo
var g = {
    mom: "Marge Simpson",
    dad: "Homer Simpson",
    children: ["Bart Simpson", "Lisa Simpson", "Maggie Simpson"]
};

//arreglo con objetos y objetos con arreglo
var h = [
    {
        mom: "Luann",
        dad: "Kirk",
        children: ["Milhouse"]
    },
    {
        mom: "Marge",
        dad: "Homer",
        children: ["Bart", "Lisa", "Maggie"]
    },
    {
        mom: "Manjula",
        dad: "Apu",
        children: ["Poonam", "Sashi", "Pria", "Uma", "Anoop", "Sandeep", "Nabendu", "Gheet"]
    }
];

```

Notemos que el contenido de `a`, `b` y `c` no se presenta entre comillas. Pero el contenido de `d` sí debe presentarse entre comillas, porque se trata de una cadena de caracteres (*string*). 

La variable `e`, que contiene un arreglo, usa paréntesis cuadrado y cada elemento, por tratarse de un *string*, usa comillas (si fuesen números o booleanos no las usarían). 

La variable `f`, que contiene un objeto, usa paréntesis de llave que en su interior contiene pares de `nombre:valor`. 

Las variables `g` y `h` son mezclas de las anteriores.

Si necesitamos el valor de las variables `a`, `b`, `c` o `d`, basta con pedirlo directamente. Pero el caso es distinto si necesitamos un valor específico dentro de las variables  `e`, `f`, `g` o `h`.

Para comprender de mejor manera lo recién expuesto, practiquemos con el siguiente código: 

```
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <title>¡Hola variables!</title>
    </head>
    <body>
        <h1>Construyamos algunas cosas a continuación, con:</h1>
        <ul></ul>
        <p id="favoritismo">Yo prefiero a</p>
        <script>
            var e = ["Marge Simpson", "Homer Simpson", "Bart Simpson", "Lisa Simpson", "Maggie Simpson"];
            var f = {
                mom: "Luann Van Houten",
                dad: "Kirk Van Houten",
                child: "Milhouse Van Houten",
            };
            var g = {
                mom: "Marge Simpson",
                dad: "Homer Simpson",
                children: ["Bart Simpson", "Lisa Simpson", "Maggie Simpson"],
            };
            var h = [
                {
                    mom: "Luann",
                    dad: "Kirk",
                    children: ["Milhouse"],
                },
                {
                    mom: "Marge",
                    dad: "Homer",
                    children: ["Bart", "Lisa", "Maggie"],
                },
                {
                    mom: "Manjula",
                    dad: "Apu",
                    children: ["Poonam", "Sashi", "Pria", "Uma", "Anoop", "Sandeep", "Nabendu", "Gheet"],
                },
            ];
            e.forEach((item) => {
                document.querySelectorAll("ul")[0].innerHTML += "<li>" + item + "</li>";
            });
            document.querySelector("#favoritismo").insertAdjacentHTML("beforeend", g.children[1]);
        </script>
    </body>
</html>
```
Habría que copiar el código, para luego pegarlo en un documento nuevo creado en Atom o Sublime Text. Guardarlo con extensión `.html`, y abrirlo en su navegador web.

En el código aprovechamos las variables `e` y `g`, además del método [`forEach()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/forEach).

Para aprovechar la variable `h`, antes convendría revisar los métodos:

- [`sort()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/sort);

- [`includes()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String/includes).

Uno de los métodos recién mencionados puede encontrarse entre [las *Top 10 Must Know JavaScript Functions*](https://www.thedailytechtalk.com/top-10-must-know-javascript-functions/).

- - - - - - -

#### Exploración

Volvamos a la variable `h`, que está más arriba y contiene un arreglo de objetos. Comparémosla con https://myjson.dit.upm.es/api/bins/1wo6

Para hacer "más legible" lo del vínculo, podemos instalar en el navegador una extensión como JSON Formatter (disponible para [Chrome](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=es) y [Firefox](https://addons.mozilla.org/es/firefox/addon/json-formatter/)). 

Lo que se hace "más legible" con tal extensión en sus navegadores web es [JSON](https://www.json.org/json-es.html) (JavaScript Object Notation), un formato ligero de intercambio de datos. Como indica su nombre, se debe a la notación de objetos de JavaScript: La única diferencia con la notación original es el uso de comillas antes y después de los dos puntos (:) que separan al par nombre y valor. Por eso `mon`, `dad` y `children` en la variable `h` tiene algo distinto en el [JSON ya referido](http://myjson.dit.upm.es/api/bins/1wo6)

¿Cómo podría ir a buscar ese JSON en línea para trabajar con él? Hay varias maneras, pero a continuación nos aprovechamos de [una petición básica de **fetch**](https://developer.mozilla.org/es/docs/Web/API/Fetch_API/Using_Fetch#on-github):

```
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <title>¡Hola fetch!</title>
    </head>
    <body>
        <h1>Por favor revisen la consola de JavaScript</h1>
        <script>
            fetch('https://myjson.dit.upm.es/api/bins/1wo6').then(response => response.json()).then(data => console.log(data));
        </script>
    </body>
</html>
```

Con tal petición, podemos aprovechar muchos datos que ya están en línea:

- Personajes de StarWars: https://swapi.dev/api/people/?format=json
- Tiempo atmosférico: https://openweathermap.org/current#current_JSON
- Movimientos telúricos: https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php
- Datos públicos: https://github.com/juanbrujo/listado-apis-publicas-en-chile
- Y un larguísimo etcéctera de [APIs](https://es.wikipedia.org/wiki/Interfaz_de_programaci%C3%B3n_de_aplicaciones) y cuanto dato se disponga en tal formato.

- - - - - - - 

#### Aplicación

Revisemos dos ejemplos más de uso de JavaScript: 

- El primero podría ser aplicado en la infografía que trabajan, en caso necesiten [seleccionar elementos en un SVG](https://profesorfaco.github.io/infografia/clase-4/favoritismo.html).

- El segundo podría servir para otroso trabajos, extendiendo lo que hemos visto sobre [consulta de datos en línea y Bootstrap](https://profesorfaco.github.io/infografia/clase-4/elecciones.html)

Tales ejemplos tienen por objetivo mostrarles el potencial de dos herramientas que podrían, incluso, mezclar en sus propias infografías.

- - - - - - - -

###### [← CLASE PASADA](https://github.com/profesorfaco/infografia/tree/main/clase-3) — [CLASE SIGUIENTE →](https://github.com/profesorfaco/infografia/tree/main/clase-5) 
