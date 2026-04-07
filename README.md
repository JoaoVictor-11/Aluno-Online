# Sistema de Cadastro de Alunos e Professores

## 1. Visão geral do projeto

Este projeto é uma **API REST desenvolvida em Spring Boot** para cadastro, consulta, atualização e exclusão de **alunos** e **professores**.

A aplicação utiliza:

- **Java 21**
- **Spring Boot**
- **Spring Data JPA**
- **PostgreSQL**
- **DBeaver** para gerenciamento do banco
- **Insomnia** para testes das requisições HTTP

O objetivo é demonstrar uma arquitetura simples, limpa e funcional para operações básicas de CRUD.

---

## 2. Funcionalidades implementadas

A API disponibiliza endpoints para:

- **Criar** aluno e professor
- **Listar todos**
- **Buscar por ID**
- **Atualizar por ID**
- **Excluir por ID**

A estrutura foi pensada para ser didática e organizada, facilitando manutenção e evolução futura.

---

## 3. Arquitetura utilizada

O projeto segue uma arquitetura em **camadas**, padrão bastante comum em aplicações Spring:

### 3.1 Controller
Responsável por receber as requisições HTTP e expor os endpoints da API.

### 3.2 Service
Contém a regra de negócio da aplicação.  
Aqui ficam as operações de criação, consulta, atualização e exclusão.

### 3.3 Repository
Responsável pela comunicação com o banco de dados usando **Spring Data JPA**.

### 3.4 Entity
Representa as tabelas do banco de dados, como:

- `Aluno`
- `Professor`

---

## 4. Estrutura do código

### 4.1 Controller
A controller recebe as requisições e repassa para o service.

Exemplo de responsabilidades:

- `POST /alunos`
- `GET /alunos`
- `GET /alunos/{id}`
- `PUT /alunos/{id}`
- `DELETE /alunos/{id}`

O mesmo padrão se aplica para `professores`.

### 4.2 Service
A camada de service centraliza a lógica da aplicação.

Exemplo:

- salvar um aluno
- listar alunos
- buscar aluno por ID
- deletar aluno por ID
- atualizar aluno por ID

### 4.3 Repository
O repository faz a persistência no banco.

Exemplo:

- `save()`
- `findAll()`
- `findById()`
- `deleteById()`

### 4.4 Entity
As entities representam os dados persistidos.

Cada entidade contém:

- `id`
- campos específicos do domínio
- anotações JPA para mapear a tabela

---

## 5. Banco de dados

O projeto utiliza **PostgreSQL** como banco relacional.

### Tabelas utilizadas
- `aluno`
- `professor`

### Observação
Os dados de teste foram inseridos para validação dos endpoints no Insomnia e conferência visual no DBeaver.

---

## 6. Endpoints da API

### Alunos

#### Criar aluno
`POST /alunos`

#### Listar alunos
`GET /alunos`

#### Buscar aluno por ID
`GET /alunos/{id}`

#### Atualizar aluno
`PUT /alunos/{id}`

#### Excluir aluno
`DELETE /alunos/{id}`

### Professores

#### Criar professor
`POST /professores`

#### Listar professores
`GET /professores`

#### Buscar professor por ID
`GET /professores/{id}`

#### Atualizar professor
`PUT /professores/{id}`

#### Excluir professor
`DELETE /professores/{id}`

---

## 7. Testes no Insomnia

Os testes foram realizados no **Insomnia**, validando:

- criação de registros
- listagem de dados
- busca por ID
- atualização de dados
- exclusão de registros

### Prints das requisições
> Inserir aqui os prints do Insomnia com:
- criação de aluno
- criação de professor
- busca por ID
- listagem geral
- atualização
- exclusão

---

## 8. Conferência no DBeaver

O banco foi validado no **DBeaver**, confirmando a persistência correta dos dados.

### Prints das tabelas
> Inserir aqui os prints do DBeaver mostrando:
- tabela `aluno`
- tabela `professor`
- registros utilizados nos testes

---

## 9. Observações técnicas

Durante o desenvolvimento, foram observados pontos importantes:

- o servidor roda na porta **8080**
- o PostgreSQL precisa estar ativo e com o banco criado
- o usuário do banco deve ter permissão de escrita
- a aplicação usa persistência com **JPA/Hibernate**
- os testes no Insomnia devem respeitar o método HTTP correto

---

## 10. Como executar o projeto

### Pré-requisitos
- Java 21
- Maven
- PostgreSQL
- IntelliJ IDEA ou outra IDE Java
- Insomnia ou Postman
- DBeaver

### Passos
1. Clonar o repositório
2. Configurar o banco PostgreSQL
3. Ajustar `application.properties`
4. Executar a aplicação
5. Testar os endpoints no Insomnia
6. Conferir os dados no DBeaver

---

## 11. Exemplo de configuração do banco
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/aluno_online
spring.datasource.username=postgres
spring.datasource.password=sua_senha
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true 
```

## 12. Conclusão

Este projeto demonstra uma API REST funcional, organizada em camadas e integrada com PostgreSQL.  
A solução atende ao ciclo básico de CRUD para **alunos** e **professores**, com validação prática via **Insomnia** e conferência dos dados no **DBeaver**.
