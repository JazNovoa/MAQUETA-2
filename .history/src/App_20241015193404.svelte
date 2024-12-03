<!-- Script JS -->
<script>
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json"; //importamos juegos
  
   // Escala para adictividad
   const adictividad = d3
    .scaleLinear()
    .domain([1, 2, 3, 4, 5])
    .range(["#000aff", "#9200b8", "#e92fed", "#ff9a51", "#ffe86f"]);

  // Función para cargar SVG desde la carpeta "public/images"
  async function loadSVG(url) {
    const response = await fetch(url);
    return await response.text();
  }

  // Cargar dinámicamente los SVGs
  let juegosSVG = [];

  // Al cargar el componente, cargamos todos los SVG necesarios
  $: (async () => {
    juegosSVG = await Promise.all(
      juegos.map(async (juego) => {
        const svgContent = await loadSVG(juego.Imagen);
        return { ...juego, svgContent };
      })
    );
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
              style="border-color: {adictividad(juego.Adictividad)}; width: {juego.Años * 5}%;"></div>
          <div class="modulos">
              <div bind:this={juego.svgContent} style="width: {juego.Años}px;">
                  {@html juego.svgContent}
              </div>
          </div>
      </div>
      {/each}
  </div>
</main>


<!-- Estilos CSS -->
<style>

.titulo,
.subtitulo {
    text-align: center;
    margin: 10px 0;
}

.contenedor {
    display: flex;
    flex-direction: column;
    align-items: center; /* Alinea los elementos en el centro */
    gap: 20px; /* Espacio entre los elementos */
    max-width: 1020px;
    margin: auto; /* Centra el contenedor */
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
      justify-content: flex-end;
      align-items: center;
      max-width: 1020px;
      gap: 30px;
      margin-bottom: 100px;
  }

  .continentes {
      display: flex;
      flex-direction: row-reverse;
      height: 40px;
      position: absolute;
      border-width: 5px;
  }

  .modulos {
    width: 50px; /* Ajusta según sea necesario */
    height: 50px; /* Ajusta según sea necesario */
}

  .modulos svg {
      width: 50px; /* Ajusta el tamaño del SVG según sea necesario */
      height: 50px;
  }

  /* Estilo para el color de los SVGs */
  .modulos path {
      fill: var(--color-svg); /* Cambia el color según el valor de adictividad */
  }
</style>
