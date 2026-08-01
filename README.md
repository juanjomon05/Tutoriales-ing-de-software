# Tutorial 02 – Errores Detectados (Express + TypeScript)

Como parte de la tarea, se revisó el código del tutorial y se encontraron **11 errores** intencionales:

1. **Layout no valida `viewData`** — el `<h1>` del layout leía `viewData.title` sin comprobar que existiera, rompiendo la app al entrar a `/main-point`.
2. **Render inconsistente en `Main_Point`** — no envuelve los datos en `{ viewData: viewData }` como sí hacen los demás métodos del controlador. Es la causa raíz del error #1.
3. **`Book` no importado en el controlador** — el método `show` lo usa sin haberlo importado, causando `ReferenceError`.
4. **Inconsistencia `category` / `Category`** — el modelo define la propiedad en mayúscula, pero varias vistas la llaman en minúscula, propiedad que no existe.
5. **Import con distinta capitalización de archivo** — se importa `data/books.js` pero el archivo creado es `Books.ts`. Funciona en Windows, falla en sistemas sensibles a mayúsculas (Linux/macOS, producción).
6. **Uso de `toLocaleString()` para precios** — formatea según el idioma del sistema (coma en vez de punto) y recorta ceros decimales, dando precios inconsistentes entre libros.
7. **Tipado `any` en vez de `Request`/`Response`** — dos métodos pierden el tipado fuerte que sí usan los demás, anulando el beneficio de TypeScript.
8. **Sin manejo de errores en `show`** — un id inexistente lanza una excepción sin capturar, mostrando un stack trace crudo al usuario.
9. **`parseInt(req.params.id)` sin validar** — un id no numérico da `NaN` sin un mensaje de error claro.
10. **Grid mal usado en la vista de detalle** — el contenedor tiene una sola columna, pero un elemento interno intenta abarcar dos, sin efecto real (CSS muerto).
11. **Imagen de portada fija para todos los libros** — se usa la misma URL para cualquier libro, y el modelo ni siquiera tiene un campo para variarla.
