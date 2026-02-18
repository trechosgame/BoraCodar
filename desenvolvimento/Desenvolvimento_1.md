# 01 - Página Principal (app.html) 

## Criar o app.html
~~~
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Oba Pizzaria - Pizzas e Delivery em Bauru</title>
  <meta name="description" content="Oba Pizzaria – Pizzas artesanais, massas, lanches e bebidas em Bauru-SP. Promoções diárias e ambiente familiar. Peça agora!">

  <link rel="stylesheet" href="https://unicons.iconscout.com/release/v4.0.0/css/line.css">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --primary: #ff6b35;
      --dark: #222;
      --light: #fff;
      --gray: #666;
    }
    * { margin:0; padding:0; box-sizing:border-box; }
    body { font-family:'Poppins',sans-serif; background:#f9f9f9; color:var(--dark); line-height:1.6; }
    .container { max-width:1400px; margin:0 auto; padding:0 15px; }

    /* Header */
    header {
      position:fixed; top:0; left:0; width:100%; z-index:1000;
      background:rgba(255,255,255,0.95); backdrop-filter:blur(10px);
      box-shadow:0 2px 10px rgba(0,0,0,0.08);
    }
    .nav { display:flex; justify-content:space-between; align-items:center; padding:1rem 0; }
    .logo { font-size:1.8rem; font-weight:700; color:var(--primary); }
    .menu-btn { display:none; flex-direction:column; gap:5px; width:35px; cursor:pointer; }
    .menu-btn span { height:3px; background:var(--dark); transition:.4s; }
    nav ul { display:flex; list-style:none; gap:1.5rem; }
    nav a { color:var(--dark); text-decoration:none; font-weight:600; }
    nav a:hover { color:var(--primary); }

    /* Hero */
    .hero { min-height:80vh; background:linear-gradient(rgba(0,0,0,0.5),rgba(0,0,0,0.3)),url('imagens/bg.jpg') center/cover fixed; color:white; display:flex; align-items:center; text-align:center; padding-top:80px; }
    .hero h1 { font-size:clamp(2.5rem,10vw,5rem); margin-bottom:1.5rem; }

    .btn { display:inline-block; padding:0.9rem 2rem; background:var(--primary); color:white; border-radius:50px; text-decoration:none; font-weight:600; transition:.3s; }
    .btn:hover { background:#e55a2d; transform:translateY(-3px); }

    /* Ofertas */
    .offers { padding:80px 0; display:grid; grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); gap:2rem; }
    .offer-card { background:white; border-radius:12px; overflow:hidden; box-shadow:0 4px 15px rgba(0,0,0,0.08); transition:.3s; }
    .offer-card:hover { transform:translateY(-8px); }
    .offer-card img { width:100%; height:200px; object-fit:cover; }
    .offer-body { padding:1.5rem; text-align:center; }
    .offer-body h5 { font-size:1.4rem; margin-bottom:0.5rem; }
    .offer-body .desconto { font-size:2.2rem; color:var(--primary); font-weight:700; }

    /* Cardápio */
    .food_section { padding:80px 0; background:white; }
    .filters_menu { display:flex; justify-content:center; flex-wrap:wrap; gap:1rem; margin:2rem 0; list-style:none; }
    .filters_menu li { padding:0.6rem 1.3rem; border-radius:50px; background:#eee; cursor:pointer; transition:.3s; }
    .filters_menu li.active, .filters_menu li:hover { background:var(--primary); color:white; }
    .menu-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:1.8rem; }
    .menu-item { background:white; border-radius:12px; overflow:hidden; box-shadow:0 4px 12px rgba(0,0,0,0.08); transition:.3s; }
    .menu-item:hover { transform:translateY(-6px); }
    .menu-item img { width:100%; height:180px; object-fit:cover; }
    .menu-body { padding:1.2rem; text-align:center; }
    .menu-body .preco { color:var(--primary); font-weight:700; font-size:1.3rem; }

    /* Footer */
    footer { background:var(--dark); color:white; text-align:center; padding:3rem 0 1.5rem; }
    .social a { color:white; font-size:1.8rem; margin:0 1rem; }

    /* WhatsApp flutuante */
    .whatsapp-float { position:fixed; bottom:20px; right:20px; z-index:9999; }
    .whatsapp-float a { display:flex; align-items:center; justify-content:center; width:60px; height:60px; background:#25D366; color:white; border-radius:50%; font-size:2rem; box-shadow:0 4px 15px rgba(37,211,102,0.4); transition:.3s; }
    .whatsapp-float a:hover { transform:scale(1.1); }

    /* Mobile */
    @media (max-width:991px){
      .menu-btn{display:flex}
      nav ul{position:fixed;inset:0;background:rgba(255,255,255,0.98);backdrop-filter:blur(10px);flex-direction:column;justify-content:center;align-items:center;transform:translateY(-100%);transition:.4s;z-index:999}
      nav ul.active{transform:translateY(0)}
      .menu-btn.active span:nth-child(1){transform:rotate(45deg) translate(8px,8px)}
      .menu-btn.active span:nth-child(2){opacity:0}
      .menu-btn.active span:nth-child(3){transform:rotate(-45deg) translate(7px,-7px)}
      .about-grid{grid-template-columns:1fr}
    }

    @media (max-width:576px){
      .hero{padding-top:100px;min-height:70vh}
      .hero h1{font-size:2.8rem}
      section{padding:50px 0}
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
          <li><a href="#">Início</a></li>
          <li><a href="#">Cardápio</a></li>
          <li><a href="#">Sobre</a></li>
          <li><a href="#">Reservas</a></li>
        </ul>
      </nav>
    </div>
  </div>
</header>

<section class="hero">
  <div class="container">
    <h1>Bem-vindo à Oba Pizzaria</h1>
    <a href="#" class="btn">Ver Cardápio</a>
  </div>
</section>

<section class="offer_section">
  <div class="container">
    <div class="offers">
      <div class="offer-card">
        <img src="imagens/o1.jpg" alt="Tasty Thursdays" loading="lazy">
        <div class="offer-body">
          <h5>Tasty Thursdays</h5>
          <div class="desconto">20% OFF</div>
          <a href="#" class="btn">Peçar Agora</a>
        </div>
      </div>
      <div class="offer-card">
        <img src="imagens/o2.jpg" alt="Pizza Days" loading="lazy">
        <div class="offer-body">
          <h5>Pizza Days</h5>
          <div class="desconto">15% OFF</div>
          <a href="#" class="btn">Peçar Agora</a>
        </div>
      </div>
    </div>
  </div>
</section>

<section class="food_section">
  <div class="container">
    <h2>Nosso Cardápio</h2>
    <ul class="menu-filters">
      <li class="active">Todos</li>
      <li>Pizzas</li>
      <li>Massas</li>
      <li>Lanches</li>
      <li>Bebidas</li>
    </ul>
    <div class="menu-grid">
      <div class="menu-item">
        <img src="imagens/f1.png" alt="Massa" loading="lazy">
        <div class="menu-body">
          <h5>Massa Especial</h5>
          <div class="preco">R$ 20,00</div>
        </div>
      </div>
      <!-- Adicione mais itens aqui -->
    </div>
  </div>
</section>

<section class="about">
  <div class="container">
    <div class="about-grid">
      <img src="imagens/about-img.png" alt="Sobre a Oba Pizzaria" loading="lazy">
      <div>
        <h2>A Oba Pizzaria</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
        <a href="#" class="btn mt-3">+ Saiba Mais</a>
      </div>
    </div>
  </div>
</section>

<section class="book">
  <div class="container">
    <h2>Faça sua Reserva</h2>
    <form class="book-form">
      <input class="form-control" placeholder="Nome" required>
      <input class="form-control" placeholder="Contato / WhatsApp" required>
      <input class="form-control" type="email" placeholder="Email" required>
      <select class="form-control">
        <option>Mesa para quantos?</option>
        <option>2 pessoas</option>
        <option>3 pessoas</option>
        <option>4 pessoas</option>
        <option>5+ pessoas</option>
      </select>
      <input class="form-control" type="date" required>
      <button class="btn">Reservar Agora</button>
    </form>
  </div>
</section>

<div class="whatsapp-float">
  <a href="https://wa.me/5514999993333?text=Olá!%20Quero%20fazer%20um%20pedido%20na%20Oba%20Pizzaria" target="_blank">
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
  document.querySelector('.menu-btn').onclick = () => {
    document.querySelector('.menu-btn').classList.toggle('active');
    document.querySelector('nav ul').classList.toggle('active');
  };
</script>
</body>
</html>
            
          


~~~html


