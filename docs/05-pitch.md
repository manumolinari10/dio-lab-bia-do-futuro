# Pitch (3 minutos)

> [!TIP]
> Você pode usar alguns slides pra apoiar no seu Pitch e mostrar sua solução na prática.
 
## Roteiro Sugerido

### 1. O Problema (30 seg)
> Qual dor do cliente você resolve?

Você já chegou no fim do mês sem entender onde foi parar o seu dinheiro? Esse problema tem nome: vazamento de orçamento. São pequenos gastos no iFood, no cinema, no restaurante, que individualmente parecem inofensivos — mas que somados comprometem o planejamento financeiro inteiro, sem que a pessoa perceba antes que seja tarde demais. Os aplicativos de banco mostram o extrato, mas ninguém te avisa enquanto você ainda pode agir.

### 2. A Solução (1 min)
> Como seu agente resolve esse problema?

Apresento a Gabi, uma assistente financeira inteligente que age de forma proativa — não reativa.

A Gabi monitora as transações do usuário em tempo real, compara cada gasto com os limites definidos por categoria (alimentação, lazer, transporte) e emite alertas antes que o orçamento estoure. Quando você atinge 80% do seu limite de lazer, ela te avisa com uma mensagem amigável e ainda conecta aquele gasto com a sua meta de longo prazo — como a reserva de emergência.

A arquitetura foi pensada para ser confiável: os cálculos matemáticos são feitos em Python com Pandas, e o LLM entra apenas para transformar esses números em linguagem natural, acessível e humana. Isso elimina o risco de alucinações financeiras — o agente nunca inventa um saldo ou um limite.

A Gabi também sabe o que não é papel dela: ela recusa educadamente pedidos de pagamento, transferências ou recomendações de investimento — mantendo a segurança e a transparência em primeiro lugar.

### 3. Demonstração (1 min)
> Mostre o agente funcionando (pode ser gravação de tela)

Na demonstração, será exibida a interface em Streamlit rodando localmente com o modelo llama3 via Ollama.
Fluxo mostrado:

1. O contexto dinâmico é gerado automaticamente a partir dos arquivos CSV e JSON — mostrando o perfil do João, os gastos do mês e os alertas calculados pelo Python
2. A Gabi inicia a conversa com um alerta proativo: a categoria Lazer atingiu 83% do limite após uma transação no Restaurante Gourmet
3. O usuário pergunta se pode gastar mais R$ 120 num rodízio — a Gabi consulta o saldo restante e responde de forma consultiva
4. O usuário tenta pedir um pagamento de boleto — a Gabi recusa com clareza e gentileza, sem "travar"
5. O usuário pergunta sobre a previsão do tempo — a Gabi redireciona para o seu propósito de forma natural

### 4. Diferencial e Impacto (30 seg)
> Por que essa solução é inovadora e qual é o impacto dela na sociedade?

O diferencial da Gabi não é a tecnologia em si — é o posicionamento. Ela não é mais um painel de controle financeiro. Ela é uma presença ativa, como uma amiga que entende de dinheiro e que te avisa no momento certo, com a linguagem certa.

O impacto é direto: pessoas que hoje não têm disciplina para abrir planilhas ou conferir extratos diariamente passam a ter um acompanhamento contínuo, acessível e sem julgamento. Isso democratiza o planejamento financeiro e aproxima as pessoas das suas próprias metas — não no fim do mês, mas enquanto ainda dá tempo de mudar.

---

## Checklist do Pitch

- [X] Duração máxima de 3 minutos
- [X] Problema claramente definido
- [X] Solução demonstrada na prática
- [X] Diferencial explicado
- [ ] Áudio e vídeo com boa qualidade

---

## Link do Vídeo

> Cole aqui o link do seu pitch (YouTube, Loom, Google Drive, etc.)

[Link do vídeo]
