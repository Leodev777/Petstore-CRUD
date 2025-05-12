# 🧪 API Testing con Postman – Flujo Completo CRUD Petstore

Este proyecto está orientado a validar de manera estructurada y manual el comportamiento de la API pública de [Petstore](https://petstore.swagger.io/) mediante la herramienta Postman. Se simulan operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre dos entidades como: **Mascotas** y **Usuarios**.

> ⚠️ Esta colección NO está automatizada mediante scripts o integraciones CI/CD. Está diseñada para ser ejecutada y validada manualmente dentro del entorno Postman.

---

## 🚀 Objetivos del Proyecto

- Comprender el flujo completo de pruebas en una API REST.
- Validar las respuestas del servidor en operaciones clave.
- Simular casos de uso reales aplicando buenas prácticas de testing.
- Registrar datos dinámicos entre requests mediante variables de entorno.

---

## 🧩 Funcionalidades Probadas

El proyecto incluye pruebas manuales para los siguientes endpoints agrupados por entidad:

### 🐾 Mascotas (Pets)

| Etapa                  | Método | Endpoint                   | Descripción                                                   |
|------------------------|--------|----------------------------|---------------------------------------------------------------|
| ① Crear Mascota        | POST   | `/pet`                     | Crea una nueva mascota en el sistema con datos definidos.     |
| ② Consultar Mascota    | GET    | `/pet/{petId}`             | Verifica que la mascota creada exista.                        |
| ③ Actualizar Mascota   | PUT    | `/pet`                     | Modifica atributos como el nombre o el estado.                |
| ④ Validar Actualización| GET    | `/pet/{petId}`             | Confirma que los cambios hayan sido correctamente aplicados.  |
| ⑤ Eliminar Mascota     | DELETE | `/pet/{petId}`             | Elimina la mascota del sistema.                               |

### 👤 Usuarios (Users)

| Etapa                  | Método | Endpoint                   | Descripción                                                   |
|------------------------|--------|----------------------------|---------------------------------------------------------------|
| ① Crear Usuario        | POST   | `/user`                    | Registra un nuevo usuario con los datos especificados.        |
| ② Consultar Usuario    | GET    | `/user/{username}`         | Verifica la creación del usuario.                             |
| ③ Actualizar Usuario   | PUT    | `/user/{username}`         | Actualiza datos como el nombre o el email del usuario.        |
| ④ Validar Actualización| GET    | `/user/{username}`         | Confirma que los datos modificados estén reflejados.          |
| ⑤ Eliminar Usuario     | DELETE | `/user/{username}`         | Elimina el usuario del sistema.                               |

---

## ⚙️ Variables de Entorno Requeridas

Para ejecutar correctamente la colección, se deben definir las siguientes variables en un entorno de Postman:

| Variable        | Descripción                                 | Ejemplo                          |
|-----------------|---------------------------------------------|----------------------------------|
| `URLBase`       | URL base de la API                          | `https://petstore.swagger.io/v2`|
| `petId`         | ID dinámico de la mascota creada            | Se asigna desde la respuesta del POST |
| `username`      | Nombre del usuario creado                   | `bobby123`                       |

> 🧠 **Nota:** Las variables `key` o `token` no son necesarias ya que la API de Petstore es pública, pero podrías incluirlas si estás probando con un entorno autenticado alternativo.

---

## ✅ Ejemplos de Validaciones

Se pueden utilizar snippets básicos de Postman en la pestaña **Tests** de cada request para asegurar que las respuestas sean correctas:

```javascript
pm.test("Código de estado 200 OK", function () {
    pm.response.to.have.status(200);
});

pm.test("La mascota contiene el nombre esperado", function () {
    let jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("Bobby");
});
