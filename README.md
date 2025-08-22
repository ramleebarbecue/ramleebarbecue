<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Ramlee Barbecue — Order Online</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #fafafa;
      color: #333;
    }
    header {
      background: #111;
      color: #fff;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    header h1 {
      margin: 0;
    }
    nav a {
      color: #fff;
      margin-left: 1rem;
      text-decoration: none;
    }
    .container {
      width: 90%;
      max-width: 900px;
      margin: 2rem auto;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1rem;
    }
    .card {
      background: #fff;
      border-radius: 8px;
      padding: 1rem;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
    }
    button {
      padding: 0.5rem 1rem;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 0.5rem;
    }
    button:hover {
      background: #218838;
    }
    .cart-section {
      margin-top: 2rem;
      padding: 1rem;
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .cart-item {
      margin: 0.5rem 0;
    }
    .error {
      color: red;
      margin-top: 1rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>Ramlee Barbecue</h1>
    <nav>
      <a href="#menu">Menu</a>
      <a href="#cart">Cart</a>
    </nav>
  </header>

  <main class="container">
    <!-- Menu Section -->
    <section id="menu">
      <h2>Our Menu</h2>
      <div id="menuList" class="grid"></div>
    </section>

    <!-- Cart Section -->
    <section id="cart" class="cart-section">
      <h2>Your Cart</h2>
      <div id="cartItems"></div>
      <p id="cartTotal"></p>

      <h3>Customer Details</h3>
      <form id="checkoutForm">
        <label>Name:<br><input type="text" id="custName" required></label><br><br>
        <label>Phone:<br><input type="text" id="custPhone" required></label><br><br>
        <label>Pickup Time:<br><input type="time" id="pickupTime" required></label><br><br>
        <button type="submit">Checkout via WhatsApp</button>
      </form>
      <p id="error" class="error"></p>
    </section>
  </main>

  <script>
    // === CONFIG ===
    const WHATSAPP_NUMBER = "6738121098"; // change to your number

    // === MENU DATA ===
    const menuItems = [
      { id: 1, name: "Chicken BBQ", price: 5.00 },
      { id: 2, name: "Beef BBQ", price: 6.50 },
      { id: 3, name: "Nasi Lemak", price: 3.00 },
      { id: 4, name: "Teh Tarik", price: 1.50 },
    ];

    // === CART LOGIC ===
    let cart = [];

    function addToCart(id, name, price) {
      let existing = cart.find(item => item.id === id);
      if (existing) {
        existing.qty++;
      } else {
        cart.push({ id, name, price, qty: 1 });
      }
      renderCart();
    }

    function renderMenu() {
      const menuContainer = document.getElementById("menuList");
      menuItems.forEach(item => {
        const div = document.createElement("div");
        div.classList.add("card");
        div.innerHTML = `
          <h3>${item.name}</h3>
          <p>BND ${item.price.toFixed(2)}</p>
          <button onclick="addToCart(${item.id}, '${item.name}', ${item.price})">
            Add to Cart
          </button>
        `;
        menuContainer.appendChild(div);
      });
    }

    function renderCart() {
      const cartDiv = document.getElementById("cartItems");
      const totalP = document.getElementById("cartTotal");
      cartDiv.innerHTML = "";
      let total = 0;

      if (cart.length === 0) {
        cartDiv.innerHTML = "<p>Your cart is empty.</p>";
        totalP.textContent = "";
        return;
      }

      cart.forEach(item => {
        const line = document.createElement("div");
        line.classList.add("cart-item");
        line.textContent = `${item.qty} × ${item.name} — BND ${(item.qty * item.price).toFixed(2)}`;
        cartDiv.appendChild(line);
        total += item.qty * item.price;
      });

      totalP.textContent = `Total: BND ${total.toFixed(2)}`;
    }

    // === CHECKOUT ===
    document.addEventListener("DOMContentLoaded", () => {
      renderMenu();
      renderCart();

      const form = document.getElementById("checkoutForm");
      form.addEventListener("submit", e => {
        e.preventDefault();
        let name = document.getElementById("custName").value.trim();
        let phone = document.getElementById("custPhone").value.trim();
        let time = document.getElementById("pickupTime").value;

        if (!name || !phone || !time || cart.length === 0) {
          document.getElementById("error").textContent = "Please complete all fields and add items to cart.";
          return;
        }

        let msg = `New Order:%0AName: ${name}%0APhone: ${phone}%0APickup: ${time}%0A%0AItems:%0A`;
        cart.forEach(item => {
          msg += `${item.qty} × ${item.name} — BND ${(item.qty * item.price).toFixed(2)}%0A`;
        });

        let total = cart.reduce((sum, i) => sum + i.qty * i.price, 0);
        msg += `%0ATotal: BND ${total.toFixed(2)}`;

        let url = `https://wa.me/${WHATSAPP_NUMBER}?text=${msg}`;
        window.location.href = url;
      });
    });
  </script>
</body>
</html>


<!--
**ramleebarbecue/ramleebarbecue** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
