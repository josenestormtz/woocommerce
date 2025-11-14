# 🛠 Ocultar el botón “Agregar al carrito” en la página de producto individual

WooCommerce imprime el botón usando la acción:

woocommerce_single_product_summary


Así que solo necesitamos removerla.

✅ Opción 1 (Recomendada): Quitar el botón desde el hook principal

Agrega este snippet:

// Ocultar el botón "Añadir al carrito" en la página individual
add_action( 'wp', function() {
    remove_action( 'woocommerce_single_product_summary', 'woocommerce_template_single_add_to_cart', 30 );
});

🔍 ¿Qué hace este código?

Usa remove_action() para eliminar el bloque que genera el botón.

Funciona en todos los productos.

Respeta el orden de cargas del tema (por eso usamos wp y no init).
