# STRIPE testing

## Create a product on COMMAND-LINE
curl https://api.stripe.com/v1/products/ \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d name="Gold Special"

# Copy ID Property and REPLACE {{PRODUCT_ID}}
prod_O42xbUmapcvCON

curl https://api.stripe.com/v1/prices/ \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d product="{{PRODUCT_ID}}" \
  -d unit_amount=2000 \
  -d currency=usd

curl https://api.stripe.com/v1/prices \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d unit_amount=1200 \
  -d currency=usd \
  -d product=prod_O42xbUmapcvCON

curl https://api.stripe.com/v1/prices \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d product="prod_O3MaUvnsiPNlQ7" \
  -d unit_amount=2000 \
  -d currency=usd

## Create a Session
NOTE: Copy Price ID and REPLACE {{PRICE_ID}}
price_1NHv2V2eZvKYlo2C6FhxvPIT

curl https://api.stripe.com/v1/checkout/sessions \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d "payment_method_types[]"=card \
  -d "line_items[][price]"="price_1NHv2V2eZvKYlo2C6FhxvPIT" \
  -d "line_items[][quantity]"=1 \
  -d mode=payment \
  -d success_url="https://example.com/success?session_id=cs_test_a1AxgGeqKcdgLlIXffW6XqrNMZ49OIO1dVUlLCRuLLS3y4Z2EkmGDbKhPT" \
  -d cancel_url="https://example.com/cancel"

curl https://api.stripe.com/v1/checkout/sessions \
-u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
-d "payment_method_types[]"=card \
-d "line_items[][price]"="price_1NHFvM2eZvKYlo2CxvMGwZi8" \
-d "line_items[][quantity]"=1 \
-d mode=payment \
-d success_url="https://example.com/success?session_id={CHECKOUT_SESSION_ID}" \
-d cancel_url="https://example.com/cancel"

# Copy and paste this code block to an HTML and REPLACE {{CHECKOUT_SESSION_ID}}
cs_test_a1clkJ49CswbcGaCj2fPj8Doi5HVzMKOTlN3509XR5fU9KretllQiqbimz

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!-- cdn for stripe library -->
  <script src="https://js.stripe.com/v3/"></script>

  <script>
    // use client-side test api key
    var stripe = Stripe('pk_test_TYooMQauvdEDq54NiTphI7jx');

    // immediately redirect to stripe using your checkout session
    stripe.redirectToCheckout({
      sessionId: '{{CHECKOUT_SESSION_ID}}'
    });
  </script>
</body>
</html>
```

# Node.js
node session.js

{
  "products": {
    "id": [
      "6484e7407f404a24582b9b2d",
      "6484e7407f404a24582b9b2e"
    ],
    "name": [
      "Tin of Cookies",
      "Canned Coffee"
    ]
  }
}