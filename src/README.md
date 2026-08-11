# 🤖 Clara — Agente Financeiro Inteligente

Assistente virtual financeiro construído com IA Generativa, capaz de antecipar necessidades, personalizar sugestões e apoiar decisões financeiras do cliente de forma consultiva e segura (anti-alucinação).

## Stack

- **LLM:** Ollama (modelo local)
- **Interface:** Streamlit
- **Base de conhecimento:** dados mockados (transações, histórico de atendimento, perfil do investidor, produtos financeiros)

## Arquitetura

```
Usuário
   │
   ▼
Interface (Streamlit)
   │  pergunta do cliente
   ▼
Clara (orquestração)
   │  monta o prompt com contexto
   ├──► Base de conhecimento (data/)
   │      transações, histórico de atendimento,
   │      perfil do investidor, produtos financeiros
   │
   ▼
Ollama (LLM local)
   │  gera resposta com base no contexto
   ▼
Camada de segurança
   │  valida a resposta contra os dados reais
   │  (evita alucinação / recomendação indevida)
   ▼
Resposta final ao usuário
```

**Fluxo:** a Clara recebe a pergunta do cliente pela interface, busca o contexto relevante na base de conhecimento (perfil, histórico e produtos) e monta um prompt com essas informações. O Ollama gera a resposta localmente, que passa por uma checagem de consistência com os dados antes de ser exibida — garantindo que a Clara só afirme o que pode comprovar na base.

## Estrutura do repositório

```
├── data/     # Dados mockados usados pelo agente (CSV/JSON)
├── docs/     # Documentação: caso de uso, base de conhecimento, prompts, métricas e pitch
├── src/      # Código da aplicação (app Streamlit + integração com Ollama)
├── assets/   # Imagens e diagramas
└── examples/ # Referências de implementação
```

## Como executar

```bash
# instalar dependências
pip install -r requirements.txt

# ter o Ollama rodando localmente com o modelo desejado
ollama pull <nome-do-modelo>

# iniciar a aplicação
streamlit run src/app.py
```

## Documentação

Os detalhes de arquitetura, prompts, base de conhecimento e métricas de avaliação estão na pasta [`docs/`](./docs).

---
Projeto desenvolvido a partir do lab **Agente Financeiro Inteligente com IA Generativa** da Digital Innovation One.
# Passo a Passo de Execução

## Setup do Ollama

```bash
1. Instalar Ollama (ollama.com)
2. Baixar um modelo leve
ollama pull gpt-oss

3. Testar se funciona
ollama run gpt-oss "Olá!"

## Código Completo

Todo o código-fonte está no arquivo `app.py`.


## Como Rodar

# 1. Instalar dependências  
pip install streamlit pandas requests  

# 2. Garantir que Ollama está rodando  
ollama serve  

# 3. Rodar o app  
streamlit run .\src\app.py

```
## Evidencia de Execução
<img width="874" height="576" alt="image" src="https://github.com/user-attachments/assets/96151817-f534-4bca-91ba-d9b400486f4c" />

##Pitch
Link: https://youtu.be/0ZlUpJacJbI

