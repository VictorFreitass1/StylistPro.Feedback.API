# StylistPro.Feedback.API

# Visão Geral
Esta API foi desenvolvida utilizando uma arquitetura de microservices e segue os princípios de um sistema escalável e modular. As principais funcionalidades são a implementação de operações CRUD utilizando o banco de dados ORACLE e a documentação da API configurada com OpenAPI. O padrão de design Singleton também foi aplicado para controlar instâncias específicas durante a execução.

# Funcionalidades
• ObterTodos: Retorna todos os registros do banco de dados.
• ObterPorId: Retorna um registro específico com base no ID fornecido.
• SalvarDados: Insere um novo registro no banco de dados.
• EditarDados: Atualiza um registro existente.
• DeletarDados: Remove um registro com base no ID.

# Design Patterns Utilizados

# 1. Singleton
O padrão Singleton foi utilizado para garantir que algumas classes críticas tenham apenas uma instância ao longo da execução da aplicação, evitando a criação desnecessária de múltiplos objetos e promovendo a eficiência de recursos. Este padrão foi aplicado, por exemplo, no gerenciamento de conexões com o banco de dados.

# 2. Microservices
A API foi desenvolvida seguindo a arquitetura de microservices, o que permite que cada serviço seja independente e escalável de forma autônoma. Cada módulo da aplicação está isolado e focado em uma funcionalidade específica, o que facilita a manutenção e a evolução contínua do sistema.

# Tecnologias Utilizadas
Oracle Database: Utilizado para operações CRUD.
ASP.NET Core: Framework utilizado para o desenvolvimento da API.
OpenAPI/Swagger: Configurado para gerar a documentação da API, facilitando o entendimento e o uso por desenvolvedores.

# Requisitos
.NET SDK 6.0 ou superior
Oracle Database (com conexão configurada)
Ferramenta de gerenciamento de dependências (ex: NuGet)

# Instruções para Executar a API

# 1. Clone o repositório:
git clone <link-do-repositorio>

# 2. Navegue até a pasta do projeto:
cd StylistPro.Feedback.API

# 3. Restaure os pacotes NuGet:
dotnet restore

# 4. Configure a string de conexão com o banco de dados ORACLE no arquivo appsettings.json:
"ConnectionStrings": {
  "OracleDb": "Data Source=<oracle-db-url>;User Id=<username>;Password=<password>;"
}

# 5. Execute a aplicação:
dotnet run

# 6. Acesse a documentação da API gerada pelo Swagger:
Após executar a API, navegue até http://localhost:<porta>/swagger para visualizar e interagir com a documentação.

