# 🧾 Cambiar el texto “Acceder” en WooCommerce

## 📋 Descripción
Este snippet reemplaza el texto **“Acceder”** (o “Login”) que aparece en el formulario de la página **Mi cuenta** de WooCommerce, por cualquier texto personalizado.  
Es ideal si deseas que el botón diga, por ejemplo, **“Iniciar sesión”**, **“Entrar a mi cuenta”** o cualquier otro mensaje más personalizado.

---

## ⚙️ Instrucciones (usando Code Snippets)

1. En el panel de WordPress, ve a **Code Snippets → Añadir nuevo**.  
2. Asigna un nombre descriptivo, por ejemplo:  
   **Cambiar texto “Acceder” en WooCommerce**.  
3. Copia y pega el siguiente código en el área de código PHP:  

```php
/**
 * Cambiar el texto "Acceder" o "Login" en WooCommerce.
 * 
 * Este filtro reemplaza el texto traducido por uno personalizado
 * sin necesidad de modificar archivos del core o del tema.
 */

add_filter('gettext', 'cambiar_texto_acceder', 20, 3);

function cambiar_texto_acceder($translated_text, $text, $domain) {
    
    // Verifica si el texto proviene de WooCommerce
    if ($domain === 'woocommerce') {

        // Cambia "Acceder" (traducción en español) o "Login" (original)
        if ($text === 'Acceder' || $text === 'Login') {
            $translated_text = 'Entrar a mi cuenta'; // ← texto personalizado
        }
    }

    return $translated_text;
}
```

4. En la sección **Ubicación**, elige **Ejecutar en toda la web**.  
5. Guarda y activa el snippet.  
6. Actualiza la página **Mi cuenta** (`/mi-cuenta`) y verifica el cambio.

---

## 🧩 Personalización
Puedes cambiar esta línea:
```php
$translated_text = 'Entrar a mi cuenta';
```
por el texto que desees mostrar, por ejemplo:
```php
$translated_text = 'Iniciar sesión';
```

---

## 🧠 Notas
- Este método usa el **filtro `gettext`**, que intercepta las cadenas de traducción de WordPress.  
- Es una solución **segura y actualizable**, ya que no modifica los archivos originales de WooCommerce.  
- Funciona para cualquier texto de WooCommerce; solo debes cambiar la condición `$text === '...'`.

---

## 🏁 Ejemplo de resultado
**Antes:**  
> Botón: “Acceder”

**Después:**  
> Botón: “Entrar a mi cuenta”
