# Medvoll API

Uma API REST desenvolvida em Spring Boot para gerenciamento de médicos e pacientes em uma clínica médica.

## 🩺 Sobre o Projeto

A Medvoll API é um sistema de gerenciamento clínico que permite o cadastro, listagem, atualização e exclusão lógica de médicos e pacientes. O projeto implementa autenticação JWT, validação de dados e paginação para uma experiência completa de API REST.

## 🚀 Tecnologias Utilizadas

- **Java 17+**
- **Spring Boot 3.x**
- **Spring Data JPA** - Persistência de dados
- **Spring Security** - Autenticação e autorização
- **Spring Validation** - Validação de dados
- **MySQL** - Banco de dados
- **Flyway** - Migração de banco de dados
- **JWT (Java JWT)** - Autenticação por token
- **Lombok** - Redução de código boilerplate
- **Maven** - Gerenciamento de dependências

## 📋 Funcionalidades

### Médicos
- ✅ Cadastro de médicos
- ✅ Listagem paginada de médicos ativos
- ✅ Atualização de dados do médico
- ✅ Exclusão lógica (soft delete)
- ✅ Busca de médico por ID
- ✅ Especialidades: Cardiologia, Dermatologia, Ginecologia, Ortopedia, etc.

### Pacientes
- ✅ Cadastro de pacientes
- ✅ Listagem paginada de pacientes ativos
- ✅ Atualização de dados do paciente
- ✅ Exclusão lógica (soft delete)
- ✅ Busca de paciente por ID

### Segurança
- 🔐 Autenticação JWT
- 🔒 Endpoints protegidos
- 🛡️ Criptografia de senhas com BCrypt
- 🔧 Tratamento global de exceções

## 🏗️ Arquitetura

O projeto segue uma arquitetura em camadas:

```
src/main/java/med/voll/api/
├── controller/          # Controladores REST
│   ├── MedicoController.java
│   ├── PacienteController.java
│   └── AutenticacaoController.java
├── domain/             # Entidades e regras de negócio
│   ├── medico/        # Domínio dos médicos
│   ├── paciente/      # Domínio dos pacientes
│   ├── usuario/       # Domínio dos usuários
│   └── endereco/      # Domínio de endereços
├── infra/             # Infraestrutura
│   ├── security/      # Configurações de segurança
│   └── exception/     # Tratamento de exceções
└── ApiApplication.java # Classe principal
```

## 🔧 Pré-requisitos

- Java 17 ou superior
- Maven 3.6+
- MySQL 8.0+

## 📦 Instalação e Execução

1. **Clone o repositório**
```bash
git clone https://github.com/MrClaro/medvoll-api.git
cd medvoll-api
```

2. **Configure o banco de dados MySQL**
```sql
CREATE DATABASE medvoll_api;
```

3. **Configure as variáveis de ambiente**
```properties
# application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/medvoll_api
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha
api.security.token.secret=sua_chave_secreta_jwt
```

4. **Execute o projeto**
```bash
mvn spring-boot:run
```

A API estará disponível em: `http://localhost:9090`

## 📚 Endpoints da API

### 🔐 Autenticação

#### Login - Obter token
```http
POST http://localhost:9090/login
Content-Type: application/json

{
  "login": "teste@gmail.com",
  "senha": "123456"
}
```

**Resposta:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### 👨‍⚕️ Médicos

#### Criar um novo médico
```http
POST http://localhost:9090/medicos
Content-Type: application/json
Authorization: Bearer {token}

{
  "crm": "888887",
  "email": "teste7@gmail.com",
  "endereco": {
    "bairro": "Centro",
    "cep": "12345678",
    "cidade": "São Paulo",
    "complemento": "Apto 1",
    "logradouro": "Rua Exemplo",
    "numero": "123",
    "uf": "SP"
  },
  "especialidade": "ORTOPEDIA",
  "nome": "Dr. Exemplo",
  "telefone": "11987654321"
}
```

#### Listar todos os médicos (paginado)
```http
GET http://localhost:9090/medicos
Authorization: Bearer {token}
```

#### Buscar médico por ID
```http
GET http://localhost:9090/medicos/1
Authorization: Bearer {token}
```

#### Atualizar médico
```http
PUT http://localhost:9090/medicos
Content-Type: application/json
Authorization: Bearer {token}

{
  "id": 1,
  "nome": "Dr. Exemplo Atualizado",
  "telefone": "11999888777"
}
```

#### Excluir médico (soft delete)
```http
DELETE http://localhost:9090/medicos/4
Authorization: Bearer {token}
```

---

### 🏥 Pacientes

#### Criar um novo paciente
```http
POST http://localhost:9090/pacientes
Content-Type: application/json
Authorization: Bearer {token}

{
  "cpf": "12345678901",
  "email": "joao.silva@gmail.com",
  "endereco": {
    "bairro": "Jardim Primavera",
    "cep": "01234567",
    "cidade": "São Paulo",
    "complemento": "Casa 2",
    "logradouro": "Rua das Flores",
    "numero": "456",
    "uf": "SP"
  },
  "nome": "João Silva",
  "telefone": "11987654321"
}
```

#### Listar todos os pacientes (paginado)
```http
GET http://localhost:9090/pacientes
Authorization: Bearer {token}
```

#### Buscar paciente por ID
```http
GET http://localhost:9090/pacientes/1
Authorization: Bearer {token}
```

#### Atualizar paciente
```http
PUT http://localhost:9090/pacientes
Content-Type: application/json
Authorization: Bearer {token}

{
  "endereco": {
    "bairro": "Vila Nova",
    "cep": "09876543",
    "cidade": "São Paulo",
    "complemento": "Apto 15",
    "logradouro": "Rua das Rosas",
    "numero": "789",
    "uf": "SP"
  },
  "id": 1,
  "nome": "João Silva Santos",
  "telefone": "11999777666"
}
```

#### Excluir paciente (soft delete)
```http
DELETE http://localhost:9090/pacientes/2
Authorization: Bearer {token}
```

---

### 🏥 Especialidades Médicas Disponíveis
- `CARDIOLOGIA`
- `DERMATOLOGIA`
- `GINECOLOGIA`
- `NEUROLOGIA`
- `ORTOPEDIA`

## 🔒 Segurança

A API utiliza JWT (JSON Web Tokens) para autenticação. Após fazer login, inclua o token no header das requisições:

```
Authorization: Bearer {seu_token_jwt}
```

**Endpoints públicos:**
- `POST /login` - Não requer autenticação

**Endpoints protegidos:**
- Todos os endpoints de médicos e pacientes requerem autenticação

## ⚠️ Tratamento de Erros

A API possui tratamento global de exceções que retorna respostas padronizadas para:

- **400 Bad Request** - Dados inválidos ou malformados
- **401 Unauthorized** - Credenciais inválidas ou token expirado
- **403 Forbidden** - Acesso negado
- **404 Not Found** - Recurso não encontrado
- **500 Internal Server Error** - Erro interno do servidor

## 🗄️ Banco de Dados

O projeto utiliza Flyway para migração automática do banco de dados. As migrações são executadas automaticamente na inicialização da aplicação.

**Principais tabelas:**
- `medicos` - Dados dos médicos
- `pacientes` - Dados dos pacientes
- `usuarios` - Dados de autenticação

## 🧪 Testes

Execute os testes com:
```bash
mvn test
```

## 📄 Paginação

As listagens suportam paginação através dos parâmetros:
- `page` - Número da página (padrão: 0)
- `size` - Tamanho da página (padrão: 10)
- `sort` - Campo para ordenação (padrão: "nome")

Exemplo:
```
GET /medicos?page=0&size=20&sort=nome
```

## 🤝 Contribuição

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👨‍💻 Autor

**MrClaro**
- GitHub: [@MrClaro](https://github.com/MrClaro)

---

⭐ Se este projeto te ajudou, deixe uma estrela!
