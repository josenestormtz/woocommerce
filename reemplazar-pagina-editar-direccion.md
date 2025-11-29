# 📝 Reemplazar la página “Editar dirección” de WooCommerce con una plantilla de Elementor (Método 1)

Este método consiste en crear tu propia página en Elementor, y luego redirigir la URL nativa de WooCommerce hacia tu nueva página personalizada.

✅ Paso 1 — Crear tu página personalizada en Elementor

Ve a Páginas → Añadir nueva.

Ponle un nombre, por ejemplo:
Editar Dirección Personalizada

Haz clic en Editar con Elementor.

Construye tu diseño con widgets, formularios o lo que necesites.

Publica la página y copia su URL (la vas a necesitar).

✅ Paso 2 — Redirigir la URL original de WooCommerce a tu nueva página

La URL nativa es:

/my-account/edit-address/


Sigue estos pasos:

Instala y activa el plugin Code Snippets (si no lo tienes).

Ve a Snippets → Añadir nuevo.

Ponle un nombre:
Redirigir Editar Dirección WooCommerce

Pega este código:

add_action('template_redirect', function() {
    if (is_account_page() && isset($_GET['edit-address'])) {
        wp_redirect('/editar-direccion-personalizada/'); // ← cambia por tu URL
        exit;
    }
});


Cambia la parte:

/editar-direccion-personalizada/


por el slug real de tu nueva página de Elementor.
6. Guarda y activa el snippet.

✅ Paso 3 — Probar la redirección

Ve a tu cuenta de WooCommerce:

/my-account/edit-address/billing/


o

/mi-cuenta/editar-direccion/billing/


Debes ser enviado automáticamente a tu nueva página personalizada.

🎉 ¡Listo!

Ahora tu sitio ya no usa la página nativa de Editar dirección de WooCommerce:
💠 el usuario siempre verá tu plantilla de Elementor,
💠 sin tocar archivos del core,
💠 sin riesgos en actualizaciones.
