<!DOCTYPE html>
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
            background: radial-gradient(circle at 30% 30%, #1b1b1b, #0d0d0d);
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        .petal {
            position: fixed;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle at 30% 30%, #2a2a2a, #1a1a1a);
            border-radius: 50% 0 50% 0;
            opacity: 0.4;
            pointer-events: none;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 0.4;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: linear-gradient(135deg, #1a1a1a 0%, #242424 100%);
            border-radius: 20px;
            border: 1px solid #3a3a3a;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
            padding: 30px;
            position: relative;
            z-index: 1;
        }

        h1 {
            text-align: center;
            color: #ffffff;
            font-size: 2.2em;
            margin-bottom: 20px;
            text-shadow: 0 0 20px rgba(47, 169, 33, 0.5);
            letter-spacing: 2px;
        }

        .worker-section {
            margin-bottom: 25px;
            text-align: center;
        }

        .worker-section label {
            color: #ffffff;
            font-weight: 600;
            margin-right: 10px;
            font-size: 1.1em;
        }

        .worker-section input {
            padding: 12px 20px;
            border: 2px solid #2fa921;
            border-radius: 10px;
            font-size: 1em;
            width: 280px;
            outline: none;
            background: #2a2a2a;
            color: #ffffff;
            transition: all 0.3s;
        }

        .worker-section input:focus {
            border-color: #3fff20;
            box-shadow: 0 0 15px rgba(47, 169, 33, 0.3);
        }

        .tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .tab {
            padding: 10px 18px;
            background: linear-gradient(135deg, #2a2a2a, #353535);
            border: 2px solid #444444;
            border-radius: 10px;
            cursor: pointer;
            font-size: 0.9em;
            font-weight: 600;
            color: #ffffff;
            transition: all 0.3s;
            min-width: 120px;
            text-align: center;
        }

        .tab:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(47, 169, 33, 0.2);
            border-color: #2fa921;
        }

        .tab.active {
            color: white;
            background: linear-gradient(135deg, #2fa921, #25880f);
            box-shadow: 0 5px 20px rgba(47, 169, 33, 0.5);
            border: 2px solid #3fff20;
        }

        .products-container {
            max-height: 450px;
            overflow-y: auto;
            padding-right: 10px;
            margin-bottom: 20px;
        }

        .products-container::-webkit-scrollbar {
            width: 10px;
        }

        .products-container::-webkit-scrollbar-track {
            background: #1a1a1a;
            border-radius: 10px;
        }

        .products-container::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #2fa921, #25880f);
            border-radius: 10px;
        }

        .products-container::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(135deg, #3fff20, #2fa921);
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
            padding: 12px 15px;
            background: linear-gradient(135deg, #2a2a2a, #333333);
            border: 1px solid #444444;
            border-radius: 10px;
            margin-bottom: 8px;
            transition: all 0.3s;
        }

        .product:hover {
            transform: translateX(5px);
            box-shadow: 0 3px 15px rgba(47, 169, 33, 0.3);
            border-color: #2fa921;
        }

        .product input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
            accent-color: #2fa921;
        }

        .product-name {
            font-weight: 600;
            color: #ffffff;
            font-size: 0.95em;
        }

        .product-price {
            color: #3fff20;
            font-weight: bold;
            font-size: 1.05em;
        }

        .product input[type="number"] {
            width: 80px;
            padding: 8px;
            border: 2px solid #2fa921;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
            background: #1a1a1a;
            color: #ffffff;
            transition: all 0.3s;
        }

        .product input[type="number"]:focus {
            border-color: #3fff20;
            box-shadow: 0 0 10px rgba(47, 169, 33, 0.3);
            outline: none;
        }

        .price-input-container {
            display: flex;
            flex-direction: column;
            align-items: flex-end;
        }

        .price-input {
            width: 100px;
            padding: 8px;
            border: 2px solid #2fa921;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
            background: #1a1a1a;
            color: #3fff20;
            font-size: 1em;
        }

        .price-input:focus {
            border-color: #3fff20;
            box-shadow: 0 0 10px rgba(47, 169, 33, 0.3);
            outline: none;
        }

        .price-range {
            font-size: 0.7em;
            color: #888;
            margin-top: 2px;
        }

        .info-text {
            background: linear-gradient(135deg, #3a2a00, #4a3600);
            border: 2px solid #ffaa00;
            padding: 10px;
            border-radius: 10px;
            color: #ffdd77;
            font-weight: 600;
            text-align: center;
            margin-bottom: 10px;
            font-size: 0.9em;
        }

        .total-section {
            margin-top: 20px;
            padding: 20px;
            background: linear-gradient(135deg, #1a1a1a, #242424);
            border: 1px solid #3a3a3a;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
            border-radius: 15px;
            color: white;
        }

        .total-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            font-size: 1.2em;
            font-weight: bold;
        }

        .discount-buttons {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }

        .discount-btn {
            padding: 8px 15px;
            background: linear-gradient(135deg, #2a2a2a, #353535);
            color: #ffffff;
            border: 2px solid #444444;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9em;
            transition: all 0.3s;
        }

        .discount-btn:hover {
            background: linear-gradient(135deg, #2fa921, #25880f);
            border-color: #3fff20;
            transform: scale(1.05);
        }

        .discount-btn.active {
            background: linear-gradient(135deg, #2fa921, #25880f);
            color: #ffffff;
            border-color: #3fff20;
            box-shadow: 0 0 15px rgba(47, 169, 33, 0.5);
        }

        .custom-discount {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .custom-discount input {
            width: 70px;
            padding: 8px;
            border: 2px solid #2fa921;
            border-radius: 8px;
            text-align: center;
            font-weight: bold;
            background: #1a1a1a;
            color: #ffffff;
        }

        .save-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #2fa921, #25880f);
            border: 2px solid #3fff20;
            border-radius: 10px;
            font-size: 1.2em;
            font-weight: bold;
            color: #ffffff;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 15px;
            box-shadow: 0 5px 20px rgba(47, 169, 33, 0.3);
        }

        .save-btn:hover {
            transform: scale(1.02);
            background: linear-gradient(135deg, #3fff20, #2fa921);
            box-shadow: 0 8px 30px rgba(47, 169, 33, 0.5);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 20px 30px;
            background: linear-gradient(135deg, #2fa921, #25880f);
            color: white;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.5);
            z-index: 1000;
            animation: slideIn 0.3s, slideOut 0.3s 2.7s;
            font-weight: bold;
            border: 2px solid #3fff20;
        }

        .notification.error {
            background: linear-gradient(135deg, #f44336, #da190b);
            border-color: #ff6659;
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

        <div id="comida" class="tab-content active">
            <div class="products-container" id="comida-products"></div>
        </div>
        <div id="objetos" class="tab-content">
            <div class="products-container" id="objetos-products"></div>
        </div>
        <div id="bailes" class="tab-content">
            <div class="info-text">⚠️ EL 50% ES PARA LA BAILARINA</div>
            <div class="products-container" id="bailes-products"></div>
        </div>
        <div id="escorts" class="tab-content">
            <div class="info-text">⚠️ EL TIEMPO LO ELIGE LA ESCORT Y EL 70% ES PARA LA ESCORT</div>
            <div class="products-container" id="escorts-products"></div>
        </div>
        <div id="habitaciones" class="tab-content">
            <div class="products-container" id="habitaciones-products"></div>
        </div>

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

            <div class="total-row" style="font-size: 1.5em; color: #3fff20;">
                <span>TOTAL:</span>
                <span id="total">$0</span>
            </div>

            <button class="save-btn" onclick="saveVenta()">💾 GUARDAR VENTA</button>
        </div>
    </div>

    <script>
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
                {name: 'Baile Privado (15min)', min: 350, max: 950},
                {name: 'Baile VIP (30min)', min: 550, max: 1850},
                {name: 'Baile Duo (25min)', min: 700, max: 2100},
            ],
            escorts: [
                {name: 'Baile Sin Ropa', min: 550, max: 1000},
                {name: 'Sexo Oral', min: 1000, max: 1500},
                {name: 'Masturbación', min: 830, max: 1200},
                {name: 'Sexo', min: 1800, max: 2500},
                {name: 'Sexo Oral + Masturbación', min: 1400, max: 2000},
                {name: 'Completo', min: 2400, max: 3500}
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

        function initProducts() {
            for(let category in productos) {
                const container = document.getElementById(`${category}-products`);
                productos[category].forEach((prod, index) => {
                    const div = document.createElement('div');
                    div.className = 'product';
                    
                    if(prod.price !== undefined) {
                        div.innerHTML = `
                            <input type="checkbox" id="${category}-${index}" onchange="calculateTotal()">
                            <span class="product-name">${prod.name}</span>
                            <span class="product-price">$${prod.price}</span>
                            <input type="number" id="${category}-qty-${index}" value="1" min="1" onchange="calculateTotal()">
                        `;
                    } else {
                        div.innerHTML = `
                            <input type="checkbox" id="${category}-${index}" onchange="calculateTotal()">
                            <span class="product-name">${prod.name}</span>
                            <div class="price-input-container">
                                <input type="number" class="price-input" id="${category}-price-${index}" 
                                       value="${prod.min}" min="${prod.min}" max="${prod.max}" 
                                       placeholder="$" onchange="calculateTotal()">
                                <span class="price-range">$${prod.min}-$${prod.max}</span>
                            </div>
                            <input type="number" id="${category}-qty-${index}" value="1" min="1" onchange="calculateTotal()">
                        `;
                    }
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
                        let price;
                        if(prod.price !== undefined) {
                            price = prod.price;
                        } else {
                            const priceInput = document.getElementById(`${category}-price-${index}`);
                            price = parseFloat(priceInput.value) || prod.min;
                            if(price < prod.min) price = prod.min;
                            if(price > prod.max) price = prod.max;
                            priceInput.value = price;
                        }
                        subtotal += price * parseInt(qty.value || 1);
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
                        let price;
                        
                        if(prod.price !== undefined) {
                            price = prod.price;
                        } else {
                            const priceInput = document.getElementById(`${category}-price-${index}`);
                            price = parseFloat(priceInput.value) || prod.min;
                        }
                        
                        const precioTotal = price * cantidad;
                        subtotal += precioTotal;
                        productosVendidos.push({
                            categoria: category,
                            producto: prod.name,
                            precio: price,
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

        createPetals();
        initProducts();
        calculateTotal();
    </script>
</body>
</html>
