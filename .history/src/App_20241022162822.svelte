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
  main {
    height: 100vh; /* Ocupa toda la pantalla */
    margin: 0;
    background-color: black;
    color: white;
    display: flex;
    justify-content: center; /* Centra horizontalmente */
    align-items: center; /* Centra verticalmente */
    flex-direction: column;
  }

  .contenedor {
    display: flex;
    flex-direction: column;
    align-items: flex-end; /* Alinea todos los juegos a la derecha */
    justify-content: center;
    gap: 5px; /* Espacio mínimo entre las filas */
  }

  .juego-item {
    display: flex;
    align-items: center;
    justify-content: flex-end; /* Asegura que todo esté alineado a la derecha */
  }

  .modulos {
    display: flex;
    gap: 2px; /* Espacio entre SVGs */
  }

  .svg-wrapper {
    width: 40px;
    height: 40px;
  }

  .svg-wrapper svg {
    width: 100%;
    height: 100%;
    display: block;
  }

  .nombre-juego {
    font-size: 16px;
    color: white;
    margin: 0 0 0 5px; /* 5px de margen entre los SVGs y el nombre */
    padding: 0;
    white-space: nowrap; /* Evita que los títulos se dividan en varias líneas */
  }

  .header {
    margin-bottom: 30px;
    text-align: center;
  }
</style>
