# boutique-stormex
Boutique en ligne Stormex - Vente de produits officiels avec paiement PayPal
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Boutique Stormex</title>
  <script src="https://www.paypal.com/sdk/js?client-id=TON_CLIENT_ID"></script>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; background:#111; color:#eee; }
    h1 { color: #00bfff; }
    .product { border: 1px solid #333; padding: 20px; margin: 20px auto; width: 300px; border-radius: 10px; background:#1c1c1c; }
    .price { font-size: 20px; margin: 10px 0; }
    #paypal-button-container { margin-top: 20px; }
  </style>
</head>
<body>
  <h1>🛒 Boutique Stormex</h1>

  <div class="product">
    <h2>T-shirt Stormex</h2>
    <p class="price">19,99 €</p>
    <div id="paypal-button-container"></div>
  </div>

  <script>
    paypal.Buttons({
      createOrder: function(data, actions) {
        return actions.order.create({
          purchase_units: [{
            amount: { value: '19.99' },
            description: 'T-shirt Stormex Taille M'
          }]
        });
      },
      onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
          alert('Merci ' + details.payer.name.given_name + ' pour ton achat !');
          console.log("Détails de la commande :", details);
          // 👉 Ici tu pourrais envoyer les infos vers ton backend
        });
      }
    }).render('#paypal-button-container');
  </script>
</body>
</html>
