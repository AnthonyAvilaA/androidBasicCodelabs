# Basics Codelab – Jetpack Compose (Versión Detallada)

Este README ofrece una explicación completa y detallada del proyecto **Basics Codelab**, desarrollado con **Jetpack Compose**. Es ideal como documentación de referencia técnica y como apoyo para comprender los fundamentos de Compose: estados, animaciones, listas perezosas, composables y navegación simple.

---

## 📌 Estructura Fundamental de la Aplicación

### 🏁 Activity Principal: `MainActivity`

La aplicación inicia su interfaz mediante:

* **`setContent {}`** → punto de entrada de Jetpack Compose.
* **`BasicsCodelabTheme`** → aplica esquemas de color, tipografía y estilos basados en Material 3.
* **`MyApp()`** → composable principal que controla qué pantalla mostrar.

La Activity no contiene lógica adicional, siguiendo buenas prácticas y manteniendo la UI completamente declarativa.

---

## 🧭 Navegación Interna: `MyApp`

`MyApp` gestiona una navegación muy simple basada en un booleano:

* Si `shouldShowOnboarding = true` → se muestra la pantalla de bienvenida.
* Si `false` → se muestran las tarjetas de saludo.

Esto se logra mediante:

```kotlin
var shouldShowOnboarding by rememberSaveable { mutableStateOf(true) }
```

**Por qué usar `rememberSaveable`:**

* Conserva el estado al rotar la pantalla.
* Permite recomposición sin perder el valor.
* Es ideal para pasos de navegación entre pantallas.

La estructura base del contenedor es:

```kotlin
Surface(color = MaterialTheme.colorScheme.background) { ... }
```

---

## 👋 Pantalla de Onboarding

`OnboardingScreen()` muestra:

* Un mensaje de bienvenida.
* Un botón centrado que cambia el estado.

**Características clave:**

* Uso de `Column` para centrar contenido.
* Padding vertical para separar el botón.
* Sencillez de navegación basada en un callback.

```kotlin
Column(
    verticalArrangement = Arrangement.Center,
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Text("Welcome to the Basics Codelab!")
    Button(onClick = onContinueClicked) {
        Text("Continue")
    }
}
```

Esta pantalla es un ejemplo claro de cómo Compose permite estructuras limpias y declarativas.

---

## 📜 Lista de Saluditos (`Greetings`)

Cuando el onboarding termina, `Greetings()` muestra una lista con:

* 1000 elementos generados dinámicamente.
* Renderizados de forma eficiente mediante **LazyColumn**.

```kotlin
LazyColumn {
    items(names) { name -> Greeting(name) }
}
```

### ¿Por qué LazyColumn?

* Solo renderiza los elementos visibles.
* Reduce carga en memoria.
* Es perfecto para listas largas.

Cada item es gestionado por `Greeting(name)`.

---

## 🃏 Tarjeta de Saludo: `Greeting`

Cada saludo está contenido dentro de un **Card** Material 3 con:

* Color primario del tema.
* Padding horizontal y vertical.

```kotlin
Card(
    colors = CardDefaults.cardColors(
        containerColor = MaterialTheme.colorScheme.primary
    )
) {
    CardContent(name)
}
```

Esta separación facilita reutilizar estilos y componentes.

---

## 🎚️ Contenido Expandible: `CardContent`

Este composable incluye:

* Texto principal "Hello"
* Nombre estilizado con `headlineMedium` y `ExtraBold`
* Texto adicional opcional que se muestra al expandir
* Botón de icono para gestionar expansión

### 🔁 Estado interno

```kotlin
var expanded by rememberSaveable { mutableStateOf(false) }
```

### ✨ Animación de expansión

Usa `animateContentSize` para animar suavemente el cambio de altura.

```kotlin
.animateContentSize(
    animationSpec = spring(
        dampingRatio = Spring.DampingRatioMediumBouncy,
        stiffness = Spring.StiffnessLow
    )
)
```

✔ Transiciones fluidas
✔ Estética profesional
✔ Sin código complejo de animación

### 🧩 Texto extra

El texto expandido es un demo que muestra cómo gestionar contenido adicional.

---

## 🧪 Previsualizaciones

El proyecto incluye varias previews para desarrollo ágil:

### ✔ Tema oscuro

### ✔ Vistas compactas

### ✔ Pantallas específicas

📸 **My App Preview:**

![My App Preview](My%20App%20Preview.png)

Ejemplo de preview:

```kotlin
@Preview(showBackground = true)
@Composable
fun MyAppPreview() {
    MyApp(Modifier.fillMaxSize())
}
```

Las previews agilizan la iteración visual del diseño.

---

## 🧠 Conceptos Importantes Ilustrados en Este Proyecto

### 🔹 Estado y persistencia

* `rememberSaveable` evita perder datos tras recomposición.
* Ideal para navegación y mantenimiento de UI.

### 🔹 Listas perezosas

* Eficientes y esenciales para apps con contenido dinámico.

### 🔹 Animación declarativa

* `animateContentSize` simplifica cambios visuales sin código imperativo.

### 🔹 Material 3

* Colores, tipografía y contro- les están completamente integrados.

### 🔹 Composables modulares

* Cada parte de la UI está separada, lo que facilita escalabilidad.

---

## 📚 Recursos Recomendados

* Jetpack Compose: [https://developer.android.com/jetpack/compose](https://developer.android.com/jetpack/compose)
* Material 3 en Compose: [https://m3.material.io](https://m3.material.io)
* Lazy layouts: [https://developer.android.com/jetpack/compose/lists](https://developer.android.com/jetpack/compose/lists)
* Estado en Compose: [https://developer.android.com/jetpack/compose/state](https://developer.android.com/jetpack/compose/state)

