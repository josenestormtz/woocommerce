# 📝 Insertar una plantilla de Elementor dentro de una plantilla de WooCommerce

Este tutorial explica cómo mostrar una plantilla creada con Elementor directamente dentro de un template personalizado de WooCommerce, por ejemplo en la página Editar cuenta.

✅ 1. Crear o identificar una plantilla en Elementor

Ve a Elementor → Plantillas → Guardadas.

Abre la plantilla que quieres usar.

Mira la URL del navegador; verás algo así como:

post=12345


El número es el ID de la plantilla (ejemplo: 12345).

✅ 2. Copiar la plantilla de WooCommerce al tema hijo

Para modificar la plantilla “Editar cuenta”, copia:

wp-content/plugins/woocommerce/templates/myaccount/form-edit-account.php


Dentro de tu tema hijo en:

wp-content/themes/tu-child-theme/woocommerce/myaccount/form-edit-account.php


WooCommerce usará esta versión en lugar de la original.

✅ 3. Insertar la plantilla de Elementor dentro del archivo PHP

Dentro del archivo form-edit-account.php, en el lugar donde quieras mostrar tu diseño, agrega:

<?php
echo \Elementor\Plugin::$instance->frontend->get_builder_content_for_display( 12345 );
?>


Reemplaza 12345 por el ID de tu plantilla de Elementor.

Este método carga:

El contenido

El diseño

El CSS generado por Elementor

Directamente dentro de la pantalla de WooCommerce.

✅ 4. Guardar y probar

Guarda el archivo PHP.

Ve a Mi cuenta → Editar cuenta.

Verás tu diseño de Elementor dentro de la plantilla nativa de WooCommerce.

🎉 Resultado

Con esto logras:

Mantener el menú lateral, header y footer de tu sitio.

Reemplazar completamente el contenido estándar.

Usar Elementor para diseñar la página sin perder la estructura de WooCommerce.
