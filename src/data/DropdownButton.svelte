<!-- DropdownButton.svelte -->
<script>
    export let options = []; // Opciones que se pasarán al componente
    let selectedOption = null;
    let isMenuOpen = false;

    const toggleDropdown = () => {
    isOpen = !isOpen;
  };
  
    function selectOption(option) {
      selectedOption = option;
      isMenuOpen = false; // Cierra el menú
    }
  </script>
  
<!-- HTML -->
  <div class="menu-container">
    <!-- Botón principal -->
    <button class="button" on:click={() => (isMenuOpen = !isMenuOpen)}>
      {selectedOption ? selectedOption.label : "Elegí"}
      <span class="dropdown-arrow {isMenuOpen ? 'open' : ''}"></span>
    </button>
  
  
    <!-- Menú desplegable -->
    {#if isMenuOpen}
      <div class="dropdown">
        {#each options as option}
          <button on:click={() => selectOption(option)}>{option.label}</button>
        {/each}
      </div>
    {/if}
  
    <!-- Contenido seleccionado -->
    {#if selectedOption}
      <div class="info-box">
        {@html selectedOption.content}
      </div>
    {/if}
  </div>


  <style>
    .menu-container {
      position: relative;
      display: inline-block;
      margin: 60px; /* Espacio entre botones */
    }
  
    .button {
    padding: 10px 20px;
    cursor: pointer;
    background-color: black;
    display: flex;
    position: absolute;
    color: white;
    font-size: 25px;
    border: white;
    border-radius: 60px;
    border-width: 6px;
    border-style:inset;
    margin-top: 70px;
    margin-left: 170px;
    width: 380px;
    height: 50px;
    align-items: center;
    justify-content: flex-start;
    
    }
  
    .button:hover {
    background-image: url('./images/HoverDropdown.png');
    background-size: cover;
    border: none;
    width: 350px;
    }
  
    .dropdown {
      position: absolute;
      left: 0;
      background-color: white;
      border: 1px solid #ddd;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
      border-radius: 20px;
      width: 643px;
      z-index: 10;
      margin-top: 130px;
      margin-left: 170px;
    }
  
    .dropdown button {
      background: none;
      border: none;
      border-radius: 20px;
      padding: 10px;
      width: 100%;
      text-align: left;
      cursor: pointer;
      font-size: 20px;
    }
  
    .dropdown button:hover {
      background-color: #000AFF;
      color: white;
    }
  
    .info-box {
    display: flex;
    padding: 10px;
    border-radius: 5px;
    width: 750px;
    height: 250px;
    margin-top: 140px;
    margin-left: 150px;
    }

    .dropdown-arrow {
    display: inline-block;
    width: 0;
    height: 0;
    position: absolute; /* Fija la posición respecto al botón */
    right: 30px; /* Espaciado desde el borde derecho del botón */
    top: 35%; /* Centra verticalmente */
    transform: translateY(-50%); /* Ajusta para centrar exactamente */
    border-left: 13px solid transparent;
    border-right: 13px solid transparent;
    border-top: 13px solid white; /* Color de la flecha */
    transform: rotate(0deg); /* Rotación normal */
    transition: transform 0.3s ease; /* Animación de rotación */
}

.dropdown-arrow.open {
    transform: rotate(180deg); /* Rotación hacia arriba */
  }
  </style>
  
  