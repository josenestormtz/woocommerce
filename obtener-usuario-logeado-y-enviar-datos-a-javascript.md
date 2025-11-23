# 📘 Obtener el usuario logeado y enviar sus datos a JavaScript

Cómo obtener los datos del usuario logeado desde PHP

Cómo enviarlos a JavaScript

Qué otros valores puedes obtener del usuario

Cómo usarlos en tu archivo JS

✅ 1. Snippet para obtener usuario y enviarlo a JS

Coloca esto en Code Snippets o en functions.php:

add_action( 'wp_enqueue_scripts', function() {

    // Encolar tu JS
    wp_enqueue_script(
        'mi-script',
        get_stylesheet_directory_uri() . '/js/mi-script.js',
        array('jquery'),
        false,
        true
    );

    // Obtener usuario logeado
    $user = wp_get_current_user();

    // Pasar datos a JS
    wp_localize_script( 'mi-script', 'MiUsuario', array(
        'id'           => $user->ID,
        'username'     => $user->user_login,
        'nombre'       => $user->display_name,
        'nombre_real'  => $user->first_name,
        'apellido'     => $user->last_name,
        'email'        => $user->user_email,
        'rol'          => isset($user->roles[0]) ? $user->roles[0] : null,
        'capabilities' => $user->caps,
        'logeado'      => is_user_logged_in(),
    ));
});

🧾 2. ¿Qué valores puedo obtener del usuario logeado?

Aquí está la lista completa de propiedades estándar del objeto $user que WordPress te permite obtener:

Propiedad PHP	Descripción
$user->ID	ID numérico del usuario
$user->user_login	Nombre de usuario (login)
$user->user_email	Email del usuario
$user->display_name	Nombre público que se muestra
$user->first_name	Nombre real
$user->last_name	Apellido real
$user->user_nicename	URL amigable del perfil
$user->user_registered	Fecha de registro
$user->roles	Lista de roles del usuario
$user->caps	Capacidades (permisos)
$user->user_url	Sitio web del usuario
$user->description	Biografía
$user->nickname	Apodo del usuario
$user->user_status	Estado (normalmente 0)
🔧 3. ¿Y los metadatos personalizados?

Si usas plugins como WooCommerce, puedes obtener datos adicionales:

📦 Campos de WooCommerce
get_user_meta( $user->ID, 'billing_first_name', true );
get_user_meta( $user->ID, 'billing_last_name', true );
get_user_meta( $user->ID, 'billing_phone', true );
get_user_meta( $user->ID, 'billing_address_1', true );
get_user_meta( $user->ID, 'billing_city', true );


Puedes enviarlos también a JS así:

'billing_city' => get_user_meta( $user->ID, 'billing_city', true )

🧩 4. Ejemplo en tu archivo JS (mi-script.js)
console.log("Datos del usuario:", MiUsuario);

if (MiUsuario.logeado) {
    console.log("Nombre:", MiUsuario.nombre);
    console.log("Email:", MiUsuario.email);
    console.log("Rol:", MiUsuario.rol);
}

🧠 5. Ejemplo práctico en HTML

Si quieres mostrar el nombre del usuario:

if (MiUsuario.logeado) {
    document.querySelector(".bienvenida").innerText =
        "Hola " + MiUsuario.nombre + "!";
}
