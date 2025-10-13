# MNM-Pulseras
Pulseras de lana hechas 100% a mano

<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tienda de Pulseras MNM</title>
<style>
body {
    margin:0;
    font-family:Arial,sans-serif;
    background: linear-gradient(to bottom,#a7c7e7,#b0d4f1,#c0e0fa); /* azul claro degradado */
    color:#333;
}
header {
    background-color: rgba(30,144,255,0.85); /* azul dodger semitransparente */
    padding:10px 20px;
    color:white;
    text-align:center;
}
.products {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:20px;
}
.product {
    background: rgba(240,248,255,0.95); /* azul muy claro */
    border-radius:8px;
    padding:15px;
    text-align:center;
    transition: transform 0.2s;
}
.product:hover {transform:translateY(-5px);}
.color-button {
    width:30px;
    height:30px;
    display:inline-block;
    margin:3px;
    border-radius:5px;
    border:1px solid #333;
    cursor:pointer;
}
.color-selected {border:3px solid #000;}
.product input[type="number"]{width:50px;padding:3px;margin-top:5px;}
.product button{
    margin-top:10px;
    padding:10px 15px;
    background-color:#87CEFA; /* azul claro botones */
    border:none;
    color:white;
    border-radius:5px;
    cursor:pointer;
    font-weight:bold;
    transition: background 0.3s, transform 0.2s;
}
.product button:hover{
    background-color:#00BFFF; /* azul más intenso al pasar */
    transform:scale(1.05);
}
#cart{
    position:fixed;
    top:10px;
    right:20px;
    background-color: rgba(30,144,255,0.85);
    color:white;
    padding:10px;
    border-radius:5px;
    cursor:pointer;
}
#cart-details{
    display:none;
    position:absolute;
    top:40px;
    right:0;
    background-color: rgba(30,144,255,0.9);
    padding:10px;
    border-radius:5px;
    width:300px;
    max-height:400px;
    overflow-y:auto;
    z-index:1000;
}
.cart-item{display:flex;justify-content:space-between;margin-bottom:5px;color:white;}
.cart-item button{background-color:red;padding:2px 6px;border-radius:3px;border:none;cursor:pointer;color:white;}
#popup{
    position: fixed;
    bottom:20px;
    right:20px;
    background-color:#87CEFA;
    color:white;
    padding:15px 20px;
    border-radius:8px;
    display:none;
    z-index:2000;
    animation: fadeInOut 2s forwards;
}
@keyframes fadeInOut{
    0%{opacity:0; transform:translateY(20px);}
    10%{opacity:1;transform:translateY(0);}
    90%{opacity:1;transform:translateY(0);}
    100%{opacity:0; transform:translateY(20px);}
}
#orders{background: rgba(240,248,255,0.9); margin:20px; padding:15px; border-radius:8px;}
#color-preview {margin-top:10px;}
</style>
</head>
<body>

<header>
<h1>Tienda de Pulseras Personalizadas M&M</h1>
<p>Elige tus colores favoritos y envía tu pedido por correo. </p>
<div id="cart" onmouseover="showCart()" onmouseleave="hideCart()">
    Carrito: <span id="cart-count">0</span>
    <div id="cart-details">
        <h3>Pedidos</h3>
        <div id="cart-items"></div>
    </div>
</div>
</header>

<div class="products" id="product-list">
<div class="product" data-name="Pulsera Personalizable">
    <h3>Pulsera Personalizable</h3>
    <p>Elige hasta 11 colores:</p>
    <div id="color-buttons">
        <div class="color-button" style="background:red;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:orange;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:yellow;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:#90ee90;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:green;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:#add8e6;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:blue;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:pink;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:purple;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:white; border:1px solid #ccc;" onclick="toggleColor(this)"></div>
        <div class="color-button" style="background:black;" onclick="toggleColor(this)"></div>
    </div>
    <div id="color-preview"></div>
    <label>Cantidad: <input type="number" id="quantity" min="1" value="1"></label><br>
    <button onclick="addToCart('Pulsera Personalizable')">Agregar al carrito</button>
    <button onclick="sendEmail()">📧 Enviar pedido por correo</button>
</div>
</div>

<div id="popup"></div>

<div id="orders">
<h3>Pedidos Recibidos</h3>
<div id="orders-list"></div>
</div>

<script>
let cart=[];
let selectedColors=[];

function toggleColor(element){
    const color = element.style.backgroundColor;
    if(selectedColors.includes(color)){
        selectedColors = selectedColors.filter(c=>c!==color);
        element.classList.remove('color-selected');
    } else if(selectedColors.length<11){
        selectedColors.push(color);
        element.classList.add('color-selected');
    } else {
        alert("Máximo 11 colores.");
    }
    updatePreview();
}

function updatePreview(){
    const previewDiv=document.getElementById('color-preview');
    previewDiv.innerHTML='';
    selectedColors.forEach(color=>{
        const rect=document.createElement('div');
        rect.className='color-button';
        rect.style.background=color;
        previewDiv.appendChild(rect);
    });
}

function addToCart(productName){
    if(selectedColors.length===0){
        alert("Selecciona al menos un color");
        return;
    }
    const quantity=parseInt(document.getElementById('quantity').value);
    cart.push({producto:productName,colores:[...selectedColors],cantidad:quantity});
    selectedColors=[];
    document.querySelectorAll('.color-button').forEach(b=>b.classList.remove('color-selected'));
    updatePreview();
    updateCart();
    showPopup(`${productName} (${quantity}) agregado al carrito!`);
}

function sendEmail(){
    if(selectedColors.length===0){
        alert("Selecciona al menos un color antes de enviar el pedido");
        return;
    }
    const quantity=parseInt(document.getElementById('quantity').value);
    const subject = encodeURIComponent("Pedido de pulsera personalizada");
    const body = encodeURIComponent(
        `Hola,\n\nQuisiera hacer el siguiente pedido:\n\nProducto: Pulsera Personalizable\nColores elegidos: ${selectedColors.join(", ")}\nCantidad: ${quantity}\n\nMétodo de pago: Efectivo al entregar\nGracias 💫`
    );
    const mailtoLink = `mailto:mnm1pulseras@gmail.com?subject=${subject}&body=${body}`;
    window.location.href = mailtoLink;
}

function updateCart(){
    document.getElementById('cart-count').textContent=cart.reduce((sum,item)=>sum+item.cantidad,0);
    const cartItems=document.getElementById('cart-items');
    cartItems.innerHTML='';
    cart.forEach((item,index)=>{
        const div=document.createElement('div');
        div.className='cart-item';
        div.innerHTML=`${item.producto} - Colores: ${item.colores.join(", ")} - Cantidad: ${item.cantidad} <button onclick="removeFromCart(${index})">X</button>`;
        cartItems.appendChild(div);
    });
    updateOrdersPanel();
}

function removeFromCart(index){ cart.splice(index,1); updateCart(); }
function showCart(){ document.getElementById('cart-details').style.display='block'; }
function hideCart(){ document.getElementById('cart-details').style.display='none'; }
function showPopup(msg){ const popup=document.getElementById('popup'); popup.textContent=msg; popup.style.display='block'; popup.style.animation='fadeInOut 2s forwards'; setTimeout(()=>popup.style.display='none',2000);}
function updateOrdersPanel(){
    const ordersDiv=document.getElementById('orders-list'); ordersDiv.innerHTML='';
    cart.forEach((item,index)=>{
        const div=document.createElement('div');
        div.textContent=`Pedido ${index+1}: ${item.producto} - Colores: ${item.colores.join(", ")} - Cantidad: ${item.cantidad}`;
        ordersDiv.appendChild(div);
    });
}
</script>

</body>
</html>
