# Nerdearla 2025 - Postman + IA

---

## Endpoints de prueba

- `https://fakeapi.platzi.com/en/rest/products/`

---

## Prompt Template para armar collections

> Usa este template para pedirle a la IA que genere una colección de Postman lista para importar.

```text
Rol: [Especifica el rol como el que quieres que actúe la IA.]
Tarea: [Describe el objetivo principal de lo que quieres obtener.]
Información Clave: [Proporciona toda la información necesaria para que la IA pueda trabajar:]
  - Endpoint
  - Request de ejemplo
  - Respuestas de ejemplo (success / error)
Especificaciones de la Colección:
  - La colección debe llamarse "[nombre de la colección]".
  - Crea [#] requests: "request 1", "request 2" y "request 3".
  - Para cada request, incluir un test. Cada test debe:
    - Especificación 1
    - Especificación 2
    - Especificación 3
Instrucción Final: [Indica el formato de la respuesta. El mejor formato es un bloque de código con la estructura completa de la colección en Postman, lista para copiar y pegar. Esto puede ser un objeto JSON que Postman pueda importar.]
```

# Ejemplo usando el Prompt Template para armar collections

**Rol:** Actúa como un experto en pruebas de API y automatización de QA.

**Tarea:** Ayúdame a crear una colección de Postman completa y funcional para validar los responses de una API. Cada request en la colección debe tener tests integrados que validen el código de estado, la estructura del cuerpo y los valores específicos de la respuesta.

**Información Clave:**

* **Endpoint:** `https://api.escuelajs.co/api/v1/products/`
* **Request Base (JSON):**
    ```json
    {
      "title": "New Product",
      "price": 10,
      "description": "A description",
      "categoryId": 1,
      "images": ["[https://placehold.co/600x400](https://placehold.co/600x400)"]
    }
    ```

**Respuestas de Ejemplo (JSON):**

* **Caso de Éxito (Status 201):**
    ```json
    {
      "title": "New Product",
      "slug": "new-product",
      "price": 10,
      "description": "A description",
      "images": ["[https://placehold.co/600x400](https://placehold.co/600x400)"],
      "category": {
        "id": 1,
        "name": "Clothes",
        "image": "[https://placehold.co/600x400](https://placehold.co/600x400)",
        "slug": "clothes"
      },
      "id": 210,
      "creationAt": "2023-01-03T16:51:33.000Z",
      "updatedAt": "2023-01-03T16:51:33.000Z"
    }
    ```

* **Caso de Error por No enviar item categoryID como parte del request (Status 400):**
    ```json
    {
      "message": [
        "categoryId should not be empty",
        "categoryId must be a number conforming to the specified constraints"
      ],
      "error": "Bad Request",
      "statusCode": 400
    }
    ```

* **Caso de Error por enviar un categoryID con valor de tipo string (Status 400):**
    ```json
    {
      "message": [
        "categoryId should not be empty",
        "categoryId must be a number conforming to the specified constraints"
      ],
      "error": "Bad Request",
      "statusCode": 400
    }
    ```

* **Caso de Error por Producto con el mismo nombre de uno ya existente (Status 409):**
    ```json
    {
      "message": [
        "Nombre de producto ya existe"
      ],
      "error": "Conflict",
      "statusCode": 409
    }
    ```

**Especificaciones de la Colección:**

* La colección debe llamarse `"Pruebas API Crear Productos"`.
* Crea 4 requests:
    * `"Crear Producto Exitoso"`
    * `"Error - categoryID no enviado"`
    * `"Error - categoryID con valor de tipo string"`
    * `“Error - Nombre de producto ya existente”`
* Para cada request, el test debe:
    * Verificar que el status code coincida con el caso de ejemplo.
    * Verificar que el cuerpo de la respuesta tenga la estructura y campos del ejemplo.
    * Para el caso de éxito, valida que el atributo `creationAt` sea una fecha válida y que sea la fecha de hoy.
    * Para el caso de éxito, valida que el atributo `updatedAt` sea una fecha válida y que sea igual a la del atributo `creationAt`.

**Instrucción Final:** Genera el objeto JSON de la colección de Postman que contenga los requests con sus respectivos tests, siguiendo todas las especificaciones. Indícame paso a paso como importar esta colección a Postman.

