<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gestión de Solicitudes | I&H</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&family=Montserrat:wght@500;600;700&display=swap">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #008f5f;
            --primary-dark: #006e48;
            --primary-light: #e6f5ef;
            --secondary-color: #5f8fff;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
            --light-color: #f8f9fa;
            --dark-color: #343a40;
            --gray-medium: #6c757d;
            --gray-light: #e9ecef;
            --text-color: #212529;
            --text-light: #6c757d;
        }

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            background-color: #f8f9fa;
            color: var(--text-color);
            line-height: 1.6;
        }

        .app-container {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* Header estilizado */
        .app-header {
            background: linear-gradient(135deg, var(--primary-color), var(--primary-dark));
            color: white;
            padding: 1rem 2rem;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 10;
            width:100%;
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .logo-svg {
            width: 42px;
            height: 42px;
            fill: white;
        }

        .app-title {
            font-family: 'Montserrat', sans-serif;
            font-size: 1.5rem;
            font-weight: 600;
            margin: 0;
            letter-spacing: 0.5px;
        }

        /* Contenido principal */
        .main-content {
            flex: 1;
            padding: 2rem;
            max-width: 1400px;
            width: 100%;
            margin: 0 auto;
        }

        /* Panel de control */
        .dashboard-panel {
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 24px rgba(0, 0, 0, 0.06);
            padding: 2rem;
            margin-bottom: 2rem;
            border: 1px solid var(--gray-light);
        }

        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding-bottom: 1.25rem;
            border-bottom: 1px solid var(--gray-light);
        }

        .panel-title {
            font-family: 'Montserrat', sans-serif;
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--primary-color);
            margin: 0;
        }

        /* Barra de búsqueda mejorada */
        .search-container {
            position: relative;
            width: 100%;
            max-width: 500px;
        }

        .search-input {
            width: 80%;
            padding: 0.85rem 1.5rem 0.85rem 3.25rem;
            font-size: 0.95rem;
            border: 1px solid var(--gray-light);
            border-radius: 50px;
            background-color: white;
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
        }

        .search-input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 4px 12px rgba(0, 143, 95, 0.15);
        }

        .search-icon {
            position: absolute;
            left: 1.5rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--gray-medium);
        }

        /* Badge de contador */
        .badge {
            display: inline-block;
            padding: 0.35rem 0.85rem;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 500;
            background-color: var(--primary-light);
            color: var(--primary-color);
        }

        /* Botones */
        .track-button, .chart-button {
            display: inline-flex;
            align-items: center;
            padding: 0.5rem 1.25rem;
            margin-left: 0.75rem;
            border-radius: 50px;
            text-decoration: none;
            font-weight: 500;
            font-size: 0.85rem;
            transition: all 0.2s ease;
            border: none;
            cursor: pointer;
            box-shadow: 0 2px 8px rgba(95, 143, 255, 0.3);
        }

        .track-button {
            background-color: #008f5f;
            color: white;
        }

        .chart-button {
            background-color: #008f5f
            ;
            color: white;
        }

        .track-button:hover {
            background-color: #87BB59;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(95, 143, 255, 0.4);
        }

        .chart-button:hover {
            background-color: #87BB59
            ;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(95, 143, 255, 0.4);
        }

        /* Tabla profesional */
        .table-responsive {
            overflow-x: auto;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.04);
        }

        .data-table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            font-size: 0.92rem;
            min-width: 800px;
        }

        .data-table thead th {
            background-color: var(--primary-color);
            color: white;
            font-weight: 500;
            padding: 1rem 1.5rem;
            text-align: left;
            position: sticky;
            top: 0;
            font-family: 'Montserrat', sans-serif;
        }

        .data-table thead th:first-child {
            border-top-left-radius: 10px;
        }

        .data-table thead th:last-child {
            border-top-right-radius: 10px;
        }

        .data-table tbody tr {
            transition: all 0.25s ease;
        }

        .data-table tbody tr:nth-child(even) {
            background-color: var(--light-color);
        }

        .data-table tbody tr:hover {
            background-color: var(--primary-light);
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0, 143, 95, 0.1);
        }

        .data-table td {
            padding: 1.25rem 1.5rem;
            border-bottom: 1px solid var(--gray-light);
            vertical-align: middle;
        }

        /* Estilos de estado */
        .status-badge {
            display: inline-flex;
            align-items: center;
            padding: 0.4rem 1rem;
            border-radius: 50px;
            font-size: 0.82rem;
            font-weight: 500;
            text-transform: capitalize;
            letter-spacing: 0.3px;
        }

        .status-badge:before {
            content: "";
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            margin-right: 8px;
        }

        .status-closed {
            background-color: rgba(0, 143, 95, 0.1);
            color: var(--primary-color);
        }

        .status-closed:before {
            background-color: var(--primary-color);
        }

        .status-open {
            background-color: rgba(95, 143, 255, 0.1);
            color: var(--secondary-color);
        }

        .status-open:before {
            background-color: var(--secondary-color);
        }

        .status-cancelled {
            background-color: rgba(220, 53, 69, 0.1);
            color: var(--danger-color);
        }

        .status-cancelled:before {
            background-color: var(--danger-color);
        }

        /* Modal para el gráfico */
        .modal {
            display: none;
            position: fixed;
            z-index: 100;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            animation: fadeIn 0.3s;
        }

        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 2rem;
            border-radius: 12px;
            width: 80%;
            max-width: 600px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 1rem;
            right: 1.5rem;
            font-size: 1.5rem;
            color: var(--gray-medium);
            cursor: pointer;
        }

        .chart-container {
            width: 100%;
            height: 400px;
            margin-top: 1.5rem;
        }

        /* Footer */
        .app-footer {
            background-color: var(--dark-color);
            color: white;
            text-align: center;
            padding: 1.5rem;
            font-size: 0.85rem;
            margin-top: auto;
        }

        .app-footer a {
            color: var(--primary-color);
            text-decoration: none;
            font-weight: 500;
        }

        /* Efectos y transiciones */
        .fade-in {
            animation: fadeIn 0.5s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Responsive */
        @media (max-width: 992px) {
            .main-content {
                padding: 1.5rem;
            }
            
            .dashboard-panel {
                padding: 1.5rem;
            }
        }

        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                align-items: flex-start;
                gap: 1rem;
                padding: 1rem 0;
            }
            
            .app-header {
                padding: 1rem;
            }
            
            .search-container {
                max-width: 100%;
            }
            
            .panel-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 1rem;
            }
            
            .panel-actions {
                display: flex;
                flex-wrap: wrap;
                gap: 0.5rem;
            }
            
            .track-button, .chart-button {
                margin-left: 0;
            }
            
            .data-table td, 
            .data-table th {
                padding: 1rem;
            }
            
            .modal-content {
                width: 90%;
                margin: 10% auto;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <header class="app-header">
            <div class="header-content">
                <div class="logo-container">
                    <svg class="logo-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm0 16H5V5h14v14z"/>
                        <path d="M8.5 15H10v-5H7v1.5h1.5zM13.5 12.75L16.25 15H18l-2.25-3L18 9h-1.75l-2.75 3.75V9H12v6h1.5z"/>
                        <path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6z"/>
                        <path d="M16 16H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L18.5 9H13z" fill="#fff"/>
                        <path d="M9.55 15.45l-2.1-2.1-1.4 1.4 3.5 3.5 6-6-1.4-1.4z" fill="#fff"/>
                    </svg>
                    <h1 class="app-title">Gestión de Solicitudes I&H</h1>
                </div>
                <div class="search-container">
                    <svg class="search-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M11 19C15.4183 19 19 15.4183 19 11C19 6.58172 15.4183 3 11 3C6.58172 3 3 6.58172 3 11C3 15.4183 6.58172 19 11 19Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                        <path d="M21 21L16.65 16.65" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                    <input type="text" id="search-bar" class="search-input" placeholder="Buscar por ID, estado o descripción..." oninput="searchTable()">
                </div>
            </div>
        </header>

        <main class="main-content">
            <section class="dashboard-panel fade-in">
                <div class="panel-header">
                    <h2 class="panel-title">Registro de Solicitudes</h2>
                    <div class="panel-actions">
                        <span id="total-count" class="badge">Cargando...</span>
                        <button id="chart-button" class="chart-button">
                            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path d="M3 3v17h18" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                                <path d="M18 17V9M12 17V5M6 17v-3" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                            </svg>
                            Ver Gráfico
                        </button>
                        <a href="https://interrapidisimo.com/" target="_blank" class="track-button">Rastrear</a>
                    </div>
                </div>
                
                <div class="table-responsive">
                    <table class="data-table" id="data-table">
                        <thead>
                            <tr>
                                <!-- Las cabeceras de las columnas se insertarán aquí con JavaScript -->
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Las filas de datos se insertarán aquí con JavaScript -->
                        </tbody>
                    </table>
                </div>
            </section>
        </main>

        <!-- Modal para el gráfico -->
        <div id="chart-modal" class="modal">
            <div class="modal-content">
                <span class="close-modal">&times;</span>
                <h3>Estadísticas de Solicitudes</h3>
                <p>Distribución de solicitudes por estado</p>
                <div class="chart-container">
                    <canvas id="requests-chart"></canvas>
                </div>
            </div>
        </div>

        <footer class="app-footer">
            <p>© 2025 <a href="#" target="_blank">I&H</a> - Sistema de Gestión de Solicitudes. Versión 1.0.0<hr>Creado por: Daniel Martinez- Operaciones</p>
        </footer>
    </div>

    <script>
        // URL del archivo CSV generado desde Google Sheets
        const CSV_URL = 'https://docs.google.com/spreadsheets/d/12C9OBKWeBLaBTxOzhq9fsr5S3U-fe1MPKJdeYTG7gSE/export?format=csv&id=12C9OBKWeBLaBTxOzhq9fsr5S3U-fe1MPKJdeYTG7gSE&gid=1708695779&range=A2:BX';

        // Configuración de columnas modificada para incluir la columna "e" (columna 4)
        const COLUMNS_TO_SHOW = [0, 1, 4, 5, 9, 10, 51, 52];
        const STATE_COLUMN_INDEX = 51;
        const REQUEST_NUMBER_COLUMN_INDEX = 0;
        const STATE_DISPLAY_INDEX = 6; // Actualizado porque añadimos una columna antes
        const BA_COLUMN_INDEX = 7;

        // Datos de la tabla
        let tableData = [];
        let headers = [];
        let requestsChart = null;

        // Función para obtener los datos del CSV
        async function fetchCSVData() {
            try {
                document.getElementById('total-count').textContent = "Cargando datos...";
                
                const response = await fetch(CSV_URL);
                if (!response.ok) throw new Error('Error en la red');
                
                const csvText = await response.text();
                const data = parseCSV(csvText);
                
                if (!data || data.length === 0) throw new Error('Datos no válidos');
                
                headers = data[0] || [];
                tableData = data.slice(1) || [];
                
                populateTable(tableData);
                updateTotalCount(tableData.length);
                
            } catch (error) {
                console.error('Error al cargar los datos:', error);
                document.getElementById('total-count').textContent = "Error al cargar datos";
            }
        }

        // Función para parsear CSV mejorada
        function parseCSV(csvText) {
            const rows = [];
            let currentRow = [];
            let currentField = '';
            let inQuotes = false;
            
            for (let i = 0; i < csvText.length; i++) {
                const char = csvText[i];
                
                if (char === '"') {
                    inQuotes = !inQuotes;
                } else if (char === ',' && !inQuotes) {
                    currentRow.push(currentField.trim());
                    currentField = '';
                } else if (char === '\n' && !inQuotes) {
                    currentRow.push(currentField.trim());
                    rows.push(currentRow);
                    currentRow = [];
                    currentField = '';
                } else {
                    currentField += char;
                }
            }
            
            // Añadir la última fila
            if (currentField.trim() !== '' || currentRow.length > 0) {
                currentRow.push(currentField.trim());
                rows.push(currentRow);
            }
            
            return rows;
        }

        // Función para contar solicitudes por estado (modificada para incluir cancelados)
        function countRequestsByStatus() {
            let openCount = 0;
            let closedCount = 0;
            let cancelledCount = 0;

            tableData.forEach(row => {
                const estado = String(row[STATE_COLUMN_INDEX] || '').toLowerCase();
                if (estado.includes('abierto')) {
                    openCount++;
                } else if (estado.includes('cerrado')) {
                    closedCount++;
                } else if (estado.includes('cancelado')) {
                    cancelledCount++;
                }
            });

            return { openCount, closedCount, cancelledCount };
        }

        // Función para crear el gráfico (actualizada con categoría cancelados)
        function createRequestsChart() {
            const { openCount, closedCount, cancelledCount } = countRequestsByStatus();
            const ctx = document.getElementById('requests-chart').getContext('2d');
            
            if (requestsChart) {
                requestsChart.destroy();
            }
            
            requestsChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Abiertas', 'Cerradas', 'Canceladas'],
                    datasets: [{
                        data: [openCount, closedCount, cancelledCount],
                        backgroundColor: [
                            'rgba(95, 143, 255, 0.8)',  // Azul para abiertas
                            'rgba(0, 143, 95, 0.8)',    // Verde para cerradas
                            'rgba(220, 53, 69, 0.8)'    // Rojo para canceladas
                        ],
                        borderColor: [
                            'rgba(95, 143, 255, 1)',
                            'rgba(0, 143, 95, 1)',
                            'rgba(220, 53, 69, 1)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const label = context.label || '';
                                    const value = context.raw || 0;
                                    const total = context.dataset.data.reduce((a, b) => a + b, 0);
                                    const percentage = Math.round((value / total) * 100);
                                    return `${label}: ${value} (${percentage}%)`;
                                }
                            }
                        }
                    },
                    cutout: '65%',
                    animation: {
                        animateScale: true,
                        animateRotate: true
                    }
                }
            });
        }

        // Función para mostrar el modal con el gráfico
        function showChartModal() {
            createRequestsChart();
            const modal = document.getElementById('chart-modal');
            modal.style.display = 'block';
        }

        // Función para cerrar el modal
        function closeChartModal() {
            const modal = document.getElementById('chart-modal');
            modal.style.display = 'none';
        }

        // Función para actualizar el contador total
        function updateTotalCount(count) {
            const countElement = document.getElementById('total-count');
            if (count === 0) {
                countElement.textContent = "No hay solicitudes";
            } else {
                countElement.textContent = `${count} solicitud${count !== 1 ? 'es' : ''}`;
            }
        }

        // Función para rellenar la tabla con mejor formato
        function populateTable(data) {
            const table = document.getElementById('data-table');
            const thead = table.querySelector('thead tr');
            const tbody = table.querySelector('tbody');

            // Limpiar contenido existente
            thead.innerHTML = '';
            tbody.innerHTML = '';

            // Crear encabezados con formato mejorado
            if (headers.length > 0) {
                COLUMNS_TO_SHOW.forEach(index => {
                    if (headers[index]) {
                        const th = document.createElement('th');
                        th.textContent = headers[index];
                        thead.appendChild(th);
                    }
                });
            }

            // Crear filas de datos con mejor formato
            if (data.length === 0) {
                const tr = document.createElement('tr');
                const td = document.createElement('td');
                td.colSpan = COLUMNS_TO_SHOW.length;
                td.textContent = "No se encontraron solicitudes";
                td.style.textAlign = "center";
                td.style.padding = "2rem";
                td.style.color = "var(--text-light)";
                tr.appendChild(td);
                tbody.appendChild(tr);
            } else {
                data.forEach(row => {
                    const tr = document.createElement('tr');
                    
                    COLUMNS_TO_SHOW.forEach((colIndex, displayIndex) => {
                        const td = document.createElement('td');
                        let cellContent = row[colIndex] || '';
                        
                        // Formatear celda de estado
                        if (displayIndex === STATE_DISPLAY_INDEX) {
                            const estado = String(cellContent).trim().toLowerCase();
                            const badge = document.createElement('span');
                            
                            if (estado.includes('cerrado')) {
                                badge.className = 'status-badge status-closed';
                            } else if (estado.includes('abierto')) {
                                badge.className = 'status-badge status-open';
                            } else if (estado.includes('cancelado')) {
                                badge.className = 'status-badge status-cancelled';
                            } else {
                                badge.className = 'status-badge';
                                badge.style.backgroundColor = 'var(--gray-light)';
                                badge.style.color = 'var(--text-color)';
                            }
                            
                            badge.textContent = estado;
                            td.appendChild(badge);
                        } else {
                            // Formatear otras celdas
                            td.textContent = cellContent;
                            
                            // Resaltar números de solicitud
                            if (displayIndex === 0) {
                                td.style.fontWeight = "500";
                                td.style.color = "var(--primary-color)";
                            }
                        }
                        
                        tr.appendChild(td);
                    });
                    
                    tbody.appendChild(tr);
                });
            }

            // Actualizar contador
            updateTotalCount(data.length);
        }

        // Función de búsqueda mejorada
        function searchTable() {
            const searchValue = document.getElementById('search-bar').value.trim().toLowerCase();
            
            if (!searchValue) {
                populateTable(tableData);
                return;
            }
            
            const filteredData = tableData.filter(row => {
                // Buscar en múltiples campos
                return COLUMNS_TO_SHOW.some(index => {
                    const cellValue = row[index] ? String(row[index]).toLowerCase() : '';
                    return cellValue.includes(searchValue);
                });
            });

            populateTable(filteredData);
        }

        // Inicializar la aplicación
        document.addEventListener('DOMContentLoaded', () => {
            fetchCSVData();
            
            // Configurar eventos del gráfico
            document.getElementById('chart-button').addEventListener('click', showChartModal);
            document.querySelector('.close-modal').addEventListener('click', closeChartModal);
            
            // Cerrar modal al hacer clic fuera del contenido
            window.addEventListener('click', (event) => {
                const modal = document.getElementById('chart-modal');
                if (event.target === modal) {
                    closeChartModal();
                }
            });
            
            // Opcional: Actualizar datos cada 5 minutos
            // setInterval(fetchCSVData, 300000);
        });
    </script>
</body>
</html>
