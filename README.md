<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Daraz Clone</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
  <script src="https://js.stripe.com/v3/"></script>

  <style>
    /* Global Styles */
    body, html {
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
      box-sizing: border-box;
    }

    /* Header */
    header {
      background-color: #0077b6;
      color: white;
      padding: 10px 20px;
      position: sticky;
      top: 0;
      z-index: 100;
    }

    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .logo {
      font-size: 24px;
      font-weight: 600;
      letter-spacing: 1px;
    }

    .nav-links {
      display: flex;
      gap: 20px;
    }

    .nav-links li {
      list-style-type: none;
    }

    .nav-links a {
      color: white;
      text-decoration: none;
      font-weight: 500;
      transition: color 0.3s ease;
    }

    .nav-links a:hover {
      color: #ffdd57;
    }

    .menu-toggle {
      display: none;
      font-size: 28px;
      cursor: pointer;
      color: white;
    }

    /* Main Banner */
    .main-banner {
      position: relative;
      width: 100%;
      height: 300px;
      overflow: hidden;
    }

    .main-banner img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .banner-text {
      position: absolute;
      bottom: 20px;
      left: 20px;
      color: white;
      font-size: 32px;
      font-weight: 600;
      text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.5);
    }

    .banner-text h1 {
      margin: 0;
      font-size: 48px;
    }

    .banner-text p {
      font-size: 20px;
      margin-bottom: 20px;
    }

    .btn {
      padding: 10px 20px;
      background-color: #ffdd57;
      color: #0077b6;
      border: none;
      font-weight: 600;
      cursor: pointer;
      border-radius: 5px;
      transition: background-color 0.3s ease;
    }

    .btn:hover {
      background-color: #f1c40f;
    }

    /* Product Grid */
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 20px;
      padding: 20px;
    }

    .product {
      background-color: white;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
      text-align: center;
      transition: transform 0.3s ease;
    }

    .product:hover {
      transform: translateY(-5px);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    }

    .product img {
      max-width: 100%;
      height: auto;
      border-radius: 8px;
    }

    .product h3 {
      font-size: 20px;
      margin: 10px 0;
      font-weight: 600;
    }

    .product p {
      font-size: 18px;
      color: #555;
    }

    /* Cart */
    .cart {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background-color: #ffdd57;
      padding: 15px;
      border-radius: 50%;
      cursor: pointer;
      color: #0077b6;
      font-size: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    }

    .cart-items-count {
      background-color: #0077b6;
      color: white;
      border-radius: 50%;
      padding: 5px 10px;
      margin-left: 10px;
      font-weight: 600;
    }

    /* Cart Modal */
    .cart-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
      z-index: 200;
    }

    .cart-modal.show {
      display: flex;
    }

    .cart-modal-content {
      background-color: white;
      padding: 20px;
      border-radius: 8px;
      width: 400px;
      max-height: 80%;
      overflow-y: auto;
    }

    .cart-modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .cart-modal-header h2 {
      font-size: 24px;
    }

    .close-cart-modal {
      font-size: 24px;
      cursor: pointer;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 10px;
      padding: 10px;
      background-color: #f9f9f9;
      border-radius: 5px;
    }

    .cart-item button {
      background-color: #ff5c57;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 5px;
      cursor: pointer;
    }

    .cart-item button:hover {
      background-color: #e74c3c;
    }

    /* Footer */
    footer {
      background-color: #0077b6;
      color: white;
      padding: 20px 0;
      text-align: center;
    }

    footer a {
      color: white;
      text-decoration: none;
      margin: 0 10px;
      font-weight: 500;
      transition: color 0.3s ease;
    }

    footer a:hover {
      color: #ffdd57;
    }

    /* Login Modal */
    .login-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
      z-index: 300;
    }

    .login-modal-content {
      background-color: white;
      padding: 30px;
      border-radius: 8px;
      width: 400px;
    }

    .login-modal h2 {
      margin-bottom: 20px;
      font-size: 24px;
    }

    .login-modal input {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: 1px solid #ddd;
    }

    .login-modal button {
      width: 100%;
      padding: 10px;
      background-color: #0077b6;
      color: white;
      font-weight: 600;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .login-modal button:hover {
      background-color: #005f8c;
    }
  </style>
</head>

<body>

  <!-- Header Section -->
  <header id="header">
    <div class="navbar">
      <div class="logo">Daraz Clone</div>
      <ul class="nav-links">
        <li><a href="#" id="homeBtn">Home</a></li>
        <li><a href="#" id="shopBtn">Shop</a></li>
        <li><a href="#" id="categoriesBtn">Categories</a></li>
        <li><a href="#" id="cartBtn">Cart</a></li>
        <li><a href="#" id="loginBtn">Login</a></li>
      </ul>
      <div class="menu-toggle" id="menuToggle"><i class="fas fa-bars"></i></div>
    </div>
  </header>

  <!-- Login Modal -->
  <div class="login-modal" id="loginModal">
    <div class="login-modal-content">
      <h2>Login</h2>
      <input type="text" id="username" placeholder="Username" required>
      <input type="password" id="password" placeholder="Password" required>
      <button class="btn" id="loginSubmit">Login</button>
      <button class="btn" id="closeLoginModal">Close</button>
    </div>
  </div>
  <!-- Cart Modal -->
<div class="cart-modal" id="cartModal">
  <div class="cart-modal-content">
    <div class="cart-modal-header">
      <h2>Your Cart</h2>
      <button class="close-cart-modal" id="closeCartModal">X</button>
    </div>
    <div class="cart-modal-body" id="cartModalBody">
      <!-- Cart items will be dynamically inserted here -->
    </div>
    <div class="cart-modal-footer">
      <button class="btn" id="checkoutBtn">Checkout</button>
      <button class="btn" id="paymentBtn" style="display:none;">Pay Now</button>
    </div>
  </div>
</div>


  <!-- Main Banner -->
  <section class="main-banner">
    <img src="https://plus.unsplash.com/premium_photo-1683288662040-5ca51d0880b2?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" alt="Main Banner">
    <div class="banner-text">
      <h1>Welcome to Daraz Clone</h1>
      <p>Shop the best products at amazing prices</p>
      <button class="btn" id="shopNowBtn">Shop Now</button>
    </div>
  </section>

  <!-- Product Grid -->
  <section class="product-grid" id="productGrid">
    <!-- Dynamically Generated Products -->
  </section>

  <!-- Cart Button -->
  <div class="cart" id="cartBtn">
    <i class="fas fa-shopping-cart"></i>
    <span class="cart-items-count">0</span>
  </div>

  <!-- Cart Modal -->
  <div class="cart-modal" id="cartModal">
    <div class="cart-modal-content">
      <div class="cart-modal-header">
        <h2>Your Cart</h2>
        <button class="close-cart-modal" id="closeCartModal">X</button>
      </div>
      <div class="cart-modal-body" id="cartModalBody">
        <!-- Cart items will be dynamically inserted here -->
      </div>
      <div class="cart-modal-footer">
        <button class="btn" id="checkoutBtn">Checkout</button>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer class="footer">
    <p>&copy; 2025 Daraz Clone. All Rights Reserved.</p>
    <div>
      <a href="#">About</a>
      <a href="#">Contact</a>
      <a href="#">Privacy Policy</a>
      <a href="#">Terms & Conditions</a>
    </div>
  </footer>

  <script>
    
    // Sample products for demo
    const products = [
      { id: 1, name: "Smartphone", price: 499.99, img: "https://plus.unsplash.com/premium_photo-1680710431350-1adb85d4fe22?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OXx8aXBob25lJTIwMjAwJTIweCUyMDIwMHxlbnwwfHwwfHx8MA%3D%3D" },
      { id: 2, name: "Laptop", price: 899.99, img: "https://plus.unsplash.com/premium_photo-1681302427948-2fd0eca629b1?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8bGFwdG9wMjAwJTIweCUyMDIwMHxlbnwwfHwwfHx8MA%3D%3D" },
      { id: 3, name: "Headphones", price: 99.99, img: "https://plus.unsplash.com/premium_photo-1677838847721-2bf14b48c256?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTN8fGhlYWQlMjBwaG9uZXMyMDAlMjB4JTIwMjAwfGVufDB8fDB8fHww" },
      { id: 4, name: "Smart Watch", price: 199.99, img: "https://plus.unsplash.com/premium_photo-1728759436968-db4b52249ffa?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OXx8c21hcnQlMjB3YXRjaHMyMDAlMjB4JTIwMjAwfGVufDB8fDB8fHww" }
    ];

    let cart = [];
    const cartBtn = document.getElementById("cartBtn");
    const cartModal = document.getElementById("cartModal");
    const cartModalBody = document.getElementById("cartModalBody");
    const cartItemCount = document.querySelector(".cart-items-count");

    // Populate product grid
    const productGrid = document.getElementById("productGrid");
    products.forEach(product => {
      const productDiv = document.createElement("div");
      productDiv.classList.add("product");
      productDiv.innerHTML = `
        <img src="${product.img}" alt="${product.name}">
        <h3>${product.name}</h3>
        <p>$${product.price}</p>
        <button class="btn add-to-cart" data-id="${product.id}">Add to Cart</button>
      `;
      productGrid.appendChild(productDiv);
    });

    // Handle adding products to the cart
    document.querySelectorAll(".add-to-cart").forEach(button => {
      button.addEventListener("click", (e) => {
        const productId = e.target.getAttribute("data-id");
        const product = products.find(p => p.id == productId);
        cart.push(product);
        cartItemCount.innerText = cart.length;
      });
    });

    // Open cart modal
    cartBtn.addEventListener("click", () => {
      cartModal.classList.add("show");
      renderCartItems();
    });

    // Close cart modal
    document.getElementById("closeCartModal").addEventListener("click", () => {
      cartModal.classList.remove("show");
    });

    // Render cart items in the modal
    function renderCartItems() {
      cartModalBody.innerHTML = "";
      cart.forEach(item => {
        const cartItem = document.createElement("div");
        cartItem.classList.add("cart-item");
        cartItem.innerHTML = `
          <span>${item.name} - $${item.price}</span>
          <button>Remove</button>
        `;
        cartModalBody.appendChild(cartItem);
      });
    }
    // Render cart items in the modal
function renderCartItems() {
  cartModalBody.innerHTML = ""; // Clear existing items
  cart.forEach((item, index) => {
    const cartItem = document.createElement("div");
    cartItem.classList.add("cart-item");
    cartItem.innerHTML = `
      <span>${item.name} - $${item.price}</span>
      <button data-index="${index}">Remove</button>
    `;
    
    // Add event listener to the "Remove" button
    cartItem.querySelector("button").addEventListener("click", (e) => {
      const itemIndex = e.target.getAttribute("data-index");
      cart.splice(itemIndex, 1);  // Remove item from cart array
      cartItemCount.innerText = cart.length;  // Update cart item count
      renderCartItems();  // Re-render cart items
    });

    cartModalBody.appendChild(cartItem);
  });
}


    // Checkout button functionality (for demo purposes)
    document.getElementById("checkoutBtn").addEventListener("click", () => {
      alert("Proceeding to checkout...");
      cart = [];
      cartItemCount.innerText = 0;
      renderCartItems();
    });

    // Login Modal Logic
    const loginBtn = document.getElementById("loginBtn");
    const loginModal = document.getElementById("loginModal");
    const closeLoginModal = document.getElementById("closeLoginModal");

    loginBtn.addEventListener("click", () => {
      loginModal.style.display = "flex";
    });

    closeLoginModal.addEventListener("click", () => {
      loginModal.style.display = "none";
    });

    // Handle Login
    document.getElementById("loginSubmit").addEventListener("click", () => {
      const username = document.getElementById("username").value;
      const password = document.getElementById("password").value;
      
      // Basic validation (for demo purposes)
      if (username && password) {
        alert("Logged in successfully!");
        loginModal.style.display = "none";
      } else {
        alert("Please enter valid credentials.");
      }
    });
    
    // Initialize Stripe with your public key
const stripe = Stripe("YOUR_PUBLIC_STRIPE_KEY");  // Replace with your actual public key
const checkoutBtn = document.getElementById("checkoutBtn");
const paymentBtn = document.getElementById("paymentBtn");

// Function to calculate the total price of the cart
function calculateTotal() {
  return cart.reduce((total, item) => total + item.price, 0).toFixed(2);
}

// Handle the checkout button click
checkoutBtn.addEventListener("click", () => {
  // Display the payment button after checkout
  const totalAmount = calculateTotal();
  paymentBtn.style.display = "inline-block";
  paymentBtn.innerText = `Pay Now ($${totalAmount})`;
});

// Handle the payment button click (triggering Stripe Checkout)
paymentBtn.addEventListener("click", async () => {
  const totalAmount = calculateTotal();
  
  // Make an API call to your backend to create a checkout session
  // Here we'll assume that you have a server-side endpoint that handles Stripe session creation
  const response = await fetch("/create-checkout-session", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ amount: totalAmount * 100 })  // Convert to cents
  });
  
  const session = await response.json();
  
  // Redirect the user to the Stripe Checkout page
  const { error } = await stripe.redirectToCheckout({
    sessionId: session.id
  });
  
  if (error) {
    alert("Payment failed: " + error.message);
  }
});
// Calculate the total amount of the cart
function calculateTotal() {
  return cart.reduce((total, item) => total + item.price, 0).toFixed(2);
}

// Checkout button functionality
checkoutBtn.addEventListener("click", () => {
  const totalAmount = calculateTotal();
  // Show the Pay Now button with the total amount
  paymentBtn.style.display = "inline-block";
  paymentBtn.innerText = `Pay Now ($${totalAmount})`;
});

// Handle the payment button click (triggering Stripe Checkout)
paymentBtn.addEventListener("click", async () => {
  const totalAmount = calculateTotal();

  // Making an API call to create a checkout session on your backend
  const response = await fetch("/create-checkout-session", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ amount: totalAmount * 100 })  // Convert to cents
  });

  // Expecting a session response from the backend
  const session = await response.json();

  // Redirect the user to Stripe Checkout
  const { error } = await stripe.redirectToCheckout({
    sessionId: session.id
  });

  if (error) {
    alert("Payment failed: " + error.message);
  }
});





  </script>
  <script>
    // Existing JavaScript code for cart functionality and product display...
  
    // Calculate the total amount of the cart
    function calculateTotal() {
      return cart.reduce((total, item) => total + item.price, 0).toFixed(2);
    }
  
    // Checkout button functionality
    checkoutBtn.addEventListener("click", () => {
      const totalAmount = calculateTotal();
      // Show the Pay Now button with the total amount
      paymentBtn.style.display = "inline-block";
      paymentBtn.innerText = `Pay Now ($${totalAmount})`;
    });
  
    // Handle the payment button click (triggering Stripe Checkout)
    paymentBtn.addEventListener("click", async () => {
      const totalAmount = calculateTotal();
  
      // Making an API call to create a checkout session on your backend
      const response = await fetch("/create-checkout-session", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ amount: totalAmount * 100 })  // Convert to cents
      });
  
      // Expecting a session response from the backend
      const session = await response.json();
  
      // Redirect the user to Stripe Checkout
      const { error } = await stripe.redirectToCheckout({
        sessionId: session.id
      });
  
      if (error) {
        alert("Payment failed: " + error.message);
      }
    });
    
  </script>
  
  

</body>

</html>
