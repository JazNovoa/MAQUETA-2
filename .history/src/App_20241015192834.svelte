<!-- Script JS -->
<script>
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json"; // Importamos juegos
  
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
      {#each juegos as juego}
      <div><p>{juego.Juego}</p></div>
      
      <div 
          class="continentes"
          style="border-color: {continente(juego.Continente)}; width: {años(juego.Años)}%;">
      </div>
  
      <div class="modulos">
          <img 
              src={genero(juego.Juego)} 
              alt="{juego.Juego}" 
              style="width: {años(juego.Años)}px;" 
          />
      </div>
  {/each}
  </div>
</main>

<!-- Estilos CSS -->

<style>
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
      display: flex;
      flex-direction: row-reverse;
      width: 20px;
      height: 20px;
  }
</style>
