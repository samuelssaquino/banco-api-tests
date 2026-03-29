# banco-api-tests

Projeto de automação de testes de API REST desenvolvido em **JavaScript** para validar os principais fluxos da API do projeto **banco-api**.

O foco deste repositório é exercitar autenticação, transferência bancária e consultas de transferências, utilizando uma stack simples e objetiva para testes automatizados de API.

## Objetivo

Automatizar testes da API REST, cobrindo cenários de:

- autenticação de usuário;
- criação de transferências;
- validações de regras de negócio;
- consulta de transferência por ID;
- paginação de transferências.

## Stack utilizada

- **JavaScript**
- **Node.js**
- **Mocha** — framework de testes
- **Chai** — biblioteca de asserções
- **Supertest** — envio de requisições HTTP e validação de respostas
- **.env** — carregamento de variáveis de ambiente
- **Mochawesome** — geração de relatório HTML

## Dependências do projeto

As dependências atualmente declaradas no `package.json` são:

### Dependências de desenvolvimento

- `chai` `^6.2.2`
- `mocha` `^11.7.5`
- `supertest` `^7.2.2`

### Dependências de execução

- `dotenv` `^17.3.1`
- `mochawesome` `^7.1.4`

## Estrutura de diretórios

```text
banco-api-tests/
├── fixtures/
│   ├── postLogin.json
│   └── postTransferencias.json
├── helpers/
│   └── autenticacao.js
├── test/
│   ├── login.test.js
│   └── transferencia.test.js
├── .gitignore
├── package.json
├── package-lock.json
└── .env                  # deve ser criado manualmente pelo usuário
```

### Descrição das pastas e arquivos

- **fixtures/**: massas de dados utilizadas nas requisições.
- **helpers/**: funções auxiliares reutilizáveis, como obtenção de token.
- **test/**: arquivos com os cenários automatizados.
- **.env**: arquivo local com a configuração da URL base da API.
- **mochawesome-report/**: diretório gerado automaticamente após a execução dos testes com relatório HTML.

## Arquivo `.env`

Este projeto utiliza a variável de ambiente `BASE_URL`, que deve ser criada manualmente na raiz do projeto.

Crie um arquivo chamado **`.env`** com o seguinte conteúdo:

```env
BASE_URL=http://localhost:3000
```

> Esse valor considera a API REST do projeto `banco-api` rodando localmente na porta `3000`.

## Fixtures utilizadas

### `fixtures/postLogin.json`

```json
{
  "username": "julio.lima",
  "senha": "123456"
}
```

### `fixtures/postTransferencias.json`

```json
{
  "contaOrigem": 1,
  "contaDestino": 2,
  "valor": 11,
  "token": ""
}
```

## Pré-requisitos

Antes de executar os testes, você precisa ter instalado:

- **Node.js**
- **npm**
- a API do projeto **banco-api** em execução

## Como executar este projeto de testes

1. Clone este repositório:

```bash
git clone https://github.com/samuelssaquino/banco-api-tests.git
```

2. Acesse a pasta do projeto:

```bash
cd banco-api-tests
```

3. Instale as dependências:

```bash
npm install
```

4. Crie o arquivo `.env` na raiz do projeto:

```env
BASE_URL=http://localhost:3000
```

5. Execute os testes:

```bash
npm test
```

## Script disponível

O script configurado no `package.json` para execução dos testes é:

```json
"test": "mocha \"./test/**/*.test.js\" --timeout 200000 --reporter mochawesome"
```

Esse comando:

- executa todos os arquivos `*.test.js` dentro da pasta `test`;
- utiliza timeout de `200000` ms;
- gera relatório com o reporter **Mochawesome**.

## Relatório de execução

Após executar:

```bash
npm test
```

será criado automaticamente o diretório:

```text
mochawesome-report/
```

Os principais arquivos gerados são:

```text
mochawesome-report/
├── mochawesome.html
└── mochawesome.json
```

Para visualizar o relatório, abra o arquivo abaixo no navegador:

```text
mochawesome-report/mochawesome.html
```

## Cenários atualmente automatizados

### Login

- `POST /Login`
  - deve retornar `200` com token em formato string quando forem informadas credenciais válidas.

### Transferências

- `POST /transferencias`
  - deve retornar `201` quando o valor da transferência for igual ou superior a **R$ 10,00**;
  - deve retornar `422` quando o valor da transferência for inferior a **R$ 10,00**.

- `GET /transferencias/{id}`
  - deve retornar `200` e os dados esperados quando o ID for válido.

- `GET /transferencias?page=1&limit=10`
  - deve retornar `200` com **10 elementos** na paginação quando o limite informado for `10`.

## Exemplo de execução

```bash
npm install
npm test
```

## Documentação das dependências

- **Mocha**: https://mochajs.org/
- **Chai**: https://www.chaijs.com/
- **Supertest**: https://github.com/forwardemail/supertest
- **dotenv**: https://www.npmjs.com/package/dotenv
- **Mochawesome**: https://github.com/adamgruber/mochawesome

## Observações importantes

- O arquivo **`.env`** não está versionado e precisa ser criado manualmente.
- O diretório **`mochawesome-report/`** é gerado após a execução dos testes e não deve ser versionado.
