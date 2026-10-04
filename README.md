# Conversor de AFND para AFD

Projeto em Python para converter um **autômato finito não determinístico
(AFND)** em um **autômato finito determinístico (AFD)** equivalente e
comparar o reconhecimento de palavras nos dois autômatos.

O projeto atende ao Trabalho 1B de Linguagens Formais e Autômatos. O
enunciado original está em
[`docs/Trabalho_1B_2026-2-2.pdf`](docs/Trabalho_1B_2026-2-2.pdf).

> **Status atual:** a estrutura inicial do projeto está criada, mas a
> implementação da conversão e dos testes ainda está pendente. No estado
> atual, `src/main.py` apenas exibe uma mensagem de teste.

## Objetivos do trabalho

- Receber os dados de um AFND fornecidos no laboratório no dia da avaliação.
- Gerar um AFD equivalente por meio da construção de subconjuntos.
- Testar palavras no AFND antes da conversão.
- Testar as mesmas palavras no AFD depois da conversão.
- Confirmar que os resultados de aceitação e rejeição são iguais.
- Desenhar o AFND de entrada e o AFD de saída no JFLAP, conforme solicitado
  no enunciado.

## Fundamentação

Um AFND pode possuir zero, uma ou várias transições para o mesmo símbolo a
partir de um estado. No AFD, cada estado possui exatamente uma transição para
cada símbolo do alfabeto. A conversão representa cada estado do AFD como um
**conjunto de estados do AFND**:

1. O estado inicial do AFD é o conjunto que contém o estado inicial do AFND
   (incluindo o fecho-ε, caso o formato aceite transições vazias).
2. Para cada conjunto de estados e símbolo do alfabeto, calcula-se a união dos
   destinos possíveis no AFND.
3. Cada conjunto ainda não visitado torna-se um novo estado do AFD.
4. Um estado do AFD é final quando contém pelo menos um estado final do AFND.
5. O processo termina quando não há novos conjuntos a processar.

Essa construção preserva a linguagem reconhecida:

```text
L(AFND) = L(AFD)
```

## Organização do repositório

```text
.
├── README.md
├── docs/
│   └── Trabalho_1B_2026-2-2.pdf  # enunciado-base
└── src/
    └── main.py                    # ponto de entrada da aplicação
```

## Como executar

O projeto não possui dependências externas previstas. Com Python 3 instalado:

```bash
python3 src/main.py
```

Quando a implementação estiver concluída, o ponto de entrada deverá permitir
carregar ou informar o AFND e executar a conversão e a validação. O formato
definitivo da entrada deve ser definido antes da avaliação, considerando que
os dados oficiais serão fornecidos no laboratório.

## Fluxo de uso planejado

1. Ler e validar estados, alfabeto, estado inicial, estados finais e
   transições do AFND.
2. Exibir ou registrar o AFND carregado.
3. Simular cada palavra de teste no AFND.
4. Converter o AFND para AFD pela construção de subconjuntos.
5. Exibir ou registrar estados e transições do AFD.
6. Simular as mesmas palavras no AFD.
7. Comparar os resultados e informar eventuais divergências.
8. Reproduzir os dois autômatos no JFLAP para a entrega/apresentação.

## Critérios de aceitação

- O conversor deve aceitar AFNDs com múltiplos destinos para um mesmo par
  estado/símbolo.
- Todos os subconjuntos alcançáveis devem ser considerados como estados do
  AFD.
- Estados finais do AFD devem ser identificados corretamente.
- Palavras aceitas pelo AFND devem ser aceitas pelo AFD equivalente.
- Palavras rejeitadas pelo AFND devem ser rejeitadas pelo AFD equivalente.
- A comparação deve usar exatamente as mesmas palavras nos dois simuladores.
- O programa deve informar entradas inválidas de forma explícita, sem produzir
  um resultado de conversão aparentemente válido.

## OKRs

### Objetivo 1 — Entregar uma conversão correta e reproduzível

| Key Result | Meta de conclusão |
|---|---|
| KR1.1 | Implementar a construção de subconjuntos para todos os estados alcançáveis do AFND. |
| KR1.2 | Garantir que 100% dos estados do AFD que contêm um estado final do AFND sejam marcados como finais. |
| KR1.3 | Validar a conversão com pelo menos um caso com múltiplas transições para o mesmo símbolo e um caso com estado inalcançável. |
| KR1.4 | Obter resultados idênticos de aceitação/rejeição para todas as palavras do conjunto de testes. |

### Objetivo 2 — Tornar a validação do trabalho objetiva

| Key Result | Meta de conclusão |
|---|---|
| KR2.1 | Implementar simuladores independentes para AFND e AFD. |
| KR2.2 | Executar as mesmas palavras nos dois autômatos e apresentar o resultado de cada uma. |
| KR2.3 | Produzir uma mensagem clara quando houver divergência entre os autômatos. |
| KR2.4 | Cobrir palavras vazias, palavras aceitas, palavras rejeitadas e palavras com símbolos fora do alfabeto, conforme o formato de entrada adotado. |

### Objetivo 3 — Preparar a apresentação conforme o enunciado

| Key Result | Meta de conclusão |
|---|---|
| KR3.1 | Registrar no README o formato de entrada e um exemplo mínimo executável. |
| KR3.2 | Desenhar no JFLAP o AFND utilizado na validação. |
| KR3.3 | Desenhar no JFLAP o AFD produzido pela conversão. |
| KR3.4 | Conferir manualmente no JFLAP e no programa as mesmas palavras de teste antes da avaliação. |

## Próximas etapas

- Definir o formato de entrada compatível com os dados fornecidos no
  laboratório.
- Implementar as estruturas de dados do AFND e do AFD.
- Implementar a simulação do AFND, a conversão e a simulação do AFD.
- Adicionar casos de teste automatizados para os critérios de aceitação.
- Atualizar este README com exemplos reais de entrada e saída após a definição
  do formato.
