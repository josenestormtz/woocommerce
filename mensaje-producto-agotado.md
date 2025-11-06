```woocommerce
add_filter( 'woocommerce_get_availability_text', function( $text, $product ) {
    if ( ! $product->is_in_stock() ) {
        return ''; // ← deja vacío o pon tu propio texto
    }
    return $text;
}, 10, 2 );

add_action( 'woocommerce_single_product_summary', 'producto_agotado', 25 );
function producto_agotado() {
    global $product;
    if ( ! $product->is_in_stock() ) {    
        echo '
        <div class="aviso-stock" style="
            background: linear-gradient(135deg, #ffe5e5, #ffcccc);
            border: 1px solid #ffb3b3;
            color: #a10000;
            padding: 15px 20px;
            border-radius: 10px;
            font-weight: 600;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 15px 0;
        ">
            <span style="font-size:22px;">🚫</span>
            <span>Producto Agotado</span>
        </div>';
     }
}
```
