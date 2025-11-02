# 💡 Mostrar precios sin IVA y ahorro unitario en el carrito de WooCommerce

Este mini tutorial explica cómo personalizar la visualización de precios en el carrito de WooCommerce para mostrar:

- El **precio regular** sin IVA (tachado si hay descuento).  
- El **precio actual** sin IVA.  
- El **ahorro por unidad** mostrado en una etiqueta debajo del precio.

---

## 🧩 Código completo

Agrega este snippet al archivo `functions.php` de tu tema hijo (por ejemplo: `salient-child/functions.php`) o a un plugin de snippets:

```php
add_filter( 'filtro_precio', function( $html, $precio_linea_sin_iva, $cart_item, $cart_item_key ) {
    $product   = $cart_item['data'];
    $cantidad  = $cart_item['quantity'];

    // Precio regular unitario sin IVA
    $precio_regular_unitario = wc_get_price_excluding_tax( $product, array( 'price' => $product->get_regular_price() ) );

    // Precio de venta unitario sin IVA (considerando descuento)
    $precio_venta_unitario   = wc_get_price_excluding_tax( $product, array( 'price' => $product->get_price() ) );

    // Si no hay descuento, muestra solo el precio normal
    if ( $precio_regular_unitario <= 0 || $precio_regular_unitario == $precio_venta_unitario ) {
        return '<span class="precio-normal">' . wc_price( $precio_venta_unitario ) . '</span>';
    }

    // Calcular ahorro por unidad
    $ahorro_unitario = $precio_regular_unitario - $precio_venta_unitario;

    // Generar HTML con formato (por unidad)
    $html  = '<div class="precio-con-descuento" style="display:flex; flex-direction:column;">';

    // Línea superior: precio tachado + precio actual
    $html .= '<div class="precios" style="display:flex; align-items:center; gap:6px;">';
    $html .= '<span class="precio-regular" style="text-decoration:line-through;">' . wc_price( $precio_regular_unitario ) . '</span>';
    $html .= '<span class="precio-descuento">' . wc_price( $precio_venta_unitario ) . '</span>';
    $html .= '</div>';

    // Línea inferior: texto de ahorro por unidad
    $html .= '<div class="ahorro" style="font-size:13px; border:1px solid #000000; border-radius:5px; margin-right:auto; margin-top:5px; padding:1px 7px;">';
    $html .= 'AHORRA ' . wc_price( $ahorro_unitario );
    $html .= '</div>';

    $html .= '</div>';

    return $html;
}, 10, 4);

```

🧠 Explicación paso a paso

Se obtiene el producto y la cantidad actual del carrito

$product = $cart_item['data'];
$cantidad = $cart_item['quantity'];


Se calculan los precios sin IVA, tanto el regular como el de oferta:

wc_get_price_excluding_tax( $product, array( 'price' => $product->get_regular_price() ) );
wc_get_price_excluding_tax( $product, array( 'price' => $product->get_price() ) );


Si el producto no tiene descuento, se muestra solo el precio sin IVA.

Si hay descuento, se muestran ambos precios y se calcula el ahorro por unidad:

$ahorro_unitario = $precio_regular_unitario - $precio_venta_unitario;


El resultado se muestra con formato visual:

Precio regular tachado

Precio con descuento

Ahorro resaltado en un recuadro

🎨 Resultado visual

Antes (sin descuento):

$120.00


Con descuento:

$150.00  ~$180.00~  
AHORRA $30.00

🧾 Notas

El snippet calcula todos los precios sin IVA, ideal si tu tienda muestra impuestos por separado.

Puedes ajustar los estilos (style="") para personalizar colores, bordes o tamaños de texto.

Si deseas mostrar también el IVA unitario, se puede extender fácilmente el mismo código.

✅ Recomendación

Guarda este código en un archivo llamado, por ejemplo:

/wp-content/themes/salient-child/inc/custom-cart-prices.php


Y en tu functions.php agrega:

require_once get_stylesheet_directory() . '/inc/custom-cart-prices.php';


Así mantienes tu tema limpio y organizado. 🧹
