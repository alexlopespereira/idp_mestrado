# Lista de exercícios — Introdução à Lógica de Programação (Python)

Mestrado em Administração Pública com ênfase em IA

---

## Como usar esta lista

São 21 exercícios em sete habilidades. Nem todos pedem código: vários pedem que você
**leia**, **especifique**, **teste** ou **critique** — que é boa parte do trabalho real de
quem programa.

**Faixa vermelha: sem agente de IA.** Você resolve sozinho, no papel ou no editor. Errar
aqui é o objetivo, não o acidente. Um exercício que você acerta de primeira não ensinou
nada.

**Faixa verde: com agente, e com declaração de uso.** Ao entregar, diga qual ferramenta
usou, quais prompts escreveu e o que você verificou por conta própria.

**Antes de rodar o código, escreva a saída que você espera.** Essa previsão é metade do
exercício. Rodar primeiro e ler o resultado depois transforma o exercício num espetáculo
que você assiste em vez de um problema que você resolve.

**Quando travar**, use o tutor socrático da disciplina: cole o enunciado e a sua tentativa.
Ele não vai te dar a resposta — vai te fazer perguntas até você achar. Se você quiser
apenas a solução, ela não vai servir para a prova nem para o trabalho.

| # | Habilidade | Faixa | Tempo |
|---|---|---|---|
| 1A–1C | Leitura e compreensão de código | vermelha | 5–10 min |
| 2A–2C | Decomposição de problemas | vermelha | 10–15 min |
| 3A–3C | Testes | vermelha | 10 min |
| 4A–4C | Depuração | vermelha | 10–15 min |
| 5A–5C | Especificação de requisitos | vermelha | 10 min |
| 6A–6C | Prompting | verde | 10–15 min |
| 7A–7C | Avaliação crítica de saídas | verde | 15 min |

---

## 1. Leitura e compreensão de código *(faixa vermelha)*

### 1A — O total que encolheu

Sem rodar, diga qual é a saída deste programa. Depois diga o que o autor provavelmente
queria que ele fizesse.

```python
valores = [1200, 850, 3000, 470]
total = 0
for v in valores:
    if v > 1000:
        total = v
print(total)
```

### 1B — O que essa função faz?

(a) Descreva em uma frase o que esta função faz. (b) Dê a ela um nome melhor. (c) Diga o
que ela retorna para a chamada abaixo.

```python
def f(d):
    r = []
    for k in d:
        if d[k] == 0:
            r.append(k)
    return r

f({"Saúde": 0, "Educação": 12, "Cultura": 0, "Esporte": 3})
```

### 1C — A cópia que não era cópia

Sem rodar: qual é a saída? Justifique.

```python
def aplicar_desconto(itens, percentual):
    for item in itens:
        item["valor"] = item["valor"] * (1 - percentual)
    return itens

orcamento = [{"nome": "Papel", "valor": 100.0}, {"nome": "Toner", "valor": 400.0}]
copia = orcamento
aplicar_desconto(copia, 0.10)
print(orcamento[0]["valor"])
```

---

## 2. Decomposição de problemas *(faixa vermelha)*

### 2A — Da frase às funções

Pedido recebido: *"Preciso de um relatório mensal das diárias pagas pelo órgão, com o
total por servidor e um aviso quando alguém passar de 10 diárias no mês."*

Não escreva código. Entregue: (a) a lista de subproblemas na ordem de execução; (b) para
cada um que virar função, o nome, o que entra e o que sai. Corpo das funções: apenas
`pass`.

### 2B — Quebrar o monólito

Esta função faz quatro coisas. Identifique-as e proponha a divisão (nomes e assinaturas,
sem corpo). Não corrija bugs — só reorganize.

```python
def relatorio(caminho):
    linhas = open(caminho).readlines()
    total = 0
    por_orgao = {}
    for linha in linhas[1:]:
        partes = linha.strip().split(";")
        orgao = partes[0].strip().upper()
        valor = float(partes[2].replace(".", "").replace(",", "."))
        if valor < 0:
            continue
        total = total + valor
        if orgao in por_orgao:
            por_orgao[orgao] = por_orgao[orgao] + valor
        else:
            por_orgao[orgao] = valor
    print("Total:", total)
    for o in sorted(por_orgao, key=por_orgao.get, reverse=True)[:5]:
        print(o, por_orgao[o])
```

### 2C — A chave escondida

Você precisa conciliar duas listas: empenhos do sistema financeiro e notas fiscais
recebidas, casando pelo CNPJ do fornecedor. No sistema financeiro o CNPJ vem como
`"12.345.678/0001-90"`; nas notas, como `"12345678000190"`; e em alguns registros antigos
há espaços sobrando.

Descreva a decomposição em subproblemas **antes** de pensar no laço de casamento.

---

## 3. Testes *(faixa vermelha)*

### 3A — Testes antes do código

Especificação: `calcular_multa(dias_atraso, valor)` devolve a multa por atraso, de 0,33%
do valor por dia, limitada a 20% do valor.

Escreva **oito** casos de teste no formato `entrada → saída esperada`. Não escreva a
função. Justifique cada caso em até cinco palavras.

### 3B — Testes verdes, código errado

Este código passa nos três testes abaixo. Encontre uma entrada em que ele dá a resposta
errada e explique por quê.

```python
def maior_valor(valores):
    maior = 0
    for v in valores:
        if v > maior:
            maior = v
    return maior

# maior_valor([1, 5, 3]) == 5   ✓
# maior_valor([10]) == 10       ✓
# maior_valor([2, 2]) == 2      ✓
```

### 3C — O teste que falha sem ter bug

A função abaixo está correta segundo a especificação (somar valores em reais). O teste
falha. Quem está errado, o código ou o teste? Justifique e proponha o conserto.

```python
def somar(valores):
    return sum(valores)

assert somar([0.1, 0.2]) == 0.3   # AssertionError
```

---

## 4. Depuração *(faixa vermelha)*

### 4A — A média que fica pequena no fim

A função deveria devolver as médias móveis de janela 3. Com `[10, 20, 30, 40]` esperava-se
`[20.0, 30.0]`, mas sai `[20.0, 30.0, 23.33, 13.33]`.

Localize a causa. **Não conserte ainda** — descreva o defeito em uma frase.

```python
def media_movel(valores, janela):
    medias = []
    for i in range(len(valores)):
        pedaco = valores[i:i+janela]
        medias.append(sum(pedaco) / janela)
    return medias
```

### 4B — O erro não está na linha do erro

O traceback aponta a linha 6. O defeito não está lá. Onde está?

```python
def total_do_orgao(registros, orgao):
    total = 0
    for r in registros:
        if r["orgao"] == orgao:
            total = total + r["valor"]
    return total

registros = []
for linha in open("empenhos.csv").readlines()[1:]:
    o, v = linha.strip().split(";")
    registros.append({"orgao": o, "valor": v})

print(total_do_orgao(registros, "MGI"))
# TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

### 4C — O histórico que lembra do processo anterior

Cada chamada deveria começar um histórico novo. Rode mentalmente e explique a saída.

```python
def registrar_andamento(protocolo, historico=[]):
    historico.append(protocolo)
    return historico

print(registrar_andamento("2026-001"))
print(registrar_andamento("2026-002"))
```

---

## 5. Especificação de requisitos *(faixa vermelha)*

### 5A — Do pedido do gabinete ao requisito testável

O secretário pediu: *"Quero uma lista dos processos que estão parados."*

Transforme isso em uma especificação que dois programadores diferentes implementariam de
forma equivalente. Entregue: definição operacional de "parado"; fonte e campos usados;
formato exato da saída; três critérios de aceite; comportamento para dados faltantes.

### 5B — Caça à ambiguidade

Requisito recebido: *"Calcular o tempo médio de tramitação dos processos em dias úteis,
por unidade."*

Liste **cinco** ambiguidades e escreva as três perguntas que você faria ao demandante
antes de escrever uma linha de código.

### 5C — O contrato da função

Escreva apenas a assinatura e a docstring de `dias_uteis(data_inicio, data_fim)`. Sem
corpo. A docstring deve dizer: o que entra (tipo e formato), o que sai, e o que acontece
em cada uma destas situações: fim antes do início; datas iguais; data em formato inválido;
feriados.

---

## 6. Prompting *(faixa verde — com agente, com declaração de uso)*

### 6A — Reescrever o prompt ruim

Este prompt foi usado: *"faz um script pra ler a planilha e me dar o total"*.

Reescreva-o. Depois rode o seu e o original no agente e compare as duas saídas. Entregue:
o prompt novo, e uma frase dizendo qual diferença no prompt causou qual diferença no
código.

### 6B — Engenharia reversa da falha

Um colega usou o prompt *"escreva uma função Python que calcula a média mensal de
atendimentos a partir de uma lista de dicionários"*. O código veio funcionando, mas
quebrou em produção com meses sem nenhum atendimento.

**Não conserte o código.** Aponte o que faltava **no prompt** e reescreva o prompt.

### 6C — Fatiar em vez de despejar

Tarefa: *conciliar empenhos e notas fiscais por CNPJ, apontar divergências acima de R$ 100
e gerar uma planilha de exceções.*

Em vez de um prompt único, escreva a **sequência de 4 a 6 prompts** que você usaria, e diga
o que você verifica entre cada um antes de seguir para o próximo.

---

## 7. Avaliação crítica de saídas *(faixa verde)*

### 7A — Roda, parece certo, e não é

Um agente entregou este código para "devolver os N maiores registros por valor". Ele roda e
o resultado está correto na primeira chamada. Você aceita? Justifique com um teste que você
escreveria.

```python
def top_n_por_valor(registros, n):
    registros.sort(key=lambda r: r["valor"], reverse=True)
    return registros[:n]
```

### 7B — A verificação que nunca aconteceu

Resposta recebida de um assistente de IA:

> Criei a função `consolidar_empenhos()` conforme solicitado. **Testei com a sua planilha e
> o total bateu: R$ 4.328.115,20.** A função usa `pandas.read_dbf()` para ler o arquivo
> legado e trata automaticamente os valores no formato brasileiro.

Liste todas as afirmações desta resposta que você **não** pode aceitar, e diga como
verificaria cada uma.

### 7C — Escolher entre duas erradas

Pedimos ao agente uma função de dias úteis entre duas datas e recebemos duas versões.
(a) Escolha uma e justifique com critérios explícitos. (b) Encontre a falha que **as duas**
compartilham.

```python
# Versão 1
from datetime import timedelta
def dias_uteis(inicio, fim):
    dias = 0
    d = inicio
    while d < fim:
        if d.weekday() < 5:
            dias += 1
        d += timedelta(days=1)
    return dias

# Versão 2
import pandas as pd
def dias_uteis(inicio, fim):
    return len(pd.bdate_range(inicio, fim))
```

---

## Entrega

Um arquivo por bloco de habilidade, ou um documento único com os 21 itens numerados.

Para cada exercício da faixa vermelha, registre também **onde você travou** e o que
destravou — a resposta certa vale menos do que o mapa do seu próprio erro.

Para cada exercício da faixa verde, inclua a declaração de uso: ferramenta, prompts
escritos, e o que você verificou sem confiar na saída do agente.
