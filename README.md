# www.hungarygagpet.com
This is a Grow a garden pets buying page if you are intrested check out theese prices
<<</!DOCTYPE> html>
<html lang="hu">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hungary Gag Pets</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
      color: #333;
    }
    header {
      background-color: #4CAF50;
      color: white;
      padding: 15px;
      text-align: center;
    }
    header img {
      max-width: 120px;
      display: block;
      margin: 0 auto 8px;
    }
    header h1 {
      margin: 5px 0;
      font-size: 22px;
    }
    .pets {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 12px;
      padding: 12px;
    }
    .pet-card {
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      padding: 10px;
      text-align: center;
      transition: transform 0.2s;
    }
    .pet-card:hover {
      transform: scale(1.03);
    }
    .pet-card img {
      max-width: 100%;
      border-radius: 8px;
      margin-bottom: 8px;
    }
    .price {
      font-weight: bold;
      color: #e91e63;
    }
    button {
      background-color: #4CAF50;
      border: none;
      color: white;
      padding: 8px 12px;
      margin-top: 6px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
    }
    button:hover {
      background-color: #45a049;
    }
    .cart {
      background: white;
      margin: 12px;
      padding: 12px;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    .cart h2 {
      margin-top: 0;
    }
  </style>
</head>
<body>
  <header>
    <img src="https://via.placeholder.com/120x60.png?text=Gag+Pets" alt="Hungary Gag Pets">
    <h1>Hungary Gag Pets</h1>
    <p>Vicces és különleges állatkák árakkal</p>
  </header>

  <section class="pets">
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Golden+Goose" alt="Golden Goose">
      <h3>Golden Goose</h3>
      <p class="price">$3.59</p>
      <button onclick="addToCart('Golden Goose', 3.59)">Kosárba</button>
    </div>
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Dragonfly" alt="Dragonfly">
      <h3>Dragonfly</h3>
      <p class="price">$6.59</p>
      <button onclick="addToCart('Dragonfly', 6.59)">Kosárba</button>
    </div>
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Griffin" alt="Griffin">
      <h3>Griffin</h3>
      <p class="price">$3.59</p>
      <button onclick="addToCart('Griffin', 3.59)">Kosárba</button>
    </div>
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Queen+Bee" alt="Queen Bee">
      <h3>Queen Bee</h3>
      <p class="price">$3.99</p>
      <button onclick="addToCart('Queen Bee', 3.99)">Kosárba</button>
    </div>
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Ferret" alt="French Frie Ferret">
      <h3>French Frie Ferret</h3>
      <p class="price">$4.59</p>
      <button onclick="addToCart('French Frie Ferret', 4.59)">Kosárba</button>
    </div>
    <div class="pet-card">
      <img src="https://via.placeholder.com/150?text=Red+Fox" alt="Red Fox">
      <h3>Red Fox</h3>
      <p class="price">$3.59</p>
      <button onclick="addToCart('Red Fox', 3.59)">Kosárba</button>
    </div>
  </section>

  <section class="cart">
    <h2>Kosár</h2>
    <ul id="cart-items"></ul>
    <p><strong>Összesen: $<span id="total">0.00</span></strong></p>
    <button onclick="checkout()">Fizetés</button>
  </section>

  <script>
    let cart = [];

    function addToCart(name, price) {
      cart.push({ name, price });
      renderCart();
    }

    function renderCart() {
      const cartList = document.getElementById('cart-items');
      const totalEl = document.getElementById('total');
      cartList.innerHTML = '';
      let total = 0;
      cart.forEach(item => {
        const li = document.createElement('li');
        li.textContent = `${item.name} - $${item.price.toFixed(2)}`;
        cartList.appendChild(li);
        total += item.price;
      });
      totalEl.textContent = total.toFixed(2);
    }

    function checkout() {
      if (cart.length === 0) {
        alert('A kosár üres!');
      } else {
        alert('Köszönjük a vásárlást! Fizetendő összeg: $' + document.getElementById('total').textContent);
        cart = [];
        renderCart();
      }
    }
  </script>
</body>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Golden_Goose.jpg/150px-Golden_Goose.jpg" alt="Golden Goose"><button id="pay-button">Fizetés</button>
<script src="https://js.stripe.com/v3/"></script>
<script>
  const stripe = Stripe('PUBLIKUS_API_KULCS');
  document.getElementById('pay-button').addEventListener('click', async () => {
    const response = await fetch('/create-payment-intent', { method: 'POST' });
    const data = await response.json();
    const result = await stripe.confirmCardPayment(data.clientSecret, {
      payment_method: {
        card: { /* kártyaadatok */ },
      }
    });
    if(result.error){
      alert(result.error.message);
    } else {
      alert('Sikeres fizetés!');
    }
  });
</script>
<button id="payButton">Fizetés bankkártyával</button>
<script>
  const stripe = Stripe('YOUR_PUBLISHABLE_KEY');

  document.getElementById('payButton').addEventListener('click', async () => {
    const response = await fetch('/create-checkout-session', { method: 'POST' });
    const session = await response.json();
    const result = await stripe.redirectToCheckout({ sessionId: session.id });
    if (result.error) alert(result.error.message);
  });
</script><script src="https://js.stripe.com/v3/"></script><!-- PayPal fizetés gomb -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
  <input type="hidden" name="cmd" value="_s-xclick">
  <input type="hidden" name="hosted_button_id" value="A_TE_GOMB_ID">
  <input type="image" src="https://www.paypalobjects.com/en_US/i/btn/btn_buynow_LG.gif" border="0" name="submit" alt="Fizetés PayPal-lal">
  <img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1">
</form><!DOCTYPE html>
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <title>PayPal Teszt Fizetés</title>
    <script src="https://www.paypal.com/sdk/js?client-id=YOUR_SANDBOX_CLIENT_ID&currency=HUF"></script>
</head>
<body>
    <h1>PayPal Teszt Fizetés</h1>
    <div id="paypal-button-container"></div>

    <script>
        paypal.Buttons({
            createOrder: function(data, actions) {
                return actions.order.create({
                    purchase_units: [{
                        amount: {
                            value: '1000' // Teszt összeg: 1000 HUF
                        }
                    }]
                });
            },
            onApprove: function(data, actions) {
                return actions.order.capture().then(function(details) {
                    alert('Fizetés sikeres! Üdv, ' + details.payer.name.given_name);
                });
            }
        }).render('#paypal-button-container');
    </script>
</body>
</html><!-- Fizetés gomb PayPal-lal -->
<a href="https://www.paypal.me/TEFIOKNEVED/10" target="_blank" 
   style="display:inline-block;padding:12px 24px;background-color:#0070ba;color:white;
          text-decoration:none;font-size:16px;border-radius:6px;">
    Fizetés $6 USD PayPal-lal
</a><a href="https://www.paypal.me/SAJATNEVED/10" target="_blank"
   style="display:inline-block;padding:12px 24px;background-color:#0070ba;color:white;
          text-decoration:none;font-size:16px;border-radius:6px;">
    Fizetés $4 USD PayPal-lal
</a><a href="https://www.paypal.me/SAJATNEVED/10" target="_blank"
   style="display:inline-block;padding:12px 24px;background-color:#0070ba;color:white;
          text-decoration:none;font-size:16px;border-radius:6px;">
    Fizetés 10 USD PayPal-lal
</a><!-- PayPal JavaScript SDK, a "funding" paraméterrel engedélyezzük a kártyás fizetést -->
<script src="https://www.paypal.com/sdk/js?client-id=SAJAT_CLIENT_ID&currency=USD&enable-funding=card"></script>

<div id="paypal-button-container"></div>

<script>
paypal.Buttons({
    createOrder: function(data, actions) {
        return actions.order.create({
            purchase_units: [{
                amount: {
                    value: '10' // fizetendő összeg USD-ben
                }
            }]
        });
    },
    onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
            alert('Köszönjük a fizetést, ' + details.payer.name.given_name + '!');
        });
    },
    onError: function(err) {
        console.error(err);
        alert('Hiba történt a fizetés során.');
    }
}).render('#paypal-button-container'); // Gomb renderelése
</script><!-- PayPal JavaScript SDK, kártyás fizetés engedélyezése -->
<script src="https://www.paypal.com/sdk/js?client-id=SAJAT_CLIENT_ID&currency=USD&enable-funding=card"></script>

<div id="paypal-button-container"></div>

<script>
paypal.Buttons({
    createOrder: function(data, actions) {
        return actions.order.create({
            purchase_units: [{
                amount: {
                    value: '10' // Fizetendő összeg USD-ben
                }
            }]
        });
    },
    onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
            alert('Köszönjük a fizetést, ' + details.payer.name.given_name + '!');
        });
    },
    onError: function(err) {
        console.error(err);
        alert('Hiba történt a fizetés során.');
    }
}).render('#paypal-button-container');
app.listen(8158, '0.0.0.0', () => {
    console.log('Server running on port 8158');
});<!DOCTYPE html>
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fizetés Visa/MasterCard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        #paypal-button-container {
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            padding: 20px;
            border-radius: 10px;
            background-color: white;
        }
    </style>
</head>
<body>
    <div id="paypal-button-container"></div>

    <!-- PayPal SDK, kártyás fizetés engedélyezve -->
    <script src="https://www.paypal.com/sdk/js?client-id=SAJAT_CLIENT_ID&currency=USD&enable-funding=card"></script>

    <script>
        paypal.Buttons({
            style: {
                layout: 'vertical',
                color: 'blue',
                shape: 'rect',
                label: 'pay'
            },
            createOrder: function(data, actions) {
                return actions.order.create({
                    purchase_units: [{
                        amount: {
                            value: '10' // Fizetendő összeg USD-ben
                        }
                    }]
                });
            },
            onApprove: function(data, actions) {
                return actions.order.capture().then(function(details) {
                    alert('Köszönjük a fizetést, ' + details.payer.name.given_name + '!');
                });
            },
            onError: function(err) {
                console.error(err);
                alert('Hiba történt a fizetés során.');
            }
        }).render('#paypal-button-container');
    </script>
</body>
</html>

    
