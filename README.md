# 💰 Gabi — Monitora de Finanças Pessoais

Agente financeiro inteligente e proativo que monitora gastos em tempo real, emite alertas preventivos de orçamento e protege as metas financeiras do usuário. Desenvolvido como solução para o desafio **Lab Agente Financeiro** da DIO.

---

## O Problema

Muitas pessoas sofrem com "vazamento de orçamento": pequenos gastos diários que, somados, comprometem o planejamento mensal sem que o usuário perceba a tempo. A Gabi resolve isso com **monitoramento proativo**, não apenas relatórios retroativos.

---

## A Solução

A Gabi é uma assistente financeira que age como uma amiga conselheira: não julga o usuário por gastar, mas avisa com gentileza quando ele está saindo do caminho que ele mesmo traçou.

**Funcionalidades principais:**
- Alerta automático ao atingir 80% do limite de uma categoria de gastos
- Análise de transações em tempo real com categorização inteligente
- Conexão entre gastos atuais e metas de longo prazo (ex: reserva de emergência)
- Tratamento de edge cases: recusa de pagamentos, investimentos fora de escopo e compras parceladas

---

## Arquitetura

```
Extrato (CSV) + Perfil (JSON) + Limites (JSON)
        ↓
  Backend Python (Pandas)
  - Soma gastos por categoria
  - Calcula % de uso do orçamento
  - Identifica última transação
        ↓
  Contexto Dinâmico injetado no prompt
        ↓
  LLM (Ollama / llama3)
        ↓
  Interface Streamlit (Chat)
```

> **Princípio de segurança:** cálculos matemáticos são feitos pelo Python — nunca pelo LLM — para evitar alucinações numéricas.

---

## Base de Conhecimento

| Arquivo | Descrição |
|---|---|
| `data/extrato_transacoes.csv` | Histórico de gastos do mês corrente |
| `data/perfil_clientes.json` | Perfil, renda e metas do usuário (João Silva) |
| `data/limites_categorias.json` | Tetos de gastos por categoria e thresholds de alerta |
| `data/historico_atendimento.csv` | Atendimentos anteriores (evita repetição de explicações) |

---

## Como Rodar

```bash
# 1. Instalar dependências
pip install streamlit pandas requests

# 2. Garantir que o Ollama está rodando localmente
ollama run llama3

# 3. Iniciar a aplicação
streamlit run src/app.py
```

---

## Estrutura do Projeto

```
├── data/
│   ├── extrato_transacoes.csv
│   ├── perfil_clientes.json
│   ├── limites_categorias.json
│   └── historico_atendimento.csv
├── docs/
│   ├── 01-documentacao-agente.md   # Caso de uso, persona e arquitetura
│   ├── 02-base-conhecimento.md     # Estratégia de dados e contexto
│   ├── 03-prompts.md               # System prompt, cenários e edge cases
│   ├── 04-metricas.md              # Testes e avaliação de qualidade
│   └── 05-pitch.md                 # Roteiro do pitch
└── src/
    └── app.py                      # Aplicação Streamlit + integração Ollama
```

---

## Exemplo de Interação

> **Contexto:** João gastou R$ 150 no Restaurante Gourmet. Lazer está em 83% do limite.

**Gabi:**
> Oi! Sou a Gabi. Notei uma nova transação de R$ 150,00 no "Restaurante Gourmet" e vim te atualizar sobre seu orçamento.
> Com esse valor, você já usou 83% do seu limite de Lazer para este mês. Faltam só R$ 250,00 para atingir o teto! Vamos segurar um pouco as saídas nos próximos dias para garantir que a gente consiga poupar aqueles R$ 625,00 para a sua Reserva de Emergência?

---

## Métricas de Qualidade

| Métrica | Critério |
|---|---|
| **Assertividade** | Lê corretamente os dados calculados pelo Python |
| **Segurança** | Recusa pagamentos, transferências e recomendações de investimento |
| **Coerência** | Resposta amigável, não punitiva, conectada às metas do usuário |

---

## Stack

`Python` · `Streamlit` · `Pandas` · `Ollama (llama3)` · `REST API`
