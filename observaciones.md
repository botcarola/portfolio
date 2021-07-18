# Observaciones

Caro, felicitaciones por tu trabajo. Tu portfolio se ve muy lindo; me alegra ver que en general seguiste las pautas del diseño solicitado pero a la vez le diste tu toque personal. Me gustan muchisimo las imagenes e iconos elegidos, la eleccion de colores. Se nota, y aprecia, que hubo mucho trabajo para lograr una web que te represente y que sea amable con el usuario.

Viendo tu codigo, se nota mucho el esfuerzo por lograr que tu web se vea bien en distintos dispositivos. La estrategia que hiciste fue enfocarte en algunos dispositivos, con una consecuencia indeseada: tu web se ve bien sólo en ellos, pero mal en cualquier dispositivo que no tenga esas medidas específicas (entre ellas, mi computadora). Tu diseño no es "responsive" (responde y se adapta a distintas medidas) en el sentido estricto: esta adaptado a algunas medidas de mobile. 

No quiero dejar pasar el enorme esfuerzo que pusiste aquí, porque se nota que invertiste mucho tiempo, pero por decirlo con alguna metáfora, tu codigo es responsive "a martillazos": acomodaste las cosas en cada media query para que se adaptaran a esa medida en especifico, en lugar de tener un codigo que solito pueda adaptarse lo mas posible a distintas medidas de manera fluida. Esto parece muy facil decirlo, y es muy dificil de hacer, pero con el tiempo y practica se te va a hacer mas facil. Dejo en la seccion de responsive algunos comentarios mas sobre eso. 

Te dejo varios comentarios para mencionar cositas puntuales. Como comentamos en clase, este trabajo no se hace para que constates conocimientos, sino para que aprendas: en ese sentido, mi intencion es que estos comentarios te sirvan para aprender, mejorar tu codigo a futuro e ir apreciando mejor qué se espera de nosotras como desarrolladoras front end.

## Estructura correcta de documento HTML

Cumplido en general. 

Algo que me llama la atención es tu `header`, dado que allí repetís innecesariamente muchísimos links. Cosas como esta se repiten un montón:

```html
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.3/css/all.css" integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.3/css/all.css" integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.3/css/all.css" integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.3/css/all.css" integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.3/css/all.css" integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk" crossorigin="anonymous">
```

Cada uno de esos links hace exactamente lo mismo - traerse el css de fontawesome para poder usar los íconos en tu sitio. Quizá estés bajo la impresión de que por cada uno de los íconos de tu web es necesario traerse nuevamente el css, pero no, no es necesario agregarlo más de una vez. Agregar muchos de estos links innecesarios impacta negativamente en la velocidad de carga de tu web, ya que por cada uno de ellos se hace un llamado a un css externo y se lo carga. Esto para cada uno de los distintos css que te importas. Deberia haber solo uno de cada uno. 

La etiqueta `<link rel="stylesheet">`implica que vas a traer un css. Por eso una orden como esta no tiene sentido:

```html
   <!-- imagen header-->
    <link href="undraw_Portfolio_re_qwm5 (1).svg" rel="stylesheet">
```

Eso no es un stylesheet, es la imagen de tu portfolio. Esa imagen la pones en el src de la etiqueta `img`. No deberia estar en el head.

Por ultimo, esta etiqueta es para css. Si queres traerte tipografias de google font tenes que usar `<link>`. 

```html
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cookie&family=Lobster&display=swap');
    </style>
```


## Respeta la consigna 

- El portfolio cuenta con las secciones solicitadas 

Cumplido


- Al clickear en los links de navegación, debe llevar a la sección correspondiente

Cumplido con la excepcion del boton "lo que hago", que deberia llevar a "Mis proyectos". 

- Al clickear en los links de contacto, debe llevar a la página externa
correspondiente 

Cumplido, excepto por el email. Para agregar un link a un email usa el atributo `mailto`: `<a href="mailto: carola@gmail.com">Email</a>` 

- El portfolio debe tener un diseño responsivo y verse correctamente en distintos dispositivos 

Cumplido a medias. Como comenté más arriba, tu web no es estrictamente responsive sino que está adaptada a algunas medidas en especifico: se ve mal en todas las demás. 

El primer y grave problema son estas ordenes de css: 

```css
@media screen and (max-width: 360px) and (min-height: 640px){
...

@media screen and (min-width: 411px) and (max-height: 823px){
...

@media screen and (min-width: 375px) and (max-height: 812px){
```

Entiendo tu intención: querías hacer una media query para esa medida en especifico. Pero fijate bien la orden: al decir "min-width: 411px" y "max-height: 823px" estas diciendo: "esta media query se va a aplicar en **todas** las pantallas que tengan como minimo 411px de ancho y como maximo 832px de alto". La pantalla de mi computadora tiene 1200px de ancho y 750px de alto, asi que cuando entro a tu pagina, veo esa media query aunque esté viéndola en escritorio. "Max height" no significa "esta altura justa", significa "como maximo esta altura". Igual que "min width", que significa "como minimo este ancho". 

En general no hacemos media queries tomando en cuenta el alto de la pantalla - ya que asumimos que nuestro codigo se va a ver bien en cualquier altura - sino que usamos solamente el ancho. Creo que comenté en clase que lo más habitual es seguir las media queries que sugiere bootstrap. Te las dejo como una guia para futuros trabajos:

```css
/* Celulares: hasta 320px debería verse bien */
@media (max-width: 576px) {
  ...;
}

/* Celulares en modo horizontal y tablets pequeñas */
@media (max-width: 768px) {
  ...;
}

/* Tablets  */
@media (max-width: 992px) {
  ...;
}

/* Monitores pequeños */
@media (max-width: 1200px) {
  ...;
}

/* Monitores grandes */
@media (max-width: 1400px) {
  ...;
}
```

Otro problema grave de tu responsive es que le diste alturas fijas a tus divs contenedores y a tus secciones, por ejemplo aqui: 

```css
.contenedorheader{
    width: 100%;
    height: 1000em;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #E5EAF5;
}
```

Los divs se acomodan naturalmente para ocupar el 100% de su ancho (por eso nunca damos esa orden, es redundante) y su altura esta dada por su contenido. Abrite un HTML y CSS nuevos y proba este codigo:

```html
<div class="sin-altura">Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolore illo sequi quos, rerum aspernatur, quasi, earum amet placeat velit labore laboriosam corrupti facilis sed totam! Placeat magnam mollitia eius ab doloribus excepturi. Saepe asperiores nemo nisi voluptatum impedit nam, dolorum non similique vero nesciunt ullam ab possimus, quisquam provident, velit necessitatibus consectetur et libero ad aperiam aliquam quos dolore? Earum provident quasi ducimus deserunt voluptatum officiis a accusamus optio, commodi, dolor facere ipsam debitis tempore eaque praesentium veniam autem dolorem quidem fugiat ad temporibus nisi iure molestiae mollitia! Eum veritatis aliquam repellat quos quae, consequuntur voluptatum voluptas minus reprehenderit. Fugiat.</div>

<div class="con-altura">Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolore illo sequi quos, rerum aspernatur, quasi, earum amet placeat velit labore laboriosam corrupti facilis sed totam! Placeat magnam mollitia eius ab doloribus excepturi. Saepe asperiores nemo nisi voluptatum impedit nam, dolorum non similique vero nesciunt ullam ab possimus, quisquam provident, velit necessitatibus consectetur et libero ad aperiam aliquam quos dolore? Earum provident quasi ducimus deserunt voluptatum officiis a accusamus optio, commodi, dolor facere ipsam debitis tempore eaque praesentium veniam autem dolorem quidem fugiat ad temporibus nisi iure molestiae mollitia! Eum veritatis aliquam repellat quos quae, consequuntur voluptatum voluptas minus reprehenderit. Fugiat.</div>
```

```css
.sin-altura {
    width: 300px;
    background-color: pink;
}

.con-altura {
    width: 300px;
    height: 400px;
    background-color: pink;
}
```

Ves como el div "sin-altura" se vuelve muuuy alto, para que entren todas las palabras? Y como el div "con altura" se queda de la altura que le dijimos, pero las palabras "rebalsan"? Pasa lo mismo con todos los demas elementos de html como titulos, listas, imagenes, otros divs: si no tienen espacio en la altura que vos les diste, rebalsan. 

No podes saber por adelantado cual sera el tamaño de los dispositivos de tus usuarios, asi que no podes saber por adelantado si height: 1000em;  es una medida apropiada. Mucho mejor es no darles una altura a tus secciones y dejar que ellas solitas se adapten a su contenido. La excepcion, por supuesto, son las cosas que si tienen una medida fija como tarjetas: ahi ponemos poco texto y confiamos en que se veran bien en cualquier pantalla. 

- El portfolio debe estar deployado y ser accesible desde una URL 

Cumplido

- El repositorio en GitHub debe tener un readme adecuado 

Cumplido. 

### Respeta el diseño dado 

Cumplido. 

### Buena estructura de proyecto 

Usás muchas imágenes en tu proyecto, y viéndolo a primera vista en github no es tan fácil ver cuáles son los archivos principales. Siempre que uses imágenes locales, como en este caso, agregalas a una carpeta que se llame por ejemplo "imgs", "imagenes" o "assets". De esta manera solo los archivos principales - html, readme y css - son los que están en la carpeta principal. La excepción a esta regla es el favicon, que siempre debería ir en la carpeta principal. 

### Código bien indentado 

En general tabulás bien, pero muchas veces perdés la estructura que venías haciendo. Siempre que una etiqueta esté adentro de otra, dejamos dos espacios (o cuatro, eso es preferencia):

```html
<body>   
    
    <!-- SECCIÓN DEL NAV-->

    
        <nav>
            <span class="listadetalles">
            <ul class="listanav">
```

Ahi tenes ocho espacios entre body y nav (deberian ser cuatro) y ningun espacio entre span y ul (a pesar de que span es padre de ul). Debería estar así:

```html
<body>   
    <!-- SECCIÓN DEL NAV-->
    <nav>
        <span class="listadetalles">
            <ul class="listanav">
```

Recordá que con click derecho + format document, VSCode te corrige el tabulado automáticamente. 

Dejás muchiiiiisimos saltos de linea absolutamente innecesarios en tu codigo, lo que dificulta mucho su lectura. Imaginate que yo te hiciera esta devolucion



dejando espacios así


salpicados durante todo el texto. 






La lectura se dificulta un poco, no? Lo mismo ocurre con el código. LLeva tiempo entrenar el ojo para empezar a ver estas cosas, pero en unos meses se te va a hacer costumbre. Mientras antes puedas incorporar esto, mejor. 

Otras veces olvidas dejar saltos de linea entre etiquetas, como aqui:

```html
<div class="card"><i class="fab fa-html5"></i><h2 class="estilotexto">HTML 5</h2></div>
```

Es muy dificil apreciar a primera vista que ahi hay un div que adentro tiene un i y un h2. Mejor dejar saltos de linea en esas ocasiones:

```html
<div class="card">
    <i class="fab fa-html5"></i>
    <h2 class="estilotexto">HTML 5</h2>
</div>
```

Tengo las mismas observaciones para tu css: saltos de linea innecesarios, tabulado confuso, y ademas la costumbre de no dejar un espacio entre el nombre de la clase y la llave de apertura. Por ejemplo esto:

```css
.listanav{
    display: flex;
    justify-content: space-around;
    align-items: center;
    

    }
    
    .navmargen{
        margin-left: 1em ;
        margin-right: 1em;

    }
```

deberia estar asi:

```css
.listanav {
    display: flex;
    justify-content: space-around;
    align-items: center;
}    

.navmargen {
    margin-left: 1em ;
    margin-right: 1em;
}
```


### Comentarios que permiten mejorar la legibilidad del código 

Cumplido, aunque sería correcto que uses el mismo formato para todos: o todos en mayuscula, o todos con signos de exclamacion, o todos en minúscula. 

### Uso correcto de etiquetas semánticas 

En general, bien. 

`span` es la etiqueta que identifica un cachito de texto para resaltarlo. No debería tener dentro nada mas que texto. Lo usás ocasionalemente como si fuera un `div`. Eso no es correcto. 

Tu nombre es el texto mas importante de tu web, por lo que debería estar en un `h1` y no en un `p`.

No usas la etiqueta `section` para distintas secciones, lo que le dificulta la tarea a un lector de pantalla. 

Usas los titulos h con poco criterio. El h1 es el titulo principal, y debería haber sólo uno por página. El resto deberían estar en orden de jerarquía: h2 para los titulos de secciones, h3 para los títulos dentro de cada subsección, etc. En este caso, "Mis conocimientos", "Mis proyectos" etc deberían ser h2 y los títulos de las cards deberían ser h3. Los demas textos que no son titulos no deberian tener etiquetas h, deberian ser p. 

### Buenos nombres de clases 

No está cumplido. Luego del tabulado, es el factor que más atenta contra la calidad de tu código. Es muy dificil entender tu CSS porque no hay manera de saber a que se refiere cada cosa: hay que estar chequeando a cada rato el HTML para poder entenderlo. 

Cuando decimos que un nombre de clase debe ser descriptivo, lo decimos en un sentido funcional: qué rol cumple este elemento en el código. Los colores de los elementos, su forma, su estilo, su posición, todas esas cosas pueden cambiar y efectivamente cambian todo el tiempo en las webs que hacemos. El botón que hoy es un circulo mañana será cuadrado; la sección que estaba primera mañana estará tercera, por lo que no sirve decir "seccion2". Esos factores sos no son buenos descriptores, y no deberían ser parte de nuestros nombres de clases.

Otros nombres de clases que usas directamente no tienen sentido. "navmargen", "focus-input", "espacio" son algunos ejemplos. Entiendo que es dificil pensar buenos nombres, y es algo con lo que todos renegamos alguna vez, pero es importante que te vayas acostumbrando a darle más atención a eso. 

Cuando quieras separar palabras, poneles un guion: "navmargen", "botoncontacto", son dificiles de leer. 

En resumen, a la hora de darle un nombre de clase a algo, pensá qué es ese elemento, qué función cumple en tu página. No qué estilos tiene, ni en dónde aparece. Los links a redes sociales de tu footer son eso: links a las redes sociales de tu footer, independientemente de tener de forma un circulo o tener espacios entre ellos o el margen que puedan tener. "footer-links-redes-sociales" es el nombren apropiado. 

### Código CSS bien estructurado 

Cumplido a nivel formal. Noto muchos estilos innecesarios o confusos, que te voy indicando en tu archivo de css. 

### Reutilización de estilos 

Cumplido en general, veo mucho interés en usar las mismas clases a lo largo del trabajo.

### Cumple con criterios básicos de accesibilidad 

Eliminas el outline en el boton del formulario, y la unica indicacion en el focus es el borde del mismo color del boton, por lo que no se ve el foco cuando esta en ese elemento. 

Te faltan muchas etiquetas semanticas como te comenté en esa ssección que harían que tu web sea mas amable con el lector de pantalla. 

- Los colores tienen un contraste adecuado 

Cumplido

- Las imágenes tiene el atributo `alt` que corresponde 

Cumplido a nivel formal, pero una persona que necesita de un lector de pantalla no va a entender nada en tu pagina. 

La imagen del header: "imagen de presentacion" no le dice nada a la persona no vidente que usa tu pagina con un lector de pantalla - y no necesitas aclarar que es una imagen, eso ya lo hace el lector. Que es tu imagen? Que representa? "Mujer utilizando una computadora" es mejor nombre. 

Revisa los alt de Mis proyectos: se entienden? Alguien que no puede ver la imagen, va a sacar en limpio algo de lo que representan estas imagenes? Si la persona no entiende inglés, va a poder entender todo? Pensa que son frases leidas por un bot. Al leer podemos entender que "movienight" es "movie night", pero un bot no puede hacer ese razonamiento. Pensa que como tu web esta en español, la mayoria de los usuarios van a tener un lector de pantalla que lea español: como va a leer "movienight"?

- alt="Portfolio"
- alt="memegenerator"
- alt="player"
- alt="wallet"
- alt="calendario"
- alt="list"
- alt="movienight"

Tus iconos del footer tienen alt, pero comentamos en clase que los lectores de pantalla no ven los iconos a menos que les agreguemos "role=img", asi que son inutiles en ese caso.

- Los íconos y elementos que no presentan texto agregan la información correspondiente por otros medios (etiquetas aria, texto oculto) 

No cumplido, por ejemplo en los links a redes sociales de tu footer. Necesitan un aria-label, no un alt. 

- Los íconos y elementos que no necesitan ser anunciados por un lector de pantalla tienen la etiqueta aria
correspondiente 

No cumplido. 

- Commits con mensajes adecuados 

Cumplido, noto muchos y buenos commits en tu proyecto, lo que siempre se agradece. 

- Cuenta con un favicon

Cumplido, pero el favicon deberia llamarse `favicon.ico` ya que ese es el archivo que van a buscar la mayoria de los servicios de hosting. 

### Nota: 7