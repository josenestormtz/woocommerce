# ⚙️ Administrar scripts en una página de WooCommerce

## 🎯 Objetivo
Aprender a **agregar o quitar scripts y estilos** (como Bootstrap o los de tu tema) **solo** en la página **Editar direcciones** del área *Mi cuenta* de WooCommerce.

## 🧩 Paso 1: Detectar la página y el endpoint activo
WooCommerce utiliza *endpoints* para manejar cada pestaña de “Mi cuenta”.

✅ 1. Detectar página por slug
```php
if ( is_page( 'mi-pagina' ) ) {
    // Código para esa página
}
```

2. También funciona con ID:
```php
if ( is_page(123) ) {
    // Esta es la página con ID 123
}
```

3. Tambien Podemos detectar en qué parte está el usuario con:
```php
WC()->query->get_current_endpoint();
```

Por ejemplo:
- ```edit-address``` → Editar direcciones
- ```orders``` → Pedidos
- ```downloads``` → Descargas

## 🧠 Paso 2: Administrar scripts según la página
Agrega el siguiente snippet a tu archivo ```functions.php``` del tema hijo o en tu plugin de snippets:

```php
add_action( 'wp_enqueue_scripts', function() {

    // Verifica que estamos en el área "Mi cuenta"
    if ( is_account_page() ) {

        // Detectar el endpoint actual
        $current_endpoint = WC()->query->get_current_endpoint();

        // --- 🚀 EJEMPLO: Solo en Editar Direcciones ---
        if ( $current_endpoint === 'edit-address' ) {

            // ✅ Agregar Bootstrap
            wp_enqueue_style(
                'bootstrap-css',
                'https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css',
                array(),
                '5.3.3'
            );

            wp_enqueue_script(
                'bootstrap-js',
                'https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js',
                array('jquery'),
                '5.3.3',
                true
            );

            // ❌ Quitar un estilo del tema (opcional)
            wp_dequeue_style( 'theme-style' );

            // ❌ Quitar un script innecesario
            wp_dequeue_script( 'alguno-que-no-necesites' );

        } else {
            // En otras secciones puedes quitar Bootstrap si fue cargado antes
            wp_dequeue_style( 'bootstrap-css' );
            wp_dequeue_script( 'bootstrap-js' );
        }
    }
});
```

## 🧠 Cómo funciona
- ```wp_enqueue_style()```	Agrega un archivo CSS
- ```wp_enqueue_script()```	Agrega un archivo JS
- ```wp_dequeue_style()```	Elimina un estilo que se haya cargado previamente
- ```wp_dequeue_script()```	Elimina un script ya encolado

El código primero detecta si estás en la página de **Mi cuenta**, luego revisa si el endpoint activo es **Editar direcciones**, y dependiendo del resultado, **agrega o quita scripts**.

## 🔍 Ejemplo de URLs donde se aplica
```text
https://tusitio.com/mi-cuenta/edit-address/
https://tusitio.com/mi-cuenta/edit-address/billing/
https://tusitio.com/mi-cuenta/edit-address/shipping/
```

## ✅ Resultado
Con este método podrás:
- Agregar scripts o estilos personalizados solo donde los necesites.
- Evitar sobrecargar otras páginas con archivos innecesarios.
- Optimizar el rendimiento y mantener el control del diseño.
