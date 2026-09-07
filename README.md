# Controller — AutorController

[← Back](https://github.com/joycequoos/Controllers_Services/blob/main/README.md)

## Creating the Controller

### 1. Create the Controller

[![Creating Controller](https://github.com/JosiTubaroski/Controllers_Services/raw/main/img/20250226_Criando_Controller.png)](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/20250226_Criando_Controller.png)

### 2. The Controller Will Be of Type API

[![API Type Controller](https://github.com/JosiTubaroski/Controllers_Services/raw/main/img/Controlers/02_Controler_API.png)](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/02_Controler_API.png)

### 3. Creating AutorController.cs

[![Creating AutorController](https://github.com/JosiTubaroski/Controllers_Services/raw/main/img/Controlers/03_Criando_Autor_Controler.png)](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/03_Criando_Autor_Controler.png)

The complete code for `AutorController.cs` can be found [at this link](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/AutorController.cs).

## Code Explained

This code defines a controller for an ASP.NET Core API, responsible for managing authors.

### Imported Namespaces

These lines bring in the functionality needed for the code:

[![Imported Libraries](https://github.com/JosiTubaroski/AutorController/raw/main/img/03_Bibliotecas.png)](https://github.com/JosiTubaroski/AutorController/blob/main/img/03_Bibliotecas.png)

### Controller Definition

[![Defining the API Controller](https://github.com/JosiTubaroski/AutorController/raw/main/img/04_Definindo_API_Controller.png)](https://github.com/JosiTubaroski/AutorController/blob/main/img/04_Definindo_API_Controller.png)

- `[Route("api/[controller]")]` — defines that this controller will respond to requests at the `api/Autor` endpoint.
- `[ApiController]` — indicates that this class is an API controller in ASP.NET Core.
- `AutorController : ControllerBase` — extends the `ControllerBase` class, which provides basic functionality for a controller.

### Dependency Injection

[![Dependency Injection](https://github.com/JosiTubaroski/AutorController/raw/main/img/06_Injecao_Dependencia.png)](https://github.com/JosiTubaroski/AutorController/blob/main/img/06_Injecao_Dependencia.png)

- The `AutorController` receives, in its constructor, an instance of the `IAutorInterface` interface, which represents an authors service.
- `_autorInterface` stores this instance to be used within the controller.
- This pattern follows **Dependency Injection**, allowing greater flexibility and testability of the code.

### GET Method Definition

[![List Authors](https://github.com/JosiTubaroski/AutorController/raw/main/img/07_Listar_Autores.png)](https://github.com/JosiTubaroski/AutorController/blob/main/img/07_Listar_Autores.png)

**Explanation:**

1. `[HttpGet("ListarAutores")]` — indicates that this method will be accessed via an HTTP GET request, at the `api/Autor/ListarAutores` endpoint.
2. `Task<ActionResult<ResponseModel<List<AutorModel>>>>`:
  - `Task<>` — the method is asynchronous (uses `await`).
  - `ActionResult<>` — returns an HTTP result with the appropriate status.
  - `ResponseModel<List<AutorModel>>` — returns a structured response containing a list of authors.
3. `await _autorInterface.ListarAutores();` — calls the service that fetches the list of authors from the database.
4. `return Ok(autores);` — returns a `200 OK` status with the authors.

### Summarized Flow

1. The user makes a GET request to `api/Autor/ListarAutores`.
2. The `ListarAutores()` method calls `_autorInterface.ListarAutores()`, which fetches the data from the database.
3. The data is returned inside a `ResponseModel` object.
4. The API responds with `200 OK` and the list of authors.

## General Summary

- Defines a controller in ASP.NET Core to manage authors.
- Uses Dependency Injection to call services without direct coupling.
- Implements a GET endpoint to list authors.
- Uses asynchronous programming (`async`/`await`) for better performance.
