# Nexoradelux
Full breed cat and dog
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>nexoradulux - Pet Store</title>
    <style>
        /* =========================================================
           1. CSS STYLES
           ========================================================= */

        /* 1. Wine Color Background */
        body {
            background-color: #58111A; /* Classic deep wine color */
            color: #FFFFFF;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
        }

        /* Header & Navigation */
        header {
            background-color: #3B0B12;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: #FFD700; /* Accent gold text */
            text-decoration: none;
            text-transform: lowercase;
        }

        /* 4. Search bar for accessories */
        .search-container {
            flex-grow: 1;
            margin: 10px 20px;
            max-width: 400px;
        }

        .search-container input {
            width: 100%;
            padding: 10px;
            border-radius: 5px;
            border: none;
            outline: none;
        }

        .auth-cart-buttons {
            display: flex;
            gap: 10px;
        }

        .btn {
            background-color: #800020;
            color: white;
            border: 1px solid #FFD700;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn:hover {
            background-color: #A00028;
        }

        .container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 0 20px;
        }

        .banner {
            background-color: #420D14;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #731A28;
            margin-bottom: 20px;
        }

        /* Product Cards Grid */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .card {
            background-color: #420D14;
            border: 1px solid #731A28;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .card h3 {
            margin: 10px 0 5px 0;
            color: #FFD700;
        }

        /* Form & Checkout Sections */
        .checkout-section {
            background-color: #420D14;
            padding: 20px;
            border-radius: 8px;
            border: 1px solid #731A28;
            margin-top: 30px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
        }

        .form-group select, .form-group input {
            width: 100%;
            padding: 10px;
            border-radius: 5px;
            border: none;
            box-sizing: border-box;
        }

        /* Footer & Support Links */
        footer {
            background-color: #3B0B12;
            padding: 20px;
            text-align: center;
            margin-top: 40px;
            border-top: 1px solid #731A28;
        }

        .support-links a {
            color: #25D366; /* WhatsApp Green */
            text-decoration: none;
            margin: 0 10px;
            font-weight: bold;
        }

        .support-links a.email-link {
            color: #FFD700;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.8);
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: #420D14;
            padding: 30px;
            border-radius: 8px;
            border: 1px solid #FFD700;
            width: 300px;
            text-align: center;
        }

        .close-btn {
            float: right;
            cursor: pointer;
            color: #FFD700;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <!-- Header Section -->
    <header>
        <!-- 12. Company Name -->
        <a href="#" class="logo">nexoradulux</a>

        <!-- 4. Accessories Search Bar -->
        <div class="search-container">
            <input type="text" id="searchInput" onkeyup="searchAccessories()" placeholder="Search all pet accessories (collars, food, toys)...">
        </div>

        <!-- 10. Auth Buttons & 9. Cart Counter -->
        <div class="auth-cart-buttons">
            <button class="btn" onclick="openModal('authModal')">Sign In / Sign Up</button>
            <button class="btn" onclick="scrollToCheckout()">Cart (<span id="cartCount">0</span>)</button>
        </div>
    </header>

    <div class="container">
        <!-- 7. Return Policy Banner -->
        <div class="banner">
            <strong>📋 Return Policy:</strong> We offer a <u>Free Return within 5 business days</u> on eligible items.
        </div>

        <!-- 8. Breed Availability Statement -->
        <div class="banner" style="background-color: #3B0B12; border-color: #FFD700;">
            🐾 <strong>Pet Catalog:</strong> All cat and dog full breeds are available upon order!
        </div>

        <!-- Catalog Section -->
        <h2>Pet Accessories Catalog</h2>
        <div class="grid" id="productGrid">
            <!-- Items injected via JS -->
        </div>

        <!-- Checkout Section -->
        <div class="checkout-section" id="checkoutSection">
            <h2>Checkout</h2>
            <form id="checkoutForm" onsubmit="handleCheckout(event)">
                
                <!-- 10. Checkout as Guest Option -->
                <div class="form-group">
                    <label>Checkout Mode:</label>
                    <select id="checkoutType">
                        <option value="guest">Checkout as Guest</option>
                        <option value="user">Registered User</option>
                    </select>
                </div>

                <div class="form-group">
                    <label>Full Name:</label>
                    <input type="text" required placeholder="Enter your full name">
                </div>

                <!-- 2. Delivery Type Option -->
                <div class="form-group">
                    <label>Fulfillment Type:</label>
                    <select id="fulfillmentType" onchange="toggleDeliveryOptions()">
                        <option value="door">Door Delivery</option>
                        <option value="pickup">Pick Up Station</option>
                    </select>
                </div>

                <!-- 11. Delivery Company Options -->
                <div class="form-group" id="courierGroup">
                    <label>Select Delivery Logistics Company:</label>
                    <select id="deliveryCompany">
                        <option value="gig">GIG Logistics</option>
                        <option value="dhl">DHL Express</option>
                        <option value="fedex">FedEx</option>
                        <option value="speedaf">Speedaf Express</option>
                    </select>
                </div>

                <!-- 5. Payment Timing Options -->
                <div class="form-group">
                    <label>Payment Timing:</label>
                    <select id="paymentTiming">
                        <option value="before">Payment Before Delivery</option>
                        <option value="ondelivery">Payment on Delivery</option>
                    </select>
                </div>

                <!-- 6. Payment Method Options -->
                <div class="form-group">
                    <label>Payment Method Channel:</label>
                    <select id="paymentChannel">
                        <option value="paystack">Paystack Online Payment</option>
                        <option value="whatsapp">WhatsApp Order & Payment</option>
                    </select>
                </div>

                <button type="submit" class="btn" style="width: 100%; padding: 12px; font-weight: bold;">Complete Order</button>
            </form>
        </div>
    </div>

    <!-- 3. Support Links Footer -->
    <footer>
        <p>&copy; 2026 nexoradulux. All rights reserved.</p>
        <div class="support-links">
            <span>Customer Support:</span>
            <a href="https://wa.me/1234567890" target="_blank">💬 WhatsApp Support</a> | 
            <a href="mailto:support@nexoradulux.com" class="email-link">✉️ Email Support</a>
        </div>
    </footer>

    <!-- Auth Modal -->
    <div class="modal" id="authModal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('authModal')">&times;</span>
            <h3 style="color:#FFD700">Account Access</h3>
            <div class="form-group">
                <input type="email" placeholder="Email Address"><br><br>
                <input type="password" placeholder="Password"><br><br>
                <button class="btn" style="width: 100%;" onclick="alert('Signed In Successfully!'); closeModal('authModal');">Sign In</button><br><br>
                <button class="btn" style="width: 100%; background: transparent;" onclick="alert('Account Created!'); closeModal('authModal');">Sign Up</button>
            </div>
        </div>
    </div>

    <!-- =========================================================
         2. JAVASCRIPT
         ========================================================= -->
    <script>
        // Sample Accessories Data
        const accessories = [
            { id: 1, name: "Premium Leather Dog Collar", price: "$15" },
            { id: 2, name: "Interactive Cat Feather Toy", price: "$8" },
            { id: 3, name: "Orthopedic Pet Bed", price: "$45" },
            { id: 4, name: "Stainless Steel Food Bowl", price: "$12" },
            { id: 5, name: "Full Dog Harness & Leash", price: "$22" },
            { id: 6, name: "Cat Grooming Brush Set", price: "$10" }
        ];

        let cart = [];

        // Render products into the grid
        function renderProducts(items) {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = '';
            
            if (items.length === 0) {
                grid.innerHTML = '<p>No accessories match your search.</p>';
                return;
            }

            items.forEach(item => {
                const card = document.createElement('div');
                card.className = 'card';
                card.innerHTML = `
                    <div>
                        <h3>${item.name}</h3>
                        <p>Price: ${item.price}</p>
                    </div>
                    <!-- 9. Add to cart button -->
                    <button class="btn" onclick="addToCart('${item.name}')">Add to Cart</button>
                `;
                grid.appendChild(card);
            });
        }

        // 4. Search function for accessories
        function searchAccessories() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = accessories.filter(item => 
                item.name.toLowerCase().includes(query)
            );
            renderProducts(filtered);
        }

        // 9. Add to Cart Handler
        function addToCart(itemName) {
            cart.push(itemName);
            document.getElementById('cartCount').innerText = cart.length;
            alert(itemName + ' added to your cart!');
        }

        // 2. Toggle delivery choices based on selection
        function toggleDeliveryOptions() {
            const type = document.getElementById('fulfillmentType').value;
            const courierGroup = document.getElementById('courierGroup');
            if (type === 'pickup') {
                courierGroup.style.display = 'none';
            } else {
                courierGroup.style.display = 'block';
            }
        }

        function scrollToCheckout() {
            document.getElementById('checkoutSection').scrollIntoView({ behavior: 'smooth' });
        }

        // Modal Controls
        function openModal(id) { document.getElementById(id).style.display = 'flex'; }
        function closeModal(id) { document.getElementById(id).style.display = 'none'; }

        // Form Submit Handler
        function handleCheckout(e) {
            e.preventDefault();
            const paymentChannel = document.getElementById('paymentChannel').value;
            
            if (paymentChannel === 'whatsapp') {
                // Redirect to WhatsApp with order detail
                const text = encodeURIComponent(`Hello nexoradulux, I would like to place an order for ${cart.length} item(s).`);
                window.open(`https://wa.me/1234567890?text=${text}`, '_blank');
            } else {
                alert('Redirecting to Paystack checkout portal...');
            }
        }

        // Initial render on page load
        renderProducts(accessories);
    </script>
</body>
</html>
