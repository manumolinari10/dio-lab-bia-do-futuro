# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Para que serve na Gabi? |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Evitar repetições de explicações já dadas (ex: João já sabe o que é CDB). |
| `perfil_cliente.json` | JSON | Extração de renda (R$ 5k) e metas (Reserva de Emergência). |
| `limites_categorias.json` | JSON | (Novo) Define os tetos de gastos para Aluguel, Lazer e Alimentação. |
| `extrato_transacoes.csv` | CSV | (Dinâmico) Base para o agente calcular o consumo do orçamento em tempo real. |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

Expansão para Alertas Inteligentes:
Os dados originais foram expandidos para incluir "Thresholds de Alerta". Não basta saber o saldo; o agente agora possui uma camada lógica que define que, ao atingir 80% de um limite, uma notificação proativa deve ser gerada. Além disso, as metas de longo prazo (Apartamento) foram convertidas em parcelas mensais teóricas para monitorar se o gasto atual está "roubando" dinheiro do futuro.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos são carregados via Pandas (para os CSVs) e json.load no início da aplicação Streamlit. Eles ficam armazenados no session_state para que o agente tenha acesso instantâneo sem precisar ler o disco a cada mensagem.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados não são jogados "crus" no prompt. Existe uma função de pré-processamento que calcula:
- Soma total de gastos do mês atual.
- % de uso do limite de cada categoria.
- Distância para a meta da reserva de emergência.
Esses indicadores calculados são injetados no Contexto Dinâmico do prompt, permitindo que o LLM apenas interprete os números e gere o alerta em linguagem natural.
---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
### CONTEXTO DO USUÁRIO (JOÃO SILVA) ###
- Renda Líquida: R$ 5.000,00
- Meta Prioritária: Reserva de Emergência (Faltam R$ 5.000,00 / Prazo Jun-2026)
- Economia Mensal Necessária: R$ 625,00

### STATUS ATUAL DE GASTOS (MARÇO/2026) ###
1. Categoria LAZER:
   - Gasto: R$ 1.250,00 | Limite: R$ 1.500,00 (Utilizado: 83.3%)
   - STATUS: ALERTA EMITIDO (Threshold 80% ultrapassado)

2. Categoria ALIMENTAÇÃO:
   - Gasto: R$ 800,00 | Limite: R$ 1.200,00 (Utilizado: 66%)
   - STATUS: OK

### ÚLTIMA TRANSAÇÃO IDENTIFICADA ###
- Data: 23/03/2026 | Valor: R$ 150,00 | Local: "Restaurante Gourmet" | Categoria: Lazer
```
