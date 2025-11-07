# Personalizar la pestaña “Registrarse” en WooCommerce

Este snippet modifica la pestaña “**Registrarse**” en la pantalla **Mi cuenta** de WooCommerce, reemplazando el contenido del formulario por un mensaje personalizado y un botón, además de cambiar el título por “Registro”.

## 📌 1. Agregar contenido personalizado al inicio del formulario
```php
add_action( 'woocommerce_register_form_start', function() {
    if ( get_option( 'woocommerce_enable_myaccount_registration' ) === 'yes' ) {
        ?>
        <div style="text-align: center; margin-bottom: 20px;">
            <p>Más que velas, experiencias. En Dekandela fusionamos arte, aroma y luz en cada creación hecha a mano.</p>
            <a href="https://dk.dekandela.com.mx/registro/" class="button" style="margin-top:10px; width: 100%; font-size:14px; padding: 15px 22px;">Regístrate aquí</a>
        </div>
        <?php
    }
}, 5 );
```

### 🔍 Explicación:
- Usa el hook ```woocommerce_register_form_start``` para insertar contenido justo **antes del formulario de registro**.
- El condicional ```get_option( 'woocommerce_enable_myaccount_registration' ) === 'yes'``` asegura que el formulario esté habilitado.
- Se agrega un bloque con un mensaje centrado y un botón que redirige a una página personalizada de registro.

## 🏷️ 2. Cambiar el texto “Registrarse” por “Registro”
```php
add_filter( 'gettext', 'cambiar_texto_registrarse', 20, 3 );
function cambiar_texto_registrarse( $translated_text, $text, $domain ) {
    if ( 'woocommerce' === $domain && 'Register' === $text ) {
        $translated_text = 'Registro';
    }
    return $translated_text;
}
```

### 🔍 Explicación:
- Este filtro intercepta las traducciones de WooCommerce.
- Cada vez que WooCommerce intenta mostrar la palabra “**Register**”, la reemplaza por “**Registro**”.
- No afecta otras partes del sitio ni requiere modificar plantillas.

## ✨ Resultado final
- El título de la pestaña cambia a “**Registro**”.
- Se muestra un mensaje elegante y un botón para redirigir al registro personalizado.
- Se mantiene la estructura original del área “Mi cuenta”, sin romper la compatibilidad con WooCommerce.
