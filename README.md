# BADDIECLOSET
sklep z elegancką odzieżą w stylu lat 2000
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">

<!-- SEO DLA GOOGLE -->
<title>BADDIE CLOSET – Modny Sklep Odzieżowy Online</title>
<meta name="description" content="BADDIE CLOSET – sklep z modnymi topami, sukienkami, bluzkami i dodatkami. Najnowsze trendy, najlepsze ceny, szybkie zakupy. Sprawdź nowości!">
<meta name="keywords" content="baddie closet, sklep odzieżowy, topy, bluzki, sukienki, moda, butik online, ubrania dla dziewczyn, najnowsze trendy">
<meta name="author" content="Baddie Closet">
<meta name="robots" content="index, follow">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body {
        margin: 0;
        font-family: "Georgia", serif;

        /* TŁO NA CAŁYM EKRANIE */
        background-image: url("DIVA2.jpg");
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
        background-attachment: fixed;
    }

    header {
        text-align: center;
        padding: 20px;
        font-size: 40px;
        font-weight: bold;
        color: #ffffff;
        text-shadow: 1px 1px 6px black;
        background-color: rgba(196, 90, 123, 0.55);
    }

    #menu {
        width: 220px;
        background-color: rgba(243, 200, 213, 0.92);
        padding: 20px;
        font-size: 20px;
        height: 100vh;
        box-shadow: 2px 0 8px rgba(0,0,0,0.1);
        position: fixed;
        top: 0;
        left: 0;
        padding-top: 120px;
    }
    #menu a {
        display: block;
        margin-bottom: 15px;
        text-decoration: none;
        color: #8a3555;
        font-weight: bold;
        cursor: pointer;
    }

    #content {
        margin-left: 260px;
        padding: 30px;
        background-color: rgba(255,255,255,0.6);
        min-height: 100vh;
    }

    #cartIcon {
        position: fixed;
        right: 20px;
        top: 20px;
        font-size: 40px;
        cursor: pointer;
    }

    #cart {
        position: fixed;
        right: 20px;
        top: 80px;
        width: 260px;
        background-color: #ffe6ef;
        padding: 15px;
        border-radius: 10px;
        display: none;
        box-shadow: 0 0 10px #c45a7b;
    }

    .product {
        width: 250px;
        padding: 20px;
        background: white;
        border-radius: 10px;
        box-shadow: 0 0 10px #d59cb0;
        cursor: pointer;
        margin-bottom: 20px;
    }
    .product img {
        width: 100%;
        border-radius: 10px;
    }

    .gallery {
        display: flex;
        gap: 10px;
        overflow-x: auto;
        padding-bottom: 10px;
    }
    .gallery img {
        width: 200px;
        border-radius: 10px;
    }

    #orderForm {
        display: none;
        background: #fff0f6;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px #c45a7b;
        margin-top: 20px;
    }

    input, select {
        width: 95%;
        padding: 8px;
        margin: 6px 0;
        border-radius: 5px;
        border: 1px solid #c45a7b;
    }

    button {
        padding: 10px 20px;
        background-color: #c45a7b;
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        font-size: 18px;
    }
</style>
</head>

<body>

<header>🌸 BADDIE CLOSET – Zapraszamy na zakupy! 🌸</header>

<div id="menu">
    <a onclick="showHome()">Strona główna</a>
    <a onclick="showProducts()">Wszystkie ubrania</a>
    <a onclick="showProducts()">Topy</a>
    <a>Sukienki</a>
    <a>Spódnice</a>
    <a>Koszule</a>
    <a>Jeansy</a>
    <a>Bluzy</a>
    <a>Dresy</a>
    <a>Dodatki</a>
    <a>Promocje</a>
</div>

<div id="cartIcon" onclick="toggleCart()">🛒</div>

<div id="cart">
    <h3>Twój koszyk</h3>
    <div id="cartItems"></div>
    <button onclick="showOrderForm()">Zamów</button>
</div>

<div id="content">

    <div id="home">
        <h2>Witamy w BADDIE CLOSET 💗</h2>
        <p>Najmodniejsze ubrania dla dziewczyn z klasą!</p>
    </div>

    <div id="products" style="display:none;">
        <h2>Wszystkie ubrania</h2>

        <div class="product" onclick="openProduct()">
            <img src="bluzkaróżowa.jpg">
            <h3>Bluzka w kwiatki – 50 zł</h3>
        </div>
    </div>

    <div id="productPage" style="display:none;">
        <h2>Bluzka w kwiatki – 50 zł</h2>

        <p><b>Kolor:</b></p>
        <select id="color" onchange="updateGallery()">
            <option value="roz">Różowy</option>
            <option value="nieb">Niebieski</option>
        </select>

        <p><b>Rozmiar:</b></p>
        <select id="size">
            <option>XS</option>
            <option>S</option>
            <option>M</option>
            <option>L</option>
            <option>XL</option>
        </select>

        <div class="gallery" id="gallery"></div>

        <button onclick="addToCart()">Dodaj do koszyka</button>
    </div>

    <div id="orderForm">
        <h2>Złóż zamówienie</h2>
        <input placeholder="Imię">
        <input placeholder="Nazwisko">
        <input placeholder="Numer telefonu">
        <input placeholder="Miasto">
        <input placeholder="Województwo">
        <input placeholder="Adres">
        <input placeholder="Kod pocztowy">

        <p><b>Płatność:</b></p>
        <select>
            <option>BLIK</option>
        </select>

        <button onclick="alert('Dziękujemy za zamówienie!')">Potwierdź</button>
    </div>

</div>

<script>
/* Przełączanie koszyka */
let cartOpen = false;
function toggleCart() {
    cartOpen = !cartOpen;
    document.getElementById("cart").style.display = cartOpen ? "block" : "none";
}

function showHome() {
    document.getElementById("home").style.display = "block";
    document.getElementById("products").style.display = "none";
    document.getElementById("productPage").style.display = "none";
}

function showProducts() {
    document.getElementById("home").style.display = "none";
    document.getElementById("products").style.display = "block";
    document.getElementById("productPage").style.display = "none";
}

function openProduct() {
    document.getElementById("home").style.display = "none";
    document.getElementById("products").style.display = "none";
    document.getElementById("productPage").style.display = "block";
    updateGallery();
}

/* Galeria zdjęć */
function updateGallery() {
    const color = document.getElementById("color").value;
    let gallery = document.getElementById("gallery");
    gallery.innerHTML = "";

    let files = [];

    if (color === "roz") {
        files = ["bluzkaróżowa.jpg","bluzkaróżowa2.jpg","bluzkaróżowa3.jpg","bluzkaróżowa4.jpg"];
    } else {
        files = ["bluzkaniebieska.jpg","bluzkaniebieska2.jpg","bluzkaniebieska3.jpg","bluzkaniebieska4.jpg"];
    }

    files.forEach(f => {
        let img = document.createElement("img");
        img.src = f;
        gallery.appendChild(img);
    });
}

/* Koszyk */
function addToCart() {
    let color = document.getElementById("color").value === "roz" ? "różowy" : "niebieski";
    let size = document.getElementById("size").value;

    let item = document.createElement("p");
    item.innerText = "Bluzka w kwiatki – kolor: " + color + ", rozmiar: " + size + ", 50 zł";

    document.getElementById("cartItems").appendChild(item);
    alert("Dodano do koszyka!");
}

function showOrderForm() {
    document.getElementById("orderForm").style.display = "block";
    document.getElementById("productPage").style.display = "none";
}
</script>

</body>
</html>
