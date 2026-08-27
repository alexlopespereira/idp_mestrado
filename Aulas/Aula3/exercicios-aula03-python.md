# Lista de exercícios — Aula 03: Estruturas de Dados Nativas do Python

20 exercícios sobre o conteúdo da aula: `sorted` vs `sort`, tipos de erro, dicionários,
tuplas, conjuntos, `zip`, sentença inline, list comprehension, requisições HTTP com JSON e
`try`/`except`.

---

## Como usar esta lista

**Você pode usar tudo o que viu nas Aulas 01, 02 e 03** — e não precisa de mais nada. Se a
sua solução exigir um recurso que ainda não foi dado, procure primeiro o caminho mais
simples.

**Antes de rodar, escreva a saída que você espera.** Essa previsão é metade do exercício.
Rodar primeiro e ler o resultado depois transforma o exercício num espetáculo que você
assiste, em vez de um problema que você resolve.

**Faixa vermelha: sem agente de IA.** **Faixa verde: com agente, declarando o uso** —
ferramenta, prompts escritos, e o que você verificou por conta própria.

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

### L1 — Duas formas de ordenar

Sem rodar, diga o que cada `print` produz. Depois responda: se você precisasse manter a
ordem original de `a`, qual das duas formas usaria — e por que já é tarde neste código?

```python
a = [3, 1, 2]
b = a.sort()
c = sorted(a)
print(a)
print(b)
print(c)
```

### L2 — Agrupando em dicionário

Qual é a saída dos dois `print`?

```python
s = [['MGI', 10], ['MF', 5], ['MGI', 20], ['MEC', 7]]
d = {}
for k, v in s:
    if k in d.keys():
        d[k].append(v)
    else:
        d[k] = [v]
print(d)
print(len(d))
```

### L3 — Conjuntos

Sem rodar, diga o que cada `print` produz.

```python
a = {1, 2, 3, 3, 4}
b = {3, 4, 5}
print(len(a))
print(a | b)
print(a & b)
print(5 in a)
```

### L4 — zip, inline e comprehension

(a) Qual a saída dos dois `print`? (b) O que aconteceria com `resultado` se `gastos` tivesse
apenas `[1200, 800]`?

```python
orgaos = ["MGI", "MF", "MEC"]
gastos = [1200, 800, 1500]

resultado = [o for o, g in zip(orgaos, gastos) if g > 1000]
print(resultado)

status = ["alto" if g > 1000 else "baixo" for g in gastos]
print(status)
```

---

## Depuração *(faixa vermelha)*

### D1 — O órgão que não estava lá

O programa quebra.
(a) Explique a causa.
(b) O enunciado do problema não disse o que fazer com um órgão sem gasto registrado.
Proponha dois consertos diferentes e diga o que cada um assume sobre o requisito.

```python
gastos = {"MGI": 1200, "MF": 800}
orgaos = ["MGI", "MF", "MEC"]
total = 0
for o in orgaos:
    total = total + gastos[o]
print(total)
# KeyError: 'MEC'
```

### D2 — O except que engoliu tudo

A soma deveria ser 70, ignorando o valor inválido. O programa imprime apenas `deu erro`.
(a) Onde estão os dois problemas — um de estrutura e um de captura?
(b) Qual valor `total` tinha no instante em que a exceção aconteceu?

```python
valores = ["10", "20", "trinta", "40"]
total = 0
try:
    for v in valores:
        total = total + int(v)
    print(total)
except:
    print("deu erro")
```

### D3 — A tupla que mudou

A primeira linha levanta um erro; a segunda funciona. Explique por quê.

```python
config = ("MGI", 2026, [1, 2])

config[1] = 2027        # TypeError
config[2].append(3)     # funciona
print(config)
```

### D4 — Todos maiores que mil

A intenção era selecionar os valores acima de 1000. O programa não quebra e devolve os três.
Explique o que está sendo comparado.

```python
valores = ["1200", "800", "150"]
maiores = []
for v in valores:
    if v > "1000":
        maiores.append(v)
print(maiores)
```

---

## Testes *(faixa vermelha)*

### T1 — Testes antes do código

Especificação: `agrupar(registros)` recebe uma lista de pares `[orgao, valor]` e devolve um
dicionário que associa cada órgão à lista dos seus valores, na ordem em que apareceram.

Escreva **seis** casos no formato `entrada → saída esperada`. Não escreva a função.
Justifique cada caso em até cinco palavras.

### T2 — Testes verdes, código quebrado

Este código passa nos três testes. Encontre uma entrada em que ele falha.

```python
def total_por_orgao(registros):
    d = {}
    for orgao, valor in registros:
        d[orgao] = valor
    return d

# total_por_orgao([["MGI", 100]]) == {"MGI": 100}                      ✓
# total_por_orgao([]) == {}                                            ✓
# total_por_orgao([["MGI",100],["MF",50]]) == {"MGI":100,"MF":50}      ✓
```

### T3 — O teste que passou sem provar nada

O teste abaixo passa. Explique por que ele não permite concluir que a função funciona.

```python
import requests

def buscar_cotacao(moeda):
    try:
        r = requests.get("https://api.exchangerate-api.com/v4/latest/USD")
        return r.json()["rates"][moeda]
    except:
        return 0

assert buscar_cotacao("XYZ") == 0   # passa
```

---

## Decomposição de problemas *(faixa vermelha)*

### C1 — Da frase às funções

Você precisa produzir um relatório com as cotações de quatro moedas de interesse frente ao
dólar, ordenado por nome da moeda, a partir da API pública de câmbio.

Não escreva o corpo das funções. Entregue: (a) os subproblemas na ordem de execução; (b)
para cada função, o nome, o que entra e o que sai, com corpo `pass`; (c) diga qual dessas
funções você conseguiria testar **sem internet**, e por que isso importa.

### C2 — Quebrar o monólito

Esta função faz quatro coisas. Identifique-as e proponha a divisão, com nomes e assinaturas.
Não corrija nada — só reorganize.

```python
import requests

def relatorio():
    r = requests.get("https://api.exchangerate-api.com/v4/latest/USD")
    dados = r.json()
    rates = dados["rates"]
    interesse = {"BRL", "EUR", "GBP", "JPY"}
    linhas = []
    for k, v in rates.items():
        if k in interesse:
            linhas.append(f"{k}: {v}")
    for l in sorted(linhas):
        print(l)
```

### C3 — Quem enviou e quem devia enviar

Você tem duas listas: os órgãos que enviaram o relatório mensal e os órgãos obrigados a
enviar. Precisa produzir três números: quem faltou, quem enviou sem estar obrigado, e
quantos estão nas duas listas. Os nomes chegam com grafias inconsistentes — maiúsculas e
minúsculas misturadas, espaços sobrando.

Descreva a decomposição **antes** de pensar em conjuntos.

---

## Especificação de requisitos *(faixa vermelha)*

### E1 — Do pedido ao requisito testável

O diretor pediu: *"Me avise quando o dólar subir muito."*

Transforme em uma especificação que dois programadores implementariam de forma equivalente.
Entregue: definição operacional de "subir muito"; fonte do dado; frequência de consulta;
formato do aviso; três critérios de aceite; e o comportamento em cada uma destas falhas —
API fora do ar, resposta sem a chave `"rates"`, e cotação que não muda há dias.

### E2 — O contrato de `cotacao`

Escreva apenas a assinatura e a docstring de `cotacao(moeda)`, que devolve a taxa de
conversão do dólar para a moeda pedida. **Sem corpo.** A docstring deve declarar o
comportamento em quatro casos: moeda inexistente; API fora do ar; resposta sem a chave
`"rates"`; moeda passada em minúsculas.

Depois responda: qual exceção específica cada um dos três primeiros casos produziria, e por
que `except:` puro seria uma escolha ruim neste contrato?

---

## Prompting *(faixa verde)*

### P1 — Reescrever o prompt ruim

Este prompt foi usado: *"faz um script que pega a cotação do dólar"*.

Reescreva-o. Depois rode o seu e o original no agente e compare. Entregue o prompt novo e
uma frase dizendo qual diferença no prompt causou qual diferença no código.

### P2 — O silêncio que o prompt autorizou

Um colega pediu ao agente um script que busca a cotação e recebeu isto:

```python
try:
    r = requests.get(url)
    dados = r.json()
    total = dados["rates"]["BRL"] * quantidade
    print(f"Total: {total}")
except:
    pass
```

(a) Liste tudo que este trecho viola das boas práticas da aula.
(b) Reescreva o **prompt** — não o código — de modo que a próxima resposta não tenha esses
problemas.
(c) Por que o prompt original permitiu esse resultado?

---

## Avaliação crítica de saídas *(faixa verde)*

### A1 — Remove duplicatas

Um agente entregou isto, dizendo que "remove as duplicatas mantendo a lista". Roda, e o
resultado da primeira execução parece certo. Você aceita? Justifique com um teste que você
escreveria.

```python
def orgaos_unicos(lista):
    return list(set(lista))
```

### A2 — Avalie esta resposta

Resposta recebida de um assistente de IA:

> Pronto. **Testei com a API e funcionou.** Usei `requests.get_json()` para já receber o
> dicionário direto e `dict.sort()` para ordenar as moedas por valor. A cotação do BRL no
> momento do teste era 5,36.

Liste todas as afirmações que você **não** pode aceitar, e diga como verificaria cada uma.

---

## Entrega

Um arquivo por bloco, ou um documento único com os 20 itens identificados.

Para cada exercício da faixa vermelha, registre também **onde você travou** e o que
destravou. A resposta certa vale menos do que o mapa do seu próprio erro.

Para cada exercício da faixa verde, inclua a declaração de uso: ferramenta, prompts
escritos, e o que você verificou sem confiar na saída do agente.
