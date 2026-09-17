# POO - Atividade 3

Resolução dos exercícios de **Diagramas de Classes UML**.

## Exercício 1 — Cadastro de estudantes

```mermaid
classDiagram
    class Aluno {
        -String matricula
        -String nome
        -String email
        -LocalDate dataIngresso
        +consultarDados() void
        +alterarEmail(String novoEmail) void
    }
```

## Exercício 2 — Livros, autores e editoras

```mermaid
classDiagram
    class Livro {
        -String isbn
        -String titulo
        -int ano
        -int numeroPaginas
        +exibirFicha() void
    }

    class Autor {
        -String nome
        -String nacionalidade
        -LocalDate dataNascimento
        +obterBibliografia() void
    }

    class Editora {
        -String nome
        -String cidade
    }

    Editora "1" -- "0..*" Livro : publica
    Livro "0..*" -- "1..*" Autor : escrito por
```

## Exercício 3 — Curso, aluno e matrícula

```mermaid
classDiagram
    class Aluno {
        -String matricula
        -String nome
    }

    class Curso {
        -String codigo
        -String nome
        -int cargaHoraria
    }

    class Matricula {
        -LocalDate dataMatricula
        -String situacao
        -double notaFinal
        +registrarNota(double nota) void
        +alterarSituacao(String novaSituacao) void
    }

    Aluno "1" -- "0..*" Matricula
    Curso "1" -- "0..*" Matricula
```

## Exercício 4 — Loja virtual e itens de pedido

```mermaid
classDiagram
    class Cliente {
        -String nome
        -String email
    }

    class Pedido {
        -int numero
        -LocalDate data
        +calcularTotal() double
    }

    class ItemPedido {
        -int quantidade
        -double precoUnitario
        +calcularSubtotal() double
    }

    class Produto {
        -String codigo
        -String nome
        -double preco
    }

    Cliente "1" -- "0..*" Pedido : faz
    Pedido "1" *-- "1..*" ItemPedido : possui
    Produto "1" -- "0..*" ItemPedido : aparece em
```

**Anotação:** `ItemPedido` foi modelado como classe porque o vínculo entre `Pedido` e `Produto` possui dados próprios, como `quantidade` e `precoUnitario`. Além disso, o item faz parte do ciclo de vida do pedido, justificando a composição.

## Exercício 5 — Hotel, quartos e reservas

```mermaid
classDiagram
    class Hospede {
        -String nome
        -String cpf
        -String email
        +consultarReservas() void
    }

    class Quarto {
        -int numero
        -String tipo
        -double valorDiaria
        +estaDisponivel() boolean
    }

    class Reserva {
        -LocalDate dataEntrada
        -LocalDate dataSaida
        -String status
        +confirmar() void
        +cancelar() void
    }

    Hospede "1" -- "0..*" Reserva : realiza
    Quarto "1" -- "0..*" Reserva : recebe
```

## Exercício 6 — Clínica e consultas médicas

```mermaid
classDiagram
    class Paciente {
        -String nome
        -String cpf
    }

    class Medico {
        -String nome
        -String crm
    }

    class Consulta {
        -LocalDateTime dataHora
        -String observacoes
        -String status
        +agendar() void
        +cancelar() void
        +registrarObservacao(String texto) void
    }

    class Especialidade {
        -String nome
        -String descricao
    }

    Paciente "1" -- "0..*" Consulta : possui
    Medico "1" -- "0..*" Consulta : atende
    Especialidade "1" -- "0..*" Medico : possui
```

## Exercício 7 — Frota com especialização de veículos

```mermaid
classDiagram
    class Veiculo {
        <<abstract>>
        -String placa
        -String marca
        -String modelo
        -int ano
        +calcularCustoMensal()* double
    }

    class Automovel {
        -int quantidadePortas
        +calcularCustoMensal() double
    }

    class Motocicleta {
        -int cilindradas
        +calcularCustoMensal() double
    }

    class Caminhao {
        -double capacidadeCarga
        +calcularCustoMensal() double
    }

    Veiculo <|-- Automovel
    Veiculo <|-- Motocicleta
    Veiculo <|-- Caminhao
```

## Exercício 8 — Plataforma de cursos on-line

```mermaid
classDiagram
    class Usuario {
        -String nome
        -String email
        +exibirPerfil() void
    }

    class Aluno {
        +consultarProgresso() void
    }

    class Professor {
        +criarCurso() void
    }

    class Curso {
        -String titulo
        -String descricao
        -int cargaHoraria
        +adicionarAula(Aula aula) void
    }

    class Aula {
        -String titulo
        -String conteudo
        +exibirConteudo() void
    }

    class Matricula {
        -double progresso
        -LocalDate dataInicio
        +atualizarProgresso(double progresso) void
    }

    Usuario <|-- Aluno
    Usuario <|-- Professor
    Professor "1" -- "0..*" Curso : cria
    Curso "1" *-- "1..*" Aula : composto por
    Aluno "1" -- "0..*" Matricula
    Curso "1" -- "0..*" Matricula
```

## Exercício 9 — Formas de pagamento

```mermaid
classDiagram
    class Pagavel {
        <<interface>>
        +pagar(double valor) boolean
    }

    class PagamentoPix {
        -String chave
        +pagar(double valor) boolean
        +validarChave() boolean
    }

    class PagamentoCartao {
        -String numeroMascarado
        -int quantidadeParcelas
        +pagar(double valor) boolean
        +calcularParcela(double valor) double
    }

    class PagamentoBoleto {
        -String codigo
        -LocalDate dataVencimento
        +pagar(double valor) boolean
        +estaVencido() boolean
    }

    Pagavel <|.. PagamentoPix
    Pagavel <|.. PagamentoCartao
    Pagavel <|.. PagamentoBoleto
```

## Exercício 10 — Assistência técnica — modelo integrado

```mermaid
classDiagram
    class Cliente {
        -String nome
        -String telefone
    }

    class Equipamento {
        -String identificacao
        -String tipo
        -String modelo
    }

    class OrdemServico {
        -String descricaoDefeito
        -LocalDate dataAbertura
        -String status
        -double valorEstimado
        +abrir() void
        +atribuirTecnico(Tecnico tecnico) void
        +alterarStatus(String novoStatus) void
        +calcularTotal() double
    }

    class ItemServico {
        -String descricao
        -int quantidade
        -double valorUnitario
        +calcularSubtotal() double
    }

    class TipoServico {
        -String codigo
        -String nome
    }

    class Tecnico {
        -String nome
        -String matricula
    }

    Cliente "1" -- "0..*" Equipamento : possui
    Cliente "1" -- "0..*" OrdemServico : solicita
    Equipamento "1" -- "0..*" OrdemServico : recebe manutenção
    OrdemServico "1" *-- "0..*" ItemServico : possui
    TipoServico "1" -- "0..*" ItemServico : classifica
    Tecnico "0..1" -- "0..*" OrdemServico : responsável por
```

**Revisão do modelo:** `Cliente`, `Equipamento`, `Tecnico` e `TipoServico` não foram representados como simples atributos dentro de `OrdemServico` ou `ItemServico`. Como são conceitos próprios do domínio, com identidade e dados próprios, aparecem como classes relacionadas por associações. A multiplicidade `0..1` no lado de `Tecnico` representa que uma ordem pode ainda não possuir técnico responsável.
