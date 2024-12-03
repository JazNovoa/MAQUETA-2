<!-- Script JS -->
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
      // Ordenar juegos por almacenamiento
      const juegosOrdenados = juegos.sort(
        (a, b) => a.Almacenamiento - b.Almacenamiento,
      );

      juegosSVG = await Promise.all(
        juegosOrdenados.map(async (juego) => {
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
        <p class="nombre-juego">{juego.Juego}</p>
        <div class="modulos">
          {#each Array(juego.Años) as _}
            <div class="svg-wrapper">
              {@html juego.svgContent}
            </div>
          {/each}
        </div>
      </div>
    {/each}
  </div>

  <div>
    <img class="indice" src="./public/images/INDICE.svg" />
    <h1 class="footer">Elaborado por Jazmin Novoa y Julieta Regueira</h1>
  </div>
</main>

<style>
  /* Estilos generales */
  .titulo,
  .header {
    margin-top: 30px;
    display: flex;
    justify-content: center;
    text-align: center;
    margin-bottom: 25px;
  }

  .indice {
    justify-content: center;
   
    height: 10%;
  }

  .footer {
    font-size: 20px;
    justify-content: center;
    text-align: center;
    margin-top: 30px;
    margin-bottom: 25px;
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
    max-width: 1020px;
    margin: auto;
  }

  .juego-item {
    display: flex;
    align-items: center;
    justify-content: flex-start; /* Alinear a la izquierda */
    margin: 0; /* Sin margen entre filas */
  }

  .modulos {
    display: flex;
    justify-content: flex-start; /* Alinear módulos a la izquierda */
  }

  .svg-wrapper {
    display: block;
    width: 40px;
    height: 40px;
  }

  .nombre-juego {
    width: 150px; /* Ajustar según sea necesario */
    text-align: right; /* Alinear el texto a la derecha */
    font-size: 16px;
    color: white;
    margin: 0; /* Sin margen adicional */
    padding: 0; /* Sin padding */
    margin-right: 10px; /* Espacio entre el nombre del juego y los módulos SVG */
  }
</style>
