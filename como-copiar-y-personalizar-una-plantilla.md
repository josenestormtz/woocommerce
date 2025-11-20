# 📝 Cómo copiar y personalizar una plantilla de WooCommerce en tu theme

Cuando necesitas modificar una plantilla de WooCommerce (como Editar Cuenta), no debes editar los archivos del plugin, porque se perderán con cada actualización.
En su lugar, WooCommerce permite sobrescribir plantillas copiándolas en tu theme o child theme.

✅ 1. Ubicar la plantilla original en WooCommerce

Los archivos base están en:

/wp-content/plugins/woocommerce/templates/


Para el ejemplo que usamos —la plantilla Editar Cuenta— el archivo se encuentra en:

/wp-content/plugins/woocommerce/templates/myaccount/form-edit-account.php

✅ 2. Copiar el archivo a tu Child Theme

Copia ese archivo completo y pégalo en la siguiente ruta dentro de tu child theme:

/wp-content/themes/tu-child-theme/woocommerce/myaccount/form-edit-account.php


Si las carpetas no existen, créalas manualmente.

WooCommerce detectará automáticamente la copia y usará tu versión personalizada en lugar de la del plugin.

✅ 3. Editar la plantilla en tu child theme

Ahora sí puedes modificar el archivo libremente:

Cambiar diseño

Ocultar campos

Reorganizar elementos

Agregar HTML personalizado

Integrar Bootstrap

Crear páginas más limpias y modernas

✅ 4. Evitar el aviso de versión desactualizada

En la parte superior del archivo existe una línea como:

 * @version 9.4.0


Cámbiala por la versión actual que WooCommerce indica en el aviso, por ejemplo:

 * @version 9.7.0


Esto elimina el mensaje “plantilla obsoleta”.

📌 Resultado

Al finalizar, WooCommerce usa tu plantilla personalizada desde el child theme, mantienes compatibilidad, puedes editar sin riesgo y preservas los cambios tras futuras actualizaciones.
