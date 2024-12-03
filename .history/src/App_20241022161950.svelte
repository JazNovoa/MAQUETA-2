<!-- Script JS -->
<script>
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json";

  // Escala para la adictividad (color del relleno de los rectángulos st1)
  const adictividad = d3
    .scaleLinear()
    .domain([1, 2, 3, 4, 5])
    .range(["#000aff", "#9200b8", "#e92fed", "#ff9a51", "#ffe86f"]);

  // Escala para el continente (color del borde del path st0)
  const continente = d3
    .scaleOrdinal()
    .domain(["África", "Asia", "Europa", "America", "Oceania"])
    .range(["#000aff", "#9200b8", "#e92fed", "#ff9a51", "#ffe86f"]);

  // Función para cargar y modificar SVGs
  async function loadAndModifySVG(url, juego) {
    const response = await fetch(url);
    const svgText = await response.text();
    const parser = new DOMParser();
    const svgDoc = parser.parseFromString(svgText, "image/svg+xml");
    const svgElement = svgDoc.querySelector("svg");

    // Cambiar el color de los rectángulos con clase 'st1' según la adictividad
    svgElement.querySelectorAll(".st1").forEach((rect) => {
      rect.setAttribute("fill", adictividad(juego.Adictividad));
    });

    // Cambiar el color del path con clase 'st0' según el continente
    svgElement.querySelectorAll(".st0").forEach((path) => {
      path.setAttribute("stroke", continente(juego.Continente));
    });

    return svgElement.outerHTML;
  }

  // Cargar los SVGs con las modificaciones adecuadas
  let juegosSVG = [];

  $: (async () => {
    try {
      juegosSVG = await Promise.all(
        juegos.map(async (juego) => {
          const svgContent = await loadAndModifySVG(juego.Imagen, juego);
          return { ...juego, svgContent };
        }),
      );
    } catch (error) {
      console.error(error);
    }
  })();
</script>

<!-- Estructura contenido HTML -->
<main>
  <div class="header">
    <img class="titulo" src="./public/images/TITULO.svg" width="50%" />
  </div>

  <div class="contenedor">
    {#each juegosSVG as juego}
      <div class="juego-item">
        <div class="modulos">
          <!-- Renderizamos cada SVG 10 veces -->
          {#each Array(10) as _}
            <div class="svg-wrapper">
              {@html juego.svgContent}
            </div>
          {/each}
        </div>
        <p class="nombre-juego">{juego.Juego}</p>
      </div>
    {/each}
  </div>

  <div>
    <h1 class="titulo">Elaborado por Jazmin Novoa y Julieta Regueira</h1>
  </div>
</main>

<style>
  /* Estilos generales */
  .titulo,
  .header {
    font-size: 20px;
    margin-top: 30px;
    display: flex;
    justify-content: center;
    text-align: center;
  }

  main {
    height: 100%;
    margin: 0;
    background-color: black;
    color: white;
  }

  .contenedor {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 30px; /* Espacio entre los bloques de cada juego */
    max-width: 1020px;
    margin: auto;
  }

  .juego-item {
    display: flex;
    width: 100%;
    align-items: center; /* Alineamos verticalmente los elementos */
    justify-content: space-between; /* SVGs a la izquierda, nombre a la derecha */
    gap: 20px;
  }

  .modulos {
    display: flex;
    flex-direction: column; /* Colocamos los SVG en columna */
    gap: 0; /* Sin espacio entre los SVG */
  }

  .svg-wrapper {
    display: block;
    margin: 0;
    padding: 0;
    width: 50px; /* Tamaño fijo para cada SVG */
    height: 50px;
  }

  .svg-wrapper svg {
    width: 100%; /* Asegurar que el SVG ocupe todo el contenedor */
    height: 100%;
    display: block;
  }

  .nombre-juego {
    width: 150px;
    text-align: left;
    font-size: 16px;
    color: white;
  }
</style>
