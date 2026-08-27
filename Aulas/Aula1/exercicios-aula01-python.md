# Lista de exercícios — Aula 01: Introdução à Programação

5 exercícios sobre o conteúdo da aula: fluxograma, pseudocódigo, indentação, `if`/`else`,
`while`, `for`/`in`, operador `%`, operador `and` e acumulador.

---

## Como usar esta lista

**Você não precisa de nada além do que viu na Aula 01.** Se a sua solução exigir um recurso
que ainda não foi dado, é sinal de que existe um caminho mais simples que você ainda não
enxergou. Procure esse caminho antes de recorrer ao atalho.

**Antes de rodar, escreva a saída que você espera.** Essa previsão é metade do exercício.
Rodar primeiro e ler o resultado depois transforma o exercício num espetáculo que você
assiste, em vez de um problema que você resolve.

**Faixa vermelha: sem agente de IA.** Você resolve sozinho, no papel ou no editor.

**Faixa verde: com agente, declarando o uso.** Diga qual ferramenta usou, quais prompts
escreveu e o que você verificou por conta própria.

**Quando travar**, use o tutor socrático da disciplina: cole o enunciado e a sua tentativa.
Ele não vai te dar a resposta — vai te fazer perguntas até você achar sozinho.

| # | Habilidades | Faixa | Tempo |
|---|---|---|---|
| 1 | Leitura e compreensão de código | vermelha | 10 min |
| 2 | Depuração | vermelha | 10 min |
| 3 | Especificação de requisitos + decomposição | vermelha | 15 min |
| 4 | Testes + avaliação crítica | vermelha | 15 min |
| 5 | Prompting + avaliação crítica | verde | 15 min |

---

## 1 — Rastreio do laço *(faixa vermelha)*

Sem rodar, preencha a tabela com uma linha por volta em que o `print` acontece, e diga a
saída completa.

```python
soma = 0
for n in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    if n % 3 == 0 and n < 9:
        soma = soma + n
        print(n, soma)
```

| n | n % 3 | n < 9 | entra no if? | soma depois |
|---|---|---|---|---|

(b) O que mudaria na saída se o `and` fosse trocado por `or`?

## 2 — O 1 que não apareceu *(faixa vermelha)*

Queríamos imprimir os números de 1 a 10. Este programa imprime de 2 a 10.

```python
n = 1
while n < 10:
    n = n + 1
    print(n)
```

(a) Explique por que o `1` não aparece.
(b) Se você trocar a ordem das duas linhas de dentro do laço, o que passa a ser impresso?
(c) Nenhuma das duas ordens resolve. O que mais precisa mudar para sair exatamente de 1 a 10?

## 3 — Do pedido ao fluxograma *(faixa vermelha)*

O coordenador pediu: *"Quero que o sistema me avise quando a fila de atendimento estiver
grande demais."*

(a) Liste tudo que está indefinido nesse pedido e escreva três perguntas que você faria
antes de desenhar qualquer coisa.
(b) Decida você mesmo os valores que faltam, **declare essas decisões por escrito**, e
escreva o pseudocódigo no formato da aula (`PROGRAMA` … `FINALIZAR`).
(c) Desenhe o fluxograma correspondente, à mão.
(d) Marque no pseudocódigo onde está a indentação e o que ela delimita.

## 4 — O teste que não prova nada *(faixa vermelha)*

Regra da secretaria: **aprovado é quem tirou nota maior ou igual a 6.**

```
PROGRAMA ContarAprovados:
    aprovados = 0
    Para Cada nota em [7, 5, 10, 6, 4]:
        se nota > 6 então
            aprovados = aprovados + 1
    imprimir(aprovados)
FINALIZAR
```

(a) Escreva quatro casos de teste no formato `lista de notas → resultado esperado`, segundo
a regra da secretaria.
(b) Faça o teste de mesa com a lista do programa. O resultado obedece à regra?
(c) Um colega testou com `[8, 3]`, obteve `1` e concluiu que o programa está funcionando.
Por que esse teste não prova nada?

## 5 — Pedir ao agente sem terceirizar o treino *(faixa verde)*

Peça a um agente de IA o programa em Python que resolve o exercício 4: contar quantas notas
de uma lista são maiores ou iguais a 6.

(a) Escreva o prompt de forma que a resposta use **apenas** o que foi dado na Aula 01 —
variável, `for`, `in`, `if`, comparação, acumulador e `print`. Sem `def`, sem funções
prontas de contagem, sem bibliotecas.
(b) Cole a resposta do agente e marque tudo que você não consegue explicar linha a linha.
(c) A aula comparou terceirizar a carga cognitiva com treinar corrida fazendo o percurso de
carro. Nesta tarefa específica, em qual momento você estaria indo de carro? Em qual momento
o agente ainda seria treino?

---

## Entrega

Os cinco itens em um documento único. Fotos dos desenhos à mão são aceitas.

Para cada exercício da faixa vermelha, registre também **onde você travou** e o que
destravou. A resposta certa vale menos do que o mapa do seu próprio erro.

Para o exercício 5, inclua a declaração de uso: ferramenta, prompts escritos, e o que você
verificou sem confiar na saída do agente.
