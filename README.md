# Homies-Web-Cubing
Pàgina web de computación de resultados en cubos de Rubik 

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WCA Records & Sum of Ranks Platform</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            background: white;
            padding: 30px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        header h1 {
            color: #667eea;
            margin-bottom: 10px;
        }

        header p {
            color: #666;
        }

        .nav-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            background: white;
            border: 2px solid #667eea;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            color: #667eea;
            transition: all 0.3s;
        }

        .nav-btn.active {
            background: #667eea;
            color: white;
        }

        .nav-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .section {
            display: none;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .section.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: bold;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            font-family: inherit;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        button {
            padding: 12px 24px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        button:hover {
            background: #764ba2;
            transform: translateY(-2px);
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .card {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        .card h3 {
            color: #333;
            margin-bottom: 10px;
        }

        .card p {
            color: #666;
            font-size: 14px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        table th {
            background: #667eea;
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: bold;
        }

        table td {
            padding: 12px 15px;
            border-bottom: 1px solid #ddd;
        }

        table tr:hover {
            background: #f8f9fa;
        }

        .badge {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }

        .badge-gold {
            background: #ffd700;
            color: #333;
        }

        .badge-silver {
            background: #c0c0c0;
            color: #333;
        }

        .badge-bronze {
            background: #cd7f32;
            color: white;
        }

        .stats-box {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .stat-item {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
        }

        .stat-item .number {
            font-size: 32px;
            font-weight: bold;
        }

        .stat-item .label {
            font-size: 14px;
            opacity: 0.9;
        }

        .delete-btn {
            background: #dc3545;
            padding: 8px 12px;
            font-size: 12px;
        }

        .delete-btn:hover {
            background: #c82333;
        }

        .alert {
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
        }

        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .alert-info {
            background: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
        }

        .chart-container {
            position: relative;
            height: 400px;
            margin-top: 30px;
        }

        .two-column {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        @media (max-width: 768px) {
            .two-column {
                grid-template-columns: 1fr;
            }

            .nav-tabs {
                flex-direction: column;
            }

            .nav-btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🧩 WCA Records & Sum of Ranks Platform</h1>
            <p>Gestiona tus records, crea eventos personalizados y calcula tu SoR</p>
        </header>

        <div class="nav-tabs">
            <button class="nav-btn active" onclick="showSection('dashboard')">📊 Dashboard</button>
            <button class="nav-btn" onclick="showSection('records')">🏆 Mis Records</button>
            <button class="nav-btn" onclick="showSection('events')">🎯 Eventos</button>
            <button class="nav-btn" onclick="showSection('sor')">🎲 Sum of Ranks</button>
            <button class="nav-btn" onclick="showSection('stats')">📈 Estadísticas</button>
        </div>

        <!-- DASHBOARD -->
        <div id="dashboard" class="section active">
            <h2>Dashboard</h2>
            <div class="alert alert-info">
                <strong>Bienvenido!</strong> Esta plataforma te permite gestionar tus records de cubing, crear eventos personalizados y calcular tu Sum of Ranks.
            </div>

            <div class="stats-box">
                <div class="stat-item">
                    <div class="number" id="totalRecords">0</div>
                    <div class="label">Records Guardados</div>
                </div>
                <div class="stat-item">
                    <div class="number" id="totalEvents">0</div>
                    <div class="label">Eventos Creados</div>
                </div>
                <div class="stat-item">
                    <div class="number" id="avgTime">0.00</div>
                    <div class="label">Tiempo Promedio</div>
                </div>
                <div class="stat-item">
                    <div class="number" id="bestTime">--</div>
                    <div class="label">Mejor Tiempo</div>
                </div>
            </div>

            <div class="chart-container" style="height: 300px; margin-top: 40px;">
                <canvas id="dashboardChart"></canvas>
            </div>
        </div>

        <!-- MIS RECORDS -->
        <div id="records" class="section">
            <h2>Mis Records</h2>
            
            <div class="form-group" style="margin-bottom: 30px;">
                <h3>Agregar Nuevo Record</h3>
                <div class="grid" style="grid-template-columns: 1fr 1fr;">
                    <div class="form-group">
                        <label>Categoría</label>
                        <select id="categorySelect">
                            <option value="">-- Selecciona categoría --</option>
                            <option value="2x2">2x2</option>
                            <option value="3x3">3x3</option>
                            <option value="4x4">4x4</option>
                            <option value="5x5">5x5</option>
                            <option value="6x6">6x6</option>
                            <option value="7x7">7x7</option>
                            <option value="Skewb">Skewb</option>
                            <option value="Pyraminx">Pyraminx</option>
                            <option value="Megaminx">Megaminx</option>
                            <option value="Clock">Clock</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Tiempo (segundos)</label>
                        <input type="number" id="recordTime" placeholder="Ej: 45.32" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <label>Intento (1-5)</label>
                        <select id="attemptNumber">
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                            <option value="5">5</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>¿DNF (No Terminado)?</label>
                        <select id="isDNF">
                            <option value="false">No</option>
                            <option value="true">Sí</option>
                        </select>
                    </div>
                </div>
                <button onclick="addRecord()" style="width: 100%;">➕ Agregar Record</button>
            </div>

            <h3>Mis Records Guardados</h3>
            <div id="recordsList" class="grid"></div>
        </div>

        <!-- EVENTOS PERSONALIZADOS -->
        <div id="events" class="section">
            <h2>Eventos Personalizados</h2>

            <div class="form-group" style="margin-bottom: 30px;">
                <h3>Crear Nuevo Evento</h3>
                <div class="form-group">
                    <label>Nombre del Evento</label>
                    <input type="text" id="eventName" placeholder="Ej: Competencia Local 2026">
                </div>
                <div class="form-group">
                    <label>Descripción</label>
                    <textarea id="eventDesc" placeholder="Detalles del evento..." rows="3"></textarea>
                </div>
                <div class="form-group">
                    <label>Categorías (selecciona múltiples con Ctrl+Click)</label>
                    <select id="eventCategories" multiple size="5">
                        <option value="2x2">2x2</option>
                        <option value="3x3">3x3</option>
                        <option value="4x4">4x4</option>
                        <option value="5x5">5x5</option>
                        <option value="6x6">6x6</option>
                        <option value="7x7">7x7</option>
                        <option value="Skewb">Skewb</option>
                        <option value="Pyraminx">Pyraminx</option>
                    </select>
                </div>
                <button onclick="createEvent()" style="width: 100%;">🎯 Crear Evento</button>
            </div>

            <h3>Mis Eventos</h3>
            <div id="eventsList" class="grid"></div>
        </div>

        <!-- SUM OF RANKS -->
        <div id="sor" class="section">
            <h2>Sum of Ranks (SoR)</h2>
            
            <div class="alert alert-info">
                <strong>¿Qué es SoR?</strong> Es la suma de tus posiciones en diferentes categorías. Cuanto menor sea, mejor es tu ranking general.
            </div>

            <div class="form-group" style="margin-bottom: 30px;">
                <h3>Calcular SoR</h3>
                <p style="margin-bottom: 15px; color: #666;">Ingresa tu ranking en cada categoría para calcular tu Sum of Ranks</p>
                <div class="grid" style="grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));">
                    <div class="form-group">
                        <label>Ranking 3x3</label>
                        <input type="number" id="rank3x3" placeholder="Ej: 5" min="1">
                    </div>
                    <div class="form-group">
                        <label>Ranking 2x2</label>
                        <input type="number" id="rank2x2" placeholder="Ej: 12" min="1">
                    </div>
                    <div class="form-group">
                        <label>Ranking 4x4</label>
                        <input type="number" id="rank4x4" placeholder="Ej: 8" min="1">
                    </div>
                    <div class="form-group">
                        <label>Ranking 5x5</label>
                        <input type="number" id="rank5x5" placeholder="Ej: 15" min="1">
                    </div>
                    <div class="form-group">
                        <label>Ranking Skewb</label>
                        <input type="number" id="rankSkewb" placeholder="Ej: 10" min="1">
                    </div>
                    <div class="form-group">
                        <label>Ranking Pyraminx</label>
                        <input type="number" id="rankPyraminx" placeholder="Ej: 20" min="1">
                    </div>
                </div>
                <button onclick="calculateSoR()" style="width: 100%;">🎲 Calcular SoR</button>
            </div>

            <div id="sorResult" style="display: none; margin-top: 30px;">
                <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 30px; border-radius: 8px; text-align: center;">
                    <div style="font-size: 14px; opacity: 0.9; margin-bottom: 10px;">Tu Sum of Ranks</div>
                    <div style="font-size: 48px; font-weight: bold; margin-bottom: 20px;" id="sorValue">0</div>
                    <div id="sorBreakdown"></div>
                </div>
            </div>

            <div id="sorTable" style="margin-top: 30px; display: none;">
                <h3>Ranking Global por SoR</h3>
                <table>
                    <thead>
                        <tr>
                            <th>#</th>
                            <th>Usuario</th>
                            <th>Sum of Ranks</th>
                            <th>3x3</th>
                            <th>2x2</th>
                            <th>4x4</th>
                            <th>5x5</th>
                        </tr>
                    </thead>
                    <tbody id="sorTableBody">
                    </tbody>
                </table>
            </div>
        </div>

        <!-- ESTADÍSTICAS -->
        <div id="stats" class="section">
            <h2>Estadísticas</h2>

            <div class="two-column">
                <div>
                    <h3>Records por Categoría</h3>
                    <div class="chart-container">
                        <canvas id="categoryChart"></canvas>
                    </div>
                </div>
                <div>
                    <h3>Distribución de Tiempos</h3>
                    <div class="chart-container">
                        <canvas id="timeChart"></canvas>
                    </div>
                </div>
            </div>

            <div style="margin-top: 40px;">
                <h3>Resumen por Categoría</h3>
                <table>
                    <thead>
                        <tr>
                            <th>Categoría</th>
                            <th>Mejor Tiempo</th>
                            <th>Promedio</th>
                            <th>Total de Intentos</th>
                        </tr>
                    </thead>
                    <tbody id="statsTable">
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // ==================== DATA MANAGEMENT ====================
        let data = {
            records: JSON.parse(localStorage.getItem('wcaRecords')) || [],
            events: JSON.parse(localStorage.getItem('wcaEvents')) || [],
            users: JSON.parse(localStorage.getItem('wcaUsers')) || [],
            currentUser: localStorage.getItem('currentUser') || 'Usuario1'
        };

        function saveData() {
            localStorage.setItem('wcaRecords', JSON.stringify(data.records));
            localStorage.setItem('wcaEvents', JSON.stringify(data.events));
            localStorage.setItem('wcaUsers', JSON.stringify(data.users));
        }

        // ==================== NAVIGATION ====================
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(el => el.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
            
            document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
            event.target.classList.add('active');

            // Cargar datos cuando se cambia de sección
            if (sectionId === 'dashboard') updateDashboard();
            else if (sectionId === 'records') displayRecords();
            else if (sectionId === 'events') displayEvents();
            else if (sectionId === 'stats') updateStats();
        }

        // ==================== RECORDS ====================
        function addRecord() {
            const category = document.getElementById('categorySelect').value;
            const time = parseFloat(document.getElementById('recordTime').value);
            const attempt = document.getElementById('attemptNumber').value;
            const isDNF = document.getElementById('isDNF').value === 'true';

            if (!category || (isNaN(time) && !isDNF)) {
                alert('Por favor completa todos los campos');
                return;
            }

            const record = {
                id: Date.now(),
                category,
                time: isDNF ? null : time,
                attempt,
                isDNF,
                date: new Date().toLocaleDateString(),
                user: data.currentUser
            };

            data.records.push(record);
            saveData();
            
            // Limpiar formulario
            document.getElementById('categorySelect').value = '';
            document.getElementById('recordTime').value = '';
            document.getElementById('isDNF').value = 'false';

            alert('✅ Record agregado exitosamente');
            displayRecords();
            updateDashboard();
        }

        function displayRecords() {
            const userRecords = data.records.filter(r => r.user === data.currentUser);
            const recordsList = document.getElementById('recordsList');
            
            if (userRecords.length === 0) {
                recordsList.innerHTML = '<div class="card">No hay records guardados. ¡Agreg
