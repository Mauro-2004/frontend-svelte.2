<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import jsPDF from 'jspdf';
    import autoTable from 'jspdf-autotable';
  
    let fechaInicio = '';
    let fechaFin = '';
    let categoria = '';
    let estadoPedido = '';
    let cliente = '';
  
    let productosVendidos = writable([]);
    let historialPedidos = writable([]);
    let ingresosTotales = writable(0);
  
    onMount(() => {
      productosVendidos.set([
        { nombre: 'Laptop', cantidad: 5 },
        { nombre: 'Celular', cantidad: 8 }
      ]);
      historialPedidos.set([
        { id: 1, cliente: 'Juan Pérez', producto: 'Laptop', estado: 'Pendiente', total: 1500 },
        { id: 2, cliente: 'Ana Gómez', producto: 'Celular', estado: 'Entregado', total: 800 }
      ]);
      ingresosTotales.set(2300);
    });
  
    function generarPDF() {
      const doc = new jsPDF();
      doc.text('Reporte de Ventas y Alquileres', 10, 10);
      doc.text(`Fecha: ${new Date().toLocaleDateString()}`, 10, 20);
      
      autoTable(doc, {
        startY: 30,
        head: [['Producto', 'Cantidad Vendida']],
        body: $productosVendidos.map(p => [p.nombre, p.cantidad])
      });
  
      autoTable(doc, {
        startY: doc.lastAutoTable.finalY + 10,
        head: [['ID', 'Cliente', 'Producto', 'Estado', 'Total']],
        body: $historialPedidos.map(p => [p.id, p.cliente, p.producto, p.estado, `$${p.total}`])
      });
  
      doc.save('Reporte_Ventas_Alquileres.pdf');
    }
</script>
  
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: #f4f4f4;
      color: #333;
    }
    .container {
      max-width: 1200px;
      margin: auto;
      padding: 20px;
    }
    .card {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      margin-bottom: 20px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      padding: 10px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }
    th {
      background-color: #007bff;
      color: white;
    }
  </style>
  
  <div class="container">
    <div class="card">
      <h2>Reporte de Ventas y Alquileres</h2>
      <p>Seleccione un rango de fechas y filtros para generar el reporte.</p>
      <input type="date" bind:value={fechaInicio} />
      <input type="date" bind:value={fechaFin} />
      <select bind:value={categoria}>
        <option value="">Todas las categorías</option>
        <option value="Electrónica">Electrónica</option>
      </select>
      <select bind:value={estadoPedido}>
        <option value="">Todos los estados</option>
        <option value="Pendiente">Pendiente</option>
        <option value="Entregado">Entregado</option>
      </select>
      <input type="text" bind:value={cliente} placeholder="Buscar cliente o ID" />
      <button>Generar Reporte</button>
    </div>
  
    <div class="card">
      <h3>Productos más vendidos</h3>
      <table>
        <thead>
          <tr>
            <th>Producto</th>
            <th>Cantidad Vendida</th>
          </tr>
        </thead>
        <tbody>
          {#each $productosVendidos as producto}
            <tr>
              <td>{producto.nombre}</td>
              <td>{producto.cantidad}</td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  
    <div class="card">
      <h3>Historial de Pedidos</h3>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Cliente</th>
            <th>Producto</th>
            <th>Estado</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody>
          {#each $historialPedidos as pedido}
            <tr>
              <td>{pedido.id}</td>
              <td>{pedido.cliente}</td>
              <td>{pedido.producto}</td>
              <td>{pedido.estado}</td>
              <td>${pedido.total}</td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  
    <div class="card">
      <h3>Resumen de Ingresos</h3>
      <p>Total generado: ${$ingresosTotales}</p>
    </div>
  
    <div class="card">
      <button on:click={generarPDF}>Descargar Reporte (PDF)</button>
      <button>Exportar a Excel</button>
      <button>Compartir por Correo</button>
    </div>
  </div>
  