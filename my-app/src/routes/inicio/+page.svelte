<script>
  import { onMount } from "svelte";
  

  let productos = [
    { id: 1, nombre: "Laptop Gamer", precio: 1500, imagen: "https://th.bing.com/th/id/OIP.oHUhYouCvPf8Nv7mw7ug2wHaE8?w=266&h=180&c=7&r=0&o=5&dpr=1.3&pid=1.7" },
    { id: 2, nombre: "Smartphone Pro", precio: 800, imagen: "data:image/jpeg;base64,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" },
    { id: 3, nombre: "Auriculares Bluetooth", precio: 120, imagen: "data:image/jpeg;base64,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" },
    { id: 4, nombre: "Smartwatch", precio: 250, imagen: "https://th.bing.com/th/id/OIP.37pktTb-fY_VfUGveXLb2wHaHa?w=209&h=209&c=7&r=0&o=5&dpr=1.3&pid=1.7" },
    { id: 5, nombre: "Tablet", precio: 600, imagen: "https://th.bing.com/th/id/OIP.i5qPz-s-vn_QdVqiUQBCswHaHa?w=182&h=183&c=7&r=0&o=5&dpr=1.3&pid=1.7" },
    { id: 6, nombre: "Teclado Mecánico", precio: 100, imagen: "https://th.bing.com/th/id/OIP.HW3Zo-IA5nYVaC0EwgB-WgHaD7?w=253&h=180&c=7&r=0&o=5&dpr=1.3&pid=1.7" }
  ];

  let carrito = [];
  let total = 0;
  let factura = null;
  let metodoPago = "";
  let mostrarFactura = false;

  function agregarAlCarrito(producto) {
    let item = carrito.find((p) => p.id === producto.id);
    if (item) {
      item.cantidad += 1;
    } else {
      carrito = [...carrito, { ...producto, cantidad: 1 }];
    }
    calcularTotal();
  }

  function calcularTotal() {
    total = carrito.reduce((acc, item) => acc + item.precio * item.cantidad, 0);
  }

  function eliminarDelCarrito(id) {
    carrito = carrito.filter((item) => item.id !== id);
    calcularTotal();
  }

  function actualizarCantidad(id, cantidad) {
    carrito = carrito.map((item) =>
      item.id === id ? { ...item, cantidad: Math.max(1, cantidad) } : item
    );
    calcularTotal();
  }

  function generarFactura() {
    factura = {
      items: [...carrito],
      total,
      metodoPago,
      fecha: new Date().toLocaleString()
    };
    mostrarFactura = true;
  }

  function pagar() {
    if (!metodoPago) {
      alert("Seleccione un método de pago.");
      return;
    }
    generarFactura();
    carrito = [];
    total = 0;
  }
</script>

<nav class="navbar">
  <h1>🛒 Mi Tienda</h1>
 
  <div class="menu">
    <a href="#">login</a>
    
    <a href="#">Alquiler</a>
    <a href="#">Servicio al Cliente</a>
  </div>
</nav>



<div class="container">
  <main>
    <div class="productos">
      {#each productos as producto}
        <div class="producto">
          <img src={producto.imagen} alt={producto.nombre} />
          <h3>{producto.nombre}</h3>
          <p class="precio">${producto.precio}</p>
          <button class="btn-agregar" on:click={() => agregarAlCarrito(producto)}>Agregar</button>
        </div>
      {/each}
    </div>
  </main>

  <aside class="carrito">
    <h2>Carrito de Compras</h2>
    {#if carrito.length === 0}
      <p>Tu carrito está vacío.</p>
    {:else}
      <ul class="carrito-lista">
        {#each carrito as item}
          <li class="carrito-item">
            {item.nombre} - ${item.precio} x 
            <input type="number" min="1" bind:value={item.cantidad} on:change={() => actualizarCantidad(item.id, item.cantidad)}>
            <button class="btn-eliminar" on:click={() => eliminarDelCarrito(item.id)}>❌</button>
          </li>
        {/each}
      </ul>
      <h3>Total: ${total}</h3>
      <select bind:value={metodoPago}>
        <option value="">Método de Pago</option>
        <option value="Efectivo">Efectivo</option>
        <option value="PSE">PSE</option>
      </select>
      <button class="btn-pago" on:click={pagar}>Pagar</button>
    {/if}
  </aside>
</div>

{#if mostrarFactura}
  <div class="modal">
    <div class="modal-content">
      <h2>Factura Electrónica</h2>
      <p>Fecha: {factura.fecha}</p>
      <ul>
        {#each factura.items as item}
          <li>{item.nombre} - ${item.precio} x {item.cantidad}</li>
        {/each}
      </ul>
      <h3>Total: ${factura.total}</h3>
      <p>Método de pago: {factura.metodoPago}</p>
      <button class="btn-cerrar" on:click={() => mostrarFactura = false}>Cerrar</button>
    </div>
  </div>
{/if}

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #111;
  color: white;
  font-family: Arial, sans-serif;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #222;
  padding: 15px 30px;
  color: white;
}

.navbar h1 {
  font-size: 24px;
}

.menu {
  display: flex;
  gap: 20px;
}

.menu a {
  text-decoration: none;
  color: white;
  font-size: 18px;
  font-weight: bold;
  padding: 10px 15px;
  border-radius: 5px;
  transition: background 0.3s, transform 0.2s;
}

.menu a:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.05);
}

  .navbar {
    background: #ff6600;
    color: white;
    padding: 15px;
    text-align: center;
    font-size: 1.5rem;
    font-weight: bold;
  }

  .container {
    display: flex;
    justify-content: space-between;
    padding: 20px;
  }

  .productos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
  }

  .producto {
    border: 1px solid #ddd;
    padding: 15px;
    border-radius: 10px;
    text-align: center;
    background: white;
    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }

  .producto:hover {
    transform: scale(1.05);
  }

  .carrito-lista {
    list-style: none;
    padding: 0;
  }

  .carrito-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background: white;
    margin-bottom: 10px;
    border-radius: 8px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  }

  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0px 3px 10px rgba(0, 0, 0, 0.2);

  }
  
</style>
