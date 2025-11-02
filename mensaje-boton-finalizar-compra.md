# 💡 Agrega un mensaje personalizado justo encima del botón **“Finalizar compra”**:  

> Por ejemplo: 🔒 Tu pago es 100% seguro y tus datos están protegidos con cifrado SSL.

---

## 🧩 Código PHP

```php
add_action( 'woocommerce_review_order_before_submit', function() {
    echo '<p style="font-size:14px; color:#0073aa; margin-bottom:10px;">🔒 Tu pago es 100% seguro y tus datos están protegidos con cifrado SSL.</p>';
});
```

## 📍 Dónde colocarlo

En tu archivo functions.php o en un plugin de snippets.

## 🚀 Por qué usarlo

Mejora la percepción de seguridad y reduce el abandono del carrito, especialmente en usuarios nuevos.
