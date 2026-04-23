<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ventas al Extremo - Tracker</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Urbanist:wght@400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --primary: #deff9a;
            --secondary: #f97316;
            --text-main: #f8fafc;
            --accent: #38bdf8;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            font-family: 'Urbanist', sans-serif;
            margin: 0;
            display: flex;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }

        .app-container {
            width: 100%;
            max-width: 500px;
            background: var(--card-bg);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            border: 1px solid rgba(222, 255, 154, 0.1);
            position: relative;
            overflow: hidden;
        }

        /* --- SETUP SCREEN --- */
        #setup-screen {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 20px;
        }

        .header h1 {
            font-size: 32px;
            color: var(--primary);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin: 0;
        }

        .input-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        label { font-weight: 600; color: #94a3b8; }

        input {
            background: #0f172a;
            border: 1px solid #334155;
            padding: 15px;
            border-radius: 12px;
            color: white;
            font-size: 18px;
            font-family: inherit;
        }

        input:focus {
            outline: none;
            border-color: var(--primary);
        }

        .btn-start {
            background: var(--primary);
            color: black;
            border: none;
            padding: 18px;
            border-radius: 12px;
            font-weight: 800;
            font-size: 18px;
            cursor: pointer;
            margin-top: 10px;
            transition: transform 0.2s;
        }

        .btn-start:active { transform: scale(0.95); }

        /* --- DASHBOARD SCREEN --- */
        #dashboard { display: none; }

        .profile-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .welcome-text h2 { margin: 0; font-size: 24px; }
        .welcome-text p { margin: 0; color: var(--accent); font-weight: 600; }

        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: #0f172a;
            padding: 20px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid rgba(255,255,255,0.05);
        }

        .stat-value {
            font-size: 40px;
            font-weight: 800;
            display: block;
            margin: 10px 0;
        }

        .stat-label { color: #94a3b8; font-size: 14px; text-transform: uppercase; }

        .progress-container {
            margin-bottom: 30px;
        }

        .progress-bar-bg {
            height: 12px;
            background: #334155;
            border-radius: 10px;
            margin-top: 10px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), #22c55e);
            width: 0%;
            transition: width 0.5s ease-out;
        }

        .action-buttons {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .counter-btn {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #334155;
            padding: 20px;
            border-radius: 16px;
            cursor: pointer;
            transition: background 0.3s;
            border: none;
            color: white;
            font-family: inherit;
        }

        .counter-btn:hover { background: #475569; }
        .counter-btn i { font-size: 24px; color: var(--primary); }
        .counter-btn span { font-weight: 700; font-size: 18px; }

        .btn-reset {
            background: none;
            border: 1px solid #ef4444;
            color: #ef4444;
            padding: 10px;
            border-radius: 8px;
            margin-top: 20px;
            cursor: pointer;
            width: 100%;
        }

        .daily-quote {
            text-align: center;
            font-style: italic;
            color: #94a3b8;
            margin-top: 30px;
            font-size: 14px;
        }

        /* --- ANIMATIONS --- */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .goal-reached {
            animation: pulse 0.5s infinite;
            box-shadow: 0 0 20px var(--primary);
        }
    </style>
</head>
<body>

    <div class="app-container">
        
        <!-- SETUP SCREEN -->
        <div id="setup-screen">
            <div class="header">
                <i class="fa-solid fa-rocket" style="font-size: 40px; color: var(--primary); margin-bottom: 10px;"></i>
                <h1>Bootcamp V2</h1>
                <p>Configura tu meta de Clase Mundial</p>
            </div>
            
            <div class="input-group">
                <label>Nombre del Asesor</label>
                <input type="text" id="user-name" placeholder="Ej. Juan Pérez">
            </div>

            <div class="input-group">
                <label>Meta Diaria de Informes</label>
                <input type="number" id="goal-informes" placeholder="Ej. 10">
            </div>

            <div class="input-group">
                <label>Meta Diaria de Registros</label>
                <input type="number" id="goal-registros" placeholder="Ej. 2">
            </div>

            <button class="btn-start" onclick="startApp()">¡EMPEZAR EL JUEGO!</button>
        </div>

        <!-- DASHBOARD SCREEN -->
        <div id="dashboard">
            <div class="profile-bar">
                <div class="welcome-text">
                    <p id="date-text">Hoy es un buen día</p>
                    <h2 id="display-name">Asesor Elite</h2>
                </div>
                <i class="fa-solid fa-crown" style="color: var(--primary); font-size: 24px;"></i>
            </div>

            <div class="stats-grid">
                <div class="stat-card" id="card-informes">
                    <span class="stat-label">Informes</span>
                    <span class="stat-value" id="val-informes">0</span>
                    <span class="stat-label" id="label-goal-inf">Meta: 0</span>
                </div>
                <div class="stat-card" id="card-registros">
                    <span class="stat-label">Registros</span>
                    <span class="stat-value" id="val-registros">0</span>
                    <span class="stat-label" id="label-goal-reg">Meta: 0</span>
                </div>
            </div>

            <div class="progress-container">
                <div style="display: flex; justify-content: space-between;">
                    <span style="font-weight: 600;">Progreso Total</span>
                    <span id="percent-text" style="color: var(--primary);">0%</span>
                </div>
                <div class="progress-bar-bg">
                    <div class="progress-fill" id="progress-fill"></div>
                </div>
            </div>

            <div class="action-buttons">
                <button class="counter-btn" onclick="updateStat('informes')">
                    <span>+1 Informe</span>
                    <i class="fa-solid fa-phone-volume"></i>
                </button>
                <button class="counter-btn" onclick="updateStat('registros')">
                    <span>+1 Registro</span>
                    <i class="fa-solid fa-user-plus" style="color: var(--accent);"></i>
                </button>
            </div>

            <div class="daily-quote" id="dynamic-quote">
                "Hambre por vender, pero sin enseñarla."
            </div>

            <button class="btn-reset" onclick="resetApp()">Cambiar Metas / Reiniciar</button>
        </div>

    </div>

    <script>
        let userData = {
            name: "",
            goalInformes: 0,
            goalRegistros: 0,
            currInformes: 0,
            currRegistros: 0
        };

        const quotes = [
            "Hambre por vender, pero sin enseñarla.",
            "El 80% del éxito es aparecer.",
            "Lo que no se mide, no mejora.",
            "¡Eres un profesional de Clase Mundial!",
            "Cada informe te acerca a tu sueño.",
            "Vender es un acto de amor."
        ];

        function startApp() {
            const name = document.getElementById('user-name').value;
            const gInf = parseInt(document.getElementById('goal-informes').value);
            const gReg = parseInt(document.getElementById('goal-registros').value);

            if(!name || !gInf || !gReg) {
                alert("Por favor llena todos los campos para iniciar tu entrenamiento.");
                return;
            }

            userData = { name, goalInformes: gInf, goalRegistros: gReg, currInformes: 0, currRegistros: 0 };
            
            document.getElementById('display-name').innerText = userData.name;
            document.getElementById('label-goal-inf').innerText = `Meta: ${userData.goalInformes}`;
            document.getElementById('label-goal-reg').innerText = `Meta: ${userData.goalRegistros}`;
            
            document.getElementById('setup-screen').style.display = 'none';
            document.getElementById('dashboard').style.display = 'block';
            
            updateUI();
        }

        function updateStat(type) {
            if(type === 'informes') userData.currInformes++;
            if(type === 'registros') userData.currRegistros++;
            
            updateUI();
            checkGoals();
        }

        function updateUI() {
            document.getElementById('val-informes').innerText = userData.currInformes;
            document.getElementById('val-registros').innerText = userData.currRegistros;

            // Progreso
            const totalPoints = (userData.currInformes * 1) + (userData.currRegistros * 5);
            const totalGoal = (userData.goalInformes * 1) + (userData.goalRegistros * 5);
            const percent = Math.min(Math.round((totalPoints / totalGoal) * 100), 100);

            document.getElementById('percent-text').innerText = `${percent}%`;
            document.getElementById('progress-fill').style.width = `${percent}%`;

            // Cambiar frase aleatoria
            if(userData.currInformes % 3 === 0) {
                const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
                document.getElementById('dynamic-quote').innerText = `"${randomQuote}"`;
            }
        }

        function checkGoals() {
            if(userData.currInformes >= userData.goalInformes) {
                document.getElementById('card-informes').classList.add('goal-reached');
            }
            if(userData.currRegistros >= userData.goalRegistros) {
                document.getElementById('card-registros').classList.add('goal-reached');
            }
        }

        function resetApp() {
            if(confirm("¿Quieres reiniciar tus metas del día?")) {
                document.getElementById('setup-screen').style.display = 'flex';
                document.getElementById('dashboard').style.display = 'none';
                document.getElementById('card-informes').classList.remove('goal-reached');
                document.getElementById('card-registros').classList.remove('goal-reached');
            }
        }

        // Set date
        const options = { weekday: 'long', month: 'long', day: 'numeric' };
        document.getElementById('date-text').innerText = new Date().toLocaleDateString('es-ES', options);
    </script>
</body>
</html>
