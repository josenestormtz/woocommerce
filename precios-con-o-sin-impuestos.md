# 💰 Mostrar precios con o sin impuestos en WooCommerce
En WooCommerce existen funciones que te permiten **controlar cómo se muestran los precios** en tus plantillas o snippets personalizados.
A continuación, se explica cómo usar tres de las más útiles.

## 🧾 1. ```wc_get_price_excluding_tax()```
Devuelve el **precio del producto sin incluir impuestos (IVA)**. Ideal cuando quieres mostrar precios netos o separar el impuesto del subtotal.

Ejemplo:
```php
$precio_sin_iva = wc_get_price_excluding_tax( $product );
echo wc_price( $precio_sin_iva ); // Muestra el precio sin IVA
```

**Uso común**:
- Mostrar precios sin impuestos en el carrito o facturación.
- Cálculos personalizados de IVA o márgenes.

## 💸 2. ```wc_get_price_including_tax()```
Devuelve el **precio del producto con el impuesto incluido** según las tasas configuradas en WooCommerce. Es ideal para mostrar precios finales visibles al cliente.

Ejemplo:
```php
$precio_con_iva = wc_get_price_including_tax( $product );
echo wc_price( $precio_con_iva ); // Muestra el precio con IVA incluido
```

**Uso común**:
- Mostrar precios “finales” en la tienda, carrito o resumen de pedido.
- Etiquetas o comparativos que incluyan impuestos.

## 💰 3. ```wc_price()```
Formatea cualquier número en **formato de moneda WooCommerce**, aplicando el símbolo, separadores y decimales definidos en tu configuración. No calcula impuestos; solo da formato visual.

Ejemplo:
```php
echo wc_price( 199.99 ); // Muestra "$199.99" o su equivalente según configuración
```

**Uso común**:
- Mostrar precios personalizados calculados manualmente.
- Asegurar consistencia visual con el resto del sitio.

## ⚙️ Ejemplo práctico combinado
```php
$precio_con_iva  = wc_get_price_including_tax( $product );
$precio_sin_iva  = wc_get_price_excluding_tax( $product );

echo '<p>Precio sin IVA: ' . wc_price( $precio_sin_iva ) . '</p>';
echo '<p>Precio con IVA: ' . wc_price( $precio_con_iva ) . '</p>';
```
Esto mostrará ambos valores en formato correcto, usando los impuestos configurados en WooCommerce.

## 📌 Recomendación
Para evitar errores:
- Asegúrate de que el producto tenga impuestos configurados.
- Verifica que WooCommerce → **Ajustes** → **Impuestos** esté habilitado.
- Usa siempre **wc_price()** para mostrar valores al usuario final.
