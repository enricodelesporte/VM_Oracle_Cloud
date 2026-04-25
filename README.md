# Academia API — Gym Student Management

> API REST para gerenciamento de alunos de academia, desenvolvida com Spring Boot e hospedada na Oracle Cloud.

---

##  Índice

- [Visão Geral](#-visão-geral)
- [Tecnologias](#-tecnologias)
- [Endereço da API](#-endereço-da-api)
- [Endpoints](#-endpoints)
- [Executando na VM (Oracle Cloud)](#-executando-na-vm-oracle-cloud)
- [Build Local](#-build-local)
- [Status do Projeto](#-status-do-projeto)
- [Autor](#-autor)

---

## Visão Geral

A **Academia API** é uma aplicação backend RESTful desenvolvida para o gerenciamento de alunos de uma academia. Ela permite cadastrar e listar alunos, sendo executada em uma máquina virtual na **Oracle Cloud Infrastructure (OCI)** e acessível via IP público.

Este projeto foi desenvolvido como parte de um trabalho acadêmico na disciplina de **DevOps**, com foco em práticas de build, empacotamento e deploy de aplicações Java em ambientes cloud.

---

##  Tecnologias

| Tecnologia | Versão | Descrição |
|---|---|---|
| Java | 21 | Linguagem principal |
| Spring Boot | 3.x | Framework web e REST |
| MySQL | 8.0 | Banco de dados relacional |
| Docker | Latest | Containerização do MySQL |
| Oracle Cloud | — | Hospedagem da VM |
| Maven | Wrapper | Build e gerenciamento de dependências |

---

##  Endereço da API

```
http://163.176.238.77:8080/gym-student
```

> **Nota:** A aplicação deve estar em execução na VM para que os endpoints estejam disponíveis.

---

##  Endpoints

### `GET /gym-student` — Listar todos os alunos

Retorna a lista de todos os alunos cadastrados.

```bash
curl http://163.176.238.77:8080/gym-student
```

**Resposta esperada:** Array JSON com os alunos cadastrados.

---

### `POST /gym-student` — Cadastrar novo aluno

Cria um novo aluno no sistema.

```bash
curl -X POST http://163.176.238.77:8080/gym-student \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Enrico",
    "cpf": "123233434",
    "age": 19,
    "birthDate": "2026-06-15",
    "active": true
  }'
```

**Body da requisição:**

| Campo | Tipo | Descrição |
|---|---|---|
| `name` | `string` | Nome completo do aluno |
| `cpf` | `string` | CPF do aluno |
| `age` | `integer` | Idade do aluno |
| `birthDate` | `string` (ISO 8601) | Data de nascimento no formato `YYYY-MM-DD` |
| `active` | `boolean` | Se o aluno está ativo na academia |

---

## ☁️ Executando na VM (Oracle Cloud)

Acesse a VM via SSH e execute os comandos abaixo na ordem indicada.

### 1. Iniciar o banco de dados MySQL

```bash
docker start mysql-devops
```

### 2. Subir a aplicação em background

```bash
nohup java -jar appacademia-0.0.1-SNAPSHOT.jar > log.txt 2>&1 &
```

> O processo é iniciado em background com `nohup`. Os logs são redirecionados para `log.txt`.

### 3. Acompanhar os logs em tempo real

```bash
tail -f log.txt
```

### 4. Verificar se a API está respondendo localmente

```bash
curl http://localhost:8080/gym-student
```

### 5. Verificar via IP público

```bash
curl http://163.176.238.77:8080/gym-student
```

### 6. Parar a aplicação

```bash
pkill -f appacademia
```

---

##  Build Local

Para gerar o `.jar` da aplicação na sua máquina local:

**Windows:**
```bash
.\mvnw clean package
```

**Linux / macOS:**
```bash
./mvnw clean package
```

O arquivo gerado será:

```
target/appacademia-0.0.1-SNAPSHOT.jar
```

Após o build, copie o `.jar` para a VM e execute conforme os passos da seção anterior.

---

##  Status do Projeto

- [x] API funcionando na nuvem
- [x] Endpoint `GET` operacional
- [x] Endpoint `POST` operacional
- [x] VM configurada na Oracle Cloud
- [x] Banco MySQL rodando via Docker
- [x] Deploy via JAR concluído

---

##  Autor

**Enrico Delesporte**

Projeto acadêmico desenvolvido para a disciplina de **DevOps**.
