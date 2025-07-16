<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Control de Finanzas Personal - CLP</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --success: #27ae60;
            --danger: #e74c3c;
            --light: #ecf0f1;
            --dark: #34495e;
            --gray: #95a5a6;
            --white: #ffffff;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            --header-gradient: linear-gradient(135deg, #0052D4 0%, #4364F7 50%, #6FB1FC 100%);
            --card-gradient: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #e4e8f0 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--dark);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            margin-bottom: 30px;
            background: var(--header-gradient);
            border-radius: 12px;
            color: white;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
            position: relative;
            overflow: hidden;
        }
        
        header::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="none"><polygon points="0,0 100,0 100,100" fill="rgba(255,255,255,0.1)"/></svg>');
            background-size: cover;
        }
        
        header h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            font-weight: 700;
            position: relative;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        header p {
            font-size: 1.2rem;
            max-width: 600px;
            margin: 0 auto;
            position: relative;
            opacity: 0.9;
        }
        
        .chile-flag {
            display: inline-flex;
            margin: 0 10px;
        }
        
        .chile-flag span {
            display: inline-block;
            width: 12px;
            height: 24px;
            margin: 0 1px;
        }
        
        .chile-flag .red {
            background: #D52B1E;
        }
        
        .chile-flag .white {
            background: #FFFFFF;
        }
        
        .chile-flag .blue {
            background: #0033A0;
        }
        
        .app-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 768px) {
            .app-container {
                grid-template-columns: 1fr;
            }
        }
        
        .card {
            background: var(--card-gradient);
            border-radius: 16px;
            box-shadow: var(--shadow);
            padding: 30px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        
        .card-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 15px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f0f0;
        }
        
        .card-title i {
            color: var(--secondary);
            background: rgba(52, 152, 219, 0.1);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }
        
        .form-group {
            margin-bottom: 22px;
        }
        
        label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--dark);
            font-size: 1.05rem;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 14px 18px;
            border: 1px solid #d1d9e6;
            border-radius: 10px;
            font-size: 1.05rem;
            transition: all 0.3s;
            background: #fdfdfd;
            box-shadow: inset 2px 2px 5px #f0f0f0, inset -2px -2px 5px #ffffff;
        }
        
        input:focus, select:focus, textarea:focus {
            border-color: var(--secondary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            padding: 15px 28px;
            background: var(--secondary);
            color: var(--white);
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(52, 152, 219, 0.3);
        }
        
        .btn:hover {
            background: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(52, 152, 219, 0.4);
        }
        
        .btn:active {
            transform: translateY(1px);
            box-shadow: 0 2px 4px rgba(52, 152, 219, 0.3);
        }
        
        .btn-block {
            display: flex;
            width: 100%;
        }
        
        .btn-success {
            background: var(--success);
            box-shadow: 0 4px 8px rgba(39, 174, 96, 0.3);
        }
        
        .btn-success:hover {
            background: #219653;
            box-shadow: 0 6px 12px rgba(39, 174, 96, 0.4);
        }
        
        .btn-danger {
            background: var(--danger);
            box-shadow: 0 4px 8px rgba(231, 76, 60, 0.3);
        }
        
        .btn-danger:hover {
            background: #c0392b;
            box-shadow: 0 6px 12px rgba(231, 76, 60, 0.4);
        }
        
        .btn-group {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .btn-group .btn {
            flex: 1;
            text-align: center;
        }
        
        .summary-card {
            background: linear-gradient(135deg, #2c3e50 0%, #4a6491 100%);
            color: var(--white);
            border-radius: 14px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
        }
        
        .summary-card::before {
            content: "";
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.05);
        }
        
        .summary-card h3 {
            font-size: 1.4rem;
            margin-bottom: 20px;
            text-align: center;
            position: relative;
            font-weight: 600;
        }
        
        .summary-values {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            text-align: center;
            position: relative;
        }
        
        .summary-item {
            padding: 15px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.12);
            backdrop-filter: blur(4px);
            transition: transform 0.3s ease;
        }
        
        .summary-item:hover {
            transform: scale(1.05);
        }
        
        .summary-item p:first-child {
            font-size: 1rem;
            margin-bottom: 10px;
            opacity: 0.85;
        }
        
        .summary-item p:last-child {
            font-size: 1.6rem;
            font-weight: 700;
            letter-spacing: 0.5px;
        }
        
        .chart-container {
            height: 320px;
            margin-top: 25px;
            background: white;
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
        }
        
        .transactions-list {
            max-height: 320px;
            overflow-y: auto;
            margin-top: 25px;
            border: 1px solid #eee;
            border-radius: 12px;
            padding: 5px;
            background: white;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.03);
        }
        
        .transactions-list::-webkit-scrollbar {
            width: 8px;
        }
        
        .transactions-list::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }
        
        .transactions-list::-webkit-scrollbar-thumb {
            background: #bdc3c7;
            border-radius: 4px;
        }
        
        .transactions-list::-webkit-scrollbar-thumb:hover {
            background: #95a5a6;
        }
        
        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            border-bottom: 1px solid #f0f0f0;
            transition: background 0.2s;
        }
        
        .transaction-item:hover {
            background: #f9f9f9;
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-income {
            border-left: 5px solid var(--success);
        }
        
        .transaction-expense {
            border-left: 5px solid var(--danger);
        }
        
        .transaction-amount {
            font-weight: 600;
            font-size: 1.1rem;
        }
        
        .income-amount {
            color: var(--success);
        }
        
        .expense-amount {
            color: var(--danger);
        }
        
        .transaction-info {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        
        .transaction-info strong {
            font-size: 1.1rem;
        }
        
        .transaction-info div {
            color: var(--gray);
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .report-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f0f0;
        }
        
        footer {
            text-align: center;
            padding: 30px 0;
            color: var(--gray);
            font-size: 1rem;
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
        }
        
        .empty-message {
            text-align: center;
            padding: 50px 20px;
            color: var(--gray);
        }
        
        .empty-message i {
            font-size: 3.5rem;
            margin-bottom: 20px;
            color: #bdc3c7;
            opacity: 0.7;
        }
        
        .empty-message p {
            font-size: 1.1rem;
            margin-bottom: 8px;
        }
        
        .highlight-max {
            font-weight: 700;
            color: var(--danger);
            text-shadow: 0 1px 2px rgba(0,0,0,0.1);
        }
        
        .highlight-min {
            font-weight: 700;
            color: var(--success);
            text-shadow: 0 1px 2px rgba(0,0,0,0.1);
        }
        
        .clp-symbol {
            font-size: 0.9em;
            margin-right: 3px;
            font-weight: 400;
        }
        
        .category-tag {
            display: inline-block;
            padding: 3px 10px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            background: #eef2f7;
        }
        
        .currency-input {
            position: relative;
        }
        
        .currency-input::before {
            content: "$";
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.2rem;
            color: #7f8c8d;
            font-weight: 500;
        }
        
        .currency-input input {
            padding-left: 35px;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            border-radius: 8px;
            background: var(--success);
            color: white;
            font-weight: 500;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transform: translateX(200%);
            transition: transform 0.4s ease;
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .notification.error {
            background: var(--danger);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .card {
            animation: fadeIn 0.6s ease-out;
        }
        
        .card:nth-child(2) {
            animation-delay: 0.2s;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Control de Finanzas Personal</h1>
            <p>Administra tus ingresos y gastos en pesos chilenos <span class="chile-flag"><span class="red"></span><span class="white"></span><span class="blue"></span></span></p>
        </header>
        
        <div class="app-container">
            <!-- Sección de formulario -->
            <div class="card">
                <h2 class="card-title"><i class="fas fa-edit"></i> Nueva Transacción</h2>
                
                <form id="transaction-form">
                    <div class="form-group">
                        <label for="transaction-type">Tipo de transacción</label>
                        <select id="transaction-type" required>
                            <option value="">Seleccionar tipo</option>
                            <option value="income">Ingreso</option>
                            <option value="expense">Gasto</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="transaction-category">Categoría</label>
                        <select id="transaction-category" required>
                            <option value="">Seleccionar categoría</option>
                            <option value="salary" class="income-option">Salario</option>
                            <option value="freelance" class="income-option">Trabajo freelance</option>
                            <option value="investment" class="income-option">Inversiones</option>
                            <option value="other-income" class="income-option">Otros ingresos</option>
                            <option value="housing" class="expense-option">Vivienda</option>
                            <option value="food" class="expense-option">Alimentación</option>
                            <option value="transport" class="expense-option">Transporte</option>
                            <option value="entertainment" class="expense-option">Entretenimiento</option>
                            <option value="health" class="expense-option">Salud</option>
                            <option value="education" class="expense-option">Educación</option>
                            <option value="other-expense" class="expense-option">Otros gastos</option>
                        </select>
                    </div>
                    
                    <div class="form-group currency-input">
                        <label for="transaction-amount">Monto (CLP)</label>
                        <input type="number" id="transaction-amount" min="0" step="100" placeholder="Ej: 250000" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="transaction-date">Fecha</label>
                        <input type="date" id="transaction-date" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="transaction-description">Descripción (opcional)</label>
                        <textarea id="transaction-description" rows="2" placeholder="Detalles de la transacción"></textarea>
                    </div>
                    
                    <button type="submit" class="btn btn-block"><i class="fas fa-plus-circle"></i> Agregar Transacción</button>
                </form>
            </div>
            
            <!-- Sección de informes -->
            <div class="card">
                <h2 class="card-title"><i class="fas fa-chart-pie"></i> Informes Financieros</h2>
                
                <div class="btn-group">
                    <button id="btn-monthly" class="btn"><i class="fas fa-calendar-week"></i> Mensual</button>
                    <button id="btn-semester" class="btn"><i class="fas fa-calendar-alt"></i> Semestral</button>
                    <button id="btn-annual" class="btn"><i class="fas fa-calendar-day"></i> Anual</button>
                </div>
                
                <div class="summary-card">
                    <h3>Resumen Financiero</h3>
                    <div class="summary-values">
                        <div class="summary-item">
                            <p>Total Ingresos</p>
                            <p id="total-income">$0</p>
                        </div>
                        <div class="summary-item">
                            <p>Total Gastos</p>
                            <p id="total-expenses">$0</p>
                        </div>
                        <div class="summary-item">
                            <p>Saldo Final</p>
                            <p id="total-balance">$0</p>
                        </div>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="expense-chart"></canvas>
                </div>
                
                <div class="transactions-list" id="transactions-list">
                    <div class="empty-message">
                        <i class="fas fa-file-invoice-dollar"></i>
                        <p>No hay transacciones para mostrar</p>
                        <p>Seleccione un período para ver los datos</p>
                    </div>
                </div>
            </div>
        </div>
        
        <footer>
            <p>Sistema de Control Financiero Personal &copy; 2023 - Pesos Chilenos (CLP)</p>
        </footer>
    </div>

    <div class="notification" id="notification">
        <i class="fas fa-check-circle"></i>
        <span id="notification-message">Transacción agregada correctamente</span>
    </div>

    <script>
        // Datos de ejemplo en pesos chilenos
        let transactions = [
            { id: 1, type: 'income', category: 'salary', amount: 850000, date: '2023-06-15', description: 'Salario mensual' },
            { id: 2, type: 'expense', category: 'housing', amount: 320000, date: '2023-06-05', description: 'Arriendo' },
            { id: 3, type: 'expense', category: 'food', amount: 185000, date: '2023-06-10', description: 'Supermercado' },
            { id: 4, type: 'expense', category: 'transport', amount: 75000, date: '2023-06-12', description: 'Combustible y transporte' },
            { id: 5, type: 'income', category: 'freelance', amount: 250000, date: '2023-06-20', description: 'Proyecto freelance' },
            { id: 6, type: 'expense', category: 'entertainment', amount: 45000, date: '2023-06-18', description: 'Cine y restaurante' },
            { id: 7, type: 'expense', category: 'health', amount: 65000, date: '2023-06-22', description: 'Consulta médica' },
            { id: 8, type: 'expense', category: 'education', amount: 120000, date: '2023-06-25', description: 'Cursos online' }
        ];
        
        // Referencias a elementos del DOM
        const transactionForm = document.getElementById('transaction-form');
        const transactionType = document.getElementById('transaction-type');
        const transactionCategory = document.getElementById('transaction-category');
        const transactionAmount = document.getElementById('transaction-amount');
        const transactionDate = document.getElementById('transaction-date');
        const transactionDescription = document.getElementById('transaction-description');
        const btnMonthly = document.getElementById('btn-monthly');
        const btnSemester = document.getElementById('btn-semester');
        const btnAnnual = document.getElementById('btn-annual');
        const totalIncome = document.getElementById('total-income');
        const totalExpenses = document.getElementById('total-expenses');
        const totalBalance = document.getElementById('total-balance');
        const transactionsList = document.getElementById('transactions-list');
        const expenseChartCanvas = document.getElementById('expense-chart');
        const notification = document.getElementById('notification');
        const notificationMessage = document.getElementById('notification-message');
        
        // Variables globales
        let expenseChart = null;
        let currentReportType = 'monthly';
        
        // Función para formatear moneda (pesos chilenos)
        function formatCurrency(amount) {
            return new Intl.NumberFormat('es-CL', {
                style: 'currency',
                currency: 'CLP',
                minimumFractionDigits: 0,
                maximumFractionDigits: 0
            }).format(amount);
        }
        
        // Función para mostrar notificación
        function showNotification(message, isError = false) {
            notificationMessage.textContent = message;
            notification.className = 'notification';
            
            if (isError) {
                notification.classList.add('error');
                notification.innerHTML = `<i class="fas fa-exclamation-circle"></i> ${message}`;
            } else {
                notification.innerHTML = `<i class="fas fa-check-circle"></i> ${message}`;
            }
            
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // Función para traducir categorías
        function translateCategory(category) {
            const categories = {
                'salary': 'Salario',
                'freelance': 'Freelance',
                'investment': 'Inversiones',
                'other-income': 'Otros ingresos',
                'housing': 'Vivienda',
                'food': 'Alimentación',
                'transport': 'Transporte',
                'entertainment': 'Entretenimiento',
                'health': 'Salud',
                'education': 'Educación',
                'other-expense': 'Otros gastos'
            };
            
            return categories[category] || category;
        }
        
        // Función para mostrar transacciones
        function renderTransactions(transactions) {
            if (transactions.length === 0) {
                transactionsList.innerHTML = `
                    <div class="empty-message">
                        <i class="fas fa-file-invoice-dollar"></i>
                        <p>No hay transacciones para mostrar</p>
                        <p>Intente con otro período o agregue nuevas transacciones</p>
                    </div>
                `;
                return;
            }
            
            let html = '';
            transactions.forEach(transaction => {
                const formattedDate = new Date(transaction.date).toLocaleDateString('es-CL');
                const formattedAmount = formatCurrency(transaction.amount);
                const categoryName = translateCategory(transaction.category);
                
                html += `
                    <div class="transaction-item ${transaction.type === 'income' ? 'transaction-income' : 'transaction-expense'}">
                        <div class="transaction-info">
                            <strong>${categoryName}</strong>
                            <div>
                                <span class="category-tag">${categoryName}</span>
                                <span>${formattedDate}</span>
                                <span>•</span>
                                <span>${transaction.description || 'Sin descripción'}</span>
                            </div>
                        </div>
                        <div class="transaction-amount ${transaction.type === 'income' ? 'income-amount' : 'expense-amount'}">
                            ${transaction.type === 'income' ? '+' : '-'} ${formattedAmount}
                        </div>
                    </div>
                `;
            });
            
            transactionsList.innerHTML = html;
        }
        
        // Función para generar informe
        function generateReport(reportType) {
            currentReportType = reportType;
            
            // Actualiza el botón activo
            document.querySelectorAll('.btn-group .btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.getElementById(`btn-${reportType}`).classList.add('active');
            
            // Filtra las transacciones según el tipo de informe
            let filteredTransactions = [];
            const today = new Date();
            
            switch(reportType) {
                case 'monthly':
                    filteredTransactions = transactions.filter(t => {
                        const transDate = new Date(t.date);
                        return transDate.getMonth() === today.getMonth() && 
                               transDate.getFullYear() === today.getFullYear();
                    });
                    break;
                    
                case 'semester':
                    filteredTransactions = transactions.filter(t => {
                        const transDate = new Date(t.date);
                        const semester = Math.floor(today.getMonth() / 6);
                        return Math.floor(transDate.getMonth() / 6) === semester && 
                               transDate.getFullYear() === today.getFullYear();
                    });
                    break;
                    
                case 'annual':
                    filteredTransactions = transactions.filter(t => {
                        const transDate = new Date(t.date);
                        return transDate.getFullYear() === today.getFullYear();
                    });
                    break;
            }
            
            // Calcula los totales
            const income = filteredTransactions
                .filter(t => t.type === 'income')
                .reduce((sum, t) => sum + t.amount, 0);
            
            const expenses = filteredTransactions
                .filter(t => t.type === 'expense')
                .reduce((sum, t) => sum + t.amount, 0);
            
            const balance = income - expenses;
            
            // Actualiza los valores en la UI
            totalIncome.textContent = formatCurrency(income);
            totalExpenses.textContent = formatCurrency(expenses);
            totalBalance.textContent = formatCurrency(balance);
            
            // Actualiza las transacciones mostradas
            renderTransactions(filteredTransactions);
            
            // Genera el gráfico de gastos
            generateExpenseChart(filteredTransactions);
        }
        
        // Función para generar el gráfico de gastos
        function generateExpenseChart(transactions) {
            // Filtra solo los gastos
            const expenses = transactions.filter(t => t.type === 'expense');
            
            if (expenses.length === 0) {
                if (expenseChart) {
                    expenseChart.destroy();
                }
                
                expenseChartCanvas.innerHTML = `
                    <div class="empty-message" style="height: 100%; display: flex; flex-direction: column; justify-content: center;">
                        <i class="fas fa-chart-pie" style="font-size: 3rem;"></i>
                        <p>No hay datos de gastos para mostrar</p>
                    </div>
                `;
                return;
            }
            
            // Agrupa gastos por categoría
            const categories = {};
            expenses.forEach(expense => {
                if (categories[expense.category]) {
                    categories[expense.category] += expense.amount;
                } else {
                    categories[expense.category] = expense.amount;
                }
            });
            
            // Encuentra el mayor y menor gasto
            let maxCategory = null;
            let minCategory = null;
            let maxAmount = 0;
            let minAmount = Infinity;
            
            for (const [category, amount] of Object.entries(categories)) {
                if (amount > maxAmount) {
                    maxAmount = amount;
                    maxCategory = category;
                }
                if (amount < minAmount) {
                    minAmount = amount;
                    minCategory = category;
                }
            }
            
            // Prepara datos para el gráfico
            const labels = Object.keys(categories).map(translateCategory);
            const data = Object.values(categories);
            
            // Colores para el gráfico
            const backgroundColors = data.map((amount, index) => {
                const category = Object.keys(categories)[index];
                if (category === maxCategory) return 'rgba(231, 76, 60, 0.8)'; // Rojo para el mayor gasto
                if (category === minCategory) return 'rgba(46, 204, 113, 0.8)'; // Verde para el menor gasto
                return `hsl(${index * 50}, 70%, 60%)`;
            });
            
            // Destruye el gráfico anterior si existe
            if (expenseChart) {
                expenseChart.destroy();
            }
            
            // Limpia el contenedor
            expenseChartCanvas.innerHTML = '<canvas id="expense-chart"></canvas>';
            const ctx = document.getElementById('expense-chart').getContext('2d');
            
            // Crea el nuevo gráfico
            expenseChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: labels,
                    datasets: [{
                        data: data,
                        backgroundColor: backgroundColors,
                        borderWidth: 1,
                        borderColor: '#fff'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '60%',
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                font: {
                                    size: 12
                                },
                                usePointStyle: true,
                                pointStyle: 'circle'
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const label = context.label || '';
                                    const value = context.raw || 0;
                                    const total = data.reduce((a, b) => a + b, 0);
                                    const percentage = Math.round((value / total) * 100);
                                    return `${label}: ${formatCurrency(value)} (${percentage}%)`;
                                }
                            }
                        },
                        title: {
                            display: true,
                            text: 'Distribución de Gastos',
                            font: {
                                size: 16,
                                weight: 'normal'
                            },
                            padding: 10
                        }
                    }
                }
            });
        }
        
        // Función para agregar nueva transacción
        function addTransaction(type, category, amount, date, description) {
            const newTransaction = {
                id: Date.now(),
                type,
                category,
                amount: parseFloat(amount),
                date,
                description
            };
            
            transactions.push(newTransaction);
            
            // Actualiza el informe actual
            generateReport(currentReportType);
            
            // Muestra notificación
            showNotification('Transacción agregada correctamente');
        }
        
        // Event Listeners
        transactionForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const type = transactionType.value;
            const category = transactionCategory.value;
            const amount = transactionAmount.value;
            const date = transactionDate.value;
            const description = transactionDescription.value;
            
            if (!type || !category || !amount || !date) {
                showNotification('Por favor complete todos los campos requeridos', true);
                return;
            }
            
            if (parseFloat(amount) <= 0) {
                showNotification('El monto debe ser mayor a cero', true);
                return;
            }
            
            addTransaction(type, category, amount, date, description);
            
            // Resetear formulario
            transactionForm.reset();
            transactionType.dispatchEvent(new Event('change'));
        });
        
        // Actualiza las opciones de categoría según el tipo de transacción seleccionado
        transactionType.addEventListener('change', function() {
            const type = this.value;
            const options = transactionCategory.querySelectorAll('option');
            
            options.forEach(option => {
                if (!option.value) return;
                
                if (type === 'income') {
                    option.style.display = option.classList.contains('income-option') ? '' : 'none';
                } else if (type === 'expense') {
                    option.style.display = option.classList.contains('expense-option') ? '' : 'none';
                } else {
                    option.style.display = 'none';
                }
            });
            
            // Restablecer selección
            transactionCategory.value = '';
        });
        
        // Botones de informes
        btnMonthly.addEventListener('click', () => generateReport('monthly'));
        btnSemester.addEventListener('click', () => generateReport('semester'));
        btnAnnual.addEventListener('click', () => generateReport('annual'));
        
        // Inicializar la aplicación
        document.addEventListener('DOMContentLoaded', function() {
            // Establecer fecha actual como valor predeterminado
            const today = new Date().toISOString().split('T')[0];
            transactionDate.value = today;
            
            // Generar informe mensual por defecto
            generateReport('monthly');
        });
    </script>
</body>
</html> app_control_gastos
