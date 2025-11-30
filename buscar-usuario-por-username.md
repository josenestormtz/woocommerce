# 📘 Cómo buscar un usuario por Username en WordPress

En WordPress, cada usuario tiene un identificador único llamado user_login, que es su username para iniciar sesión.
A veces necesitas obtener el usuario desde PHP usando ese username, por ejemplo para APIs, validaciones o integraciones.

A continuación tienes dos formas correctas de hacerlo.

✅ Método 1 (recomendado): get_user_by('login', $username)

La forma más simple y directa.

Ejemplo:
$username = 'nestor';
$user = get_user_by('login', $username);

if ($user) {
    echo "ID del usuario: " . $user->ID;
} else {
    echo "Usuario no encontrado.";
}

✔ Ventajas:

Es rápido.

Es nativo de WordPress.

No requiere configuraciones adicionales.

🟦 ¿Cuándo usar este método?

Cuando sabes el username exacto.

Cuando solo necesitas obtener un único usuario.

Cuando vas a trabajar con su ID, email o metadata.

✅ Método 2: Usar WP_User_Query (alternativa)

Si por alguna razón get_user_by() falla (pocos casos, pero ocurre en sitios con demasiados filtros), puedes usar una consulta más robusta.

Ejemplo:
$username = 'nestor';

$query = new WP_User_Query([
    'search'         => $username,
    'search_columns' => ['user_login']
]);

$results = $query->get_results();

if (!empty($results)) {
    $user = $results[0]; // Primer resultado
    echo "Usuario encontrado. ID: " . $user->ID;
} else {
    echo "Usuario no encontrado.";
}

✔ Ventajas:

Funciona incluso si hay hooks que modifican get_user_by().

Permite búsquedas más avanzadas.

🟩 Diferencias importantes entre ambos métodos
Método	Para qué sirve	Uso
get_user_by('login', …)	Obtener un usuario exacto	Más rápido y recomendado
WP_User_Query	Buscar por columnas o con filtros	Más flexible
🔍 ¿Qué campo representa el username en WordPress?

El username siempre es el campo:

user_login

Ese es el valor que debes usar para buscar usuarios por nombre de acceso.

🎯 Conclusión

Si necesitas obtener información de un usuario usando su username:

👉 Usa get_user_by('login', $username) como primera opción.
👉 Usa WP_User_Query si necesitas más flexibilidad o si el primer método falla.
