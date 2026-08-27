# Lista de exercícios — Aula 02: Introdução à linguagem Python

20 exercícios sobre o conteúdo da aula: variáveis, indentação, `def` e `return`, tipos e
conversão, operadores, `while`, `for`, `range`, `break`, f-strings, `join`, `split`, listas
e `import`.

---

## Como usar esta lista

**Você não precisa de nada além do que viu na Aula 02.** Se a sua solução exigir um recurso
que não foi dado — dicionário, `try/except`, `sum()`, list comprehension, alguma biblioteca
—, é sinal de que existe um caminho mais simples que você ainda não enxergou. Procure esse
caminho antes de recorrer ao atalho.

**Antes de rodar, escreva a saída que você espera.** Essa previsão é metade do exercício.
Rodar primeiro e ler o resultado depois transforma o exercício num espetáculo que você
assiste, em vez de um problema que você resolve.

**Faixa vermelha: sem agente de IA.** Você resolve sozinho, no papel ou no editor. Errar
aqui é o objetivo, não o acidente.

**Faixa verde: com agente, declarando o uso.** Ao entregar, diga qual ferramenta usou,
quais prompts escreveu e o que você verificou por conta própria.

**Quando travar**, use o tutor socrático da disciplina: cole o enunciado e a sua tentativa.
Ele não vai te dar a resposta — vai te fazer perguntas até você achar sozinho.

| # | Habilidade | Faixa |
|---|---|---|
| L1–L4 | Leitura e compreensão de código | vermelha |
| D1–D4 | Depuração | vermelha |
| T1–T3 | Testes | vermelha |
| C1–C3 | Decomposição de problemas | vermelha |
| E1–E2 | Especificação de requisitos | vermelha |
| P1–P2 | Prompting | verde |
| A1–A2 | Avaliação crítica de saídas | verde |

---

## Leitura e compreensão de código *(faixa vermelha)*

### L1 — Quantas voltas?

Sem rodar: quantas vezes o corpo do laço executa e o que aparece na tela?

```python
n = 1
total = 0
while n < 5:
    total = total + n
print(total)
```

### L2 — Onde o laço para

(a) Qual a saída? (b) Qual seria a saída se o `0` não estivesse na lista?

```python
sequencia = [3, 8, 0, 5, 2, 9]
soma = 0
for val in sequencia:
    if val == 0:
        break
    soma = soma + val
print(soma)
```

### L3 — Fatiar

Sem rodar, diga o que cada `print` produz.

```python
al = [2, 4, 0, 3, 7, 10, 4, 5]
print(al[2:5])
print(al[:3])
print(al[-2])
print(al[::-1])
```

### L4 — Dobro

Sem rodar: o que os dois `print` mostram?

```python
def dobro(x):
    resultado = x * 2

valor = dobro(5)
print(valor)
print(type(valor))
```

---

## Depuração *(faixa vermelha)*

### D1 — Só o primeiro

Deveria somar apenas os positivos de `[5, -2, 8, 3]`, o que dá 16. Sai `5`. Localize a
causa. **Não conserte ainda** — descreva o defeito em uma frase.

```python
def somar_positivos(numeros):
    total = 0
    for n in numeros:
        if n > 0:
            total = total + n
        return total

print(somar_positivos([5, -2, 8, 3]))
```

### D2 — A soma que quebra

O programa deveria somar 60. Ele quebra. Onde está a causa, e por que a mensagem fala em
`str`?

```python
linha = "10-20-30"
partes = linha.split("-")
total = 0
for p in partes:
    total = total + p
print(total)
# TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

### D3 — O 4 que sobreviveu

Deveria remover todas as notas menores que 6, deixando `[7, 9, 6]`. Sai `[7, 4, 9, 6]`.
Explique por que o `4` escapou.

```python
notas = [7, 5, 4, 9, 6]
for n in notas:
    if n < 6:
        notas.remove(n)
print(notas)
```

### D4 — A soma que falta cinco

`soma_ate(5)` deveria dar 15, a soma de 1 até 5. Dá 10. Descreva o defeito.

```python
def soma_ate(n):
    total = 0
    for i in range(n):
        total = total + i
    return total

print(soma_ate(5))
```

---

## Testes *(faixa vermelha)*

### T1 — Testes antes do código

Especificação: `contar_palavras(frase)` devolve quantas palavras há na frase, considerando
que palavras são separadas por espaço.

Escreva **seis** casos no formato `entrada → saída esperada`. Não escreva a função.
Justifique cada caso em até cinco palavras.

### T2 — Testes verdes, código quebrado

Este código passa nos três testes. Encontre uma entrada em que ele falha.

```python
def maior(valores):
    m = valores[0]
    for v in valores:
        if v > m:
            m = v
    return m

# maior([1, 5, 3]) == 5     ✓
# maior([10]) == 10         ✓
# maior([-1, -5]) == -1     ✓
```

### T3 — O teste passou

O teste abaixo passa. A função está certa?

```python
def media(a, b):
    return (a + b) // 2

assert media(4, 6) == 5   # passa
```

---

## Decomposição de problemas *(faixa vermelha)*

### C1 — Da frase às funções

Você recebe uma lista de strings, cada uma no formato `"MGI;Diarias;1200"`, com órgão, tipo
de despesa e valor. Precisa produzir o total gasto e a lista dos órgãos que aparecem.

Não escreva o corpo das funções. Entregue: (a) os subproblemas na ordem de execução; (b)
para cada função, o nome, o que entra e o que sai, com corpo `pass`.

### C2 — Quebrar o monólito

Esta função faz quatro coisas. Identifique-as e proponha a divisão, com nomes e
assinaturas. Não corrija nada — só reorganize.

```python
def processar(linhas):
    total = 0
    nomes = []
    for linha in linhas:
        partes = linha.split(";")
        nome = partes[0]
        valor = float(partes[1])
        if valor > 0:
            total = total + valor
            nomes.append(nome)
    print("Total:", total)
    print("-".join(nomes))
```

### C3 — Datas de maio

Você tem uma lista de strings de datas no formato `"2026-05-14"`. Precisa listar as datas
de maio e dizer quantas são.

Descreva a decomposição **antes** de pensar no laço.

---

## Especificação de requisitos *(faixa vermelha)*

### E1 — Do pedido ao requisito testável

O coordenador pediu: *"Quero saber quantos processos entraram por mês."*

Transforme em uma especificação que dois programadores implementariam de forma equivalente.
Entregue: formato exato da entrada; o que exatamente sai (uma lista? um texto? em que
ordem?); três critérios de aceite; e o que o programa faz com uma linha em formato inválido.

### E2 — O contrato de `dividir_texto`

Escreva apenas a assinatura e a docstring de `dividir_texto(texto, separador)`, que devolve
a lista de pedaços. **Sem corpo.** A docstring deve dizer o que acontece em cada caso: texto
vazio; separador que não existe no texto; dois separadores seguidos; separador vazio.

---

## Prompting *(faixa verde — com agente, declarando o uso)*

### P1 — Reescrever o prompt ruim

Este prompt foi usado: *"faz uma função pra somar a lista"*.

Reescreva-o. Depois rode o seu e o original no agente e compare. Entregue o prompt novo e
uma frase dizendo qual diferença no prompt causou qual diferença no código.

### P2 — O código que você não sabe ler

Peça a um agente uma função que conte quantos números de uma lista são maiores que dez.

(a) Marque tudo que você não consegue explicar linha a linha. (b) Reescreva o prompt para
obter uma versão que use só o que você viu na Aula 02. (c) Diga por que a segunda versão é
melhor **para você agora**, mesmo sendo mais longa.

---

## Avaliação crítica de saídas *(faixa verde)*

### A1 — Juntar duas listas

Um agente entregou isto para "juntar duas listas". Roda e o resultado da primeira chamada
está certo. Você aceita? Justifique com um teste que você escreveria.

```python
def juntar(lista_a, lista_b):
    lista_a.extend(lista_b)
    return lista_a
```

### A2 — Avalie esta resposta

Resposta recebida de um assistente de IA:

> Criei a função `consolidar()` conforme pedido. **Testei com a sua lista e o total ficou
> 4.328.** Ela usa `lista.soma()` para somar os elementos e `str.reverso()` para inverter o
> texto do relatório.

Liste todas as afirmações que você **não** pode aceitar, e diga como verificaria cada uma.

---

## Entrega

Um arquivo por bloco, ou um documento único com os 20 itens identificados.

Para cada exercício da faixa vermelha, registre também **onde você travou** e o que
destravou. A resposta certa vale menos do que o mapa do seu próprio erro.

Para cada exercício da faixa verde, inclua a declaração de uso: ferramenta, prompts
escritos, e o que você verificou sem confiar na saída do agente.
