# 🏥 Voll.med - API REST para Gestão de Clínica Médica

## 📋 Índice
- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Arquitetura](#-arquitetura)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#-instalação-e-configuração)
- [Banco de Dados](#-banco-de-dados)
- [Segurança](#-segurança)
- [Documentação da API](#-documentação-da-api)
- [Testes](#-testes)
- [Ambientes](#-ambientes)
- [Regras de Negócio](#-regras-de-negócio)
- [Referências](#-referências)

---

## 📖 Sobre o Projeto

A **Voll.med** é uma aplicação backend desenvolvida para gerenciar consultas em uma clínica médica fictícia. O sistema oferece uma API REST completa para cadastro de médicos e pacientes, além de agendamento e cancelamento de consultas médicas.

Este projeto foi desenvolvido durante o **Curso de Spring Boot 3: documente, teste e prepare uma API para o deploy** da **DevMedia**, com foco em boas práticas de desenvolvimento, documentação técnica, testes automatizados e preparação para ambiente de produção.

O backend é responsável por toda a lógica de negócio e persistência de dados, enquanto aplicações mobile e web consumirão esta API para interface com os usuários finais.

### 🎯 Objetivos do Projeto
- Implementar uma API REST robusta e escalável
- Aplicar padrões de arquitetura em camadas
- Garantir segurança com autenticação JWT
- Documentar endpoints com OpenAPI/Swagger
- Implementar validações complexas de regras de negócio
- Preparar aplicação para deploy em produção

---

## ⚙️ Funcionalidades

### Médicos
- ✅ Cadastro de médicos com especialidade
- ✅ Listagem paginada de médicos ativos
- ✅ Atualização de dados cadastrais
- ✅ Exclusão lógica (inativação) de médicos
- ✅ Detalhamento de médico específico

### Pacientes
- ✅ Cadastro de pacientes
- ✅ Listagem paginada de pacientes ativos
- ✅ Atualização de dados cadastrais
- ✅ Exclusão lógica (inativação) de pacientes
- ✅ Detalhamento de paciente específico

### Consultas
- ✅ Agendamento de consultas com validações
- ✅ Cancelamento de consultas com motivo
- ✅ Seleção automática de médico disponível
- ✅ Validação de regras de negócio

### Autenticação
- ✅ Login com geração de token JWT
- ✅ Proteção de rotas com autenticação
- ✅ Gerenciamento de sessão stateless

---

## 🏗️ Arquitetura

O projeto segue uma **arquitetura em camadas**, separando responsabilidades e facilitando manutenção:

```
├── Controller Layer (Apresentação)
│   ├── Recebe requisições HTTP
│   ├── Valida dados de entrada
│   └── Retorna respostas padronizadas
│
├── Service Layer (Lógica de Negócio)
│   ├── Processa regras de negócio
│   ├── Coordena validações
│   └── Orquestra operações complexas
│
├── Domain Layer (Domínio)
│   ├── Entidades JPA
│   ├── Validadores de negócio
│   ├── Repositories
│   └── DTOs (Records)
│
└── Infrastructure Layer (Infraestrutura)
    ├── Configurações de segurança
    ├── Tratamento de exceções
    └── Configuração de documentação
```

### Padrões Implementados
- **DTO Pattern**: Uso de Records para transferência de dados
- **Repository Pattern**: Abstração de acesso a dados com Spring Data JPA
- **Strategy Pattern**: Validadores intercambiáveis para regras de negócio
- **Dependency Injection**: Gerenciamento de dependências com Spring
- **RESTful API**: Arquitetura REST com recursos bem definidos

---

## 🛠 Tecnologias Utilizadas

### Core
- **[Java 17](https://www.oracle.com/java)** - Linguagem de programação principal
- **[Spring Boot 3.0.0](https://spring.io/projects/spring-boot)** - Framework base da aplicação
- **[Maven](https://maven.apache.org)** - Gerenciador de dependências e build

### Persistência
- **[Spring Data JPA](https://spring.io/projects/spring-data-jpa)** - Abstração para acesso a dados
- **[Hibernate](https://hibernate.org)** - Implementação JPA
- **[MySQL](https://www.mysql.com)** - Banco de dados relacional
- **[Flyway](https://flywaydb.org)** - Versionamento e migração de banco de dados

### Segurança
- **[Spring Security](https://spring.io/projects/spring-security)** - Framework de segurança
- **[Auth0 Java JWT 4.2.1](https://github.com/auth0/java-jwt)** - Geração e validação de tokens JWT

### Documentação
- **[SpringDoc OpenAPI 2.0.2](https://springdoc.org)** - Documentação automática da API (Swagger UI)

### Desenvolvimento
- **[Spring Boot DevTools](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.devtools)** - Hot reload em desenvolvimento
- **[Lombok](https://projectlombok.org)** - Redução de código boilerplate
- **[Bean Validation](https://beanvalidation.org)** - Validação de dados

### Testes
- **[Spring Boot Test](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing)** - Framework de testes
- **[JUnit 5](https://junit.org/junit5/)** - Framework de testes unitários
- **[Spring Security Test](https://docs.spring.io/spring-security/reference/servlet/test/index.html)** - Testes de segurança

---

## 📁 Estrutura do Projeto

```
spring-boot-api-deploy-main/
│
├── src/
│   ├── main/
│   │   ├── java/med/voll/api/
│   │   │   ├── controller/                    # Camada de apresentação
│   │   │   │   ├── AutenticacaoController.java
│   │   │   │   ├── ConsultaController.java
│   │   │   │   ├── MedicoController.java
│   │   │   │   └── PacienteController.java
│   │   │   │
│   │   │   ├── domain/                        # Camada de domínio
│   │   │   │   ├── consulta/
│   │   │   │   │   ├── AgendaDeConsultas.java     # Service
│   │   │   │   │   ├── Consulta.java              # Entidade
│   │   │   │   │   ├── ConsultaRepository.java
│   │   │   │   │   ├── MotivoCancelamento.java    # Enum
│   │   │   │   │   ├── validacoes/
│   │   │   │   │   │   ├── agendamento/          # Validadores de agendamento
│   │   │   │   │   │   └── cancelamento/         # Validadores de cancelamento
│   │   │   │   │   └── DTO's (Records)
│   │   │   │   │
│   │   │   │   ├── medico/
│   │   │   │   │   ├── Medico.java                # Entidade
│   │   │   │   │   ├── MedicoRepository.java
│   │   │   │   │   ├── Especialidade.java         # Enum
│   │   │   │   │   └── DTO's (Records)
│   │   │   │   │
│   │   │   │   ├── paciente/
│   │   │   │   │   ├── Paciente.java              # Entidade
│   │   │   │   │   ├── PacienteRepository.java
│   │   │   │   │   └── DTO's (Records)
│   │   │   │   │
│   │   │   │   ├── usuario/
│   │   │   │   │   ├── Usuario.java               # Entidade
│   │   │   │   │   ├── UsuarioRepository.java
│   │   │   │   │   └── AutenticacaoService.java
│   │   │   │   │
│   │   │   │   ├── endereco/
│   │   │   │   │   └── Endereco.java              # Embeddable
│   │   │   │   │
│   │   │   │   └── ValidacaoException.java        # Exceção customizada
│   │   │   │
│   │   │   ├── infra/                         # Camada de infraestrutura
│   │   │   │   ├── security/
│   │   │   │   │   ├── SecurityConfigurations.java
│   │   │   │   │   ├── SecurityFilter.java
│   │   │   │   │   ├── TokenService.java
│   │   │   │   │   └── DadosTokenJWT.java
│   │   │   │   │
│   │   │   │   ├── exception/
│   │   │   │   │   └── TratadorDeErros.java      # Global exception handler
│   │   │   │   │
│   │   │   │   └── springdoc/
│   │   │   │       └── SpringDocConfigurations.java
│   │   │   │
│   │   │   └── ApiApplication.java            # Classe principal
│   │   │
│   │   └── resources/
│   │       ├── application.properties             # Configurações base
│   │       ├── application-test.properties        # Configurações de teste
│   │       ├── application-prod.properties        # Configurações de produção
│   │       └── db/migration/                      # Scripts Flyway
│   │           ├── V1__create-table-medicos.sql
│   │           ├── V2__alter-table-medicos-add-column-telefone.sql
│   │           ├── V3__alter-table-medicos-add-column-ativo.sql
│   │           ├── V4__create-table-pacientes.sql
│   │           ├── V5__create-table-usuarios.sql
│   │           ├── V6__create-table-consultas.sql
│   │           └── V7__alter-table-consulta-add-column-motivo-cancelamento.sql
│   │
│   └── test/
│       └── java/med/voll/api/
│           ├── controller/
│           │   ├── ConsultaControllerTest.java
│           │   └── MedicoControllerTest.java
│           └── domain/
│               └── medico/
│                   └── MedicoRepositoryTest.java
│
├── .mvn/                                      # Maven wrapper
├── pom.xml                                    # Configuração Maven
└── README.md
```

---

## 📦 Pré-requisitos

Antes de iniciar, certifique-se de ter instalado:

- **Java 17** ou superior ([Download](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html))
- **Maven 3.8+** ([Download](https://maven.apache.org/download.cgi))
- **MySQL 8.0+** ([Download](https://dev.mysql.com/downloads/mysql/))
- **IDE** (IntelliJ IDEA, Eclipse ou VS Code)

### Verificando Instalação

```bash
# Verificar versão do Java
java -version

# Verificar versão do Maven
mvn -version

# Verificar MySQL
mysql --version
```

---

## 🚀 Instalação e Configuração

### 1. Clonar o Repositório

```bash
git clone <url-do-repositorio>
cd spring-boot-api-deploy-main
```

### 2. Configurar Banco de Dados

Crie o banco de dados MySQL:

```sql
CREATE DATABASE vollmed_api;
```

### 3. Configurar Variáveis de Ambiente

Configure as credenciais do banco de dados no arquivo `application.properties` ou através de variáveis de ambiente:

```properties
spring.datasource.url=jdbc:mysql://localhost/vollmed_api
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha
```

Configure a chave secreta JWT (recomendado via variável de ambiente):

```bash
export JWT_SECRET=sua-chave-secreta-super-segura-aqui
```

### 4. Instalar Dependências

```bash
mvn clean install
```

### 5. Executar a Aplicação

```bash
mvn spring-boot:run
```

Ou utilizando o wrapper:

```bash
./mvnw spring-boot:run
```

A aplicação estará disponível em: `http://localhost:8080`

---

## 🗄️ Banco de Dados

### Gerenciamento de Migrations

O projeto utiliza **Flyway** para versionamento automático do banco de dados. As migrations são executadas automaticamente na inicialização da aplicação.

### Scripts de Migration

| Versão | Descrição |
|--------|-----------|
| V1 | Criação da tabela `medicos` |
| V2 | Adiciona coluna `telefone` em médicos |
| V3 | Adiciona coluna `ativo` em médicos |
| V4 | Criação da tabela `pacientes` |
| V5 | Criação da tabela `usuarios` |
| V6 | Criação da tabela `consultas` |
| V7 | Adiciona coluna `motivo_cancelamento` em consultas |

### Modelo de Dados

```
medicos
├── id (PK)
├── nome
├── email (UNIQUE)
├── crm (UNIQUE)
├── especialidade (ENUM)
├── telefone
├── ativo (BOOLEAN)
└── endereco (embedded)

pacientes
├── id (PK)
├── nome
├── email (UNIQUE)
├── cpf (UNIQUE)
├── telefone
├── ativo (BOOLEAN)
└── endereco (embedded)

usuarios
├── id (PK)
├── login (UNIQUE)
└── senha (HASH)

consultas
├── id (PK)
├── medico_id (FK)
├── paciente_id (FK)
├── data
└── motivo_cancelamento (ENUM)
```

### Especialidades Médicas

O sistema suporta as seguintes especialidades:
- **ORTOPEDIA**
- **CARDIOLOGIA**
- **GINECOLOGIA**
- **DERMATOLOGIA**

---

## 🔒 Segurança

### Autenticação JWT

A API utiliza autenticação baseada em **JSON Web Tokens (JWT)**:

1. **Login**: POST `/login` com credenciais
2. **Recebimento do Token**: JWT retornado no corpo da resposta
3. **Uso do Token**: Incluir header `Authorization: Bearer {token}` nas requisições

### Fluxo de Autenticação

```
Cliente                  API                      Banco de Dados
   |                      |                             |
   |-- POST /login ------>|                             |
   |  (user/password)     |-- Validar credenciais ----> |
   |                      |<--- Usuário válido ---------|
   |<--- JWT Token -------|                             |
   |                      |                             |
   |-- GET /medicos ----->|                             |
   |  (Bearer Token)      |-- Validar Token             |
   |                      |-- Buscar dados ------------>|
   |<--- Dados -----------|<--- Médicos ----------------|
```

### Configurações de Segurança

- Senhas criptografadas com **BCrypt**
- Tokens JWT com expiração configurável
- Proteção CSRF desabilitada (API stateless)
- Sessões stateless
- CORS configurado

### Endpoints Públicos

- `POST /login` - Autenticação

### Endpoints Protegidos

Requerem token JWT válido:
- Todos os endpoints de `/medicos`
- Todos os endpoints de `/pacientes`
- Todos os endpoints de `/consultas`

---

## 📚 Documentação da API

### Swagger UI

A documentação interativa da API está disponível via **Swagger UI**:

**URL**: `http://localhost:8080/swagger-ui.html`

### Recursos Disponíveis

#### Autenticação

```http
POST /login
Content-Type: application/json

{
  "login": "usuario@email.com",
  "senha": "senha123"
}
```

#### Médicos

```http
# Cadastrar médico
POST /medicos
Authorization: Bearer {token}

# Listar médicos (paginado)
GET /medicos?page=0&size=10&sort=nome

# Detalhar médico
GET /medicos/{id}

# Atualizar médico
PUT /medicos

# Excluir (inativar) médico
DELETE /medicos/{id}
```

#### Pacientes

```http
# Cadastrar paciente
POST /pacientes
Authorization: Bearer {token}

# Listar pacientes (paginado)
GET /pacientes?page=0&size=10

# Detalhar paciente
GET /pacientes/{id}

# Atualizar paciente
PUT /pacientes

# Excluir (inativar) paciente
DELETE /pacientes/{id}
```

#### Consultas

```http
# Agendar consulta
POST /consultas
Authorization: Bearer {token}

{
  "idPaciente": 1,
  "idMedico": 2,
  "data": "2024-12-20T10:00:00",
  "especialidade": "CARDIOLOGIA"
}

# Cancelar consulta
DELETE /consultas

{
  "idConsulta": 1,
  "motivo": "PACIENTE_DESISTIU"
}
```

---

## 🧪 Testes

### Executar Testes

```bash
# Executar todos os testes
mvn test

# Executar com relatório de cobertura
mvn clean test jacoco:report
```

### Tipos de Testes Implementados

#### Testes de Controller
- `MedicoControllerTest` - Testes de integração dos endpoints de médicos
- `ConsultaControllerTest` - Testes de integração dos endpoints de consultas

#### Testes de Repository
- `MedicoRepositoryTest` - Testes de consultas customizadas

### Cobertura de Testes

Os testes cobrem:
- ✅ Validação de dados de entrada
- ✅ Regras de negócio
- ✅ Autenticação e autorização
- ✅ Consultas customizadas ao banco
- ✅ Tratamento de exceções

---

## 🌍 Ambientes

### Desenvolvimento (development)

```properties
# application.properties
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
server.error.include-stacktrace=never
```

### Teste (test)

```properties
# application-test.properties
spring.datasource.url=jdbc:mysql://localhost/vollmed_api_test
```

### Produção (prod)

```properties
# application-prod.properties
spring.datasource.url=${DATABASE_URL}
spring.datasource.username=${DATABASE_USERNAME}
spring.datasource.password=${DATABASE_PASSWORD}
api.security.token.secret=${JWT_SECRET}
```

### Ativando Perfil

```bash
# Via linha de comando
mvn spring-boot:run -Dspring-boot.run.profiles=prod

# Via variável de ambiente
export SPRING_PROFILES_ACTIVE=prod
```

---

## 📋 Regras de Negócio

### Agendamento de Consultas

O sistema valida as seguintes regras ao agendar uma consulta:

1. **Horário de Antecedência**
   - Consulta deve ser agendada com no mínimo 30 minutos de antecedência

2. **Horário de Funcionamento**
   - Clínica funciona de segunda a sábado
   - Horário: 07:00 às 19:00

3. **Médico Ativo**
   - Médico deve estar ativo no sistema

4. **Paciente Ativo**
   - Paciente deve estar ativo no sistema

5. **Médico Sem Consulta no Mesmo Horário**
   - Médico não pode ter outra consulta agendada no mesmo horário

6. **Paciente Sem Consulta no Mesmo Dia**
   - Paciente não pode ter mais de uma consulta agendada no mesmo dia

7. **Escolha de Médico**
   - Se não informado, sistema escolhe médico aleatório disponível da especialidade
   - Especialidade é obrigatória quando médico não é escolhido

### Cancelamento de Consultas

1. **Antecedência Mínima**
   - Consulta só pode ser cancelada com no mínimo 24 horas de antecedência

2. **Motivos de Cancelamento**
   - `PACIENTE_DESISTIU`
   - `MEDICO_CANCELOU`
   - `OUTROS`

3. **Consulta Existente**
   - Consulta deve existir no sistema

### Exclusão Lógica

- Médicos e pacientes não são excluídos fisicamente
- Utiliza-se inativação (soft delete)
- Registros inativos não aparecem em listagens

---

## 🎓 Referências

Este projeto foi desenvolvido como parte do curso:

**Curso**: Spring Boot 3: documente, teste e prepare uma API para o deploy  
**Plataforma**: [DevMedia](https://www.devmedia.com.br)  
**Instrutor**: Rodrigo Ferreira

### Links Úteis

- **[Documentação Spring Boot 3](https://docs.spring.io/spring-boot/docs/3.0.0/reference/htmlsingle/)**
- **[Spring Security Reference](https://docs.spring.io/spring-security/reference/)**
- **[Documentação Flyway](https://flywaydb.org/documentation/)**
- **[Auth0 JWT Java](https://github.com/auth0/java-jwt)**
- **[SpringDoc OpenAPI](https://springdoc.org/)**
- **[Trello do Projeto](https://trello.com/b/O0lGCsKb/api-voll-med)**
- **[Layout Figma](https://www.figma.com/file/N4CgpJqsg7gjbKuDmra3EV/Voll.med)**

---

## 📄 Licença

Projeto desenvolvido pela [Alura](https://www.alura.com.br) para fins educacionais.

---

## 👨‍💻 Autor

Projeto baseado no curso da DevMedia, adaptado e documentado para fins de estudo.

---

## 🤝 Contribuindo

Este é um projeto educacional. Sinta-se à vontade para:

1. Fazer fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abrir um Pull Request

---

## 📞 Suporte

Para dúvidas sobre o curso, acesse:
- [DevMedia](https://www.devmedia.com.br)
- [Alura](https://www.alura.com.br)

---

**Desenvolvido com ❤️ e Spring Boot**
