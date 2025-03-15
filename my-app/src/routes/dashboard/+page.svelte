<script>
    import { onMount } from "svelte";

    let pieCanvas, barCanvas;
    let pieChart, barChart;

    onMount(() => {
        if (typeof Chart === "undefined") {
            console.error("Chart.js no se ha cargado. Verifica el CDN.");
            return;
        }

        if (pieCanvas) {
            pieChart = new Chart(pieCanvas.getContext("2d"), {
                type: "pie",
                data: {
                    labels: ["Laptops", "Cámaras", "Drones", "Tablets"],
                    datasets: [{
                        data: [40, 25, 20, 15],
                        backgroundColor: ["#007bff", "#ff5733", "#28a745", "#ffc107"]
                    }]
                },
                options: {
                    plugins: {
                        legend: { position: "bottom" }
                    }
                }
            });
        }

        if (barCanvas) {
            barChart = new Chart(barCanvas.getContext("2d"), {
                type: "bar",
                data: {
                    labels: ["Enero", "Febrero", "Marzo", "Abril"],
                    datasets: [{
                        label: "Alquileres Mensuales",
                        data: [30, 40, 50, 60],
                        backgroundColor: "#007bff"
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            });
        }
    });
</script>

<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f4f4f4;
        display: flex;
    }
    .container {
        display: flex;
        width: 100%;
        height: 100vh;
    }
    .sidebar {
        width: 250px;
        background: #007bff;
        padding: 20px;
        color: white;
        display: flex;
        flex-direction: column;
    }
    .sidebar h2 {
        text-align: center;
        margin-bottom: 20px;
    }
    .sidebar ul {
        list-style: none;
        padding: 0;
    }
    .sidebar ul li {
        padding: 10px;
        cursor: pointer;
        text-align: center;
        transition: background 0.3s;
    }
    .sidebar ul li:hover {
        background: rgba(255, 255, 255, 0.2);
        border-radius: 5px;
    }
    .dashboard {
        flex: 1;
        padding: 20px;
        display: flex;
        flex-direction: column;
    }
    .dashboard-header {
        background: #fff;
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        text-align: center;
        font-size: 24px;
        font-weight: bold;
        margin-bottom: 15px;
    }
    .content {
        display: flex;
        flex-wrap: wrap;
        gap: 15px;
        align-items: flex-start;
    }
    .chart-container, .stats-container, .graph-container, .table-container {
        background: #fff;
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        flex: 1;
        min-width: 300px;
    }
    .chart-container, .graph-container {
        height: 300px;
    }
    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
    }
    th, td {
        padding: 10px;
        border: 1px solid #ddd;
        text-align: center;
    }
    th {
        background-color: #007bff;
        color: white;
    }
</style>

<div class="container">
    <div class="sidebar">
        <h2>Menú</h2>
        <ul>
           
            <li>Reportes</li>
            <li>power bi</li>
            <li>inicio</li>
            <li>Salir</li>
            <li>gestion producto y pedidos</li>
            




            
        </ul>
    </div>
    <div class="dashboard">
        <div class="dashboard-header">Dashboard de Alquiler de Electrónicos</div>
        <div class="content">
            <div class="chart-container">
                <h2>Distribución de Alquileres</h2>
                <canvas bind:this={pieCanvas}></canvas>
            </div>
            <div class="stats-container">
                <h2>Estadísticas</h2>
                <p>Total Alquileres: <strong>120</strong></p>
                <p>Clientes Activos: <strong>45</strong></p>
                <p>Productos Disponibles: <strong>30</strong></p>
            </div>
            <div class="graph-container">
                <h2>Tendencias de Alquiler</h2>
                <canvas bind:this={barCanvas}></canvas>
            </div>
        </div>
        <div class="table-container">
            <h2>Gestión de Productos</h2>
            <table>
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Producto</th>
                        <th>Precio</th>
                        <th>Acciones</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>1</td>
                        <td>Laptop</td>
                        <td>$50/día</td>
                        <td>
                            <button>Editar</button>
                            <button>Eliminar</button>
                        </td>
                    </tr>
                    <tr>
                        <td>2</td>
                        <td>Cámara</td>
                        <td>$30/día</td>
                        <td>
                            <button>Editar</button>
                            <button>Eliminar</button>
                        </td>
                    </tr>
                </tbody>
            </table>
            <button>Agregar Nuevo</button>
        </div>
    </div>
</div>
