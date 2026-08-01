# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização da Clara |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar e entender o que deve ser ensinado dependendo do perfil do usuario. |
| `produtos_financeiros.json` | JSON | Conhecer os produtos que podem ser apresentados e ensinados ao usuario  |
| `transacoes.csv` | CSV | Analisar padrão de gastos para aprender melhor sobre o usuario |

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Realizei a adição de alguns produtos pra aumentar o conhecimento da Clara e atualizei algumas informações como o rendimento atual do CDB.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

```python
import pandas as pd
import json

historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
    perfil = json.load(f)

with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
    produtos = json.load(f)

```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

[Sua descrição aqui]

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
