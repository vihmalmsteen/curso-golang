# GO

## 1.Intro

- Bastante tipada;
- Compilada (rápida);
- Não é OOP, mas, é totalmente possível criar uma orientação a objetos;
- De propósito genérico, é útil para APIs, CLIs, web, microserviços, backend.

## 2. A estrutura de arquivos

No Go, a estrutura não é apenas estética. Ela define como você importa o código:

- Pastas: São pacotes que contêm arquivos go do código do pacote.
- go.mod: Contém as dependências. Pacotes de terceiros ou criados (sendo oriundos das pastas)
- main.go: Arquivo principal que inicia o projeto.

Para iniciar um projeto, basicamente é com o comando `go mod init modulo` no terminal. Isso criará o `go.mod` contendo o nome do módulo ('modulo') e a versão do go:

```go
module modulo

go 1.25.0
```

**NOTA:** Esse arquivo nunca é editado manualmente. Sempre via terminal com comandos como `go mod init`, `go get` e `go mod tidy`.

Em seguida, criar um arquivo `main.go` na raíz do projeto. Exemplo:

```go
// Sempre 'package' vem primeiro. E aqui é main porque arquivo é o main.
package main

// Após 'package' vem os imports. Importar mais pacotes é feito sem vírgula em linhas separadas.
import (
	"fmt"
)

// A função main é a principal. É o que diz ao compilador: "Este é um programa executável, não apenas um package".
func main ()  {
	fmt.Println("Olá mundo!")
}
```

No terminal, já é possível executar `go run main.go` e printará "Olá mundo!".

Para adicionar outro pacote, criar uma nova pasta chamada 'idade' ela terá os códigos do novo pacote obrigatoriamente chamado de 'saudacao' (o pacote em 'package', não o nome do arquivo, este pode ser outra coisa como 'salute.go'):

```go
// Deve ser o nome da pasta. Pois a pasta indica o pacote, não o nome do arquivo
package salute

import (
    "fmt"
)

// A função pode ter o nome que quiser. Mas, vale um DETALHE IMPORTANTE:
// Go não é OOP então não tem private, public, etc. Para uma função deste pacote 'saudacao' ser acessível
// no import de outros pacotes, ela deve ser iniciada com LETRA MAIÚSCULA, como em 'Salute_from_go'.
func Salute_from_go () {
    fmt.printLn("Eu sou o Go!")
}
```

Agora, se quisessemos chamar essa função 'Salute_from_go' no pacote principal main.go:

```go
package main

// O módulo criado tem nome 'modulo' e o package é o nome da pasta 'saudacao', ou seja, importar "modulo/saudacao"
import (
    "fmt"
    "modulo/saudacao"
)

// chamar a função 'Salute_from_go' contida no módulo 'saudacao'
func main () {
    fmt.printLn("Olá mundo!")
    saudacao.Salute_from_go()
}
```

No terminal, rodando `go run main.go` retornará "Olá mundo! Eu sou o Go!". A estrutura final será:

```py
├── 📁 saudacao                 # package 'saudacao'
│   └── 🐹 salute.go            # lógica do pkg 'saudacao' que contém a função acessível 'Salute_from_go'
├── 📄 go.mod                   # versionamento de pacotes, criado com 'go mod init modulo'
└── 🐹 main.go                  # criado manualmente, sendo o pacote principal do programa que será compilado em um binário executável
```

**NOTA:** Agora, sobre funções "públicas" e "privadas", ou seja, exportadas e não exportadas, as funções não exportadas - em minúsculo - ainda são acessíveis pelas demais funções do mesmo pacote.

Dentro do pacote/pasta 'saudacao', vamos criar um arquivo 'creator.go' e nele uma função chamada 'my_reator':

```go
// continua no pacote 'saudacao'
package saudacao

// imports únicos podem ser feitos assim, mesma linha sem parênteses
import "fmt"

// Comentários da função são feitos assim mesmo, coments sobre ela
func my_reator() {
	fmt.Println("Fui criado pelo Google.")
}
```


Essa função NÃO pode ser chamada em 'main.go' uma vez que **ela é privada ao pacote (está escrita em minúsculo)**. Mas, pode ser chamada dentro da função 'Salute_from_go':

```go
package saudacao

// Não é nem mesmo necessário importar, já sendo acessível por estar dentro do mesmo pkg
import (
	"fmt"
)

// chamando a func 'my_reator' diretamente dentro da func 'Saudacao_do_go'
func Saudacao_do_go()  {
	fmt.Println("Eu sou o Go!")
	my_reator()
}
```

Ao rodar `go run main.go`, a função 'my_creator' também rodará por estar contida em uma função extortada e executada dentro de 'main.go', printando:

```txt
Olá mundo!
Eu sou o Go!
Fui criado pelo Google.
```

Para buildar o projeto, executar no terminal `go build`. Com isso, o executável do módulo 'modulo' será criado. O projeto terá a seguinte estrutura ao final:

```md
📁 me
├── 📁 saudacao
│   ├── 🐹 creator.go
│   └── 🐹 salute.go
├── 📝 README.md
├── 📄 go.mod
├── 🐹 main.go
└── ⚙️ modulo.exe
```
