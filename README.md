# boutique-stormex
Boutique en ligne Stormex - Vente de produits officiels avec paiement PayPal
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Boutique Stormex - T-shirt Blanc</title>
  <!-- Remplace TON_CLIENT_ID par ton vrai Client ID PayPal -->
  <script src="https://www.paypal.com/sdk/js?client-id=TON_CLIENT_ID&currency=EUR"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .product {
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      text-align: center;
      max-width: 400px;
      width: 100%;
    }
    .product img {
      width: 100%;
      border-radius: 8px;
      margin-bottom: 15px;
    }
    .product h2 {
      font-size: 24px;
      margin: 15px 0;
    }
    .product .price {
      font-size: 20px;
      color: #333;
      margin-bottom: 20px;
    }
    #paypal-button-tshirt {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="product">
    <img src="https://media.discordapp.net/attachments/1328445021371895909/1417156130941177886/Capture_decran_2025-09-15_162807.png" alt="T-shirt Stormex Blanc">
    <h2>T-shirt Stormex Blanc</h2>
    <p class="price">12,00 €</p>
    <div id="paypal-button-tshirt"></div>
  </div>

  <script>
    paypal.Buttons({
      style: {
        layout: 'vertical',
        color:  'blue',
        shape:  'rect',
        label:  'paypal'
      },
      createOrder: function(data, actions) {
        return actions.order.create({
          purchase_units: [{
            amount: { value: '12.00' },
            description: 'T-shirt Stormex Blanc'
          }]
        });
      },
      onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
          alert('Merci ' + details.payer.name.given_name + ' pour ton achat !');
          console.log("Détails de la commande :", details);
        });
      }
    }).render('#paypal-button-tshirt');
  </script>
</body>
</html>
