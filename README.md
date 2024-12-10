# Avaliação 2 - IMD0040 - Linguagem de Programação 2

## Instruções

1. Leia atentamente o enunciado antes de começar a resolver.
2. Certifique-se de implementar todos os requisitos descritos.


---

## Sistema de Gerenciamento Acadêmico

**Objetivo**: Implementar um sistema de gerenciamento de notas e desempenho acadêmico que utiliza uma interface funcional para o cálculo da média das notas.

---

### Requisitos

#### 1. Estrutura Básica

1. **Classe `Pessoa` (abstrata)**:
    - Atributos:
        - `String nome` (Protegido)
        - `String matricula` (Protegido)
    - Método abstrato:
        - `void exibirDetalhes()`

2. **Classe `Aluno` (extende `Pessoa`)**:
    - Atributos:
        - `List<Double> notas`
    - Métodos:
        - Implementação de `exibirDetalhes()`:
            - Exibe o nome, a matrícula e as notas do aluno.

3. **Enum `Status`**:
    - Valores possíveis:
        - `APROVADO`
        - `REPROVADO`

4. **Classe `Resultado`**:
    - Atributos:
        - `String matriculaAluno`
        - `Status status`
        - `double media`
    - Construtor:
        - Inicializa `matriculaAluno`, `media` e `status`.
    - Métodos:
        - `String getMatriculaAluno()`: Retorna a matrícula do aluno.
        - `double getMedia()`: Retorna a média.
        - `Status getStatus()`: Retorna o status.

5. **Interface Funcional `CalculadoraMedia`**:
    - Método funcional:
        - `double calcularMedia(List<Double> notas)`

6. **Classe `MediaAritmetica` (implementa `CalculadoraMedia`)**:
    - Método:
        - Implementação de `calcularMedia`:
            - Calcula a média aritmética das notas fornecidas.

7. **Interface `ITurma`**:
    - Métodos:
        - `void adicionarAluno(Aluno aluno)`
        - `Aluno buscarAlunoPorMatricula(String matricula)`
        - `List<Aluno> getAlunos()`
        - `List<Resultado> processarNotas()`

8. **Classe `Turma` (implementa `ITurma`)**:
    - Atributos:
        - `String codigo`
        - `Map<String, Aluno> alunos` (utilize a matrícula como chave)
        - `CalculadoraMedia calculadoraMedia`
    - Construtor:
        - Aceita um parâmetro do tipo `CalculadoraMedia` e o armazena no atributo correspondente.
    - Métodos:
        - `void adicionarAluno(Aluno aluno)`:
            - Adiciona um aluno ao mapa de alunos.
        - `Aluno buscarAlunoPorMatricula(String matricula)`:
            - Retorna o aluno correspondente à matrícula ou lança a exceção `AlunoNaoEncontradoException`.
        - `List<Aluno> getAlunos()`:
            - Retorna uma lista com todos os alunos da turma.
        - `List<Resultado> processarNotas()`:
            - Para cada aluno no mapa:
                - Usa a instância de `CalculadoraMedia` para calcular a média das notas.
                - Define o status como `APROVADO` se a média for maior ou igual a 7, ou `REPROVADO` caso contrário.
                - Cria e adiciona um objeto `Resultado` a uma lista.
            - Ordena a lista de `Resultado` em ordem crescente pela média das notas.
            - Retorna a lista ordenada.

9. **Exceção `AlunoNaoEncontradoException`**:
    - Mensagem: "Aluno não encontrado na turma."

---

#### 2. Testes e Demonstração

1. **No Método `main`**:
    - Crie pelo menos 3 alunos com diferentes notas.
    - Crie uma instância de `MediaAritmetica` e passe como parâmetro ao construtor de `Turma`.
    - Adicione os alunos à turma.
    - Utilize `processarNotas()` para calcular e ordenar os resultados.
    - Exiba os resultados indicando matrícula, média e status (APROVADO/REPROVADO) em ordem crescente pela média.

---

### Estrutura Esperada do Código

- Classe Pessoa (abstrata)
  - Classe Aluno (extende Pessoa)
- Classe Resultado
- Enum Status
- Interface Funcional CalculadoraMedia
  - Classe MediaAritmetica (implementa CalculadoraMedia)
- Interface ITurma
- Classe Turma (implementa ITurma)
- Exceção AlunoNaoEncontradoException

---

### Exemplo de uso

```java
public static void main(String[] args) {
    CalculadoraMedia calculadora = new MediaAritmetica();
    ITurma turma = new Turma("Turma 1", calculadora);

    Aluno aluno1 = new Aluno("Alice", "202301", Arrays.asList(8.0, 7.5, 9.0));
    Aluno aluno2 = new Aluno("Bob", "202302", Arrays.asList(6.0, 5.5, 4.0));
    Aluno aluno3 = new Aluno("Carlos", "202303", Arrays.asList(7.0, 8.0, 6.5));

    turma.adicionarAluno(aluno1);
    turma.adicionarAluno(aluno2);
    turma.adicionarAluno(aluno3);

    List<Resultado> resultados = turma.processarNotas();

    for (Resultado resultado : resultados) {
        System.out.println("Aluno: " + resultado.getMatriculaAluno() + 
                           ", Média: " + resultado.getMedia() +
                           ", Status: " + resultado.getStatus());
    }
}

