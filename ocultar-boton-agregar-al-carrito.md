# 🛠 Cómo ocultar el botón Agregar al carrito en el listado de productos (WooCommerce)

En algunos temas —incluyendo Salient— el botón “Agregar al carrito” no se elimina usando los hooks tradicionales (woocommerce_after_shop_loop_item) porque el tema imprime el botón mediante el filtro:

woocommerce_loop_add_to_cart_link


Por eso, la forma más efectiva es interceptar ese filtro y devolver una cadena vacía.

✅ 1. Agrega este código en tu child theme o plugin de snippets
// Ocultar el botón "Añadir al carrito" en el loop (tienda y categorías)
add_filter( 'woocommerce_loop_add_to_cart_link', function( $html, $product, $args ) {
    return '';
}, 10, 3 );

🔍 ¿Qué hace este código?

Intercepta el HTML que WooCommerce o el tema genera para el botón.

Lo reemplaza por una cadena vacía, eliminando el botón por completo.

Funciona en:

Tienda (/shop)

Categorías de productos

Búsquedas

Cualquier loop de productos

🎯 Ventajas de este método

Funciona incluso en temas que sobrescriben plantillas (como Salient).

No requiere editar archivos del tema.

Elimina completamente el botón del frontend (no solo lo oculta con CSS).
