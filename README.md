# meu diário-secreto
aqui está um diario para voce desabafar sempre que precisar 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meu Diário Secreto</title>
    <style>
        /* Variáveis de Temas (Customização de Cores) */
        :root {
            --bg-color: #f4f4f9;
            --card-bg: #ffffff;
            --text-color: #333333;
            --primary-color: #6c5ce7;
            --danger-color: #ff7675;
            --border-color: #dddddd;
            --font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        [data-theme="dark"] {
            --bg-color: #1e1e24;
            --card-bg: #2a2a32;
            --text-color: #f5f5f5;
            --primary-color: #a29bfe;
            --danger-color: #ff7675;
            --border-color: #444444;
        }

        [data-theme="romantic"] {
            --bg-color: #fdf6ec;
            --card-bg: #fffbf5;
            --text-color: #5c4033;
            --primary-color: #d4a373;
            --danger-color: #e07a5f;
            --border-color: #e9d8a6;
        }

        /* Classes de Fontes */
        .font-modern { font-family: 'Segoe UI', Helvetica, Arial, sans-serif; }
        .font-elegant { font-family: 'Georgia', Cambria, Times, serif; }
        .font-typewriter { font-family: 'Courier New', Courier, monospace; font-weight: bold; }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: background 0.3s, color 0.3s;
        }

        .container {
            width: 100%;
            max-width: 800px;
            background: var(--card-bg);
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: background 0.3s;
        }

        /* Painel de Customização Visual */
        .customizer-panel {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            background: var(--card-bg);
            padding: 12px 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            width: 100%;
            max-width: 800px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            align-items: center;
            font-size: 14px;
            border: 1px solid var(--border-color);
        }

        .customizer-group {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .customizer-panel select {
            padding: 6px 10px;
            border-radius: 4px;
            border: 1px solid var(--border-color);
            background: var(--bg-color);
            color: var(--text-color);
            cursor: pointer;
            font-family: inherit;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }

        h1 { margin: 0; font-size: 24px; color: var(--primary-color); }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
            font-family: inherit;
        }

        button:hover { filter: brightness(0.9); }
        button.danger { background-color: var(--danger-color); }

        .auth-screen {
            text-align: center;
            padding: 40px 20px;
        }

        .auth-screen input {
            padding: 12px;
            width: 200px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            margin-right: 10px;
            font-size: 16px;
            background: var(--bg-color);
            color: var(--text-color);
        }

        .diary-section { display: none; }

        .entry-form {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 30px;
        }

        .entry-form input, .entry-form textarea {
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            font-size: 16px;
            background: var(--bg-color);
            color: var(--text-color);
            font-family: inherit;
        }

        .entry-form textarea { resize: vertical; height: 120px; }

        .entries-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .entry-card {
            background: var(--bg-color);
            padding: 20px;
            border-radius: 8px;
            position: relative;
            border: 1px solid var(--border-color);
        }

        .entry-card h3 { margin: 0 0 10px 0; color: var(--primary-color); }
        .entry-card .date { font-size: 12px; opacity: 0.7; margin-bottom: 10px; }
        .entry-card p { margin: 0; white-space: pre-wrap; line-height: 1.5; }
        
        .delete-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            color: var(--danger-color);
            border: none;
            padding: 5px;
            cursor: pointer;
            font-size: 14px;
        }
    </style>
</head>
<body class="font-modern" id="mainBody">

<!-- Barra de Customização Visual -->
<div class="customizer-panel">
    <div class="customizer-group">
        <label for="themeSelect">🎨 Tema:</label>
        <select id="themeSelect" onchange="changeTheme(this.value)">
            <option value="light">Claro Padrão</option>
            <option value="dark">Modo Escuro</option>
            <option value="romantic">Vintage Romântico</option>
        </select>
    </div>
    <div class="customizer-group">
        <label for="fontSelect">✍️ Fonte:</label>
        <select id="fontSelect" onchange="changeFont(this.value)">
            <option value="font-modern">Moderna Sans</option>
            <option value="font-elegant">Clássica Serifada</option>
            <option value="font-typewriter">Máquina de Escrever</option>
        </select>
    </div>
</div>

<div class="container">
    <!-- Tela de Autenticação -->
    <div id="authScreen" class="auth-screen">
        <h2 id="authTitle">Defina uma senha para o seu Diário</h2>
        <p style="opacity: 0.7; font-size: 14px; margin-bottom: 20px;">
            Seus dados e preferências são salvos localmente de forma privada.
        </p>
        <input type="password" id="passwordInput" placeholder="Digite a senha...">
        <button id="authBtn" onclick="handleAuth()">Confirmar</button>
    </div>

    <!-- Seção Principal do Diário -->
    <div id="diarySection" class="diary-section">
        <header>
            <h1>🔒 Meu Diário Secreto</h1>
            <button class="danger" onclick="lockDiary()">Bloquear Diário</button>
        </header>

        <!-- Formulário para nova entrada -->
        <div class="entry-form">
            <input type="text" id="entryTitle" placeholder="Título do segredo ou do dia...">
            <textarea id="entryContent" placeholder="Escreva o seu segredo aqui..."></textarea>
            <button onclick="saveEntry()">Salvar no Diário</button>
        </div>

        <!-- Lista de memórias salvas -->
        <h2>Minhas Notas Anteriores</h2>
        <div id="entriesList" class="entries-list"></div>
    </div>
</div>

<script>
    let isAuthenticated = false;

    // Funções de Customização Visual
    function changeTheme(themeName) {
        if (themeName === 'light') {
            document.documentElement.removeAttribute('data-theme');
        } else {
            document.documentElement.setAttribute('data-theme', themeName);
        }
        localStorage.setItem('diary_theme', themeName);
    }

    function changeFont(fontClassName) {
        const body = document.getElementById('mainBody');
        body.className = ''; // Limpa classes anteriores
        body.classList.add(fontClassName);
        localStorage.setItem('diary_font', fontClassName);
    }

    // Carrega as preferências visuais salvas pelo usuário
    function loadSavedPreferences() {
        const savedTheme = localStorage.getItem('diary_theme') || 'light';
        const savedFont = localStorage.getItem('diary_font') || 'font-modern';
        
        document.getElementById('themeSelect').value = savedTheme;
        document.getElementById('fontSelect').value = savedFont;
        
        changeTheme(savedTheme);
        changeFont(savedFont);
    }

    function checkExistingPassword() {
        const hasPassword = localStorage.getItem('diary_hash');
        const authTitle = document.getElementById('authTitle');
        if (hasPassword) {
            authTitle.innerText = "Digite sua senha para desbloquear";
        } else {
            authTitle.innerText = "Crie uma senha para o seu Diário";
        }
    }

    function handleAuth() {
        const password = document.getElementById('passwordInput').value;
        if (!password) {
            alert('Por favor, insira uma senha válida.');
            return;
        }

        const savedHash = localStorage.getItem('diary_hash');

        if (!savedHash) {
            localStorage.setItem('diary_hash', btoa(password));
            alert('Senha criada com sucesso! Não a esqueça.');
            proceedToDiary();
        } else {
            if (btoa(password) === savedHash) {
                proceedToDiary();
            } else {
                alert('Senha incorreta! Tente novamente.');
            }
        }
        document.getElementById('passwordInput').value = '';
    }

    function proceedToDiary() {
        isAuthenticated = true;
