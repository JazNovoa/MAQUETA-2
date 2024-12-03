<!-- Script JS -->
<script>
  // Importamos las dependencias necesarias
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json"; // Importamos juegos

  // Escala para adictividad (color de relleno)
  const adictividad = d3
    .scaleLinear()
    .domain([1, 2, 3, 4, 5])
    .range(["#000aff", "#9200b8", "#e92fed", "#ff9a51", "#ffe86f"]);

  // Escala para continente (color de borde)
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

    // Modificamos los atributos de los rectángulos
    svgElement.querySelectorAll("rect").forEach((rect) => {
      rect.setAttribute("fill", adictividad(juego.Adictividad));
      rect.setAttribute("stroke", continente(juego.Continente));
      rect.setAttribute("stroke-width", "1.5");
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
        }),
      );
    } catch (error) {
      console.error(error);
    }
  })();

  // Al cargar el componente, cargamos todos los SVG necesarios
  $: (async () => {
    try {
      juegosSVG = await Promise.all(
        juegos.map(async (juego) => {
          const svgContent = await loadSVG(juego.Imagen);

          // Cambia el color de los rectángulos en el SVG según la adictividad
          const updatedSVGContent = svgContent.replace(
            /<rect/g,
            `<rect fill="${adictividad(juego.Adictividad)}"`,
          );

          return { ...juego, svgContent: updatedSVGContent };
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
    <h1 class="titulo">Gamer de bolsillo</h1>
    <h2 class="subtitulo">Relevamiento de datos sobre jueguitos de celu</h2>
  </div>

  <div class="contenedor">
    {#each juegosSVG as juego}
      <div class="juego-item">
        <p>{juego.Juego}</p>
        <div
          class="continentes"
          style="border-color: {adictividad(
            juego.Adictividad,
          )}; width: {juego.Años * 5}%;"
        ></div>
        <div class="modulos">
          {@html juego.svgContent}
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
  }

  .modulos {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
    height: 50px;
  }
</style>
