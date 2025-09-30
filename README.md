<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Club Pétalos - Calculadora de Ventas</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: radial-gradient(circle at 30% 30%, #1b1b1b, #1b1b1b);
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        .petal {
            position: fixed;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle at 30% 30%, #111111, #111111);
            border-radius: 50% 0 50% 0;
            opacity: 0.7;
            pointer-events: none;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 0.7;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgb(20, 20, 20);
            border-radius: 20px;
            border: 1px solid #707070;
            box-shadow: 0 0 20px rgba(23, 23, 23, 0.773);
            padding: 30px;
            position: relative;
            z-index: 1;
        }

        h1 {
            text-align: center;
            color: #ffffff;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(255, 255, 255, 0.3);
        }

        .worker-section {
            margin-bottom: 25px;
            text-align: center;
        }

        .worker-section label {
            color: #ffffff;
            font-weight: bold;
            margin-right: 10px;
        }

        .worker-section input {
            padding: 10px 15px;
            border: 2px solid #000000;
            border-radius: 10px;
            font-size: 1em;
            width: 250px;
            outline: none;
            transition: border-color 0.3s;
        }

        .worker-section input:focus {
            border-color: #000000;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .tab {
            flex: 1;
            padding: 15px;
            background: linear-gradient(135deg, #ffffffe3, #ffffffe3);
            border: 2px solid #ffffffe3;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1em;
            font-weight: bold;
            color: black;
            transition: all 0.3s;
            min-width: 220px;
        }

        .tab:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(16, 15, 15, 0.4);
        }

        .tab.active {
            color: white;
            background: linear-gradient(135deg, #2fa921e3, #2fa921e3);
            box-shadow: 0 5px 15px rgba(59, 255, 20, 0.4);
            border: 2px solid #2fa9218d;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .product {
            display: grid;
            grid-template-columns: auto 1fr auto auto;
            gap: 15px;
            align-items: center;
            padding: 15px;
            background: linear-gradient(135deg, #ffffff, #ffffff);
            border-radius: 10px;
            margin-bottom: 10px;
            transition: all 0.3s;
        }

        .product:hover {
            transform: translateX(5px);
            box-shadow: 0 3px 10px rgba(11, 11, 11, 0.2);
        }

        .product input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .product-name {
            font-weight: bold;
            color: #000000;
        }

        .product-price {
            color: #33ff21;
            font-weight: bold;
        }

        .product input[type="number"] {
            width: 80px;
            padding: 8px;
            border: 2px solid #000000;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
        }

        .total-section {
            margin-top: 30px;
            padding: 20px;
            background: rgb(20, 20, 20);
            border-radius: 20px;
            border: 1px solid #707070;
            box-shadow: 0 0 20px rgba(23, 23, 23, 0.773);
            border-radius: 15px;
            color: white;
        }

        .total-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            font-size: 1.3em;
            font-weight: bold;
        }

        .discount-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }

        .discount-btn {
            padding: 10px 15px;
            background: white;
            color: #111111;
            border: 2px solid white;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        .discount-btn:hover {
            background: #b7ffb3;
            transform: scale(1.05);
        }

        .discount-btn.active {
            background: #1aff00;
            color: #ffffff;
        }

        .custom-discount {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .custom-discount input {
            width: 80px;
            padding: 8px;
            border: 2px solid white;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
        }

        .save-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #1aff003e, #1aff003e);
            border: 1px solid #1aff00;
            border-radius: 10px;
            font-size: 1.2em;
            font-weight: bold;
            color: #ffffff;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 15px;
        }

        .save-btn:hover {
            transform: scale(1.02);
            background: linear-gradient(135deg, #1aff00b8, #1aff00b8);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 20px 30px;
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            animation: slideIn 0.3s, slideOut 0.3s 2.7s;
            font-weight: bold;
        }

        .notification.error {
            background: linear-gradient(135deg, #f44336, #da190b);
        }

        @keyframes slideIn {
            from { transform: translateX(400px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes slideOut {
            from { transform: translateX(0); opacity: 1; }
            to { transform: translateX(400px); opacity: 0; }
        }


    </style>
</head>
<body>
    <div class="container">
        <h1>🌸 CLUB PÉTALOS 🌸</h1>
        
        <div class="worker-section">
            <label for="workerName">👤 Nombre del Trabajador:</label>
            <input type="text" id="workerName" placeholder="Ingresa tu nombre">
        </div>

        <div class="tabs">
            <button class="tab active" onclick="switchTab('comida')">🍕 Comida</button>
            <button class="tab" onclick="switchTab('objetos')">🎁 Objetos</button>
            <button class="tab" onclick="switchTab('bailes')">💃 Bailes</button>
            <button class="tab" onclick="switchTab('escorts')">👥 Escorts</button>
            <button class="tab" onclick="switchTab('habitaciones')">🏡 Habitaciones</button>
        </div>

        <div id="comida" class="tab-content active"></div>
        <div id="objetos" class="tab-content"></div>
        <div id="bailes" class="tab-content"></div>
        <div id="escorts" class="tab-content"></div>
        <div id="habitaciones" class="tab-content"></div>

        <div class="total-section">
            <div class="total-row">
                <span>Subtotal:</span>
                <span id="subtotal">$0</span>
            </div>
            
            <div class="discount-buttons">
                <button class="discount-btn" onclick="applyDiscount(5)">5% OFF</button>
                <button class="discount-btn" onclick="applyDiscount(10)">10% OFF</button>
                <button class="discount-btn" onclick="applyDiscount(15)">15% OFF</button>
                <div class="custom-discount">
                    <input type="number" id="customDiscount" placeholder="%" min="0" max="100">
                    <button class="discount-btn" onclick="applyCustomDiscount()">Aplicar</button>
                </div>
            </div>

            <div class="total-row" style="font-size: 1.5em;">
                <span>TOTAL:</span>
                <span id="total">$0</span>
            </div>

            <button class="save-btn" onclick="saveVenta()">💾 GUARDAR VENTA</button>
        </div>
    </div>

    <script>
        // CONFIGURACIÓN DEL WEBHOOK
        const DISCORD_WEBHOOK_URL = 'https://discord.com/api/webhooks/1422219977850880020/ggrjBeIDrQPYCrKlj_I9EzRz2ppW7-AweT4akGoGzClp5BJqcujNPfA50RHhHpIhFmtC';
        
        const productos = {
            comida: [
            {name: 'Comida', price: 50},
            {name: 'Bebidas', price: 55},
            {name: 'Pack 1x1', price: 80},
            {name: 'Pack 2x2', price: 145},
            {name: 'Pack 3x3', price: 220},
            ],
            objetos: [
                {name: 'Condones', price: 125},
                {name: 'Coleccionables', price: 150},
                {name: 'Juego de Cartas(7)', price: 400},
            ],
            bailes: [
                {name: 'Baile Privado (15min)', price: 350},
                {name: 'Baile VIP (30min)', price: 550},
                {name: 'Baile Duo (25min)', price: 700},
            ],
            escorts: [
                {name: 'Baile Sin Ropa', price: 550},
                {name: 'Sexo Oral', price: 1000},
                {name: 'Masturbación', price: 830},
                {name: 'Sexo', price: 1800},
                {name: 'Sexo Oral + Masturbación', price: 1400},
                {name: 'Completo', price: 2400}
            ],
            habitaciones: [
                {name: 'Habitación Roja (30min)', price: 5000},
                {name: 'Habitación Casino (30min)', price: 2500},
                {name: 'Habitación Pequeña (30min)', price: 1500},
                {name: 'Habitación Roja (60min)', price: 8000},
                {name: 'Habitación Casino (60min)', price: 3500},
                {name: 'Habitación Pequeña (60min)', price: 2500},
            ]
        };

        let currentDiscount = 0;

        // Crear pétalos cayendo
        function createPetals() {
            for(let i = 0; i < 15; i++) {
                const petal = document.createElement('div');
                petal.className = 'petal';
                petal.style.left = Math.random() * 100 + '%';
                petal.style.animationDuration = (Math.random() * 3 + 5) + 's';
                petal.style.animationDelay = Math.random() * 5 + 's';
                document.body.appendChild(petal);
            }
        }

        // Inicializar productos
        function initProducts() {
            for(let category in productos) {
                const container = document.getElementById(category);
                productos[category].forEach((prod, index) => {
                    const div = document.createElement('div');
                    div.className = 'product';
                    div.innerHTML = `
                        <input type="checkbox" id="${category}-${index}" onchange="calculateTotal()">
                        <span class="product-name">${prod.name}</span>
                        <span class="product-price">$${prod.price}</span>
                        <input type="number" id="${category}-qty-${index}" value="1" min="1" onchange="calculateTotal()">
                    `;
                    container.appendChild(div);
                });
            }
        }

        function switchTab(tabName) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tabName).classList.add('active');
        }

        function calculateTotal() {
            let subtotal = 0;
            
            for(let category in productos) {
                productos[category].forEach((prod, index) => {
                    const checkbox = document.getElementById(`${category}-${index}`);
                    const qty = document.getElementById(`${category}-qty-${index}`);
                    
                    if(checkbox.checked) {
                        subtotal += prod.price * parseInt(qty.value || 1);
                    }
                });
            }

            document.getElementById('subtotal').textContent = '$' + subtotal.toFixed(2);
            
            const total = subtotal * (1 - currentDiscount / 100);
            document.getElementById('total').textContent = '$' + total.toFixed(2);
        }

        function applyDiscount(percent) {
            currentDiscount = percent;
            document.querySelectorAll('.discount-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            document.getElementById('customDiscount').value = '';
            calculateTotal();
            showNotification(`Descuento del ${percent}% aplicado`);
        }

        function applyCustomDiscount() {
            const custom = document.getElementById('customDiscount').value;
            if(custom && custom >= 0 && custom <= 100) {
                currentDiscount = parseFloat(custom);
                document.querySelectorAll('.discount-btn').forEach(btn => btn.classList.remove('active'));
                calculateTotal();
                showNotification(`Descuento del ${custom}% aplicado`);
            }
        }

        function showNotification(message, isError = false) {
            const notification = document.createElement('div');
            notification.className = 'notification' + (isError ? ' error' : '');
            notification.textContent = message;
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }

        async function saveVenta() {
            const workerName = document.getElementById('workerName').value;

            if(!workerName) {
                showNotification('Por favor ingresa el nombre del trabajador', true);
                return;
            }

            if(!DISCORD_WEBHOOK_URL || DISCORD_WEBHOOK_URL === 'TU_WEBHOOK_URL_AQUI') {
                showNotification('Por favor configura el webhook en el código', true);
                return;
            }

            let productosVendidos = [];
            let subtotal = 0;

            for(let category in productos) {
                productos[category].forEach((prod, index) => {
                    const checkbox = document.getElementById(`${category}-${index}`);
                    const qty = document.getElementById(`${category}-qty-${index}`);
                    
                    if(checkbox.checked) {
                        const cantidad = parseInt(qty.value || 1);
                        const precioTotal = prod.price * cantidad;
                        subtotal += precioTotal;
                        productosVendidos.push({
                            categoria: category,
                            producto: prod.name,
                            precio: prod.price,
                            cantidad: cantidad,
                            total: precioTotal
                        });
                    }
                });
            }

            if(productosVendidos.length === 0) {
                showNotification('No hay productos seleccionados', true);
                return;
            }

            const total = subtotal * (1 - currentDiscount / 100);
            const fecha = new Date().toLocaleString('es-ES');

            let mensaje = `**🌸 CLUB PÉTALOS - NUEVA VENTA 🌸**\n\n`;
            mensaje += `**👤 Trabajador:** ${workerName}\n`;
            mensaje += `**📅 Fecha:** ${fecha}\n\n`;
            mensaje += `**📦 Productos Vendidos:**\n`;
            
            productosVendidos.forEach(p => {
                mensaje += `• ${p.producto} (${p.categoria}) - $${p.precio} x ${p.cantidad} = $${p.total}\n`;
            });

            mensaje += `\n**💰 Subtotal:** $${subtotal.toFixed(2)}\n`;
            if(currentDiscount > 0) {
                mensaje += `**🎟️ Descuento:** ${currentDiscount}%\n`;
            }
            mensaje += `**💵 TOTAL:** $${total.toFixed(2)}`;

            try {
                const response = await fetch(DISCORD_WEBHOOK_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        content: mensaje
                    })
                });

                if(response.ok) {
                    showNotification('✅ Venta guardada exitosamente');
                    // Reset form
                    document.querySelectorAll('input[type="checkbox"]').forEach(cb => cb.checked = false);
                    currentDiscount = 0;
                    calculateTotal();
                } else {
                    showNotification('Error al enviar a Discord. Verifica la URL del webhook', true);
                }
            } catch(error) {
                showNotification('Error de conexión. Verifica la URL del webhook', true);
            }
        }

        // Inicializar
        createPetals();
        initProducts();
        calculateTotal();
    </script>
</body>
</html>
