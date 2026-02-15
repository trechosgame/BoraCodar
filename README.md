<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Carrinho - Oba Pizzaria</title>
  <meta name="description" content="Veja os itens no seu carrinho e finalize seu pedido agora!">

  <link rel="stylesheet" href="https://unicons.iconscout.com/release/v4.0.0/css/line.css">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    :root{--primary:#ff6b35;--dark:#222;--light:#fff;--gray:#666;--success:#28a745;--danger:#dc3545;--warning:#ffc107}
    *{margin:0;padding:0;box-sizing:border-box}
    body{font-family:'Poppins',sans-serif;background:#f9f9f9;color:var(--dark);line-height:1.6}
    .container{max-width:1100px;margin:0 auto;padding:0 15px}

    header{position:fixed;top:0;left:0;width:100%;background:rgba(255,255,255,0.95);backdrop-filter:blur(10px);box-shadow:0 2px 10px rgba(0,0,0,0.08);z-index:1000}
    .nav{display:flex;justify-content:space-between;align-items:center;padding:1rem 0}
    .logo{font-size:1.8rem;font-weight:700;color:var(--primary)}
    .menu-btn{display:none;flex-direction:column;gap:5px;width:35px;cursor:pointer}
    .menu-btn span{height:3px;background:var(--dark);transition:.4s}
    nav ul{display:flex;list-style:none;gap:1.5rem;align-items:center}
    nav a{color:var(--dark);text-decoration:none;font-weight:600}
    nav a:hover{color:var(--primary)}

    section{padding:100px 0 60px}
    h2{text-align:center;font-size:clamp(2rem,6vw,3.5rem);margin-bottom:2rem}

    .cart-empty{text-align:center;padding:4rem 0;font-size:1.3rem;color:var(--gray)}
    .cart-items{margin-bottom:3rem}
    .cart-item{display:flex;align-items:center;background:white;border-radius:12px;padding:1rem;margin-bottom:1rem;box-shadow:0 4px 12px rgba(0,0,0,0.08);gap:1rem}
    .cart-item img{width:80px;height:80px;object-fit:cover;border-radius:8px}
    .item-info{flex-grow:1}
    .item-info h4{margin-bottom:0.3rem;font-size:1.1rem}
    .item-info .price{color:var(--primary);font-weight:600}
    .quantity{display:flex;align-items:center;gap:0.8rem}
    .quantity button{width:32px;height:32px;border:1px solid #ddd;border-radius:50%;background:none;cursor:pointer;font-size:1.1rem}
    .quantity span{font-weight:600;min-width:30px;text-align:center}
    .remove-btn{background:none;border:none;color:var(--danger);font-size:1.4rem;cursor:pointer}

    .cart-summary{background:white;border-radius:12px;padding:1.5rem;box-shadow:0 4px 12px rgba(0,0,0,0.08)}
    .cart-summary h3{margin-bottom:1rem}
    .discount-row{margin:1rem 0;padding:0.8rem;background:#f8f9fa;border-radius:8px;display:flex;justify-content:space-between;align-items:center}
    .discount-info{color:var(--success);font-weight:600}
    .coupon-form{display:flex;gap:0.8rem;margin:1.5rem 0;flex-wrap:wrap}
    .coupon-form input{flex:1;padding:0.8rem;border:1px solid #ddd;border-radius:8px;font-size:1rem;min-width:180px}
    .coupon-form button{background:var(--primary);color:white;border:none;padding:0.8rem 1.5rem;border-radius:8px;cursor:pointer;font-weight:600}
    .coupon-form button:hover{background:#e55a2d}
    .coupon-message{font-size:0.9rem;margin-top:0.5rem}
    .coupon-message.success{color:var(--success)}
    .coupon-message.error{color:var(--danger)}
    .coupon-message.warning{color:var(--warning)}

    .total-row{display:flex;justify-content:space-between;font-size:1.6rem;font-weight:700;color:var(--primary);margin:1rem 0}
    .checkout-btn{background:var(--primary);color:white;border:none;padding:1rem 2rem;border-radius:50px;font-size:1.1rem;font-weight:600;cursor:pointer;margin-top:1.5rem;width:100%;max-width:300px}
    .checkout-btn:hover{background:#e55a2d}
    .clear-btn{background:var(--danger);color:white;border:none;padding:0.8rem 1.5rem;border-radius:50px;margin-top:1rem;cursor:pointer}

    footer{background:var(--dark);color:white;text-align:center;padding:3rem 0 1.5rem}
    .social a{color:white;font-size:1.8rem;margin:0 1rem}

    .whatsapp-float{position:fixed;bottom:20px;right:20px;z-index:9999}
    .whatsapp-float a{display:flex;align-items:center;justify-content:center;width:60px;height:60px;background:#25D366;color:white;border-radius:50%;font-size:2rem;box-shadow:0 4px 15px rgba(37,211,102,0.4);transition:.3s}
    .whatsapp-float a:hover{transform:scale(1.1)}

    @media (max-width:991px){
      .menu-btn{display:flex}
      nav ul{position:fixed;inset:0;background:rgba(255,255,255,0.98);backdrop-filter:blur(10px);flex-direction:column;justify-content:center;align-items:center;transform:translateY(-100%);transition:.4s;z-index:999}
      nav ul.active{transform:translateY(0)}
      .menu-btn.active span:nth-child(1){transform:rotate(45deg) translate(8px,8px)}
      .menu-btn.active span:nth-child(2){opacity:0}
      .menu-btn.active span:nth-child(3){transform:rotate(-45deg) translate(7px,-7px)}
      .cart-item{flex-direction:column;text-align:center}
      .cart-item img{width:120px;height:120px}
      .coupon-form{flex-direction:column}
    }

    @media (max-width:576px){
      section{padding:90px 0 40px}
    }
  </style>
</head>
<body>

<header>
  <div class="container">
    <div class="nav">
      <div class="logo">Oba Pizzaria</div>
      <button class="menu-btn"><span></span><span></span><span></span></button>
      <nav>
        <ul>
          <li><a href="index.html">Início</a></li>
          <li><a href="menu.html">Cardápio</a></li>
          <li><a href="about.html">Sobre</a></li>
          <li><a href="#">Reservas</a></li>
          <li><a href="carrinho.html">Carrinho <span id="cartCountHeader">0</span></a></li>
        </ul>
      </nav>
    </div>
  </div>
</header>

<section>
  <div class="container">
    <h2>Seu Carrinho</h2>

    <div class="cart-items" id="cartItems"></div>

    <div class="cart-empty" id="cartEmpty" style="display:none">
      <p>Seu carrinho está vazio.</p>
      <a href="menu.html" class="btn" style="background:var(--primary);color:white;padding:0.8rem 1.5rem;border-radius:50px;text-decoration:none;margin-top:1rem;display:inline-block">Voltar ao Cardápio</a>
    </div>

    <div class="cart-summary" id="cartSummary" style="display:none">
      <h3>Resumo do Pedido</h3>

      <!-- Área do cupom -->
      <div class="coupon-form">
        <input type="text" id="couponCode" placeholder="Digite o código do cupom" autocomplete="off">
        <button onclick="applyCoupon()">Aplicar Cupom</button>
      </div>
      <div id="couponMessage" class="coupon-message"></div>

      <div id="discountRow" class="discount-row" style="display:none">
        <span>Desconto aplicado:</span>
        <span id="discountValue" class="discount-info"></span>
      </div>

      <div class="total-row">
        <span>Total:</span>
        <span id="cartTotal">R$ 0,00</span>
      </div>

      <button class="checkout-btn" onclick="finalizeOrder()">Finalizar Pedido no WhatsApp</button>
      <button class="clear-btn" onclick="clearCart()">Limpar Carrinho</button>
    </div>
  </div>
</section>

<div class="whatsapp-float">
  <a href="https://wa.me/5514999993333?text=Olá!%20Quero%20fazer%20um%20pedido" target="_blank">
    <i class="uil uil-whatsapp"></i>
  </a>
</div>

<footer>
  <div class="container">
    <div class="social">
      <a href="#"><i class="uil uil-facebook-f"></i></a>
      <a href="#"><i class="uil uil-instagram"></i></a>
      <a href="#"><i class="uil uil-whatsapp"></i></a>
    </div>
    <p>© <script>document.write(new Date().getFullYear())</script> Oba Pizzaria - Bauru/SP</p>
  </div>
</footer>

<script>
// Configuração dos cupons válidos + data de expiração (YYYY-MM-DD)
const coupons = {
  '20OFF':    { type: 'percent', value: 20, expires: '2025-12-31' },
  '10REAL':   { type: 'fixed',   value: 10, expires: '2025-12-31' },
  'PRIMEIRA': { type: 'percent', value: 15, expires: '2025-06-30' },
  'OBAPIZZA': { type: 'fixed',   value: 8,  expires: '2025-03-31' },
  'QUINZENA': { type: 'percent', value: 10, expires: '2025-02-28' }
};

let cart = JSON.parse(localStorage.getItem('cart')) || [];
let appliedCoupon = localStorage.getItem('appliedCoupon') || null;

function isCouponValid(code) {
  const coupon = coupons[code];
  if (!coupon) return false;

  const today = new Date();
  const expiresDate = new Date(coupon.expires);
  return today <= expiresDate;
}

function updateCartDisplay() {
  const cartItemsDiv = document.getElementById('cartItems');
  const cartEmptyDiv = document.getElementById('cartEmpty');
  const cartSummaryDiv = document.getElementById('cartSummary');
  const cartCountHeader = document.getElementById('cartCountHeader');

  cartItemsDiv.innerHTML = '';
  let subtotal = 0;

  if (cart.length === 0) {
    cartItemsDiv.style.display = 'none';
    cartEmptyDiv.style.display = 'block';
    cartSummaryDiv.style.display = 'none';
    cartCountHeader.textContent = '0';
    resetCoupon();
    return;
  }

  cartEmptyDiv.style.display = 'none';
  cartItemsDiv.style.display = 'block';
  cartSummaryDiv.style.display = 'block';

  cart.forEach((item, index) => {
    const itemTotal = item.price * item.quantity;
    subtotal += itemTotal;

    const itemElement = document.createElement('div');
    itemElement.className = 'cart-item';
    itemElement.innerHTML = `
      <img src="imagens/placeholder.jpg" alt="${item.name}" loading="lazy">
      <div class="item-info">
        <h4>${item.name}</h4>
        <div class="price">R$ ${item.price.toFixed(2)}</div>
      </div>
      <div class="quantity">
        <button onclick="changeQuantity(${index}, -1)">–</button>
        <span>${item.quantity}</span>
        <button onclick="changeQuantity(${index}, 1)">+</button>
      </div>
      <div style="font-weight:600">R$ ${itemTotal.toFixed(2)}</div>
      <button class="remove-btn" onclick="removeItem(${index})">🗑️</button>
    `;
    cartItemsDiv.appendChild(itemElement);
  });

  applyCouponToTotal(subtotal);
  cartCountHeader.textContent = cart.reduce((sum, i) => sum + i.quantity, 0);
}

function applyCouponToTotal(subtotal) {
  let discount = 0;
  let discountText = '';

  if (appliedCoupon && isCouponValid(appliedCoupon)) {
    const coupon = coupons[appliedCoupon];
    if (coupon.type === 'percent') {
      discount = subtotal * (coupon.value / 100);
      discountText = `${coupon.value}% OFF (-R$ ${discount.toFixed(2)})`;
    } else if (coupon.type === 'fixed') {
      discount = coupon.value;
      discountText = `R$ ${coupon.value.toFixed(2)} OFF`;
    }
  } else if (appliedCoupon) {
    // Cupom expirado → limpa automaticamente
    resetCoupon();
  }

  const total = Math.max(0, subtotal - discount);

  document.getElementById('cartTotal').textContent = `R$ ${total.toFixed(2)}`;

  const discountRow = document.getElementById('discountRow');
  const discountValue = document.getElementById('discountValue');
  if (discount > 0) {
    discountRow.style.display = 'flex';
    discountValue.textContent = discountText;
  } else {
    discountRow.style.display = 'none';
  }
}

function applyCoupon() {
  const codeInput = document.getElementById('couponCode');
  const messageDiv = document.getElementById('couponMessage');
  const code = codeInput.value.trim().toUpperCase();

  messageDiv.className = 'coupon-message';
  messageDiv.textContent = '';

  if (!code) {
    messageDiv.classList.add('error');
    messageDiv.textContent = 'Digite um código válido.';
    return;
  }

  if (!coupons[code]) {
    messageDiv.classList.add('error');
    messageDiv.textContent = 'Cupom inválido.';
    return;
  }

  if (!isCouponValid(code)) {
    messageDiv.classList.add('warning');
    messageDiv.textContent = `O cupom ${code} expirou.`;
    return;
  }

  appliedCoupon = code;
  localStorage.setItem('appliedCoupon', code);
  messageDiv.classList.add('success');
  messageDiv.textContent = `Cupom ${code} aplicado com sucesso!`;

  updateCartDisplay();
  codeInput.value = '';
}

function resetCoupon() {
  appliedCoupon = null;
  localStorage.removeItem('appliedCoupon');
  document.getElementById('couponMessage').textContent = '';
  document.getElementById('discountRow').style.display = 'none';
}

function changeQuantity(index, delta) {
  cart[index].quantity += delta;
  if (cart[index].quantity <= 0) {
    cart.splice(index, 1);
  }
  localStorage.setItem('cart', JSON.stringify(cart));
  updateCartDisplay();
}

function removeItem(index) {
  cart.splice(index, 1);
  localStorage.setItem('cart', JSON.stringify(cart));
  updateCartDisplay();
}

function clearCart() {
  if (confirm('Tem certeza que deseja limpar todo o carrinho?')) {
    cart = [];
    localStorage.setItem('cart', JSON.stringify(cart));
    resetCoupon();
    updateCartDisplay();
  }
}

function finalizeOrder() {
  if (cart.length === 0) {
    alert('Seu carrinho está vazio!');
    return;
  }

  let message = 'Olá Oba Pizzaria! Quero fazer o seguinte pedido:\n\n';
  let subtotal = 0;
  let discount = 0;

  cart.forEach(item => {
    const itemTotal = item.price * item.quantity;
    message += `${item.quantity}x ${item.name} - R$ ${itemTotal.toFixed(2)}\n`;
    subtotal += itemTotal;
  });

  if (appliedCoupon && isCouponValid(appliedCoupon)) {
    const coupon = coupons[appliedCoupon];
    if (coupon.type === 'percent') {
      discount = subtotal * (coupon.value / 100);
      message += `\nCupom ${appliedCoupon}: ${coupon.value}% OFF (-R$ ${discount.toFixed(2)})\n`;
    } else {
      discount = coupon.value;
      message += `\nCupom ${appliedCoupon}: R$ ${coupon.value.toFixed(2)} OFF\n`;
    }
  }

  const total = Math.max(0, subtotal - discount);
  message += `\nSubtotal: R$ ${subtotal.toFixed(2)}`;
  if (discount > 0) message += `\nDesconto: -R$ ${discount.toFixed(2)}`;
  message += `\nTotal: R$ ${total.toFixed(2)}\n\nEndereço de entrega: [insira seu endereço]\nForma de pagamento: [escolha]`;

  const whatsappUrl = `https://wa.me/5514999993333?text=${encodeURIComponent(message)}`;
  window.open(whatsappUrl, '_blank');
}

// Inicialização
updateCartDisplay();

// Carregar cupom salvo (se existir e ainda válido)
const savedCoupon = localStorage.getItem('appliedCoupon');
if (savedCoupon && isCouponValid(savedCoupon)) {
  appliedCoupon = savedCoupon;
} else if (savedCoupon) {
  resetCoupon(); // Remove cupom expirado
}

// Menu mobile
document.querySelector('.menu-btn').onclick = () => {
  document.querySelector('.menu-btn').classList.toggle('active');
  document.querySelector('nav ul').classList.toggle('active');
};
</script>
</body>
</html>
