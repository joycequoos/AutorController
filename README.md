# Controller — AutorController

[← Voltar](https://github.com/JosiTubaroski/Controllers_Services/blob/main/README.md)

## Criando o Controller

### 1. Criar a Controller

![Criando Controller](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/20250226_Criando_Controller.png)

### 2. O Controller Será do Tipo API

![Controller do Tipo API](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/02_Controler_API.png)

### 3. Criando a AutorController.cs

![Criando AutorController](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/03_Criando_Autor_Controler.png)

O código completo da `AutorController.cs` pode ser consultado [neste link](https://github.com/JosiTubaroski/Controllers_Services/blob/main/img/Controlers/AutorController.cs).

## Código Explicado

Esse código define um controller para uma API no ASP.NET Core, responsável por gerenciar autores.

### Namespaces Importados

Essas linhas trazem as funcionalidades necessárias para o código:

![Bibliotecas Importadas](https://github.com/JosiTubaroski/AutorController/blob/main/img/03_Bibliotecas.png)

### Definição do Controller

![Definindo o API Controller](https://github.com/JosiTubaroski/AutorController/blob/main/img/04_Definindo_API_Controller.png)

- `[Route("api/[controller]")]` — define que este controller responderá às requisições no endpoint `api/Autor`.
- `[ApiController]` — indica que essa classe é um controller de API no ASP.NET Core.
- `AutorController : ControllerBase` — estende a classe `ControllerBase`, que fornece funcionalidades básicas para um controller.

### Injeção de Dependência

![Injeção de Dependência](https://github.com/JosiTubaroski/AutorController/blob/main/img/06_Injecao_Dependencia.png)

- O `AutorController` recebe, no construtor, uma instância da interface `IAutorInterface`, que representa um serviço de autores.
- `_autorInterface` armazena essa instância para ser usada dentro do controller.
- Esse padrão segue a **Injeção de Dependência**, permitindo maior flexibilidade e testabilidade do código.

### Definição do Método GET

![Listar Autores](https://github.com/JosiTubaroski/AutorController/blob/main/img/07_Listar_Autores.png)

**Explicação:**

1. `[HttpGet("ListarAutores")]` — indica que esse método será acessado via requisição HTTP GET, no endpoint `api/Autor/ListarAutores`.
2. `Task<ActionResult<ResponseModel<List<AutorModel>>>>`:
   - `Task<>` — o método é assíncrono (usa `await`).
   - `ActionResult<>` — retorna um resultado HTTP com status adequado.
   - `ResponseModel<List<AutorModel>>` — retorna uma resposta estruturada contendo uma lista de autores.
3. `await _autorInterface.ListarAutores();` — chama o serviço que busca a lista de autores no banco de dados.
4. `return Ok(autores);` — retorna um status `200 OK` com os autores.

### Fluxo Resumido

1. O usuário faz uma requisição GET para `api/Autor/ListarAutores`.
2. O método `ListarAutores()` chama `_autorInterface.ListarAutores()`, que busca os dados no banco.
3. Os dados são retornados dentro de um objeto `ResponseModel`.
4. A API responde com `200 OK` e a lista de autores.

## Resumo Geral

- Define um controller no ASP.NET Core para gerenciar autores.
- Utiliza Injeção de Dependência para chamar serviços sem acoplamento direto.
- Implementa um endpoint GET para listar autores.
- Usa programação assíncrona (`async`/`await`) para melhor desempenho.
