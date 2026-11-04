# Consulta de popularidade de nomes

## Descrição

Nesta atividade individual, você implementará um programa em Haskell que permite ao usuário consultar a popularidade de nomes próprios a partir de dados fornecidos em arquivos. O programa lerá dois arquivos, um com nomes de garotos (`boynames.txt`) e outro com nomes de garotas (`girlnames.txt`), contendo os 1.000 nomes mais populares nos Estados Unidos para o ano de 2003, compilados pela Administração da Segurança Social.

Após carregar os dados, o programa entrará em um laço interativo, permitindo que o usuário digite um nome e veja sua classificação de popularidade e o número de registros, ou uma mensagem caso o nome não seja encontrado.

## Comportamento do programa

1.  No início, o programa deve ler e processar os arquivos `boynames.txt` e `girlnames.txt` para criar as tabelas de dados em memória.
2.  Em seguida, o programa entra em um laço interativo que se repete:
    a. Exibe o prompt `Nome: ` e aguarda a entrada do usuário.
    b. Lê uma linha de texto.
    c. Se a linha estiver em branco, o programa deve terminar.
    d. Se um nome for digitado, o programa deve pesquisar este nome em **ambas** as listas (garotos e garotas) e exibir o resultado para cada uma.
    e. O laço então recomeça do passo (a).

---

## Formato dos Arquivos de Entrada

O repositório template incluirá os arquivos `boynames.txt` e `girlnames.txt`. Cada linha desses arquivos contém um nome, seguido por um espaço e o número de registros daquele nome no ano. A popularidade (ranking) é determinada pela posição da linha no arquivo (a primeira linha é o 1º mais popular, a segunda é o 2º, e assim por diante).

**Exemplo de registros (`girlnames.txt`):**
```

Emily 25494
Emma 22532
Madison 19986
...

````

---

## Funções a Implementar

Recomenda-se fortemente que você divida seu programa nas seguintes funções, a serem implementadas em `src/Popularidade.hs`, conforme as especificações a seguir:

1.  **`tabela :: String -> [(Int, String, Int)]`**
    * Uma função **pura** que recebe o conteúdo de um dos arquivos como uma única `String` e o transforma em uma lista de tuplas. Cada tupla deve conter `(Ranking, Nome, Número de Registros)`.

2.  **`pesquisa :: String -> [(Int, String, Int)] -> String -> IO ()`**
    * Uma **ação de E/S** que recebe o tipo da lista ("garotos" ou "garotas"), a tabela de dados correspondente, e o nome a ser pesquisado. A ação deve imprimir o resultado formatado na tela (se o nome foi encontrado ou não).

3.  **`go :: [(Int, String, Int)] -> [(Int, String, Int)] -> IO ()`**
    * A **ação de E/S recursiva** principal que implementa o laço interativo. Ela recebe as duas tabelas de nomes (garotos e garotas), solicita a entrada do usuário e chama `pesquisa` para cada tabela.

4.  **`main :: IO ()`**
    * A **ação de E/S** que orquestra todo o programa. Ela deve:
        * Configurar o buffering de saída (`hSetBuffering stdout NoBuffering`).
        * Ler os dois arquivos (`readFile`).
        * Chamar a função `tabela` para processar o conteúdo de cada arquivo.
        * Iniciar o laço interativo chamando a ação `go` com as tabelas processadas.

---

## Exemplos de Execução

Seu programa deve replicar o comportamento dos exemplos abaixo:

**Exemplo 1:**
```shellsession
Nome: Justice
Justice classificado na posição 456 entre garotas com 655 registros
Justice classificado na posição 401 entre garotos com 653 registros
Nome: 
````

**Exemplo 2:**

```shellsession
Nome: Walter
Walter não encontrado entre garotas
Walter classificado na posição 356 entre garotos com 775 registros
Nome: 
```

---

## Requisitos e convenções

- A busca deve considerar exatamente o nome digitado, com diferenciação entre maiúsculas e minúsculas. Não é necessário normalizar espaços ou grafias.
- Os arquivos são fornecidos no repositório. Cada linha contém **dois campos**: nome e número de registros; a posição da linha, começando em 1, fornece o ranking.
- Uma linha de entrada vazia encerra a interação sem realizar outra consulta. A saída da consulta deve apresentar **garotas antes de garotos**, conforme os exemplos.
- O diretório de trabalho ao executar o programa deve ser a raiz do projeto, onde se encontram `boynames.txt` e `girlnames.txt`.
- A implementação deve preservar as assinaturas das quatro funções de `src/Popularidade.hs` e manter a interpretação dos dados em funções puras.
- Use casamento de padrões quando for razoável, especialmente ao percorrer listas e tratar casos base.

## Desenvolvimento e testes

No diretório raiz do projeto:

```bash
cabal update          # se necessário na primeira utilização
cabal build
cabal test
cabal run popularidade-nomes
```

Um ciclo de consulta termina quando o usuário pressiona Enter em uma linha vazia. Os testes Hspec fornecidos verificam parte dos requisitos; o professor pode utilizar casos adicionais na avaliação.

## Entrega no GitHub

Esta atividade será distribuída por **Classroom 50** a partir de um repositório template privado na organização `UFOP-BCC222`. Não crie um repositório público nem copie uma solução de referência para o repositório do aluno.

Depois de implementar e testar o programa, faça o envio de suas alterações na branch `main`:

```bash
git status
git add src/Popularidade.hs
git commit -m "Implementa consulta de popularidade de nomes"
git push
```

**Prazo regular:** até o final da aula de 4 de novembro de 2026 (100 minutos).

**Extensão sem penalização:** até **23h59 do mesmo dia**, horário de Brasília. A confirmação da entrega será feita pelo repositório individual criado por meio do Classroom 50.
