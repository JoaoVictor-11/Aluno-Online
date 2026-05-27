# Sistema de Cadastro Acadêmico (Aluno Online)

## 1. Visão geral do projeto
Este projeto é uma **API REST desenvolvida em Spring Boot** para o gerenciamento acadêmico, incluindo o cadastro, consulta, atualização e exclusão de **alunos**, **professores**, **disciplinas** e **matrículas**.

A aplicação utiliza:
- **Java 21**
- **Spring Boot**
- **Spring Data JPA**
- **PostgreSQL**
- **DBeaver** para gerenciamento do banco
- **Insomnia** para testes das requisições HTTP

O objetivo é demonstrar uma arquitetura simples, limpa e funcional para operações de CRUD e regras de negócio, evoluindo de cadastros básicos para relacionamentos complexos.

---

## 2. Funcionalidades implementadas
A API disponibiliza endpoints para gerenciar:

- **Alunos**: Criar, listar todos, buscar por ID, atualizar e excluir.
- **Professores**: Criar, listar todos, buscar por ID, atualizar e excluir.
- **Disciplinas**: Criar (vinculando a um professor), listar, buscar, atualizar e excluir.
- **Matrículas**: 
  - Criar matrícula (vincular aluno a uma disciplina).
  - Trancar matrícula.
  - Atualizar notas (com cálculo automático de média e status de aprovação).

---

## 3. Arquitetura utilizada
O projeto segue uma arquitetura em **camadas**, padrão bastante comum em aplicações Spring:

### 3.1 Controller
Responsável por receber as requisições HTTP e expor os endpoints da API.

### 3.2 Service
Contém a regra de negócio da aplicação. Aqui ficam as operações de criação, consulta, atualização, exclusão e cálculos (como a média das notas).

### 3.3 Repository
Responsável pela comunicação com o banco de dados usando **Spring Data JPA**.

### 3.4 Entity (Model)
Representa as tabelas do banco de dados, como:
- Aluno
- Professor
- Disciplina (Relacionamento `@ManyToOne` com Professor)
- MatriculaAluno (Relacionamento com Aluno e Disciplina)

### 3.5 DTOs (Data Transfer Objects)
Classes enxutas utilizadas para transportar apenas os dados necessários entre o cliente e a API (ex: `AtualizarNotasRequestDTO`).

### 3.6 Enums
Utilizados para padronizar valores fixos, como o status da matrícula (`MATRICULADO`, `APROVADO`, `REPROVADO`, `TRANCADO`).

---

## 4. Banco de dados
O projeto utiliza **PostgreSQL** como banco relacional.

### Tabelas utilizadas
- `aluno`
- `professor`
- `disciplina`
- `matricula_aluno`

---

## 5. Endpoints da API

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
<img width="2556" height="1080" alt="Captura de Tela (53)" src="https://github.com/user-attachments/assets/e67cee9c-ea4c-4908-88d3-a0c3952b1a44" />

#### Listar professores
`GET /professores`
<img width="2564" height="1080" alt="Captura de Tela (55)" src="https://github.com/user-attachments/assets/f54e44c7-6f40-457d-baa1-159c723e305b" />

#### Buscar professor por ID
`GET /professores/{id}`
<img width="2561" height="1080" alt="Captura de Tela (54)" src="https://github.com/user-attachments/assets/2104988c-1869-40fd-8a1f-8729cc101418" />

#### Atualizar professor
`PUT /professores/{id}`
<img width="2565" height="1080" alt="Captura de Tela (57)" src="https://github.com/user-attachments/assets/c8244544-33fd-43aa-90c5-55a4386ca23d" />

#### Excluir professor
`DELETE /professores/{id}`
<img width="2561" height="1080" alt="Captura de Tela (56)" src="https://github.com/user-attachments/assets/5118f3ae-3621-45a4-9da7-30122b26dc75" />

### 📖 Disciplinas
- **Criar disciplina:** `POST /disciplinas`
  <img width="1920" height="1080" alt="Captura de Tela (102)" src="https://github.com/user-attachments/assets/d8624b52-24fa-4702-9aae-a17e4e88c779" />
- **Listar disciplinas:** `GET /disciplinas`
  <img width="1920" height="1080" alt="Captura de Tela (100)" src="https://github.com/user-attachments/assets/d5b2120d-1116-45c0-8865-5ff7957c9786" />
- **Buscar disciplina por ID:** `GET /disciplinas/{id}`
  <img width="1920" height="1080" alt="Captura de Tela (101)" src="https://github.com/user-attachments/assets/b91abaf0-3906-49c3-9f8d-9040adc7768b" />
- **Atualizar disciplina:** `PUT /disciplinas/{id}`
  <img width="1920" height="1080" alt="Captura de Tela (96)" src="https://github.com/user-attachments/assets/063aa2e4-e0e5-49dc-a86b-9bd618fcfa52" />
- **Excluir disciplina:** `DELETE /disciplinas/{id}`
  <img width="1920" height="1080" alt="Captura de Tela (98)" src="https://github.com/user-attachments/assets/6d810160-80f6-4b9a-a309-c36dacb86f49" />


### 📝 Matrículas
- **Criar matrícula:** `POST /matriculas` (Inicia com status MATRICULADO)
  <img width="1920" height="1080" alt="Captura de Tela (103)" src="https://github.com/user-attachments/assets/46885a75-a6e3-4866-bf4d-150fc0b00191" />
- **Trancar matrícula:** `PATCH /matriculas/trancar/{id}` (Altera o status para TRANCADO, se estiver MATRICULADO)
  <img width="1920" height="1080" alt="Captura de Tela (104)" src="https://github.com/user-attachments/assets/347b2cfe-2306-40e6-a978-c6bb470b0e34" />
- **Atualizar notas:** `PATCH /matriculas/atualizar-notas/{id}` (Recebe `nota1` e `nota2` via DTO. Calcula a média automaticamente e define como APROVADO ou REPROVADO).
  <img width="1920" height="1080" alt="Captura de Tela (106)" src="https://github.com/user-attachments/assets/d9ef1b61-fbb5-4575-b1bd-56dfba7eadff" />


---

## 6. Testes no Insomnia

Os testes foram realizados no **Insomnia**, validando:

- criação de registros
- listagem de dados
- busca por ID
- atualização de dados
- exclusão de registros

---

## 7. Conferência no DBeaver

O banco foi validado no **DBeaver**, confirmando a persistência correta dos dados.

### Prints das tabelas
> Inserir aqui os prints do DBeaver mostrando:
- tabela `aluno`<img width="2560" height="1080" alt="Captura de Tela (51)" src="https://github.com/user-attachments/assets/e925d2af-a8fb-44f3-963d-d5adb076f951" />
- tabela `professor`<img width="2561" height="1080" alt="Captura de Tela (52)" src="https://github.com/user-attachments/assets/e5d08582-97f9-4450-b6ab-2303b0bf2172" />
- tabela `disciplina`<img width="1920" height="1080" alt="Captura de Tela (99)" src="https://github.com/user-attachments/assets/c8fd9825-f81d-472c-afce-0b5df393c99e" />
- tabela `matricula`<img width="1920" height="1080" alt="Captura de Tela (105)" src="https://github.com/user-attachments/assets/b74acd8b-172f-455b-8d2d-22121c32e3b6" />
- registros utilizados nos testes

---

## 8. Observações técnicas

Durante o desenvolvimento, foram observados pontos importantes:

- o servidor roda na porta **8080**
- o PostgreSQL precisa estar ativo e com o banco criado
- o usuário do banco deve ter permissão de escrita
- a aplicação usa persistência com **JPA/Hibernate**
- os testes no Insomnia devem respeitar o método HTTP correto

---

## 9. Como executar o projeto

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

## 10. Exemplo de configuração do banco
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/aluno_online
spring.datasource.username=postgres
spring.datasource.password=sua_senha
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true 
```

## 11. Conclusão

Este projeto demonstra uma API REST funcional, organizada em camadas e integrada com PostgreSQL.  
A solução atende ao ciclo básico de CRUD para **alunos** e **professores**, com validação prática via **Insomnia** e conferência dos dados no **DBeaver**.
