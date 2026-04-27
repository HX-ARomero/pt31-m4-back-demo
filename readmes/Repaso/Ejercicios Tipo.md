# Ejercicios Tipo de Defensa de PI

# 1. Filtro
- Crear un FILTRO en "GET /users" de modo que:  
  - Reciba por Query el nombre del país, y devuelva solamente los usuarios residentes en el país solicitado
  - La ruta GET /users debe conservar también el paginado que ya tiene, pero sobre los usuarios filtrados

# 2. Ordenamientos
- Crear un ORDENAMIENTO en "GET /users" de modo que:
   - Reciba por Query "asc" o "desc", y cuyo valor por defecto sea "asc" (si no se envía este valor por query)
   - Si se recibe "asc": devuelva los usuarios ordenados en forma ascendente (de la "A" a la "Z") por la propiedad "name"
   - Si se recibe "des": devuelva los usuarios ordenados en forma descendente (de la "Z" a la "A") por la propiedad "name"
   - La ruta GET /users debe conservar también el paginado que ya tiene

# 3. GET /categories/:id
- Crear una Ruta "GET /categories/:id":
   - Recibir el "id" del producto a obtener por params
   - Buscar y retornar el producto correspondiente
   - Si no se encuentra el producto, retornar una excepción con un mensaje representativo

# 4. Borrado Lógico
- Implementar el borrado lógico en la ruta "DELETE /users":
   - Crear una nueva propiedad "isActive" en la entidad "User" que tenga un valor true por defecto
   - Al borrar un usuario, no eliminarlo de la base de datos, sino pasar la propiedad "isActive" a false
   - En la ruta "GET /users" filtrar los usuarios cuya propiedad "isActive: false" de modo de no retornarlos (estos usuarios son virtualmente invisibles para nosotros)

# 5. Agregar nuevo campo a la Entidad Users
- Agregar a la Entidad Users el Atributo "birthdate":
- Debe ser una fecha con el formato "dd/mm/yyyy"
- Debe marcarse como obligatorio

# 6. Auth
- Crear un nuevo rol de "SuperAdmin", y proteger la ruta "GET /products"
   - Crear lo necesario en la entidad y el dto
   - Setear la propiedad correspondiente en la Metadata de la ruta
   - Crear el Guardián que validará el paso

# 7. Estandarización de Respuesta
- Unificar la respuesta de todos los Endpoints de tal modo que:
  - Nuestro Backend siempre retorne un objeto
  - Definiendo un formato estándar de respuesta según una interfaz
  - Tipar los retornos de los métodos

```ts
export interface ApiResponse<T> {
	success: boolean;
	message: string;
	data: T;
	error: U;
	timestamp: Data;
}

{
	"success": false,
	"message": "Usuario no encontrado",
	"data": null,
	"errors": null,
	"timestamp": "..."
}

// Ejemplo de retorno de Array:
{
	"success": true,
	"message": "Usuarios obtenidos correctamente",
	"data": [{...}, {...}],
	"errors": null,
	"timestamp": "2026-01-13T20:10:00.000Z"
}

// Ejemplo de retorno de ID:
{
	"success": true,
	"message": "Usuario creado correctamente",
	"data": { "id": 42 },
	"errors": null,
	"timestamp": "2026-01-13T20:10:00.000Z"
}
```

# 9. INTERCEPTOR
- Crear un interceptor que filtre el password de los usuarios
  - getAllUsers => Interceptor (saca el password) => Al Cliente

# 10. CREAR MIDDLEWARE
Interceptores, Guardianes, Pipes

| Tipo                | Cuándo se ejecuta                | Para qué sirve                         |
| ------------------- | -------------------------------- | -------------------------------------- |
| 🧩 **Pipe**         | Antes del controlador            | Validar y transformar datos            |
| 🛡️ **Guard**        | Antes de los Pipes               | Autenticación y autorización           |
| 🎯 **Interceptor**  | Antes y después del controlador  | Transformar respuesta, logging, cache  |

# 11. Simulacro de Defensa | EJERCICIO
- Baneo de Usuarios por parte del Administrador
  1. Crear nuevo atributo en el Modelo Users de la Base de Datos
    - Llamarlo "isBlocked" y cuyo tipo sea "boolean"
    - Darle valor "false" por defecto
    - Impedir que el valor pueda ser enviado en el Body
  2. Crear una ruta "PUT /users/blocked/:id"
    - Esta ruta cambia el valor de "isBlocked" al usuario cuyo ID se recibe por params
    - Proteger la ruta para que solo sea accesible por Administradores
  3. Agregar este atributo al Payload del Token
    - Restringir el acceso a todo usuario bloqueado

# 12. Simulacro de Checkpoint
- [Checipoint de Práctica](../Regalos/SimulacroChoice.md)