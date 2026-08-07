# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |


---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Produto compatível com o perfil do cliente
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que só trata de finanças
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Agente admite não ter essa informação
- **Resultado:** [x] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- Tive respostas satisfatórias em todas a perguntas.
- Tende a dar respostas simples e oferecer ajuda em outros aspectos da pergunta.
- Oferece fontes para eu buscar mais informações sobre mesmo que ela não tenha a informação.
- Linguagem agradavél.
- Esta sempre indicando que quer explicar ou ensinar.
- Quando não tinha a informação, informou que não sabia sobre e indicou que procurasse em sites especificos.
- Quando pressionada a indicar um investimento se saiu bem com a frase "lembrando que não faço recomendações específicas", confirmando sobre seus objetivos didaticos.
- Em uma pergunta totalmente fora do assunto, ignorou completamento a pergunta e ressaltou sobre sua expecialidade.

**O que pode melhorar:**
- Criou uma expressão "pó de travesseiro" que eu não sei de onde foi retirada, parece uma leve alucinação, mas não em questão a dados, apenas na gramatica.
- Pareceu mecânica quando me respondeu "nos dados que você forneceu", ela não deveria me ver como quem a configurou e sim como um cliente.

---
