# 🧭 Ver qué plantillas está usando tu tienda WooCommerce

A veces necesitas saber **qué archivo de plantilla se está utilizando** para una página específica de WooCommerce (por ejemplo, el carrito, el checkout o el producto individual). WooCommerce te permite revisar esta información fácilmente desde el panel de administración.

## Pasos para ver las plantillas activas

1. Entra al panel de WordPress.
Inicia sesión en tu sitio y dirígete al escritorio.

2. Ve al menú lateral:
```nginx
WooCommerce → Estado → Plantillas
```

3. Revisa la sección de plantillas sobrescritas.
En esta sección verás dos columnas principales:
- **Plantilla original**: indica la ruta del archivo por defecto de WooCommerce.
- **Plantilla sobreescrita**: muestra si tu tema o child theme (por ejemplo, salient-child) está usando una versión personalizada del archivo.

4. Verifica las ubicaciones.
- Si ves una ruta como:
```bash
salient-child/woocommerce/cart/cart.php
```
significa que tu sitio está usando **una plantilla personalizada** para el carrito dentro del tema hijo.
- Si no aparece sobreescrita, WooCommerce está usando su **versión original del plugin**.

## 🧰 Tip útil
Si realizas cambios y **no se reflejan**, puede deberse a:
- Caché del servidor (por ejemplo, **LiteSpeed Cache**).
- El sitio está usando **una plantilla distinta** a la que editaste.
- El archivo sobreescrito está **desactualizado** respecto a la versión de WooCommerce.

## 💡 Recomendación
Antes de editar una plantilla, asegúrate de hacerlo **en el tema hijo**, nunca directamente en WooCommerce o en el tema principal.
Así evitarás perder tus personalizaciones cuando actualices el plugin o el tema.
