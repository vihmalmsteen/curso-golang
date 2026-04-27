# Curso de Go (Golang)

Este repositório contém o código-fonte de um curso introdutório de **Go**, organizado em 24 capítulos numerados que vão dos fundamentos da linguagem até a construção de um CRUD completo com banco de dados. Todo o conteúdo está em português.

## Pré-requisitos

- **Go 1.14+** instalado ([download](https://go.dev/dl/))
- **MySQL** local (apenas para os capítulos 23 e 24)
- Editor de sua preferência (VS Code, GoLand, etc.)

## Estrutura do Curso

Cada capítulo é uma pasta numerada. Capítulos simples possuem um único arquivo `.go` que pode ser executado diretamente com `go run`. Capítulos que dependem de pacotes externos ou que possuem múltiplos arquivos têm seu próprio `go.mod`.

### 1 - Pacotes
Como funcionam os pacotes em Go, criação de módulos com `go mod` e organização de código em arquivos separados.

### 2 - Variáveis
Declaração de variáveis, tipos explícitos e inferência de tipo, constantes e escopo.

### 3 - Tipos de Dados
Tipos primitivos da linguagem: inteiros, floats, strings, booleanos e conversões entre eles.

### 4 - Funções
Definição de funções, parâmetros, retornos múltiplos e uso básico no fluxo do programa.

### 5 - Operadores
Operadores aritméticos, de atribuição, relacionais, lógicos e unários.

### 6 - Structs
Definição de structs, instanciação e acesso a campos para representar dados estruturados.

### 7 - Herança Só que não
Como Go lida com "herança" através de composição de structs, já que a linguagem não possui herança clássica.

### 8 - Ponteiros
Conceito de ponteiros, operadores `&` e `*`, e quando passar valores por referência.

### 9 - Arrays e Slices
Diferença entre arrays (tamanho fixo) e slices (dinâmicos), `append`, `len`, `cap` e fatiamento.

### 10 - Maps
Estrutura de dados chave-valor, criação, leitura, escrita e remoção de elementos.

### 11 - If Else
Estruturas condicionais, incluindo a forma curta com inicialização de variável.

### 12 - Switch
Uso do `switch` em Go, com múltiplos casos, condições sem expressão e `fallthrough`.

### 13 - Loops
O `for` em Go (a única estrutura de repetição da linguagem) em todas as suas variações.

### 14 - Funções Avançadas
Subdividido em 9 tópicos: retorno nomeado, funções variáticas, funções anônimas, recursivas, `defer`, `panic`/`recover`, closures, ponteiros em funções e a função `init`.

### 15 - Métodos
Como associar funções a tipos, diferença entre receiver por valor e por ponteiro.

### 16 - Interfaces
Definição e implementação de interfaces, com exemplos em `Formas` (polimorfismo) e `Tipo Genérico` (interface vazia).

### 17 - Aplicação de Linha de Comando
Construção de uma CLI completa utilizando o pacote externo [`github.com/urfave/cli`](https://github.com/urfave/cli). Lógica organizada em `app/app.go`.

### 18 - Concorrência
Goroutines, `sync.WaitGroup`, channels (com e sem buffer), `select` e padrões de concorrência aplicados.

### 19 - Testes Automatizados
Testes com a biblioteca padrão `testing`, divididos em uma introdução e em testes mais avançados (table-driven).

### 20 - JSON
Serialização (`Marshal`) e desserialização (`Unmarshal`) de JSON com structs e tags.

### 21 - HTTP
Criação de um servidor HTTP simples utilizando o pacote `net/http` da biblioteca padrão.

### 22 - HTML, CSS e Javascript
Servir arquivos estáticos a partir de Go, com um `home.html` renderizado pelo servidor.

### 23 - Banco de Dados
Conexão com MySQL utilizando [`github.com/go-sql-driver/mysql`](https://github.com/go-sql-driver/mysql), executando queries básicas.

### 24 - Crud Básico
Aplicação final do curso: um CRUD completo com rotas HTTP usando [`github.com/gorilla/mux`](https://github.com/gorilla/mux) e persistência em MySQL. Código separado entre `servidor/` (handlers) e `banco/` (acesso a dados).

## Como executar

A maioria das aulas não possui `go.mod` e contém um único arquivo. Basta entrar na pasta e rodar:

```bash
cd "9 - Arrays e Slices"
go run arrays-e-slices.go
```

Para aulas com módulo próprio, rode `go mod download` na primeira execução para baixar as dependências:

```bash
cd "17 - Aplicação de Linha de Comando"
go mod download
go run .
```

Para rodar os testes do capítulo 19:

```bash
cd "19 - Testes Automatizados/1 - Introdução"
go test ./...
```

## Dependências externas

A maior parte do curso utiliza apenas a biblioteca padrão. As aulas abaixo requerem pacotes externos (já declarados no `go.mod` da respectiva pasta):

| Capítulo | Pacote |
|----------|--------|
| 17 - Aplicação de Linha de Comando | `github.com/urfave/cli` |
| 23 - Banco De Dados | `github.com/go-sql-driver/mysql` |
| 24 - Crud Básico | `github.com/gorilla/mux`, `github.com/go-sql-driver/mysql` |

## Configuração do MySQL (pastas 23 e 24)

Para executar as aulas de banco de dados, você precisa de uma instância local do MySQL rodando. Os dados de conexão (usuário, senha, host, banco) estão definidos diretamente no código de cada aula, ajuste conforme o seu ambiente local antes de rodar.
