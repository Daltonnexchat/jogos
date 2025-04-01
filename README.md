<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Confirmação de Presença e Pagamento</title>
    <style>
        :root {
            --primary: #3498db;
            --secondary: #2ecc71;
            --danger: #e74c3c;
            --dark: #34495e;
            --light: #ecf0f1;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f6fa;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        
        .header {
            background-color: var(--primary);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .menu {
            display: flex;
        }
        
        .menu-item {
            margin-left: 1.5rem;
            cursor: pointer;
        }
        
        .menu-item:hover {
            text-decoration: underline;
        }
        
        .content {
            padding: 2rem 0;
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 1.5rem;
            margin-bottom: 1.5rem;
        }
        
        .card-title {
            color: var(--dark);
            font-size: 1.25rem;
            margin-bottom: 1rem;
            font-weight: bold;
        }
        
        .form-group {
            margin-bottom: 1rem;
        }
        
        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--dark);
        }
        
        .form-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }
        
        .form-input:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .btn {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 500;
            transition: background-color 0.3s ease;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
        }
        
        .btn-success {
            background-color: var(--secondary);
            color: white;
        }
        
        .btn-success:hover {
            background-color: #27ae60;
        }
        
        .btn-danger {
            background-color: var(--danger);
            color: white;
        }
        
        .btn-danger:hover {
            background-color: #c0392b;
        }
        
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
        }
        
        .table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .table th,
        .table td {
            padding: 0.75rem;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        
        .table th {
            background-color: #f8f9fa;
            color: var(--dark);
        }
        
        .table tr:hover {
            background-color: #f8f9fa;
        }
        
        .badge {
            padding: 0.25rem 0.5rem;
            border-radius: 4px;
            font-size: 0.75rem;
            color: white;
        }
        
        .badge-success {
            background-color: var(--secondary);
        }
        
        .badge-danger {
            background-color: var(--danger);
        }
        
        .badge-primary {
            background-color: var(--primary);
        }
        
        .tabs {
            display: flex;
            margin-bottom: 1.5rem;
            border-bottom: 1px solid #ddd;
        }
        
        .tab {
            padding: 0.75rem 1.5rem;
            cursor: pointer;
            border-bottom: 2px solid transparent;
        }
        
        .tab.active {
            border-bottom: 2px solid var(--primary);
            color: var(--primary);
            font-weight: 500;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        @media (max-width: 768px) {
            .grid {
                grid-template-columns: 1fr;
            }
            
            .menu {
                display: none;
            }
        }

        .login-container {
            max-width: 400px;
            margin: 4rem auto;
        }

        .game-card {
            display: flex;
            flex-direction: column;
            height: 100%;
        }

        .game-card-header {
            background-color: #f8f9fa;
            padding: 1rem;
            border-radius: 8px 8px 0 0;
        }

        .game-card-body {
            padding: 1rem;
            flex-grow: 1;
        }

        .game-card-footer {
            padding: 1rem;
            border-top: 1px solid #ddd;
            display: flex;
            justify-content: space-between;
        }

        .payment-status {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            background-color: #f8f9fa;
            border-radius: 4px;
            margin-bottom: 1rem;
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="login-page">
        <div class="container login-container">
            <div class="card">
                <div class="card-title" style="text-align: center;">Login</div>
                <form id="login-form">
                    <div class="form-group">
                        <label class="form-label">E-mail</label>
                        <input type="email" class="form-input" placeholder="Seu e-mail" required>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Senha</label>
                        <input type="password" class="form-input" placeholder="Sua senha" required>
                    </div>
                    <div class="form-group" style="text-align: center;">
                        <button type="button" class="btn btn-primary" onclick="showMainPage()">Entrar</button>
                    </div>
                    <div style="text-align: center; margin-top: 1rem;">
                        <a href="#" onclick="showRegisterPage()">Criar nova conta</a>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Register Page -->
    <div id="register-page" style="display: none;">
        <div class="container login-container">
            <div class="card">
                <div class="card-title" style="text-align: center;">Criar Conta</div>
                <form id="register-form">
                    <div class="form-group">
                        <label class="form-label">Nome Completo</label>
                        <input type="text" class="form-input" placeholder="Seu nome completo" required>
                    </div>
                    <div class="form-group">
                        <label class="form-label">E-mail</label>
                        <input type="email" class="form-input" placeholder="Seu e-mail" required>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Telefone</label>
                        <input type="tel" class="form-input" placeholder="Seu telefone" required>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Senha</label>
                        <input type="password" class="form-input" placeholder="Sua senha" required>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Confirmar Senha</label>
                        <input type="password" class="form-input" placeholder="Confirme sua senha" required>
                    </div>
                    <div class="form-group" style="text-align: center;">
                        <button type="button" class="btn btn-primary" onclick="showMainPage()">Registrar</button>
                    </div>
                    <div style="text-align: center; margin-top: 1rem;">
                        <a href="#" onclick="showLoginPage()">Já tem uma conta? Faça login</a>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Main Application -->
    <div id="main-page" style="display: none;">
        <!-- Header -->
        <header class="header">
            <div class="container">
                <nav class="nav">
                    <div class="logo">Sistema de Jogos</div>
                    <div class="menu">
                        <div class="menu-item" onclick="showTab('games')">Jogos</div>
                        <div class="menu-item" onclick="showTab('payments')">Mensalidades</div>
                        <div class="menu-item" onclick="showTab('profile')">Perfil</div>
                        <div class="menu-item" onclick="showLoginPage()">Sair</div>
                    </div>
                </nav>
            </div>
        </header>

        <!-- Content -->
        <div class="content">
            <div class="container">
                <!-- Tabs -->
                <div class="tabs">
                    <div class="tab active" onclick="showTab('games')">Jogos</div>
                    <div class="tab" onclick="showTab('payments')">Mensalidades</div>
                    <div class="tab" onclick="showTab('profile')">Perfil</div>
                </div>

                <!-- Games Tab -->
                <div id="games-tab" class="tab-content active">
                    <div class="card">
                        <div class="card-title">Próximos Jogos</div>
                        <div class="grid">
                            <!-- Game 1 -->
                            <div class="card game-card">
                                <div class="game-card-header">
                                    <h3>Futebol Society</h3>
                                    <small>Organizado por João Silva</small>
                                </div>
                                <div class="game-card-body">
                                    <p><strong>Data:</strong> 05/04/2025</p>
                                    <p><strong>Horário:</strong> 19:00 - 21:00</p>
                                    <p><strong>Local:</strong> Quadra Central</p>
                                    <p><strong>Vagas:</strong> 12/20</p>
                                </div>
                                <div class="game-card-footer">
                                    <span class="badge badge-primary">R$ 25,00</span>
                                    <button class="btn btn-success">Confirmar Presença</button>
                                </div>
                            </div>

                            <!-- Game 2 -->
                            <div class="card game-card">
                                <div class="game-card-header">
                                    <h3>Vôlei de Praia</h3>
                                    <small>Organizado por Maria Oliveira</small>
                                </div>
                                <div class="game-card-body">
                                    <p><strong>Data:</strong> 07/04/2025</p>
                                    <p><strong>Horário:</strong> 16:00 - 18:00</p>
                                    <p><strong>Local:</strong> Praia Central</p>
                                    <p><strong>Vagas:</strong> 8/12</p>
                                </div>
                                <div class="game-card-footer">
                                    <span class="badge badge-primary">R$ 15,00</span>
                                    <button class="btn btn-success">Confirmar Presença</button>
                                </div>
                            </div>

                            <!-- Game 3 -->
                            <div class="card game-card">
                                <div class="game-card-header">
                                    <h3>Basquete 3x3</h3>
                                    <small>Organizado por Carlos Mendes</small>
                                </div>
                                <div class="game-card-body">
                                    <p><strong>Data:</strong> 10/04/2025</p>
                                    <p><strong>Horário:</strong> 20:00 - 22:00</p>
                                    <p><strong>Local:</strong> Ginásio Municipal</p>
                                    <p><strong>Vagas:</strong> 9/12</p>
                                </div>
                                <div class="game-card-footer">
                                    <span class="badge badge-primary">R$ 20,00</span>
                                    <button class="btn btn-success">Confirmar Presença</button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="card">
                        <div class="card-title">Meus Jogos Confirmados</div>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Jogo</th>
                                    <th>Data</th>
                                    <th>Horário</th>
                                    <th>Local</th>
                                    <th>Status</th>
                                    <th>Ação</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Tênis de Mesa</td>
                                    <td>03/04/2025</td>
                                    <td>18:00 - 20:00</td>
                                    <td>Clube Esportivo</td>
                                    <td><span class="badge badge-success">Confirmado</span></td>
                                    <td><button class="btn btn-danger">Cancelar</button></td>
                                </tr>
                                <tr>
                                    <td>Natação</td>
                                    <td>08/04/2025</td>
                                    <td>07:00 - 08:00</td>
                                    <td>Piscina Olímpica</td>
                                    <td><span class="badge badge-success">Confirmado</span></td>
                                    <td><button class="btn btn-danger">Cancelar</button></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Payments Tab -->
                <div id="payments-tab" class="tab-content">
                    <div class="card">
                        <div class="card-title">Status da Mensalidade</div>
                        <div class="payment-status">
                            <div>
                                <h3>Abril 2025</h3>
                                <p>Vencimento: 10/04/2025</p>
                            </div>
                            <div>
                                <span class="badge badge-danger">Pendente</span>
                                <h3>R$ 120,00</h3>
                            </div>
                        </div>
                        <button class="btn btn-primary">Pagar Mensalidade</button>
                    </div>

                    <div class="card">
                        <div class="card-title">Histórico de Pagamentos</div>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Referência</th>
                                    <th>Valor</th>
                                    <th>Data de Pagamento</th>
                                    <th>Status</th>
                                    <th>Comprovante</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Março 2025</td>
                                    <td>R$ 120,00</td>
                                    <td>05/03/2025</td>
                                    <td><span class="badge badge-success">Pago</span></td>
                                    <td><button class="btn btn-primary">Visualizar</button></td>
                                </tr>
                                <tr>
                                    <td>Fevereiro 2025</td>
                                    <td>R$ 120,00</td>
                                    <td>08/02/2025</td>
                                    <td><span class="badge badge-success">Pago</span></td>
                                    <td><button class="btn btn-primary">Visualizar</button></td>
                                </tr>
                                <tr>
                                    <td>Janeiro 2025</td>
                                    <td>R$ 120,00</td>
                                    <td>10/01/2025</td>
                                    <td><span class="badge badge-success">Pago</span></td>
                                    <td><button class="btn btn-primary">Visualizar</button></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Profile Tab -->
                <div id="profile-tab" class="tab-content">
                    <div class="card">
                        <div class="card-title">Meu Perfil</div>
                        <form>
                            <div class="form-group">
                                <label class="form-label">Nome Completo</label>
                                <input type="text" class="form-input" value="Pedro Santos" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">E-mail</label>
                                <input type="email" class="form-input" value="pedro.santos@email.com" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">Telefone</label>
                                <input type="tel" class="form-input" value="(11) 98765-4321" required>
                            </div>
                            <div class="form-group">
                                <label class="form-label">Endereço</label>
                                <input type="text" class="form-input" value="Rua das Flores, 123">
                            </div>
                            <div class="form-group">
                                <label class="form-label">Nova Senha (deixe em branco para manter a atual)</label>
                                <input type="password" class="form-input">
                            </div>
                            <div class="form-group">
                                <label class="form-label">Confirmar Nova Senha</label>
                                <input type="password" class="form-input">
                            </div>
                            <div class="form-group">
                                <button type="button" class="btn btn-primary">Salvar Alterações</button>
                            </div>
                        </form>
                    </div>

                    <div class="card">
                        <div class="card-title">Preferências de Notificação</div>
                        <form>
                            <div class="form-group">
                                <label class="form-label">
                                    <input type="checkbox" checked> Receber notificações por e-mail
                                </label>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <input type="checkbox" checked> Receber notificações por SMS
                                </label>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <input type="checkbox" checked> Lembrete de jogos (24h antes)
                                </label>
                            </div>
                            <div class="form-group">
                                <label class="form-label">
                                    <input type="checkbox" checked> Lembrete de pagamento de mensalidade
                                </label>
                            </div>
                            <div class="form-group">
                                <button type="button" class="btn btn-primary">Salvar Preferências</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Function to show/hide pages
        function showLoginPage() {
            document.getElementById('login-page').style.display = 'block';
            document.getElementById('register-page').style.display = 'none';
            document.getElementById('main-page').style.display = 'none';
        }

        function showRegisterPage() {
            document.getElementById('login-page').style.display = 'none';
            document.getElementById('register-page').style.display = 'block';
            document.getElementById('main-page').style.display = 'none';
        }

        function showMainPage() {
            document.getElementById('login-page').style.display = 'none';
            document.getElementById('register-page').style.display = 'none';
            document.getElementById('main-page').style.display = 'block';
        }

        // Function to handle tab switching
        function showTab(tabName) {
            // Hide all tab contents
            const tabContents = document.querySelectorAll('.tab-content');
            tabContents.forEach(tab => {
                tab.classList.remove('active');
            });

            // Show selected tab content
            document.getElementById(`${tabName}-tab`).classList.add('active');

            // Update tab highlighting
            const tabs = document.querySelectorAll('.tab');
            tabs.forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Find the tab with the matching onclick attribute and make it active
            tabs.forEach(tab => {
                if (tab.getAttribute('onclick').includes(tabName)) {
                    tab.classList.add('active');
                }
            });
        }
    </script>
</body>
</html>
