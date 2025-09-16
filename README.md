# boutique-stormex
Boutique en ligne Stormex - Vente de produits officiels avec paiement PayPal
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Boutique Stormex</title>
  <!-- Script PayPal avec ton Client ID -->
  <script src="https://www.paypal.com/sdk/js?client-id=Acjrbv2wUChFfr2Wp-GDFR_7a1DzQDnTnh654DgQg3XlrK0e0e9fordJ0JuF_dqCZRW5ge-wYXAKHbnN&currency=EUR"></script>
  <style>
    body { 
      font-family: Arial, sans-serif; 
      text-align: center; 
      margin: 50px 20px; 
      background:#111; 
      color:#eee; 
    }
    h1 { color: #00bfff; }
    .products-container {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 20px;
    }
    .product { 
      border: 1px solid #333; 
      padding: 20px; 
      border-radius: 10px; 
      background:#1c1c1c; 
      width: 300px; 
    }
    .product img {
      width: 100%;
      border-radius: 10px;
      margin-bottom: 15px;
    }
    .product h2 { margin: 10px 0; }
    .price { font-size: 20px; margin: 10px 0; }
    .paypal-button-container { margin-top: 20px; }
    select { padding: 5px; font-size: 16px; width: 100%; margin-bottom: 10px; }
  </style>
</head>
<body>
  <h1>🛒 Boutique Stormex</h1>

  <div class="products-container">
    <!-- Produit 1 -->
    <div class="product">
      <!-- Mets ton image dans un dossier images/ et renomme tshirt-blanc.png -->
      <img src="images/tshirt-blanc.png" alt="T-shirt Stormex Blanc">
      <h2>T-shirt Stormex Blanc</h2>
      <p class="price">12,00 €</p>
      <label for="taille-1">Taille :</label>
      <select id="taille-1">
        <option value="S">S</option>
        <option value="M" selected>M</option>
        <option value="L">L</option>
        <option value="XL">XL</option>
      </select>
      <div id="paypal-button-1" class="paypal-button-container"></div>
    </div>

    <!-- Produit 2 -->
    <div class="product">
      <img src="images/tshirt-noir.png" alt="T-shirt Stormex Noir">
      <h2>T-shirt Stormex Noir</h2>
      <p class="price">12,00 €</p>
      <label for="taille-2">Taille :</label>
      <select id="taille-2">
        <option value="S">S</option>
        <option value="M" selected>M</option>
        <option value="L">L</option>
        <option value="XL">XL</option>
      </select>
      <div id="paypal-button-2" class="paypal-button-container"></div>
    </div>
  </div>

  <script>
    // Produit 1 - T-shirt Blanc
    paypal.Buttons({
      style: { layout: 'vertical', color: 'blue', shape: 'rect', label: 'paypal' },
      createOrder: function(data, actions) {
        var taille = document.getElementById('taille-1').value;
        return actions.order.create({
          purchase_units: [{
            amount: { value: '12.00' },
            description: 'T-shirt Stormex Blanc - Taille ' + taille
          }]
        });
      },
      onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
          alert('Merci ' + details.payer.name.given_name + ' pour votre achat !');
          console.log("Détails commande Produit 1 :", details);
        });
      }
    }).render('#paypal-button-1');

    // Produit 2 - T-shirt Noir
    paypal.Buttons({
      style: { layout: 'vertical', color: 'blue', shape: 'rect', label: 'paypal' },
      createOrder: function(data, actions) {
        var taille = document.getElementById('taille-2').value;
        return actions.order.create({
          purchase_units: [{
            amount: { value: '12.00' },
            description: 'T-shirt Stormex Noir - Taille ' + taille
          }]
        });
      },
      onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
          alert('Merci ' + details.payer.name.given_name + ' pour votre achat !');
          console.log("Détails commande Produit 2 :", details);
        });
      }
    }).render('#paypal-button-2');
  </script>
</body>
</html>
