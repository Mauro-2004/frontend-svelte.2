<script>
  import { onMount } from 'svelte';
  let productos = [];
  let pedidos = [];

  onMount(() => {
    productos = [
      { id: 1, nombre: 'Laptop', categoria: 'Electrónica', stock: 10, precio: 1500, alquiler: 50 },
      { id: 2, nombre: 'Celular', categoria: 'Electrónica', stock: 5, precio: 800, alquiler: 30 }
    ];
    
    pedidos = [
      { id: 1, cliente: 'Juan Pérez', producto: 'Laptop', estado: 'Pendiente', inicio: '2025-03-10', fin: '2025-03-15' },
      { id: 2, cliente: 'Ana Gómez', producto: 'Celular', estado: 'Entregado', inicio: '2025-03-05', fin: '2025-03-10' }
    ];
  });

  function agregarProducto() {
    const nuevoProducto = { id: productos.length + 1, nombre: 'Nuevo Producto', categoria: 'General', stock: 1, precio: 100, alquiler: 10 };
    productos = [...productos, nuevoProducto];
  }

  function eliminarProducto(id) {
    productos = productos.filter(p => p.id !== id);
  }
</script>

<style>
  body {
    background-color: #6182e3;
    color: #fff;
    font-family: 'Arial', sans-serif;
  }
  .card {
    background: #d4d4f0;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(26, 201, 240, 0.753);
  }
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    padding: 10px;
    text-align: left;
  }
  th {
    background-color: #e15b1d;
  }
  tr:nth-child(even) {
    background-color: #bbdbf1;
  }
  tr:hover {
    background-color: #85baf6;
  }
  .btn {
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .btn-add {
    background: #6182e3;
    color: white;
  }
  .btn-delete {
    background: #e74c3c;
    color: white;
  }
</style>

<div class="container mx-auto p-6 space-y-6">
  <div class="card">
    <h2 class="text-2xl font-bold mb-4">Gestión de Productos</h2>
    <button class="btn btn-add" on:click={agregarProducto}>+ Agregar Producto</button>
    <table class="mt-4">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Categoría</th>
          <th>Stock</th>
          <th>Precio</th>
          <th>Alquiler</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        {#each productos as producto (producto.id)}
          <tr>
            <td>{producto.nombre}</td>
            <td>{producto.categoria}</td>
            <td>{producto.stock}</td>
            <td>${producto.precio}</td>
            <td>${producto.alquiler}</td>
            <td>
              <button class="btn btn-delete" on:click={() => eliminarProducto(producto.id)}>Eliminar</button>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>

  <div class="card">
    <h2 class="text-2xl font-bold mb-4">Gestión de Pedidos</h2>
    <table>
      <thead>
        <tr>
          <th>Cliente</th>
          <th>Producto</th>
          <th>Estado</th>
          <th>Inicio</th>
          <th>Fin</th>
        </tr>
      </thead>
      <tbody>
        {#each pedidos as pedido (pedido.id)}
          <tr>
            <td>{pedido.cliente}</td>
            <td>{pedido.producto}</td>
            <td class={pedido.estado === 'Pendiente' ? 'text-yellow-400' : 'text-green-400'}>{pedido.estado}</td>
            <td>{pedido.inicio}</td>
            <td>{pedido.fin}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>
