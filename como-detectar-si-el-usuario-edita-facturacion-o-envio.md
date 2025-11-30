# 🧩 Cómo detectar si el usuario edita facturación o envío en WooCommerce

Cuando un cliente entra a Mi Cuenta → Direcciones → Editar, WooCommerce carga el template:

woocommerce/myaccount/form-edit-address.php


En este template, WooCommerce envía automáticamente una variable llamada $load_address, que te indica qué dirección el usuario está editando.

🟦 1. Valor de $load_address

WooCommerce establece:

Valor	Significado
"billing"	Dirección de facturación
"shipping"	Dirección de envío

Puedes detectar el tipo así:

if ( $load_address === 'billing' ) {
    // Es facturación
}

if ( $load_address === 'shipping' ) {
    // Es envío
}

🟦 2. Mostrar un mensaje según el tipo de dirección

Coloca este código en cualquier parte del template, por ejemplo antes de insertar tu plantilla Elementor:

if ( $load_address === 'billing' ) {
    $tipo = "facturación";
} else {
    $tipo = "envío";
}

echo "<div class='mi-info-tipo'>Editando dirección de <strong>$tipo</strong></div>";


Esto ayudará a mostrar información dinámica según el tipo de dirección que se edita.

🟦 3. Usar $load_address para cargar diferente contenido o Elementor

Si quieres que Elementor cargue una plantilla distinta dependiendo del tipo:

if ( $load_address === 'billing' ) {
    echo do_shortcode('[elementor-template id="1234"]');
} else {
    echo do_shortcode('[elementor-template id="5678"]');
}

🟦 4. Enviar el tipo de dirección a JavaScript

Si tu plantilla Elementor o tu script necesita saberlo:

?>
<script>
    const tipoDireccion = "<?php echo esc_js( $load_address ); ?>"; 
    console.log("Editando:", tipoDireccion); // billing o shipping
</script>
<?php

🟦 5. Dónde colocar este código

Dentro de tu archivo:

/wp-content/themes/TU_TEMA/woocommerce/myaccount/form-edit-address.php


Justo en el lugar donde eliminaste el formulario original y colocaste tu shortcode Elementor.

🎉 Listo

Con este tutorial ya puedes:

✔ Saber si el usuario edita facturación o envío.
✔ Mostrar plantillas Elementor distintas.
✔ Personalizar mensajes.
✔ Enviar el tipo de dirección a JavaScript.
