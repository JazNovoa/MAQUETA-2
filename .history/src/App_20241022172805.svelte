<!-- Script JS -->
<main>
  <div class="header">
    <img class="titulo" src="./public/images/TITULO.svg" width="50%" />
  </div>

  <div class="contenedor">
    {#each juegosSVG as juego}
      <div class="juego-item">
        <p class="nombre-juego">{juego.Juego}</p>  <!-- Cambiado aquí -->
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
    justify-content: flex-start; /* Cambiado aquí */
    margin: 0; /* Sin margen entre filas */
  }

  .modulos {
    display: flex;
  }

  .svg-wrapper {
    display: block;
    width: 40px;
    height: 40px;
  }

  .svg-wrapper svg {
    width: 100%;
    height: 100%;
    display: block;
  }

  .nombre-juego {
    width: 150px; /* Ajustar según sea necesario */
    text-align: right; /* Cambiado aquí */
    font-size: 16px;
    color: white;
    margin: 0; /* Sin margen adicional */
    padding: 0; /* Sin padding */
    margin-right: 10px; /* Espacio entre el nombre del juego y los módulos SVG */
  }
</style>
