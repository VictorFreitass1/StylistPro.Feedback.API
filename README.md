# StylistPro.Feedback.API

## Integrantes
- RM98695  - Breno Giacoppini Câmara   
- RM551744 - Jaqueline Martins dos Santos   
- RM97510  - Mariana Bastos Esteves   
- RM551155 - Matheus Oliveira Macedo   
- RM99982  - Victor Freitas Silva   

## Visão Geral
Esta API foi desenvolvida utilizando uma arquitetura de microservices e segue os princípios de um sistema escalável e modular. As principais funcionalidades são a implementação de operações CRUD (Create, Read, Update e Delete) utilizando o banco de dados ORACLE e a documentação da API configurada com OpenAPI. O padrão de design Singleton também foi aplicado para controlar instâncias específicas durante a execução.

## Estrutura de Camadas

- **Presentation Layer (Camada de Apresentação)**: Essa camada lida com a comunicação entre o cliente e a aplicação. Utilizamos o framework ASP.NET Core para gerenciar os endpoints da API.

- **Application Layer (Camada de Aplicação)**: Contém a lógica de negócios de alto nível, coordenando operações entre a camada de domínio e a camada de apresentação.

- **Domain Layer (Camada de Domínio)**: Define as entidades de domínio e as regras de negócios centrais.

- **Infrastructure Layer (Camada de Infraestrutura)**: Lida com tecnologias externas como acesso ao banco de dados.

## Funcionalidades
### ObterTodos: Retorna todos os registros do banco de dados.
- Entrada: Requisição para listar feedbacks. <br/>
- Processo: Recuperação dos dados dos feedbacks do banco de dados. <br/>
- Saída: Lista de feedbacks com detalhes.

### ObterPorId: Retorna um registro específico com base no Id fornecido.
- Entrada: Id do feedback a ser listado. <br/>
- Processo: Recuperação dos dados do feedback do banco de dados <br/>
- Saída: Lista os detalhes do feedback pelo localizados pelo Id

### SalvarDados: Insere um novo registro no banco de dados.
- Entrada: Avaliação e comentário do feedback. <br/>
- Processo: Validação e armazenamento no banco de dados. <br/>
- Saída: Confirmação da criação do feedback.

### EditarDados: Atualiza um registro existente.
- Entrada: Id do feedback e dados atualizados. <br/>
- Processo: Validação e atualização do feedback no banco de dados. <br/>
- Saída: Confirmação da atualização

### DeletarDados: Remove um registro com base no Id.
- Entrada: Id do feedback a ser excluído. <br/>
- Processo: Remoção do feedback no banco de dados. <br/>
- Saída: Confirmação da exclusão

## Design Patterns Utilizados

### 1. Singleton
O padrão Singleton foi utilizado para garantir que algumas classes críticas tenham apenas uma instância ao longo da execução da aplicação, evitando a criação desnecessária de múltiplos objetos e promovendo a eficiência de recursos. Este padrão foi aplicado, por exemplo, no gerenciamento de conexões com o banco de dados.

- **Uma única instância:** A classe Singleton cria apenas uma instância de si mesma.
- **Construtor privado:** Para impedir que outras classes criem novas instâncias.
- **Ponto de acesso global:** Através de um método estático que retorna a única instância criada.

### 2. Microservices
A API foi desenvolvida seguindo a **arquitetura de microservices**, o que permite que cada serviço seja independente e escalável de forma autônoma. Cada serviço é focado em uma funcionalidade específica e opera de forma autônoma, o que oferece várias vantagens, como:
- **Escalabilidade**
- **Modularidade**
- **Resiliência**
- **Facilidade de Manutenção e Atualização**
- **Agilidade**

## Arquitetura

A arquitetura apresentada para o projeto **StylistPro** segue os princípios da **Onion Architecture**, utilizada para construir sistemas com alta desacoplagem entre camadas. Vamos detalhar os componentes da imagem:

![Challenge](https://github.com/user-attachments/assets/45f43440-f88a-486e-b5e6-06880e347b5c)


### 1. **Mobile Client:**
   - Este é o ponto de entrada do sistema, representando o cliente móvel que acessa o serviço **StylistPro**. Os pedidos realizados pelo cliente são direcionados ao **API Gateway**, que orquestra as chamadas de API para os microserviços.

### 2. **API Gateway:**
   - O **API Gateway** atua como um ponto central de entrada para todas as requisições feitas pelos usuários. Ele recebe as solicitações vindas do cliente e as direciona para as APIs correspondentes, garantindo o roteamento adequado. O **API Gateway** pode agregar, transformar ou autenticar as requisições antes de repassá-las para as APIs de **Compra**, **Feedback** ou **Produto**.

### 3. **APIs (Compra, Feedback, Produto):**
   - As três APIs que fazem parte do sistema, **Compra**, **Feedback** e **Produto**, são responsáveis por lidar com as funcionalidades específicas de cada um desses domínios. Essas APIs estão desacopladas, ou seja, cada uma delas é responsável por um conjunto de funcionalidades específico e pode ser desenvolvida e mantida independentemente.
   - Essas APIs seguem o padrão da **Onion Architecture**, que promove a separação de responsabilidades em camadas (domínio, aplicação, infraestrutura) e o princípio da inversão de dependências.

### 4. **Banco de Dados (Oracle):**
   - Cada API está conectada ao banco de dados Oracle. Esses bancos de dados armazenam informações referentes ao domínio de cada API:
     - A API de **Compra** acessa o banco de dados que armazena data e status da compra.
     - A API de **Feedback** gerencia o banco de dados que mantém as avaliações e comentários dos usuários.
     - A API de **Produto** trabalha com o banco de dados que contém o nome e descrição dos produtos.

### 5. **Arquitetura (Onion Architecture):**
   - A **Onion Architecture** é um estilo arquitetural que segue o princípio de inversão de dependência e separa as responsabilidades do sistema em camadas. Cada camada depende apenas das camadas mais internas, de modo a evitar dependências cíclicas e promover um design mais modular.
     - **Camada de Domínio**: A camada mais central, que contém as regras de negócio e entidades de domínio. Esta camada é agnóstica à infraestrutura e se preocupa apenas com a lógica de negócios.
     - **Camada de Aplicação**: Gerencia os casos de uso do sistema, orquestra a interação entre o domínio e a infraestrutura (como APIs, bancos de dados, etc.).
     - **Camada Externa (Infraestrutura)**: Interage com frameworks, bibliotecas externas e provedores de dados, como o banco de dados Oracle. É aqui que as dependências externas se conectam ao sistema.

A imagem descreve uma arquitetura que utiliza um **API Gateway** para gerenciar solicitações de um cliente móvel, direcionando-as para APIs independentes, cada uma gerenciando um banco de dados Oracle dedicado. Essas APIs seguem o padrão **Onion Architecture**, o que garante uma estrutura modular, flexível e de fácil manutenção, promovendo a separação de responsabilidades entre lógica de negócios, orquestração e infraestrutura.

## Tecnologias Utilizadas
- **Oracle Database: Utilizado para operações CRUD.**
- **ASP.NET Core: Framework utilizado para o desenvolvimento da API.**
- **OpenAPI/Swagger: Configurado para gerar a documentação da API, facilitando o entendimento e o uso por desenvolvedores.**

## Requisitos
- **.NET SDK 8.0**
- **Visual Studio 2022 ou Visual Studio Code**
- **Oracle Database (com conexão configurada)**
- **Ferramenta de gerenciamento de dependências**

## Instruções para Executar a API

### 1. Clone o repositório:
```
git clone <link-do-repositorio>
```

### 2. Navegue até a pasta do projeto:
```
cd StylistPro.Feedback.API
```

### 3. Restaure os pacotes NuGet:
```
dotnet restore
```

### 4. Configure a string de conexão com o banco de dados ORACLE no arquivo appsettings.json:
```
"ConnectionStrings": {
  "Oracle": "Data Source=<oracle-db-url>;User Id=<username>;Password=<password>;"
}
```

### 5. Execute a aplicação:
```
dotnet run
```

### 6. Acesse a documentação da API gerada pelo Swagger:
```
Após executar a API, navegue até http://localhost:<porta>/swagger para visualizar e interagir com a documentação.
```

### 7. No caso de erro no banco de dados: Se houver inconsistências entre o código e o banco de dados, você pode gerar e aplicar migrations para corrigir a estrutura do banco.
```
Remove-Migration
```
```
Add-Migration <nome-da-migração>
```
```
Update-Database
```

## Testando a API
A **StylistPro** utiliza o Swagger para expor os endpoints de forma interativa. Abra a URL fornecida após executar a API e você verá a documentação da API com opções para testar cada endpoint.

## Contato
Para qualquer dúvida ou sugestão, entre em contato com victor.fsilva45@gmail.com
