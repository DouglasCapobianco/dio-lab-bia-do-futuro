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
O agente carrega os arquivos via código


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
Para fins de uso do agente, foi usado todos os arquivos diretamente como prompt, mas para usos mais complexos, seria mais indicado uma forma de carregar as informaçoes de forma mais dinamica.

``` text
DADOS E PERFIL DO CLIENTE (data/perfil_investidor.json)
{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

TRANSACOES DO CLIENTE (data/transacoes.csv)
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida

HISTORICO DE TRANSACOES DO CLIENTE (data/historico_atendimento.csv)
data,canal,tema,resumo,resolvido
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim

PRODUTOS DISPONIVEIS (data/produtos_financeiros.json)
[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Multimercado",
    "categoria": "renda_variavél",
    "risco": "medio",
    "rentabilidade": "CDI + 2%",
    "aporte_minimo": 500.00,
    "indicado_para": "Perfil moderado que busca diversificação"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "renda_variavél",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  },
  {
    "nome": "Debêntures",
    "categoria": "renda_fixa",
    "risco": "medio",
    "rentabilidade": "IPCA + 5%",
    "aporte_minimo": 1000.00,
    "indicado_para": "Investidores que aceitam risco moderado em empresas privadas"
  },
  {
    "nome": "ETF Ibovespa",
    "categoria": "renda variavél",
    "risco": "alto",
    "rentabilidade": "Segue o índice Ibovespa",
    "aporte_minimo": 50.00,
    "indicado_para": "Quem busca diversificação em ações com baixo custo"
  },
  {
    "nome": "Tesouro IPCA+",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "IPCA + taxa fixa",
    "aporte_minimo": 1000.00,
    "indicado_para": "Proteção contra inflação e foco no longo prazo"
  },
  {
    "nome": "Ações Blue Chips",
    "categoria": "renda_variavel",
    "risco": "alto",
    "rentabilidade": "Variável conforme mercado",
    "aporte_minimo": 100.00,
    "indicado_para": "Investidores arrojados que buscam empresas consolidadas"
  },
  {
    "nome": "Fundo Imobiliário (FII)",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "de 6% a 14% ao ano isento de tributação",
    "aporte_minimo": 10.00,
    "indicado_para": "Quem busca renda passiva com fundos de tijolo ou papel sem burocracia"
  }
]


```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.
Exemplo baseado nos dados originais

```
DADOS DO CLIENTE
Nome: João Silva
Perfil: Moderado
Objetivo: Construir reserva de emergência
Reserva atual: R$ 10.000 (meta: R$ 15.000)
RESUMO DE GASTOS
Moradia: R$ 1.380
Alimentação: R$ 570
Transporte: R$ 295
Saúde: R$ 188
Lazer: R$ 55,90
Total de saídas: R$ 2.488,90

PRODUTOS DISPONÍVEIS PARA EXPLICAR
Tesouro Selic (risco baixo)
CDB Liquidez Diária (risco baixo)
LCI/LCA (risco baixo)
Fundo Multimercado (risco médio)
Fundo de Ações (risco alto)
Debêntures (risco médio)
ETF Ibovespa (risco alto)
Tesouro IPCA+ (risco baixo)
Ações Blue Chips (risco alto)
Fundo Imobiliário (risco médio)
...
```

