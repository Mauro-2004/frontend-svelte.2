<script>
  import { onMount } from 'svelte';
  let pedidos = [
      { id: 1, cliente: "James rodriquez", direccion: "itsa barranquilla", estado: "Pendiente" },
      { id: 2, cliente: "falcao garcia", direccion: "itsa soledad", estado: "En camino" },
      { id: 3, cliente: "david ospina", direccion: "posgrado", estado: "Entregado" }
  ];

  function actualizarEstado(id, nuevoEstado) {
      pedidos = pedidos.map(pedido => pedido.id === id ? { ...pedido, estado: nuevoEstado } : pedido);
  }
</script>

<header>
  <nav>
      <a href="#">Inicio</a>
      
      <a href="#">login</a>
  </nav>
</header>

<main>
  <h1>Panel del Repartidor</h1>
  <div class="pedidos-container">
      {#each pedidos as pedido}
          <div class="pedido">
              <h3>Pedido #{pedido.id}</h3>
              <p><strong>Cliente:</strong> {pedido.cliente}</p>
              <p><strong>Dirección:</strong> {pedido.direccion}</p>
              <p><strong>Estado:</strong> {pedido.estado}</p>
              <button on:click={() => actualizarEstado(pedido.id, "En camino")}>En camino</button>
              <button on:click={() => actualizarEstado(pedido.id, "Entregado")}>Entregado</button>
          </div>
      {/each}
  </div>
</main>

<style>
  body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f4f4f4;
  }

  header {
      background: #007bff;
      padding: 15px;
      text-align: center;
  }
  
  nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-size: 18px;
  }
  
  main {
      padding: 20px;
      text-align: center;
  }
  
  .pedidos-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
  }
  
  .pedido {
      background: white;
      padding: 15px;
      margin: 10px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      width: 300px;
  }
  
  button {
      background: #28a745;
      color: white;
      border: none;
      padding: 8px 12px;
      margin: 5px;
      cursor: pointer;
      border-radius: 5px;
  }
  
  button:hover {
      background: #218838;
  }
</style>
