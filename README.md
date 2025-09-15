# boutique-stormex
Boutique en ligne Stormex - Vente de produits officiels avec paiement PayPal
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Boutique Stormex - T-shirt Blanc</title>
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
      margin-bottom: 15px;
    }
    .product label {
      display: block;
      margin: 10px 0 5px;
    }
    .product select, .product input[type="number"] {
      padding: 5px;
      font-size: 16px;
      width: 100%;
      margin-bottom: 10px;
    }
    #paypal-button-tshirt {
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <div class="product">
    <img src="https://media.discordapp.net/attachments/1328445021371895909/1417156130941177886/Capture_decran_2025-09-15_162807.png" alt="T-shirt Stormex Blanc">
    <h2>T-shirt Stormex Blanc</h2>
    <p class="price">12,00 €</p>

    <label for="taille">Taille :</label>
    <select id="taille">
      <option value="S">S</option>
      <option value="M" selected>M</option>
      <option value="L">L</option>
      <option value="XL">XL</option>
    </select>

    <label for="quantite">Quantité :</label>
    <input type="number" id="quantite" value="1" min="1">

    <div id="paypal-button-tshirt"></div>
  </div>

  <script>
    paypal.Buttons({
      createOrder: function(data, actions) {
        var taille = document.getElementById('taille').value;
        var quantite = parseInt(document.getElementById('quantite').value);
        var prixUnitaire = 12.00;
        var total = (prixUnitaire * quantite).toFixed(2);

        return actions.order.create({
          purchase_units: [{
            amount: {
              value: total
            },
            description: 'T-shirt Stormex Blanc - Taille ' + taille + ' - Qté: ' + quantite
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
