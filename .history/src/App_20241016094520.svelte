<!-- Script JS -->
<script>
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json"; // Importamos juegos

  // Escala para adictividad (relleno de los rectángulos)
  const adictividad = d3
    .scaleLinear()
    .domain([1, 2, 3, 4, 5])
    .range(["#000aff", "#9200b8", "#e92fed", "#ff9a51", "#ffe86f"]);

  // Escala para continente (color del path)
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

    // Cambiar el relleno de los rectángulos según la adictividad
    svgElement.querySelectorAll("rect").forEach((rect) => {
      rect.setAttribute("fill", adictividad(juego.Adictividad));
    });

    // Cambiar el color del path con la clase 'st2' según el continente
    svgElement.querySelectorAll(".st2").forEach((path) => {
      path.setAttribute("stroke", continente(juego.Continente));
      path.setAttribute("stroke-width", "2"); // Ajustar ancho del trazo si es necesario
    });

    return svgElement.outerHTML;
  }

  // Cargar los SVGs con los colores adecuados
  let juegosSVG = [];

  $: (async () => {
    try {
      juegosSVG = await Promise.all(
        juegos.map(async (juego) => {
          const svgContent = await loadAndModifySVG(juego.Imagen, juego);
          return { ...juego, svgContent };
        })
      );
    } catch (error) {
      console.error(error);
    }
  })();
</script>


<!-- Estructura contenido HTML -->
<main>
  <div class="header">
    <h1 class="titulo">Gamer de bolsillo</h1>
    <h2 class="subtitulo">Relevamiento de datos sobre jueguitos de celu</h2>
  </div>

  <div class="contenedor">
    {#each juegosSVG as juego}
      <div class="juego-item">
        <p>{juego.Juego}</p>
        <div class="modulos">
          {@html juego.svgContent} <!-- Renderizamos el SVG modificado -->
        </div>
      </div>
    {/each}
  </div>
</main>


<!-- Estilos CSS -->
<style>
  .titulo {
    display: flex;
    flex-direction: row;
    justify-content: center;
    text-align: center;
  }

  .subtitulo {
    display: flex;
    flex-direction: row;
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
    align-items: center;
    gap: 20px;
    max-width: 1020px;
    margin: auto;
  }

  .continentes {
    display: flex;
    flex-direction: row-reverse;
    height: 40px;
    border-width: 5px;
    margin-right: 500px;
  }

  .modulos {
    display: flex;
    justify-content: center;
    align-items: center;
  width: 100%;
  height: 100%;
  }
</style>
