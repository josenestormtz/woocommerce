🛒 Agregar productos al carrito por SKU en WooCommerce

Este snippet permite que los usuarios agreguen productos directamente al carrito ingresando su clave o SKU y la cantidad deseada, sin tener que buscarlos en el catálogo.
El formulario aparece encima del listado de artículos del carrito.

🧩 Código completo
add_action( 'woocommerce_before_cart', 'agregar_formulario_por_sku' );
function agregar_formulario_por_sku() {
    ?>
    <div class="agregar-por-sku" style="margin-bottom:20px; padding:15px;">
        <form method="post" style="display:flex; gap:10px; align-items:center; flex-wrap:wrap;">
            <input type="text" name="sku_producto" placeholder="Clave o SKU" required style="padding:8px; border:1px solid #ccc; border-radius:5px; width: 200px;">
            <input type="number" name="cantidad_producto" placeholder="Cantidad" value="1" min="1" required style="padding:8px; width:100px; border:1px solid #ccc; border-radius:5px;">
            <button type="submit" name="agregar_por_sku" class="button">Agregar</button>
        </form>
    </div>
    <?php
}

add_action( 'template_redirect', 'procesar_agregar_por_sku' );
function procesar_agregar_por_sku() {
    if ( isset($_POST['agregar_por_sku']) && !empty($_POST['sku_producto']) ) {

        $sku = sanitize_text_field( $_POST['sku_producto'] );
        $cantidad = isset($_POST['cantidad_producto']) ? intval($_POST['cantidad_producto']) : 1;

        $product_id = wc_get_product_id_by_sku( $sku );

        if ( $product_id ) {
            // Agregar al carrito correctamente
            WC()->cart->add_to_cart( $product_id, $cantidad );

            // Mensaje de éxito
            wc_add_notice( '✅ Producto agregado correctamente al carrito.', 'success' );

            // Evitar reenvío del formulario al refrescar
            wp_safe_redirect( wc_get_cart_url() );
            exit;
        } else {
            wc_add_notice( '❌ No se encontró un producto con esa clave.', 'error' );
        }
    }
}

⚙️ Cómo funciona

Hook woocommerce_before_cart
Inserta el formulario justo antes del listado de productos del carrito.
El formulario incluye dos campos:

Clave o SKU del producto

Cantidad

Hook template_redirect
Este hook se ejecuta cuando la página está completamente cargada y el carrito disponible.
Aquí se procesa el formulario y se agrega el producto al carrito si el SKU existe.

Mensajes automáticos

✅ Si el producto se agrega correctamente, aparece un aviso de éxito.

❌ Si el SKU no existe, se muestra un mensaje de error.

Redirección segura
wp_safe_redirect() evita que el producto se vuelva a agregar si el usuario refresca la página.

🪄 Ventajas de esta solución

Permite ventas rápidas o repetidas sin navegar el catálogo.

Ideal para clientes que ya conocen los SKUs o trabajan con listas de productos.

Compatible con caché, sesiones y métodos de carrito AJAX.

No requiere plugins adicionales.

💡 Mejora opcional

Puedes agregar autocompletado con AJAX para que, al escribir el SKU, el formulario muestre el nombre del producto antes de agregarlo.
Esto ayuda a evitar errores de clave y mejora la experiencia del usuario.
