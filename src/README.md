# Código da Aplicação

Esta pasta contém o código do seu agente financeiro.

## Estrutura Sugerida

```
src/
├── app.py              # Aplicação principal (Streamlit/Gradio)
├── agente.py           # Lógica do agente
├── config.py           # Configurações (API keys, etc.)
└── requirements.txt    # Dependências
```

## Exemplo de requirements.txt

```
streamlit
openai
python-dotenv
```

## Como Rodar

```bash
# Instalar dependências
pip install -r requirements.txt

# Rodar a aplicação
streamlit run app.py
```

---

## Python
´´´
import pandas as pd
import json
import requests
import streamlit as st

# ======== CONFIGURAÇÃO ========
OLLAMA_URL = "http://localhost:11434/api/generate"
MODELO = "gpt-oss"



#Carregar dados
perfil = json.load(open('data/perfil_investidor.json'))
transacoes = pd.read_csv('data/transacoes.csv')
historico = pd.read_csv('data/historico_atendimento.csv')
produtos = json.load(open('data/produtos_financeiros.json'))

# ======== MONTAR CONTEXTO =========
contexto = f"""
CLIENTE: {perfil['nome']}, {perfil['idade']} anos, perfil {perfil['perfil_investidor']}
OBJETIVO: {perfil['objetivo_principal']}
PATRIMÔNIO: R$ {perfil['patrimonio_total']} | RESERVA: R$ {perfil['reserva_emergencia_atual']}

TRANSAÇÕES RECENTES:
{transacoes.to_string(index=False)}

ATENDIMENTOS ANTERIORES:
{historico.to_string(index=False)}

PRODUTOS DISPONÍVEIS:
{json.dumps(produtos, indent=2, ensure_ascii=False)}
"""

# ========  SYSTEM PROMPTS =========
SYSTEM_PROMPT = """Você é  Clara, um agente financeiro inteligente especializado em investimentos.

OBJETIVO: Seu objetivo é ajudar e ensinar sobre o mercado financeiro e investimentos."

REGRAS:
1. Sempre baseie suas respostas nos dados fornecidos e cite a fonte quando possível.
2. Nunca invente informações financeiras.
3. Se não souber algo, admita e indique fontes confiáveis alternativas.
4. Responda unica e exculsivamente a perguntas relacionadas a investimentos e educação financeira.
5. Nunca dê dicas ou recomendações de investimento; limite-se a explicar produtos e cenários.
6. A principal função é ensinar e educar.
7. Auxiliar e educar, mas sempre deixar o cliente tomar a decisão final.
8. Sempre confirme se o cliente entendeu, variando a forma de perguntar.
9. Nunca pedir ou armazenar dados sensíveis ou informações pessoais.
10. Seja transparente e informe quando a resposta for baseada em cenários hipotéticos ou suposições.
11. Mantenha neutralidade, não favoreça produtos ou instituições financeiras específicas.
12. Sempre utilize informações atualizadas em temas que mudam com o tempo, como taxas e legislação.
13. Use linguagem acessível, adaptando explicações ao nível de conhecimento do cliente (iniciante, intermediário ou avançado).
14. Dar prioridade a respostas mais diretas e educativas a não ser que seja pedido por respostas técnicas.
15. Se o cliente apenas cumprimentar ou não fizer uma pergunta de investimento, apresente-se de forma amigável e explique brevemente sua função como educadora financeira
"""


# ======== CHAMAR OLLAMA ========
def perguntar(msg):
    prompt = f"""
    {SYSTEM_PROMPT}
    
    CONTEXTO DO CLIENTE:
    {contexto}
    
    Pergunta: {msg}"""
    
    r = requests.post(OLLAMA_URL, json={"model": MODELO, "prompt": prompt, "stream": False})
    resposta = r.json()
    print(resposta)  # debug: veja no terminal o que o Ollama devolve
    return resposta.get("response", "⚠️ Erro: chave 'response' não encontrada")



# ======== INTERFACE =========
st.title("💡 Clara, Sua Assistente e Educadora de Investimentos")

if pergunta := st.chat_input("Sua dúvida sobre investimentos..."):
    st.chat_message("user").write(pergunta)
    with st.spinner("..."):
        st.chat_message("assistant").write(perguntar(pergunta))



#streamlit run .\src\app.py
´´´


