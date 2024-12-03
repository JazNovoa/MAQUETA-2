<!-- Script JS -->
<script>
  import * as d3 from "d3";
  import juegos from "/src/data/juegos.json"; //importamos juegos


  
  let modulos = [
      "/images/AVENTURA.svg",
      "/images/CASUAL.svg",
      "/images/ESTRATEGIA.svg",
      "/images/IDLE.svg",
      "/images/TYCOON.svg",
  ];

  function getImage() {
      return modulos;
  }

  //escala para almacenamiento
  const almacenamiento = d3
      .scaleLinear()
      .domain(["0-0.3", "0.3-0.6", "0.6-0.9", "0.9-1.2", "1.2-3.0"])
      .range([3, 4, 6, 8, 15]);

  //escala para años
  const años = d3
      .scaleLinear()
      .domain(["0-4", "5-8", "9-12", "13-16", "17-20"])
      .range([3, 6, 9, 12, 15]);

  //escala adictividad
  const adictividad = d3
      .scaleLinear()
      .domain([1, 2, 3, 4, 5])
      .range(["#000aff", "#9200b8", "#e92fed", "ff9a51", "ffe86f"]);

  //escala continente
  const continente = d3
      .scaleOrdinal()
      .domain(["África", "Asia", "Europa", "Norteamérica", "Sudamérica"])
      .range(["#000aff", "#9200b8", "#e92fed", "ff9a51", "ffe86f"]);

  //escala género
  const genero = d3.scaleOrdinal()
  .domain(["Aventura", "Casual", "Estrategia", "Idle", "Tycoon"])
  .range(modulos);
</script>

<!-- Estructura contenido HTML -->
<main>

  <img src="/images/AVENTURA.svg" alt="Aventura" />

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
