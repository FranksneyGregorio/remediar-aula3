<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>ReMediar - Demonstração</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f4f4f4;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }
    header {
      background: #4CAF50;
      color: #fff;
      text-align: center;
      padding: 10px 0;
    }
    .container {
      max-width: 800px;
      margin: 20px auto;
      background: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      flex: 1;
    }
    nav {
      text-align: center;
      margin-bottom: 20px;
    }
    nav button {
      margin: 5px;
      padding: 10px 15px;
      background-color: #4CAF50;
      border: none;
      color: white;
      cursor: pointer;
      border-radius: 3px;
    }
    nav button:hover {
      background-color: #45a049;
    }
    .screen {
      display: none;
    }
    .active {
      display: block;
    }
    .form-group {
      margin-bottom: 15px;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
    }
    .form-group input,
    .form-group select {
      width: 100%;
      padding: 8px;
      box-sizing: border-box;
    }
    .button {
      background-color: #4CAF50;
      border: none;
      color: #fff;
      padding: 10px 20px;
      cursor: pointer;
      border-radius: 3px;
    }
    .button:hover {
      background-color: #45a049;
    }
    .error {
      color: red;
      font-size: 0.8em;
      margin-top: 5px;
    }
    .form-group input:invalid {
      border: 1px solid red;
    }
    footer {
      background: #4CAF50;
      color: white;
      text-align: center;
      padding: 10px 0;
      margin-top: auto;
    }
  </style>
</head>
<body>
  <header>
    <h1>ReMediar</h1>
    <p>Agenda Online para Idosos</p>
  </header>
  <div class="container">
    <!-- Barra de navegação para simular as telas -->
    <nav>
      <button onclick="showScreen('login')">Login</button>
      <button onclick="showScreen('register')">Cadastro</button>
      <button onclick="showScreen('home')">Tela Inicial</button>
      <button onclick="showScreen('schedule')">Agendamento</button>
      <button onclick="showScreen('history')">Histórico</button>
    </nav>

    <!-- Tela de Login -->
    <div id="login" class="screen active">
      <h2>Login</h2>
      <div class="form-group">
        <label for="login-email">E-mail:</label>
        <input type="email" id="login-email" required placeholder="Digite seu e-mail">
        <div id="login-email-error" class="error"></div>
      </div>
      <div class="form-group">
        <label for="login-password">Senha:</label>
        <input type="password" id="login-password" required minlength="6" placeholder="Digite sua senha">
        <div id="login-password-error" class="error"></div>
      </div>
      <button class="button" onclick="login()">Entrar</button>
      <p><a href="#" onclick="showScreen('password-recovery')">Esqueci minha senha</a></p>
    </div>

    <!-- Tela de Cadastro -->
    <div id="register" class="screen">
      <h2>Cadastro</h2>
      <div class="form-group">
        <label for="register-name">Nome:</label>
        <input type="text" id="register-name" required placeholder="Digite seu nome">
        <div id="register-name-error" class="error"></div>
      </div>
      <div class="form-group">
        <label for="register-email">E-mail:</label>
        <input type="email" id="register-email" required placeholder="Digite seu e-mail">
        <div id="register-email-error" class="error"></div>
      </div>
      <div class="form-group">
        <label for="register-password">Senha:</label>
        <input type="password" id="register-password" required minlength="6" placeholder="Crie uma senha (mínimo 6 caracteres)">
        <div id="register-password-error" class="error"></div>
      </div>
      <button class="button" onclick="register()">Cadastrar</button>
    </div>

    <!-- Tela de Recuperação de Senha -->
    <div id="password-recovery" class="screen">
      <h2>Recuperação de Senha</h2>
      <div class="form-group">
        <label for="recovery-email">Informe seu e-mail:</label>
        <input type="email" id="recovery-email" required placeholder="Digite seu e-mail">
        <div id="recovery-email-error" class="error"></div>
      </div>
      <button class="button" onclick="recoverPassword()">Enviar Link</button>
      <p><a href="#" onclick="showScreen('login')">Voltar para Login</a></p>
    </div>

    <!-- Tela Inicial -->
    <div id="home" class="screen">
      <h2>Tela Inicial</h2>
      <p>Bem-vindo(a), <span id="username-display">usuário</span>!</p>
      <h3>Compromissos e Lembretes do Dia</h3>
      <ul id="today-list">
        <li>08:00 - Tomar Medicação A</li>
        <li>10:00 - Consulta Médica</li>
      </ul>
      <button class="button" onclick="simulateNotification()">Simular Notificação</button>
    </div>

    <!-- Tela de Agendamento -->
    <div id="schedule" class="screen">
      <h2>Agendar Compromisso / Lembrete</h2>
      <div class="form-group">
        <label for="event-type">Tipo:</label>
        <select id="event-type">
          <option value="medicamento">Lembrete de Medicamento</option>
          <option value="compromisso">Compromisso Médico</option>
        </select>
      </div>
      <div class="form-group">
        <label for="event-title">Título:</label>
        <input type="text" id="event-title" required placeholder="Ex: Consulta com Dr. Silva">
        <div id="event-title-error" class="error"></div>
      </div>
      <div class="form-group">
        <label for="event-date">Data:</label>
        <input type="date" id="event-date" required>
        <div id="event-date-error" class="error"></div>
      </div>
      <div class="form-group">
        <label for="event-time">Horário:</label>
        <input type="time" id="event-time" required>
        <div id="event-time-error" class="error"></div>
      </div>
      <button class="button" onclick="addEvent()">Adicionar Evento</button>
    </div>

    <!-- Tela de Histórico -->
    <div id="history" class="screen">
      <h2>Histórico</h2>
      <ul id="history-list">
        <li>05/04/2025 - Medicamento A - Tomado</li>
        <li>04/04/2025 - Consulta - Realizada</li>
      </ul>
    </div>
  </div>

  <footer>
    Versão ReMediar 3.0
  </footer>

  <script>
    // Armazenamento simples em memória
    const users = [];
    let currentUser = null;

    // Função para alternar entre as telas
    function showScreen(screenId) {
      const screens = document.getElementsByClassName('screen');
      for (let i = 0; i < screens.length; i++) {
        screens[i].classList.remove('active');
      }
      document.getElementById(screenId).classList.add('active');
    }

    // Função para limpar erros
    function clearErrors() {
      const errors = document.getElementsByClassName('error');
      for (let i = 0; i < errors.length; i++) {
        errors[i].textContent = '';
      }
    }

    // Validação de e-mail
    function validateEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(email);
    }

    // Simulação de hash de senha (em produção usar bcrypt.js)
    function hashPassword(password) {
      return 'hashed_' + password.split('').reverse().join('');
    }

    // Função de cadastro
    function register() {
      clearErrors();
      
      const name = document.getElementById('register-name').value;
      const email = document.getElementById('register-email').value;
      const password = document.getElementById('register-password').value;
      let isValid = true;

      // Validações
      if (!name) {
        document.getElementById('register-name-error').textContent = 'Nome é obrigatório';
        isValid = false;
      }

      if (!email) {
        document.getElementById('register-email-error').textContent = 'E-mail é obrigatório';
        isValid = false;
      } else if (!validateEmail(email)) {
        document.getElementById('register-email-error').textContent = 'E-mail inválido';
        isValid = false;
      }

      if (!password) {
        document.getElementById('register-password-error').textContent = 'Senha é obrigatória';
        isValid = false;
      } else if (password.length < 6) {
        document.getElementById('register-password-error').textContent = 'Senha deve ter no mínimo 6 caracteres';
        isValid = false;
      }

      if (!isValid) return;

      // Verifica se usuário já existe
      if (users.some(user => user.email === email)) {
        document.getElementById('register-email-error').textContent = 'E-mail já cadastrado';
        return;
      }

      // Adiciona usuário
      users.push({
        name,
        email,
        password: hashPassword(password)
      });

      alert('Cadastro realizado com sucesso!');
      showScreen('login');
    }

    // Função de login
    function login() {
      clearErrors();
      
      const email = document.getElementById('login-email').value;
      const password = document.getElementById('login-password').value;
      let isValid = true;

      // Validações
      if (!email) {
        document.getElementById('login-email-error').textContent = 'E-mail é obrigatório';
        isValid = false;
      }

      if (!password) {
        document.getElementById('login-password-error').textContent = 'Senha é obrigatória';
        isValid = false;
      }

      if (!isValid) return;

      // Verifica credenciais
      const user = users.find(user => user.email === email);
      
      if (!user) {
        document.getElementById('login-email-error').textContent = 'E-mail não cadastrado';
        return;
      }

      // Em produção, compararia com senha hasheada
      if (hashPassword(password) !== user.password) {
        document.getElementById('login-password-error').textContent = 'Senha incorreta';
        return;
      }

      currentUser = user;
      document.getElementById('username-display').textContent = user.name;
      alert('Login realizado com sucesso!');
      showScreen('home');
    }

    // Função de recuperação de senha
    function recoverPassword() {
      clearErrors();
      
      const email = document.getElementById('recovery-email').value;
      
      if (!email) {
        document.getElementById('recovery-email-error').textContent = 'E-mail é obrigatório';
        return;
      }

      if (!validateEmail(email)) {
        document.getElementById('recovery-email-error').textContent = 'E-mail inválido';
        return;
      }

      if (!users.some(user => user.email === email)) {
        document.getElementById('recovery-email-error').textContent = 'E-mail não cadastrado';
        return;
      }

      alert('Link de recuperação enviado para o seu e-mail.');
      showScreen('login');
    }

    // Adiciona um novo evento e atualiza a lista de hoje e o histórico
    function addEvent() {
      clearErrors();
      
      const type = document.getElementById('event-type').value;
      const title = document.getElementById('event-title').value;
      const date = document.getElementById('event-date').value;
      const time = document.getElementById('event-time').value;
      let isValid = true;

      // Validações
      if (!title) {
        document.getElementById('event-title-error').textContent = 'Título é obrigatório';
        isValid = false;
      }

      if (!date) {
        document.getElementById('event-date-error').textContent = 'Data é obrigatória';
        isValid = false;
      }

      if (!time) {
        document.getElementById('event-time-error').textContent = 'Horário é obrigatório';
        isValid = false;
      }

      if (!isValid) return;

      const listItem = document.createElement('li');
      listItem.textContent = `${date} ${time} - ${title} (${type === 'medicamento' ? 'Lembrete' : 'Compromisso'})`;

      // Adiciona na lista de compromissos do dia e ao histórico
      document.getElementById('today-list').appendChild(listItem);
      document.getElementById('history-list').appendChild(listItem.cloneNode(true));
      alert('Evento adicionado com sucesso!');

      // Limpa os campos
      document.getElementById('event-title').value = '';
      document.getElementById('event-date').value = '';
      document.getElementById('event-time').value = '';
    }

    // Simulação de notificação
    function simulateNotification() {
      alert('Notificação: Lembre-se de tomar seu medicamento!');
    }
  </script>
</body>
</html>
