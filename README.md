# Sistemas-de-automa-o-para-lanchonetes
Sistema de automação para lanchonete
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Automação de Lanchonete</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            position: relative;
        }
        .share-btn {
            position: absolute;
            top: 20px;
            right: 0px;
            background: #25D366;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 8px 15px;
            margin: 0 auto
            display: none; /* Inicialmente escondido */
            align-items: center;
            gap: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        .share-btn:hover {
            background: transparent;
        }
        .share-btn.copy {
            display:none;
            right: 0px;
            margin: 0 auto;
            background: #3498db;
        }
        .share-btn.copy:hover {
            background: #2980b9;
        }
        h1 {
            text-align: center;
            color: pink;
        }
        .menu {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        .item {
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
        }
        .item:hover {
            background: #f0f0f0;
        }
        .item img {
            width: 100%;
            height: 120px;
            object-fit: cover;
            border-radius: 5px;
        }
        .item h3 {
            margin: 10px 0 5px;
        }
        .item p {
            margin: 5px 0;
            color: #666;
        }
        .item .price {
            font-weight: bold;
            color: #e67e22;
        }
        .order-summary {
            margin-top: 20px;
            padding: 15px;
            background: #f9f9f9;
            border-radius: 5px;
        }
        .order-summary h2 {
            margin-top: 0;
        }
        #order-list {
            list-style: none;
            padding: 0;
        }
        #order-list li {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            border-bottom: 1px dashed #ddd;
        }
        #total {
            font-weight: bold;
            font-size: 1.2em;
            text-align: right;
            margin-top: 10px;
        }
        button {
            display: block;
            width: 100%;
            padding: 10px;
            background: #27ae60;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 20px;
        }
        button:hover {
            background: #2ecc71;
        }
        #receipt {
            margin-top: 20px;
            padding: 15px;
            background: #fff;
            border: 1px dashed #ccc;
            border-radius: 5px;
            display: none;
        }

        /* Modal de Endereço */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .modal-content {
            background: white;
            padding: 20px;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
        }
        .modal h2 {
            margin-top: 0;
        }
        .modal label {
            display: block;
            margin-top: 10px;
        }
        .modal input, .modal textarea {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .modal-buttons {
            display: flex;
            justify-content: flex-end;
            margin-top: 20px;
            gap: 10px;
        }
        .modal-buttons button {
            width: auto;
            margin-top: 0;
        }
        .modal-buttons .cancel {
            background: #e74c3c;
        }
        .modal-buttons .cancel:hover {
            background: #c0392b;
        }
    </style>
</head>
<body>
    
        
        <h1>🍔 Lanchonete d,gust</h1>
        
        <div class="menu">
            <div class="item" onclick="addToOrder('X-Burger', 15.00)">
             <img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd?ixlib=rb-1.2.1&auto=format&fit=crop&w=300&h=200&q=80" alt="X-Burger">   <h3>X-burguer</h3>  <p>Pão, hambúrguer, queijo, alface</p>
                <p class="price">R$ 15,00</p>
            </div>
            
            <div class="item" onclick="addToOrder('X-Salada', 18.00)">
              <img src="https://images.unsplash.com/photo-1607013251379-e6eecfffe234?w=300&h=200&fit=crop" alt="Hambúrguer Duplo">   <h3>X-Salada</h3>
                <p>Pão, hambúrguer, queijo, tomate, alface</p>
                <p class="price">R$ 18,00</p>
            </div>
            
            <div class="item" onclick="addToOrder('Refrigerante', 8.00)">
               <img src="https://images.unsplash.com/photo-1554866585-cd94860890b7?w=300&h=200&fit=crop" alt="Lata de Refrigerante">      <h3>Refrigerante</h3>
                <p>Lata 350ml</p>
                <p class="price">R$ 8,00</p>
            </div>
            
            <div class="item" onclick="addToOrder('Batata Frita', 12.00)">
              <img src="https://images.pexels.com/photos/1583884/pexels-photo-1583884.jpeg?auto=compress&cs=tinysrgb&w=300&h=200&fit=crop" alt="Batata com Ketchup">       <h3>Batata Frita</h3>
                <p>Porção média</p>
                <p class="price">R$ 12,00</p>
            </div>
        </div>
        
        <div class="order-summary">
            <h2>Seu Pedido</h2>
            <ul id="order-list"></ul>
            <div id="total">Total: R$ 0,00</div>
        </div>
        
        <button onclick="openAddressModal()">Finalizar Pedido</button>
        
        <div id="receipt">
            <h2>📝 Comprovante</h2>
            <div id="receipt-content"></div>
        </div>
    </div>

    <!-- Modal de Endereço -->
    <div id="addressModal" class="modal">
        <div class="modal-content">
            <h2>Informe o Endereço de Entrega</h2>
            <form id="addressForm">
                <label for="name">Nome:</label>
                <input type="text" id="name" required>
                
                <label for="phone">Telefone:</label>
                <input type="tel" id="phone" required>
                
                <label for="street">Rua:</label>
                <input type="text" id="street" required>
                
                <label for="number">Número:</label>
                <input type="text" id="number" required>
                
                <label for="neighborhood">Bairro:</label>
                <input type="text" id="neighborhood" required>
                
                
                <label for="complement">Complemento:</label>
                <input type="text" id="complement">
                
                
                <label for="notes">Observações:</label>
                <textarea id="notes" rows="3"></textarea>
                
                <div class="modal-buttons">
                    <button type="button" class="cancel" onclick="closeAddressModal()">Cancelar</button>
                    <button type="button" onclick="submitAddress()">Confirmar Pedido</button>
                </div>
            </form>
        </div>
    </div>




    <script>
        let order = [];
        let total = 0;
        let deliveryAddress = {};
        
        function addToOrder(itemName, itemPrice) {
            order.push({ name: itemName, price: itemPrice });
            total += itemPrice;
            updateOrderSummary();
        }
        
        function updateOrderSummary() {
            const orderList = document.getElementById('order-list');
            const totalElement = document.getElementById('total');
            
            orderList.innerHTML = '';
            order.forEach(item => {
                const li = document.createElement('li');
                li.innerHTML = `<span>${item.name}</span> <span>R$ ${item.price.toFixed(2)}</span>`;
                orderList.appendChild(li);
            });
            
            totalElement.textContent = `Total: R$ ${total.toFixed(2)}`;
        }
        
        function openAddressModal() {
            if (order.length === 0) {
                alert('Adicione itens ao pedido primeiro!');
                return;
            }
            document.getElementById('addressModal').style.display = 'flex';
        }
        
        function closeAddressModal() {
            document.getElementById('addressModal').style.display = 'none';
        }
        
        function submitAddress() {
            // Captura os dados do formulário
            deliveryAddress = {
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                street: document.getElementById('street').value,
                number: document.getElementById('number').value,
                complement: document.getElementById('complement').value,
                neighborhood: document.getElementById('neighborhood').value,
                notes: document.getElementById('notes').value
            };
            
            // Validação simples
            if (!deliveryAddress.street || !deliveryAddress.number || !deliveryAddress.neighborhood) {
                alert('Preencha pelo menos Rua, Número e Bairro!');
                return;
            }
            
            closeAddressModal();
            generateReceipt();
        }
        
        function generateReceipt() {
            const receipt = document.getElementById('receipt');
            const receiptContent = document.getElementById('receipt-content');
            
            let receiptHTML = `
             <div class="container">
        <!-- Botões de compartilhamento (inicialmente ocultos) -->
        <button class="share-btn copy" id="copyBtn" onclick="copyOrder()">
          
        </button>
        <button class="share-btn" id="shareBtn" onclick="shareOnWhatsApp()">
            📱 Enviar Comprovante via Whatsapp
        </button>
            <br>
                <h3>Dados do Cliente</h3>
                <p><strong>Nome:</strong> ${deliveryAddress.name}</p>
                <p><strong>Telefone:</strong> ${deliveryAddress.phone}</p>
                
                <h3>Endereço de Entrega</h3>
                <p>${deliveryAddress.street}, ${deliveryAddress.number} ${deliveryAddress.complement ? '(' + deliveryAddress.complement + ')' : ''}</p>
                <p>Bairro: ${deliveryAddress.neighborhood}</p>
                ${deliveryAddress.notes ? `<p><strong>Observações:</strong> ${deliveryAddress.notes}</p>` : ''}
                
                <h3>Itens do Pedido</h3>
                <ul>
            `;
            
            order.forEach(item => {
                receiptHTML += `<li>${item.name} - R$ ${item.price.toFixed(2)}</li>`;
            });
            
            receiptHTML += `
                </ul>
                <p><strong>Total: R$ ${total.toFixed(2)}</strong></p>
                <p>Pedido gerado em: ${new Date().toLocaleString()}</p>
            `;
            
            receiptContent.innerHTML = receiptHTML;
            receipt.style.display = 'block';
            
            // Mostra os botões de compartilhamento após gerar o recibo
            document.getElementById('copyBtn').style.display = 'flex';
            document.getElementById('shareBtn').style.display = 'flex';
            
            // Simula envio para a cozinha (automação)
            setTimeout(() => {
                alert('Pedido confirmado e enviado para a cozinha!');
            }, 1000);
        }
        
        // Função para copiar o pedido para a área de transferência
        function copyOrder() {
            let orderText = "📋 Pedido Lanchonete d,gust\n\n";
            orderText += "Itens do Pedido:\n";
            
            order.forEach(item => {
                orderText += `- ${item.name} - R$ ${item.price.toFixed(2)}\n`;
            });
            
            orderText += `\nTotal: R$ ${total.toFixed(2)}\n`;
            
            if (deliveryAddress.name) {
                orderText += `\nCliente: ${deliveryAddress.name}`;
                orderText += `\nTelefone: ${deliveryAddress.phone}`;
                orderText += `\nEndereço: ${deliveryAddress.street}, ${deliveryAddress.number}`;
                if (deliveryAddress.complement) {
                    orderText += ` (${deliveryAddress.complement})`;
                }
                orderText += `\nBairro: ${deliveryAddress.neighborhood}`;
                if (deliveryAddress.notes) {
                    orderText += `\nObservações: ${deliveryAddress.notes}`;
                }
            }
            
            navigator.clipboard.writeText(orderText).then(() => {
                alert('Pedido copiado para a área de transferência!');
            }).catch(err => {
                console.error('Erro ao copiar: ', err);
                // Fallback para navegadores mais antigos
                const textarea = document.createElement('textarea');
                textarea.value = orderText;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                alert('Pedido copiado para a área de transferência!');
            });
        }
        
        // Função para compartilhar no WhatsApp
        function shareOnWhatsApp() {
            let message = "🍔 Pedido Lanchonete d,gust\n\n";
            message += "Itens do Pedido:\n";
            
            order.forEach(item => {
                message += `- ${item.name} - R$ ${item.price.toFixed(2)}\n`;
            });
            
            message += `\nTotal: R$ ${total.toFixed(2)}\n`;
            
            if (deliveryAddress.name) {
                message += `\nCliente: ${deliveryAddress.name}`;
                message += `\nTelefone: ${deliveryAddress.phone}`;
                message += `\nEndereço: ${deliveryAddress.street}, ${deliveryAddress.number}`;
                if (deliveryAddress.complement) {
                    message += ` (${deliveryAddress.complement})`;
                }
                message += `\nBairro: ${deliveryAddress.neighborhood}`;
                if (deliveryAddress.notes) {
                    message += `\nObservações: ${deliveryAddress.notes}`;
                }
            }
            
            // Codifica a mensagem para URL
            const encodedMessage = encodeURIComponent(message);
            
            // Cria o link do WhatsApp
            const whatsappUrl = `https://wa.me/?text=${encodedMessage}`;
            
            // Abre em uma nova janela
            window.open(whatsappUrl, '_blank');
        }
    </script>
</body>
</html>
