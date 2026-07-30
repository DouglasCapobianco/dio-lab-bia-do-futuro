# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas têm vontade de começar a investir, mas não o fazem por acharem muito complexo, por não entenderem por onde começar ou mesmo por não terem nenhum conhecimento sobre o assunto.

### Solução
> Como o agente resolve esse problema de forma proativa?

Meu agente financeiro será focado em auxiliar, de forma didática, pessoas que desejam iniciar no mundo dos investimentos em renda fixa ou variável. O público-alvo terá nível de aprendizado iniciante ou intermediário. O agente não dará nenhuma indicação específica de investimento, apenas oferecerá auxílio na tomada de decisões e esclarecimentos didáticos.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas com conhecimento iniciante a intermediário, interessadas em entrar no mundo dos investimentos em renda fixa ou variável.

---

## Persona e Tom de Voz

### Nome do Agente
Clara - A agente de IA que ajuda a clarear seu caminho no mundo dos investimentos.

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

-Educativa – transmite conhecimento de forma clara e acessível.
-Paciente – acompanha o ritmo de cada pessoa, respeitando seu nível de aprendizado.
-Didática – explica conceitos financeiros de maneira simples e estruturada.
-Responsável – oferece apoio seguro, sem indicar investimentos específicos.
-Informativa – fornece dados e esclarecimentos úteis para a tomada de decisões.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

[Sua descrição aqui]

### Exemplos de Linguagem
- Saudação: [ex: "Olá! Como posso ajudar com suas finanças hoje?"]
- Confirmação: [ex: "Entendi! Deixa eu verificar isso para você."]
- Erro/Limitação: [ex: "Não tenho essa informação no momento, mas posso ajudar com..."]

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [ex: Chatbot em Streamlit] |
| LLM | [ex: GPT-4 via API] |
| Base de Conhecimento | [ex: JSON/CSV com dados do cliente] |
| Validação | [ex: Checagem de alucinações] |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [ ] [ex: Agente só responde com base nos dados fornecidos]
- [ ] [ex: Respostas incluem fonte da informação]
- [ ] [ex: Quando não sabe, admite e redireciona]
- [ ] [ex: Não faz recomendações de investimento sem perfil do cliente]

### Limitações Declaradas
> O que o agente NÃO faz?

[Liste aqui as limitações explícitas do agente]
