# MNM-Pulseras
Pulseras de lana hechas 100% a mano


<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MNM-Pulseras | Pulseras de lana hechas a mano</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: linear-gradient(to bottom, #a7c7e7, #b0d4f1, #c0e0fa);
      color: #333;
    }

    /* --- Encabezado --- */
    header {
      background-color: #4da3ff;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 30px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      color: white;
    }

    .logo {
      font-size: 1.5rem;
      font-weight: bold;
      letter-spacing: 1px;
    }

    nav a {
      color: white;
      text-decoration: none;
      margin: 0 12px;
      font-weight: bold;
      transition: color 0.2s;
    }

    nav a:hover {
      color: #003f7d;
    }

    .carrito {
      background-color: #6bb8ff;
      padding: 6px 14px;
      border-radius: 8px;
      font-weight: bold;
    }

    /* --- Contenido principal --- */
    main {
      text-align: center;
      padding: 30px;
    }

    h1 {
      font-size: 2rem;
      color: #2a4d75;
    }

    .pulsera-box {
      background-color: rgba(255,255,255,0.7);
      border-radius: 15px;
      padding: 20px;
      width: 90%;
      max-width: 500px;
      margin: 20px auto;
      box-shadow: 0 3px 6px rgba(0,0,0,0.1);
    }

    .colores {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      margin: 15px 0;
    }

    .color {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      margin: 5px;
      border: 2px solid #fff;
      cursor: pointer;
    }

    .color.seleccionado {
      border: 3px solid #222;
    }

    button {
      background-color: #5aaaff;
      border: none;
      color: white;
      padding: 10px 15px;
      margin: 5px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      transition: background-color 0.2s;
    }

    button:hover {
      background-color: #0074cc;
    }
  </style>
</head>
<body>

  <header>
    <div class="logo">🧶 MNM-Pulseras</div>
    <nav>
      <a href="#">Inicio</a>
      <a href="#">Tienda</a>
      <a href="#">Contacto</a>
    </nav>
    <div class="carrito">Carrito: 0</div>
  </header>

  <main>
    <h1>MNM Pulseras</h1>
    <p>Elige tus colores favoritos y envía tu pedido por correo.</p>

    <div class="pulsera-box">
      <h2>Pulsera Personalizable</h2>
      <p>Elige hasta 11 colores:</p>
      <div class="colores">
        <div class="color" style="background-color:#ff0000;"></div>
        <div class="color" style="background-color:#ff7f00;"></

