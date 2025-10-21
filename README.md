# Ragazza-Boutique
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tienda Juvenil de Moda</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* Reset básico y tipografía */
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Roboto', sans-serif; }
        body { background-color: #f7f7f7; color: #333; }
        a { text-decoration: none; color: inherit; }
        header, footer { background-color: #fff; padding: 20px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        nav ul { display: flex; list-style: none; gap: 20px; }
        nav ul li { display: inline; }
        .container { width: 90%; max-width: 1200px; margin: auto; }
        h1, h2, h3 { margin-bottom: 15px; }
        button { cursor: pointer; padding: 10px 20px; border: none; background-color: #333; color: #fff; border-radius: 5px; transition: 0.3s; }
        button:hover { background-color: #555; }

        /* Banner principal */
        .banner { background-image: url('https://source.unsplash.com/1200x400/?fashion,clothes'); background-size: cover; background-position: center; height: 400px; display: flex; align-items: center; justify-content: center; color: #fff; font-size: 2rem; font-weight: bold; text-shadow: 1px 1px 5px rgba(0,0,0,0.5); margin-bottom: 30px; }

        /* Productos */
        .products { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 40px; }
        .product { background-color: #fff; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); text-align: center; }
        .product img { width: 100%; border-radius: 10px; }
        .product h3 { margin: 10px 0; }
        .product p { margin: 5px 0; }
        .product button { margin-top: 10px; }

        /* Carrito */
        .cart { position: fixed; right: 20px; top: 80px; width: 300px; background-color: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.2); }
        .cart h3 { margin-bottom: 15px; }
        .cart ul { list-style: none; max-height: 300px; overflow-y: auto; margin-bottom: 10px; }
        .cart ul li { display: flex; justify-content: space-between; margin-bottom: 10px; }
        .cart button { width: 100%; }

        /* Contacto */
        form { display: flex; flex-direction: column; gap: 15px; margin-bottom: 40px; }
        input, textarea { padding: 10px; border: 1px solid #ccc; border-radius: 5px; }
        textarea { resize: vertical; }

        /* Footer */
        footer { text-align: center; margin-top: 40px; }
    </style>
</head>
<body>

<header>
    <div class="container">
        <h1>Tienda Juvenil de Moda</h1>
        <nav>
            <ul>
                <li><a href="#home">Inicio</a></li>
                <li><a href="#products">Catálogo</a></li>
                <li><a href="#contact">Contacto</a></li>
            </ul>
        </nav>
    </div>
</header>

<section id="home" class="banner">
    ¡Descubre la moda juvenil que te define!
</section>

<section id="products" class="container">
    <h2>Productos Destacados</h2>
    <div class="products">
        <div class="product">
            <img src="https://source.unsplash.com/400x400/?tshirt,teen" alt="Producto 1">
            <h3>Playera Urbana</h3>
            <p>Tallas: S, M, L</p>
            <p>Colores: Blanco, Negro, Azul</p>
            <p>Precio: $350 MXN</p>
            <button onclick="addToCart('Playera Urbana', 350)">Agregar al carrito</button>
        </div>
        <div class="product">
            <img src="https://source.unsplash.com/400x400/?hoodie,teen" alt="Producto 2">
            <h3>Sudadera Juvenil</h3>
            <p>Tallas: S, M, L</p>
            <p>Colores: Gris, Negro</p>
            <p>Precio: $550 MXN</p>
            <button onclick="addToCart('Sudadera Juvenil', 550)">Agregar al carrito</button>
        </div>
        <!-- Agregar más productos aquí -->
    </div>
</section>

<div class="cart">
    <h3>Carrito</h3>
    <ul id="cart-items"></ul>
    <p>Total: $<span id="cart-total">0</span> MXN</p>
    <button onclick="checkout()">Ir al Pago</button>
</div>

<section id="contact" class="container">
    <h2>Contacto</h2>
    <form id="contact-form">
        <input type="text" placeholder="Nombre" required>
        <input type="email" placeholder="Correo" required>
        <textarea placeholder="Mensaje" rows="5" required></textarea>
        <button type="submit">Enviar</button>
    </form>
</section>

<footer>
    &copy; 2025 Tienda Juvenil de Moda. Todos los derechos reservados.
</footer>

<script>
    // Carrito de compras simple
    let cart = [];
    function addToCart(name, price) {
        cart.push({name, price});
        renderCart();
    }

    function renderCart() {
        const cartItems = document.getElementById('cart-items');
        const cartTotal = document.getElementById('cart-total');
        cartItems.innerHTML = '';
        let total = 0;
        cart.forEach((item, index) => {
            const li = document.createElement('li');
            li.textContent = item.name + " - $" + item.price;
            const removeBtn = document.createElement('button');
            removeBtn.textContent = 'Eliminar';
            removeBtn.style.padding = '2px 5px';
            removeBtn.style.fontSize = '0.8rem';
            removeBtn.onclick = () => { cart.splice(index,1); renderCart(); };
            li.appendChild(removeBtn);
            cartItems.appendChild(li);
            total += item.price;
        });
        cartTotal.textContent = total;
    }

    function checkout() {
        if(cart.length === 0) {
            alert('El carrito está vacío.');
            return;
        }
        alert('Redirigiendo al pago...');
        // Aquí se integraría la pasarela de pago real
    }

    // Formulario de contacto
    document.getElementById('contact-form').addEventListener('submit', function(e) {
        e.preventDefault();
        alert('Gracias por contactarnos. Te responderemos pronto.');
        this.reset();
    });
</script>

</body>
</html>
