<!-- Script JS -->
<script>
  import { onMount } from "svelte";
  import DropdownButton from "/src/data/DropdownButton.svelte";

//variables
let contador = 0;
let respuesta1 = 0;
let respuesta2 = 0;
let respuesta3 = 0;
let respuesta4 = 0;
let respuesta5 = 0;

//cambiar el cursor
let circles = [];
  const maxCircles = 30; // Máximo de círculos en el rastro

  function handleMouseMove(event) {
    const { clientX, clientY } = event;

    // Añadimos un nuevo círculo con la posición del cursor
    circles = [
      ...circles,
      { x: clientX, y: clientY, id: Math.random() }
    ];

    // Limita el número de círculos para evitar acumulación infinita
    if (circles.length > maxCircles) {
      circles.shift();
    }
  }

  onMount(() => {
    window.addEventListener("mousemove", handleMouseMove);

    return () => {
      window.removeEventListener("mousemove", handleMouseMove);
    };
  });

  //boton desplegable
// Opciones para el primer botón
  const options1 = [
    {
      label: "Casual",
      content: `<div><img src="./images/Casual.png" alt="casual"/></div>`
    },
    {
      label: "Estrategia",
      content: `<div><img src="./images/Estrategia.png" alt="estrategia"/></div>`
    },
    {
      label: "Idle",
      content: `<div><img src="./images/Idle.png" alt="idle"/></div>`
    },
    {
      label: "Tycoon",
      content: `<div><img src="./images/Tycoon.png" alt="tycoon"/></div>`
    },
    {
      label: "Aventura",
      content: `<div><img src="./images/Aventura.png" alt="aventura"/></div>`
    }
  ];

  // Opciones para el segundo botón
  const options2 = [
    {
      label: "Suspenso",
      content: `<div><img src="./images/Suspenso.png" alt="suspenso"/></div>`
    },
    {
      label: "Acción",
      content: `<div><img src="./images/Accion.png" alt="accion"/></div>`
    },
    {
      label: "Romántico",
      content: `<div><img src="./images/Romantico.png" alt="romantico"/></div>`
    },
    {
      label: "Realista",
      content: `<div><img src="./images/Realista.png" alt="realista"/></div>`
    },
    {
      label: "Caricatura",
      content: `<div><img src="./images/Caricatura.png" alt="caricatura"/></div>`
    },
  ];

  //botones comparativos
  //Resultado 1
  const options3 = [
    {
    label: "Among Us",
    content: `<div><img src="./images/AmongUs.png" alt="amongus"/></div>`
    },
    {
      label: "Bloons TD",
      content: `<div><img src="./images/BloonsTD.png" alt="bloonstd"/></div>`
    },
    {
      label: "Cafeteria Dulce",
      content: `<div><img src="./images/CafeteriaDulce.png" alt="cafeteriadulce"/></div>`
    },
    {
      label: "Candy Crush",
      content: `<div><img src="./images/CandyCrush.png" alt="candycrush"/></div>`
    },
    {
      label: "Clash Royale",
      content: `<div><img src="./images/ClashRoyale.png" alt="clashroyale"/></div>`
    },
    {
      label: "Criminal Case",
      content: `<div><img src="./images/CriminalCase.png" alt="criminalcase"/></div>`
    },
    {
      label: "Crossy Road",
      content: `<div><img src="./images/CrossyRoad.png" alt="crossyroad"/></div>`
    },
    {
      label: "Fallout Shelter",
      content: `<div><img src="./images/FalloutShelter.png" alt="falloutshelter"/></div>`
    },
    {
      label: "Gatos y Sopa",
      content: `<div><img src="./images/GatosySopa.png" alt="gatos y sopa"/></div>`
    },
    {
      label: "Kitty Collector",
      content: `<div><img src="./images/KittyCollector.png" alt="kittycollector"/></div>`
    },
    {
      label: "League of Legends",
      content: `<div><img src="./images/LeagueofLegends.png" alt="LOL"/></div>`
    },
    {
      label: "Marvel Batalla",
      content: `<div><img src="./images/Marvel.png" alt="Marvel"/></div>`
    },
    {
      label: "Monument Valley",
      content: `<div><img src="./images/MonumentValley.png" alt="monumentvalley"/></div>`
    },
    {
      label: "Plantas vs Zombies",
      content: `<div><img src="./images/PlantasvsZombies.png" alt="plantasvszombies"/></div>`
    },
    {
      label: "Pocket Love",
      content: `<div><img src="./images/PocketLove.png" alt="pocketlove"/></div>`
    },
    {
      label: "Pockemon Unite",
      content: `<div><img src="./images/Pockemon.png" alt="pockemon"/></div>`
    },
    {
      label: "Pou",
      content: `<div><img src="./images/Pou.png" alt="Pou"/></div>`
    },
    {
      label: "Preguntados",
      content: `<div><img src="./images/Preguntados.png" alt="preguntados"/></div>`
    },
    {
      label: "RollerCoaster",
      content: `<div><img src="./images/RollerCoaster.png" alt="rollercoaster"/></div>`
    },
    {
      label: "Simcity",
      content: `<div><img src="./images/Simcity.png" alt="simcity"/></div>`
    },
    {
      label: "Sky:Niños de la luz",
      content: `<div><img src="./images/Sky.png" alt="sky"/></div>`
    },
    {
      label: "SubwaySurfers",
      content: `<div><img src="./images/SubwaySurfers.png" alt="subwaysurfers"/></div>`
    },
    {
      label: "Tiny Room Stories",
      content: `<div><img src="./images/TinyRoom.png" alt="caricatura"/></div>`
    },
    {
      label: "Tsuki Odyssey",
      content: `<div><img src="./images/Tsuki.png" alt="tsuki"/></div>`
    },
    {
      label: "Whiteout Survival",
      content: `<div><img src="./images/Whiteout.png" alt="Whiteout"/></div>`
    }
  ];
  

</script>


<!-- Estructura contenido HTML -->
<main>

<!--Condicional para cada pantalla de preguntas-->
{#if contador === 0}
<div class="Inicio">
<div class="introHeader">
<p>NOVOA, REGUEIRA</p>
<p>VISUALIZACIÓN DE DATOS</p>
<p>2024</p>
</div>
<img class="titulo" src="./images/Titulo.png" alt="Titulo"/>
<img class="flecha" src="./images/flecha.png" alt="flecha"/>
<img class="titulo1" src="./images/titulin1.png" alt="titulo1"/>
<img class="flecha2" src="./images/flecha.png" alt="flecha"/>
<p class="frase">¿Te gustaría saber con qué juegos móviles tenes más compatibilidad bajo las 3 categorías claves del gaming?</p>
<div class="categorias">
  <div class="genero">GÉNERO</div>
  <div class="adictividad">ADICTIVIDAD</div>
  <div class="estetica">ESTÉTICA</div>
  <p class="textoGenero">Qué tipo de juegos te gustan, cuál es tu dinámica favorita.</p>
  <p class="textoAdictividad">Cuán adicto sos a pasar tiempo jugando jueguitos.</p>
  <p class="textoEstetica">Cuál es el estilo que más disfrutas ver en la pantalla del celu.</p>
</div>
<img class="flecha3" src="./images/flecha.png" alt="flecha"/>

<img class="titulo2" src="./images/titulin2.png" alt="titulp2"/>
<button class="comienza" on:click={() => contador++}>START</button>
<div class="vacio"></div>

</div>


{:else if contador === 1}
<div class="barraProgreso">
  <progress class="progreso" value="10" max="100"></progress>
</div>
<h1 class="pregunta1">¿Qué preferis?</h1>
<p class="subtitulos">En el mundo perfecto, obvio</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Construir un <br>hotel 5 estrellas</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Correr de la <br>policia</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Resolver quién <br>fue el asesino de <br>tu vecino</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>Armar un ejercito <br>de monos que <br>combata el mal</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>Cuidar un gatito</button>
</div>

{:else if contador === 2}
<div class="barraProgreso">
  <progress class="progreso" value="20" max="100"></progress>
</div>
<h1 class="pregunta2">¿Cuánto tiempo estas dispuesto <br>a dedicarle a los jueguitos?</h1>
<p class="subtitulos">Sé sincero, no nos hagas pedirte acceso a tu tiempo en pantalla</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Una vez por mes</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Dos veces por mes</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Una vez por <br>semana</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>Una vez por día</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>24/7</button>
</div>

{:else if contador === 3}
<div class="barraProgreso">
  <progress class="progreso" value="30" max="100"></progress>
</div>
<h1 class="pregunta3">¿Qué preferis?</h1>
<p class="subtitulos">No juzgamos.</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Dirigir un restaurante <br>donde los mozos son <br>conejos</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Esquivar bombas <br>mientras cortas <br>frutas</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Vivir la vida de un <br>gangsta</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>Planificar una forma de sobrevivir <br>al frío solo con madera</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>Construir la ciudad más <br>grande de latinoamérica</button>
</div>

{:else if contador === 4}
<div class="barraProgreso">
  <progress class="progreso" value="40" max="100"></progress>
</div>
<h1 class="pregunta4">¿Qué mirada te gusta más?</h1>
<p class="subtitulos">El amor a primera vista existe.</p>
<div class="botones">
<button class="botonImagen" on:click={() => contador++ && respuesta1++}> <img src="./images/mirada1.png" alt="Mirada1" /></button>
<button class="botonImagen" on:click={() => contador++ && respuesta2++}> <img src="./images/mirada2.png" alt="Mirada2" /></button>
<button class="botonImagen" on:click={() => contador++ && respuesta3++}> <img src="./images/mirada3.png" alt="Mirada3" /></button>
<button class="botonImagen" on:click={() => contador++ && respuesta4++}> <img src="./images/mirada4.png" alt="Mirada4" /></button>
<button class="botonImagen" on:click={() => contador++ && respuesta5++}> <img src="./images/mirada5.png" alt="Mirada5" /></button>
</div>

{:else if contador === 5}
<div class="barraProgreso">
  <progress class="progreso" value="50" max="100"></progress>
</div>
<h1 class="pregunta1">¿Qué preferís?</h1>
<p class="subtitulos">Dejate llevar, no pienses en las consecuencias.</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Ver publicidades para <br>triplicar tu dinero y <br>mejorar tu casa</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Organizar sillas por <br>forma y color</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Vivir en una aldea <br>llena de animales <br>buenos y... raros</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>Jugar a las escondidad (sobrevive<br>solo el que gana)</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>Ser Dios</button>
</div>

{:else if contador === 6}
<div class="barraProgreso">
  <progress class="progreso" value="60" max="100"></progress>
</div>
<h1 class="pregunta4">¿En qué casa vivirías?</h1>
<p class="subtitulos">All inclusive, all.</p>
<div class="botones">
<button class="botonImagen" on:click={() => contador++ && respuesta1++}><img src="./images/casa1.png" alt="casa1" /></button>
<button  class="botonImagen" on:click={() => contador++ && respuesta2++}><img  src="./images/casa2.png" alt="casa2" /></button>
<button  class="botonImagen" on:click={() => contador++ && respuesta3++}><img src="./images/casa3.png" alt="casa3" /></button>
<button  class="botonImagen" on:click={() => contador++ && respuesta4++}><img src="./images/casa4.png" alt="casa4" /></button>
<button  class="botonImagen" on:click={() => contador++ && respuesta5++}><img src="./images/casa5.png" alt="casa5" /></button>
</div>

{:else if contador === 7}
<div class="barraProgreso">
  <progress class="progreso" value="70" max="100"></progress>
</div>
<h1 class="pregunta1">¿Qué juego de mesa preferís?</h1>
<p class="subtitulos">No vale que no te gusten.</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Idle</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Uno</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Clue</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>La isla prohibida</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>Monopoly</button>
</div>

{:else if contador === 8}
<div class="barraProgreso">
  <progress class="progreso" value="80" max="100"></progress>
</div>
<h1 class="pregunta2">¿Hace cuánto tiempo <br>jugas en el celular?</h1>
<p class="subtitulos">No mientas, nadie te juzga.</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>1-2 años</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>2-4 años</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>4-6 años</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>6-10 años</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>+10 años</button>
</div>

{:else if contador === 9}
<div class="barraProgreso">
  <progress class="progreso" value="100" max="100"></progress>
</div>
<h1 class="pregunta1">¿Qué preferís?</h1>
<p class="subtitulos">Dejate llevar, no pienses en las consecuencias.</p>
<div class="botones">
<button class="boton" on:click={() => contador++ && respuesta1++}>Hacer jueguitos con <br>la pelota por 3 horas <br>seguidas</button>
<button class="boton" on:click={() => contador++ && respuesta2++}>Poder cruzar la calle <br>con el sémaforo en <br>rojo y sobrevivir, quizás</button>
<button class="boton" on:click={() => contador++ && respuesta3++}>Robar autos de lujo <br>y matar a sus dueños</button>
<button class="boton" on:click={() => contador++ && respuesta4++}>Vencer chanchos <br>malvados usando <br>bombas</button>
<button class="boton" on:click={() => contador++ && respuesta5++}>Refugiar gente en tu <br>sotano durante un <br>ataque zombie</button>

</div>


{/if}

<!--Condicional para pantallas de resultados posibles-->
<div class="resultados">

  <!-- Respuesta 1 -->
{#if respuesta1 > 2 && contador===10}

<img class="cuadradoBlanco" src="./images/cuadradoResultados.png" alt="fondo blanco" />
<img class="juegosResultado1" src="./images/JuegosResultado1.png" alt="juegos" />
<div class="rGenero">
<h1 class="tituloGenero">Tú <strong class="resaltar">género</strong> <br>preferido es:</h1>
<h1 class="resultadoGenero">Idle</h1>
<p class="bajadaResultado1">Estos videojuegos destacan por el uso <br>del tiempo como recurso más valioso <br>frente al tiempo de presencia en la <br>pantalla. La mayoría de ellos funcionan <br>con la pantalla apagada y calculan los <br>recursos 'minados' durante el tiempo <br>de inactividad.
</p>
</div>

<div class="rAdictividad">
  <h1 class="tituloAdictividad">Tú nivel de <br><strong class="resaltar2">adictividad</strong> es:</h1>
  <h1 class="resultadoAdictividad">1</h1>
  <p class="bajadaResultado2">No te gusta perder el tiempo en <br>jueguitos. Aunque eso quizás cambie <br>cuando descargues el Gatos y Sopa.</p>
  </div>

  <div class="rEstetica">
    <h1 class="tituloEstetica">Tú <strong class="resaltar3">estética</strong> <br>preferida es:</h1>
    <h1 class="resultadoEstetica">Romántico</h1>
    <p class="bajadaResultado3">Se centra en crear una atmósfera <br>emocional y envolvente que conecta <br>con los sentimientos del jugador. Este <br>estilo utiliza paletas de colores suaves, <br>música melódica y escenarios <br>idealizados como paisajes oníricos o <br>escenas íntimas. </p>
    </div>

    <!-- Gráficos Flourish -->
    <h1 class=tituloGrafico1>TU TABLA DE <br>COMPATIBILIDAD</h1>
     <div class="chartWrapper">
      <iframe src='https://flo.uri.sh/visualisation/20500486/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20500486/?utm_source=embed&utm_campaign=visualisation/20500486' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
  </div>

   <!-- Botón para desplegar el menú -->
    <!-- Primer botón -->
      <h1 class="masGeneros">¿QUÉ OTROS <br>GÉNEROS HAY?</h1>
      <div class="ubicacionBoton">
   <DropdownButton options={options1} />
  </div>
  <!-- Segundo botón -->
    <h1 class="masGeneros2">¿QUÉ OTRAS <br>ESTÉTICAS HAY?</h1>
    <div class="ubicacionBoton2">
  <DropdownButton options={options2} />
</div>

<h1 class=tituloGrafico2>PARA QUE LOS <br>JUEGUES TODOS</h1>
<div class="chartWrapper2">
  <iframe src='https://flo.uri.sh/visualisation/20499893/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20499893/?utm_source=embed&utm_campaign=visualisation/20499893' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
  </div>

   <!-- Botón comparaciones -->
    <div class="comparaciones">
      <h1 class="titulocomparacion">COMPARÁ Y DECIDITE!</h1>
    <!-- Primer botón -->
    <div class="ubicacionBoton3">
 <DropdownButton options={options3} boxClass="info-box2"/>
</div>
<!-- Segundo botón -->
  <div class="ubicacionBoton4">
<DropdownButton options={options3} boxClass="info-box2" />
</div>
</div>

<!-- Botón para volver al principio -->
<button class="volver" on:click={() => contador=0}>VOLVER A JUGAR</button>

<!-- creditos -->
 <p class="creditos1">VISUALIZACIÓN DE DATOS REALIZADA POR <br>JAZMIN NOVOA Y JULIETA REGUEIRA</p>
 <p class="creditos2">UTDT 2024</p>

 <div class="vacio2"></div>

  <!-- Respuesta 2 -->
{:else if respuesta2 > 2 && contador===10}
<img class="cuadradoBlanco" src="./images/cuadradoResultados.png" alt="fondo blanco" />
<img class="juegosResultado1" src="./images/JuegosResultado2.png" alt="juegos" />

<div class="rGenero">
  <h1 class="tituloGenero">Tú <strong class="resaltar">género</strong> <br>preferido es:</h1>
  <h1 class="resultadoGenero">Casual</h1>
  <p class="bajadaResultado1">Caracterizados por su sencillez, estos <br>juegos son aptos para todos los <br>públicos y se pueden disfrutar de rato <br>en rato, sin que haga falta ser <br>constante, ni estar comprometido <br>propiamente a conseguir todos los <br>objetivos posibles en un juego.
  </p>
  </div>
  
  <div class="rAdictividad">
    <h1 class="tituloAdictividad">Tú nivel de <br><strong class="resaltar2">adictividad</strong> es:</h1>
    <h1 class="resultadoAdictividad">2</h1>
    <p class="bajadaResultado2">Solo descargas juegos si tenes espacio <br>en el celu, y todos sabemos que nunca <br>tenes espacio en el celu.</p>
    </div>
  
    <div class="rEstetica">
      <h1 class="tituloEstetica">Tú <strong class="resaltar3">estética</strong> <br>preferida es:</h1>
      <h1 class="resultadoEstetica">Caricatura</h1>
      <p class="bajadaResultado3">Caracterizada por un estilo visual <br>vibrante, exagerado y lleno de humor. <br>Los elementos gráficos suelen ser <br>coloridos, con personajes de <br>proporciones poco realistas y diseños <br>amigables.</p>
      </div>
  
      <!-- Gráficos Flourish -->
      <h1 class=tituloGrafico1>TU TABLA DE <br>COMPATIBILIDAD</h1>
       <div class="chartWrapper">
        <iframe src='https://flo.uri.sh/visualisation/20570953/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20570953/?utm_source=embed&utm_campaign=visualisation/20570953' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>
  
     <!-- Botón para desplegar el menú -->
      <!-- Primer botón -->
        <h1 class="masGeneros">¿QUÉ OTROS <br>GÉNEROS HAY?</h1>
        <div class="ubicacionBoton">
     <DropdownButton options={options1} />
    </div>
    <!-- Segundo botón -->
      <h1 class="masGeneros2">¿QUÉ OTRAS <br>ESTÉTICAS HAY?</h1>
      <div class="ubicacionBoton2">
    <DropdownButton options={options2} />
  </div>
  
  <h1 class=tituloGrafico2>PARA QUE LOS <br>JUEGUES TODOS</h1>
  <div class="chartWrapper2">
    <iframe src='https://flo.uri.sh/visualisation/20499893/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20499893/?utm_source=embed&utm_campaign=visualisation/20499893' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>

     <!-- Botón comparaciones -->
     <div class="comparaciones">
      <h1 class="titulocomparacion">COMPARÁ Y DECIDITE!</h1>
    <!-- Primer botón -->
    <div class="ubicacionBoton3">
 <DropdownButton options={options3} />
</div>
<!-- Segundo botón -->
  <div class="ubicacionBoton4">
<DropdownButton options={options3} />
</div>
</div>

<!-- Botón para volver al principio -->
<button class="volver" on:click={() => contador=0}>VOLVER A JUGAR</button>

<!-- creditos -->
 <p class="creditos1">VISUALIZACIÓN DE DATOS REALIZADA POR <br>JAZMIN NOVOA Y JULIETA REGUEIRA</p>
 <p class="creditos2">UTDT 2024</p>

 <div class="vacio2"></div>

    <!-- Respuesta 3 -->
{:else if respuesta3 > 2 && contador===10}
<img class="cuadradoBlanco" src="./images/cuadradoResultados.png" alt="fondo blanco" />
<img class="juegosResultado1" src="./images/JuegosResultado3.png" alt="juegos" />

<div class="rGenero">
  <h1 class="tituloGenero">Tú <strong class="resaltar">género</strong> <br>preferido es:</h1>
  <h1 class="resultadoGenero">Aventura</h1>
  <p class="bajadaResultado1">Estos videojuegos están <br>caracterizados por la investigación, <br>exploración, la solución de <br>rompecabezas, la interacción con <br>personajes del videojuego, y un <br>enfoque en el relato en vez de <br>desafíos basados en reflejos.
  </p>
  </div>
  
  <div class="rAdictividad">
    <h1 class="tituloAdictividad">Tú nivel de <br><strong class="resaltar2">adictividad</strong> es:</h1>
    <h1 class="resultadoAdictividad">3</h1>
    <p class="bajadaResultado2">Te entusiasman los juegos; hasta que <br>los abandonas. Pero no te preocupes, <br>no vas a poder separarte de Tsuki.</p>
    </div>
  
    <div class="rEstetica">
      <h1 class="tituloEstetica">Tú <strong class="resaltar3">estética</strong> <br>preferida es:</h1>
      <h1 class="resultadoEstetica">Suspenso</h1>
      <p class="bajadaResultado3">Diseñada para mantener al jugador en <br>tensión, se basa en crear una sensación <br>de misterio, intriga o peligro inminente. <br>Se emplean colores oscuros, iluminación <br>tenue y música inquietante para <br>sumergir al jugador en un ambiente <br>amenazador.</p>
      </div>
  
      <!-- Gráficos Flourish -->
      <h1 class=tituloGrafico1>TU TABLA DE <br>COMPATIBILIDAD</h1>
       <div class="chartWrapper">
        <iframe src='https://flo.uri.sh/visualisation/20571408/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20571408/?utm_source=embed&utm_campaign=visualisation/20571408' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>
  
     <!-- Botón para desplegar el menú -->
      <!-- Primer botón -->
        <h1 class="masGeneros">¿QUÉ OTROS <br>GÉNEROS HAY?</h1>
        <div class="ubicacionBoton">
     <DropdownButton options={options1} />
    </div>
    <!-- Segundo botón -->
      <h1 class="masGeneros2">¿QUÉ OTRAS <br>ESTÉTICAS HAY?</h1>
      <div class="ubicacionBoton2">
    <DropdownButton options={options2} />
  </div>
  
  <h1 class=tituloGrafico2>PARA QUE LOS <br>JUEGUES TODOS</h1>
  <div class="chartWrapper2">
    <iframe src='https://flo.uri.sh/visualisation/20499893/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20499893/?utm_source=embed&utm_campaign=visualisation/20499893' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>

     <!-- Botón comparaciones -->
     <div class="comparaciones">
      <h1 class="titulocomparacion">COMPARÁ Y DECIDITE!</h1>
    <!-- Primer botón -->
    <div class="ubicacionBoton3">
 <DropdownButton options={options3} />
</div>
<!-- Segundo botón -->
  <div class="ubicacionBoton4">
<DropdownButton options={options3} />
</div>
</div>

<!-- Botón para volver al principio -->
<button class="volver" on:click={() => contador=0}>VOLVER A JUGAR</button>

<!-- creditos -->
 <p class="creditos1">VISUALIZACIÓN DE DATOS REALIZADA POR <br>JAZMIN NOVOA Y JULIETA REGUEIRA</p>
 <p class="creditos2">UTDT 2024</p>

 <div class="vacio2"></div>

    <!-- Respuesta 4 -->
{:else if respuesta4 > 2 && contador===10}
<img class="cuadradoBlanco" src="./images/cuadradoResultados.png" alt="fondo blanco" />
<img class="juegosResultado1" src="./images/JuegosResultado4.png" alt="juegos" />

<div class="rGenero">
  <h1 class="tituloGenero">Tú <strong class="resaltar">género</strong> <br>preferido es:</h1>
  <h1 class="resultadoGenero">Estrategia</h1>
  <p class="bajadaResultado1">Estos videojuegos ponen a prueba <br>diferentes habilidades de planificación, <br>pensamiento crítico, resolución de <br>problemas y gestión de recursos; con el <br>fin de lograr un objetivo o conseguir la <br>victoria para pasar a otro nivel.
  </p>
  </div>
  
  <div class="rAdictividad">
    <h1 class="tituloAdictividad">Tú nivel de <br><strong class="resaltar2">adictividad</strong> es:</h1>
    <h1 class="resultadoAdictividad">4</h1>
    <p class="bajadaResultado2">Todo bajo control maestro, seguí <br>usando el celu en horizontal <br>tranquilo. Que nadie te juzgue.</p>
    </div>
  
    <div class="rEstetica">
      <h1 class="tituloEstetica">Tú <strong class="resaltar3">estética</strong> <br>preferida es:</h1>
      <h1 class="resultadoEstetica">Acción</h1>
      <p class="bajadaResultado3">Enfocada en dinamismo, energía y <br>emoción constante. Utiliza gráficos <br>vibrantes, efectos visuales intensos y <br>diseños llamativos que enfatizan la <br>rapidez y el movimiento. </p>
      </div>
  
      <!-- Gráficos Flourish -->
      <h1 class=tituloGrafico1>TU TABLA DE <br>COMPATIBILIDAD</h1>
       <div class="chartWrapper">
        <iframe src='https://flo.uri.sh/visualisation/20571504/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20571504/?utm_source=embed&utm_campaign=visualisation/20571504' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>
  
     <!-- Botón para desplegar el menú -->
      <!-- Primer botón -->
        <h1 class="masGeneros">¿QUÉ OTROS <br>GÉNEROS HAY?</h1>
        <div class="ubicacionBoton">
     <DropdownButton options={options1} />
    </div>
    <!-- Segundo botón -->
      <h1 class="masGeneros2">¿QUÉ OTRAS <br>ESTÉTICAS HAY?</h1>
      <div class="ubicacionBoton2">
    <DropdownButton options={options2} />
  </div>
  
  <h1 class=tituloGrafico2>PARA QUE LOS <br>JUEGUES TODOS</h1>
  <div class="chartWrapper2">
    <iframe src='https://flo.uri.sh/visualisation/20499893/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20499893/?utm_source=embed&utm_campaign=visualisation/20499893' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>

     <!-- Botón comparaciones -->
     <div class="comparaciones">
      <h1 class="titulocomparacion">COMPARÁ Y DECIDITE!</h1>
    <!-- Primer botón -->
    <div class="ubicacionBoton3">
 <DropdownButton options={options3} />
</div>
<!-- Segundo botón -->
  <div class="ubicacionBoton4">
<DropdownButton options={options3} />
</div>
</div>

<!-- Botón para volver al principio -->
<button class="volver" on:click={() => contador=0}>VOLVER A JUGAR</button>

<!-- creditos -->
 <p class="creditos1">VISUALIZACIÓN DE DATOS REALIZADA POR <br>JAZMIN NOVOA Y JULIETA REGUEIRA</p>
 <p class="creditos2">UTDT 2024</p>

 <div class="vacio2"></div>
  

    <!-- Respuesta 5 -->
{:else if respuesta5 > 2 && contador===10}
<img class="cuadradoBlanco" src="./images/cuadradoResultados.png" alt="fondo blanco" />
<img class="juegosResultado1" src="./images/JuegosResultado5.png" alt="juegos" />

<div class="rGenero">
  <h1 class="tituloGenero">Tú <strong class="resaltar">género</strong> <br>preferido es:</h1>
  <h1 class="resultadoGenero">Tycoon/Simulación</h1>
  <p class="bajadaResultado1">A nivel general, una simulación puede <br>ser descrita como una representación, <br>a menudo en forma de juego o <br>actividad práctica, que imita las <br>operaciones de un sistema o proceso <br>del mundo real.
  </p>
  </div>
  
  <div class="rAdictividad">
    <h1 class="tituloAdictividad">Tú nivel de <br><strong class="resaltar2">adictividad</strong> es:</h1>
    <h1 class="resultadoAdictividad">5</h1>
    <p class="bajadaResultado2">Un Gamer de Bolsillo autentico. Los <br>juegos son tu perdición, en serio, apaga <br>el Pou, son las 3 de la mañana. </p>
    </div>
  
    <div class="rEstetica">
      <h1 class="tituloEstetica">Tú <strong class="resaltar3">estética</strong> <br>preferida es:</h1>
      <h1 class="resultadoEstetica">Realista</h1>
      <p class="bajadaResultado3">Busca reproducir el mundo real con la <br>mayor fidelidad posible, <br>utilizando gráficos detallados y físicas avanzadas. <br>Las paletas de colores son naturales, y <br>los escenarios y personajes están <br>diseñados para parecer auténticos. </p>
      </div>
  
      <!-- Gráficos Flourish -->
      <h1 class=tituloGrafico1>TU TABLA DE <br>COMPATIBILIDAD</h1>
       <div class="chartWrapper">
        <iframe src='https://flo.uri.sh/visualisation/20571579/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20571579/?utm_source=embed&utm_campaign=visualisation/20571579' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>
  
     <!-- Botón para desplegar el menú -->
      <!-- Primer botón -->
        <h1 class="masGeneros">¿QUÉ OTROS <br>GÉNEROS HAY?</h1>
        <div class="ubicacionBoton">
     <DropdownButton options={options1} />
    </div>
    <!-- Segundo botón -->
      <h1 class="masGeneros2">¿QUÉ OTRAS <br>ESTÉTICAS HAY?</h1>
      <div class="ubicacionBoton2">
    <DropdownButton options={options2} />
  </div>
  
  <h1 class=tituloGrafico2>PARA QUE LOS <br>JUEGUES TODOS</h1>
  <div class="chartWrapper2">
    <iframe src='https://flo.uri.sh/visualisation/20499893/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20499893/?utm_source=embed&utm_campaign=visualisation/20499893' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>
    </div>

     <!-- Botón comparaciones -->
     <div class="comparaciones">
      <h1 class="titulocomparacion">COMPARÁ Y DECIDITE!</h1>
    <!-- Primer botón -->
    <div class="ubicacionBoton3">
 <DropdownButton options={options3} />
</div>
<!-- Segundo botón -->
  <div class="ubicacionBoton4">
<DropdownButton options={options3} />
</div>
</div>

<!-- Botón para volver al principio -->
<button class="volver" on:click={() => contador=0}>VOLVER A JUGAR</button>

<!-- creditos -->
 <p class="creditos1">VISUALIZACIÓN DE DATOS REALIZADA POR <br>JAZMIN NOVOA Y JULIETA REGUEIRA</p>
 <p class="creditos2">UTDT 2024</p>

 <div class="vacio2"></div>
  
{/if}
</div>

{#each circles as circle (circle.id)}
<div
  class="circle"
  style="top: {circle.y - 10}px; left: {circle.x - 10}px;"
></div>
{/each}
</main>

<style>

@import url('https://fonts.googleapis.com/css2?family=Inria+Sans:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&display=swap');

  
main{
  background-color: black;
  margin: 0px;
  padding: 0px;
  overflow: hidden;
  cursor: none; 
  
}  


.pregunta1{
  text-align: center;
  size: 40px;
  color: #000AFF;
  margin-top: 55px;
 
}

.pregunta2{
  text-align: center;
  size: 40px;
  color: #E92FED;
  margin-top: 55px;
 
}

.pregunta3{
  text-align: center;
  size: 40px;
  color: #000AFF;
  margin-top: 55px;
}

.pregunta4{
  text-align: center;
  size: 40px;
  color: #FF9A51;
  margin-top: 55px;
}

.subtitulos{
  text-align: center;
  size: 20px;
  color: white;
  padding: 0px;
  margin-bottom: 10px;
}

.botones{
  display: flex;
  width: 1400px;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 70px;
  gap: 80px;
  margin-left: 70px;
}

.boton{
  background-color: black;
  width: 300px;
  height: 150px;
  border: white;
  border-radius: 20px;
  border-width: 4px;
  border-style:inset;
  background-size: cover;
  font-size: 20px;
  color: white;
  transition: background-color 0.3s;
}

.boton:hover{
  background-image: url('./images/RectanguloHover.png');
  background-size: cover;
  border: none;
}

.botonImagen{
  background-color: black;
  background-size: cover;
  width: 300px;
  height: 150px;
  border: white;
  border-radius: 20px;
  border-width: 4px;
  border-style:inset;
  font-size: 20px;
  color: white;
  transition: background-color 0.3s;
  z-index: 2;
}

.botonImagen:hover{
  background-image: url('./images/RectanguloHover.png');
  background-size: cover;
  color: white;
  width: 300px;
  height: 150px;
  border: none;
  z-index: 2;
}

.botonImagen img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ajusta la imagen al botón */
  border-radius: inherit; /* Respeta el borde redondeado del botón */
  z-index: 1;
}

.botonImagen:hover img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ajusta la imagen al botón */
  border-radius: inherit; /* Respeta el borde redondeado del botón */
  z-index: 1;
}


.Inicio{
  display: flex;
  width: 100vw; 
  height: 100vh;
  margin: 0px;
  justify-content: center;
  position: absolute;
  
}


.titulo{
  display: flex;
  width: 661,5px;
  height: 161px;
  margin-top: 230px;
  justify-content: center;
  margin-left: 300px;

}

.titulo1{
  display: flex;
  position: absolute;
  width: 661,5px;
  height: 161px;
  margin-top: 1050px;
  justify-content: center;

}

.titulo2{
  display: flex;
  position: absolute;
  width: 661,5px;
  height: 161px;
  margin-top: 2440px;
  justify-content: center;

}

.frase{
  display: flex;
  width: 530px;
  height: 160px;
  position: absolute;
  color: white;
  text-align: center;
  justify-content: center;
  font-family: "Inria Sans", sans-serif;
  font-size: 30px;
  margin-top: 1600px;
}

.categorias{
  display: flex;
  position: absolute;
  margin-top: 1770px;
  gap: 20px;
}

.genero{
  display: flex;
  background-color: #000AFF;
  width: 190px;
  height: 35px;
  border-radius: 40px;
  align-items: center;
  justify-content: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 20px;
  font-weight: 300;
}

.adictividad{
  display: flex;
  background-color: #E92FED;
  width: 190px;
  height: 35px;
  border-radius: 40px;
  align-items: center;
  justify-content: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 20px;
  font-weight: 300;
}

.estetica{
  display: flex;
  background-color: #FF9A51;
  width: 190px;
  height: 35px;
  border-radius: 40px;
  align-items: center;
  justify-content: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 20px;
  font-weight: 300;
}

.textoGenero{
  display: flex;
  position: absolute;
  width: 190px;
  height: 190px;
  text-align: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 18px;
  font-weight: 300;
  margin-top: 50px;
}

.textoAdictividad{
  display: flex;
  position: absolute;
  width: 190px;
  height: 190px;
  text-align: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 18px;
  font-weight: 300;
  margin-top: 50px;
  margin-left: 210px;
}

.textoEstetica{
  display: flex;
  position: absolute;
  width: 190px;
  height: 190px;
  text-align: center;
  color: white;
  font-family: "Inria Sans", sans-serif;
  font-size: 18px;
  font-weight: 300;
  margin-top: 50px;
  margin-left: 420px;
}

.introHeader{
  display: flex;
  position: absolute;
  position: fixed;
  size: 27px;
  color: white;
  text-align: left;
  justify-content: space-between;
  font-family: "Inria Sans", sans-serif;
  gap: 450px;
  margin-top: 20px;
  margin-right: 25px;
  z-index: 1;
}


.flecha{
  display: flex;
  position: absolute;
  align-items: flex-end;
  margin-top: 500px;
}

.flecha2{
  display: flex;
  position: absolute;
  align-items: flex-end;
  margin-top: 1320px;
}

.flecha3{
  display: flex;
  position: absolute;
  align-items: flex-end;
  margin-top: 2000px;
}

.comienza{
  display: flex;
  position: absolute;
  background-color: black;
  color: white;
  font-size: 20px;
  border: white;
  border-radius: 25px;
  border-width: 6px;
  border-style:inset;
  margin-top: 2690px;
  margin-left: 20px;
  width: 150px;
  height: 45px;
  align-items: center;
  justify-content: center;
}

.comienza:hover{
  background-image: url('./images/hoverStart.png');
  background-size: cover;
  border: none;
}

.resultados{
  background-color: black;
  color: fuchsia;
}

.cuadradoBlanco{
  width: 1235px;
  height: 515px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 150px;
  margin-top: 120px;
}


.juegosResultado1{
  display: flex;
  width: 1235px;
  height: 500px;
  justify-content: center;
  align-items: center;
  margin-left: 150px;
  margin-top: 70px;
}

/* Barra de progreso */
progress {
  position: absolute;
    -webkit-appearance: none;
    appearance: none;
    width: 300px;
    height: 25px;
    margin-top: 650px;
    margin-left: 1150px;
    border-radius: 15px;
    border-color: white;
    border-style: inset;
    border-width: 3px;
    overflow: hidden; /* Para recortar cualquier contenido fuera del radio */
    background-color: #000000; /* Fondo detrás del valor */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }

  /* Fondo de la barra (webkit, Chrome/Safari) */
  :global(progress::-webkit-progress-bar) {
    background-color: #000000;
  }

  /* Estilo del valor de la barra en navegadores WebKit */
  :global(progress::-webkit-progress-value) {
    background: linear-gradient(to right, #000AFF, #E92FED, #FF9A51);
    border-radius: 15px; /* Asegura bordes redondeados */
  }

/* Cambiar cursor */
  .circle {
    position: fixed;
    width: 20px;
    height: 20px;
    background: radial-gradient(circle, #000AFF, #E92FED, #FF9A51, transparent);
    border-radius: 50%;
    pointer-events: none; /* Ignorar interacciones del mouse */
    animation: fadeOut 1s ease-out forwards;
  }

  /* Animación para desvanecer los círculos */
  @keyframes fadeOut {
    0% {
      opacity: 1;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(0.5);
    }
  }

/* Textos resultados */
  .rGenero{
    display: flex;
    width: 1235px;
    margin-top: 100px;
  }

  .tituloGenero{
    font-size: 40px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 360px;
  }

  .resaltar{
    font-size: 40px;
    text-align: left;
    color: #000AFF;
    font-family: "Inria Sans", sans-serif;
    font-style: italic;
  }

  .resultadoGenero{
    display: flex;
    justify-content: flex-end;
    font-size: 40px;
    text-align: left;
    color: #000AFF;
    font-family: "Inria Sans", sans-serif;
    margin-left: 115px;
    margin-top: 57px;
    font-style: bold;

  }

  .bajadaResultado1{
    display: flex;
    position: absolute;
    font-size: 20px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 690px;
    margin-top: 110px;

  }

  .rAdictividad{
    display: flex;
    width: 1235px;
    margin-top: 250px;
  }

  .tituloAdictividad{
    font-size: 40px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 360px;
  }

  .resaltar2{
    font-size: 40px;
    text-align: left;
    color: #E92FED;
    font-family: "Inria Sans", sans-serif;
    font-style: italic;
  }

  .resultadoAdictividad{
    display: flex;
    justify-content: flex-end;
    font-size: 40px;
    text-align: left;
    color: #E92FED;
    font-family: "Inria Sans", sans-serif;
    margin-left: 84px;
    margin-top: 60px;
    font-style: bold;

  }

  .bajadaResultado2{
    display: flex;
    position: absolute;
    font-size: 20px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 700px;
    margin-top: 115px;

  }

  .rEstetica{
    display: flex;
    width: 1400px;
    margin-top: 150px;
  }

  .tituloEstetica{
    font-size: 40px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 360px;
  }

  .resaltar3{
    font-size: 40px;
    text-align: left;
    color: #FF9A51;
    font-family: "Inria Sans", sans-serif;
    font-style: italic;
  }

  .resultadoEstetica{
    display: flex;
    justify-content: flex-end;
    font-size: 40px;
    text-align: left;
    color: #FF9A51;
    font-family: "Inria Sans", sans-serif;
    margin-left: 125px;
    margin-top: 60px;
    font-style: bold;

  }

  .bajadaResultado3{
    display: flex;
    position: absolute;
    font-size: 20px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 700px;
    margin-top: 112px;
  }

  .chartWrapper{
    flex: 0 0 100vw; 
    display: flex;
    justify-content: center;
    align-content: center;
    margin-top: 460px;
    margin-left: 90px;
  }

  .chartWrapper2{
    flex: 0 0 40vw; 
    display: flex;
    justify-content: center;
    align-content: center;
    margin-top: 1330px;
    margin-left: 40px;
  }

  .flourish-embed-iframe{
    display: block;
    width: 600px;
    height: auto;
    margin-top: 50px;

}

.ubicacionBoton{
  display: flex;
  position: absolute;
  margin-top: 130px;
}

.ubicacionBoton2{
  display: flex;
  position: absolute;
  margin-top: 690px;
}

.masGeneros{
  display: flex;
    position: absolute;
    font-size: 25px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 130px;
    margin-left: 240px;
}

.masGeneros2{
  display: flex;
    position: absolute;
    font-size: 25px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 695px;
    margin-left: 240px;

}

.tituloGrafico1{
  display: flex;
    position: absolute;
    font-size: 25px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 390px;
    margin-left: 240px;
}

.tituloGrafico2{
  display: flex;
    position: absolute;
    font-size: 25px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 1260px;
    margin-left: 240px;
}

.vacio{
  display: flex;
  width: 1000px;
  height: 2900px;
  background-color: black;
}

.comparaciones{
  display: flex;
  position: absolute;
  margin-top: 50px;
  margin-right: 10px;

}

.titulocomparacion{
    display: flex;
    position: absolute;
    width: 1000px;
    font-size: 25px;
    text-align: left;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-left: 240px;
}

.ubicacionBoton3{
  display: flex;
  position: absolute;
}

.ubicacionBoton4{
  display: flex;
  position: absolute;
  margin-left: 600px;
}


.volver{
  display: flex;
  position: absolute;
  background-color: black;
  color: white;
  font-size: 20px;
  border: white;
  border-radius: 30px;
  border-width: 8px;
  border-style:inset;
  margin-top: 800px;
  margin-left: 650px;
  width: 200px;
  height: 60px;
  align-items: center;
  justify-content: center;
}

.volver:hover{
  background-image: url('./images/hoverStart.png');
  background-size: cover;
  border: none;
}

.creditos1{
  display: flex;
    position: absolute;
    font-size: 15px;
    text-align: center;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 1000px;
    margin-left: 620px;
}

.creditos2{
  display: flex;
    position: absolute;
    font-size: 15px;
    text-align: center;
    color: white;
    font-family: "Inria Sans", sans-serif;
    margin-top: 1070px;
    margin-left: 720px;
}

.vacio2{
  display: flex;
  width: 1000px;
  height: 1200px;
  background-color: black;
}


</style>
