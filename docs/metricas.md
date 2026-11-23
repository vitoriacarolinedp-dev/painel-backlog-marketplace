# Dicionário de métricas

Todas as métricas são calculadas a partir das bases do dia fechado. Os comparativos usam leituras anteriores salvas diariamente.

## Protocolos das plataformas

| Métrica | Definição | Leitura |
|---|---|---|
| Protocolos abertos | Quantidade de protocolos pendentes em cada plataforma, por tipo | Menor é melhor |
| Saldo D-30 | Protocolos de hoje − protocolos de 30 dias atrás | ↓ verde = redução · ↑ vermelho = aumento |
| % do total | Protocolos da plataforma ÷ total de protocolos | Mostra onde o backlog está concentrado |
| Maior tipo | Tipo de protocolo com mais pendências na plataforma | Indica onde atuar primeiro |

Tipos de protocolo: pós-compra, entrega, cancelamento, troca e devolução, pré-compra.

## Chamados internos

| Métrica | Definição | Leitura |
|---|---|---|
| Chamados abertos | Chamados internos em aberto, de todas as plataformas | Menor é melhor |
| Aguardando retorno | Chamados ainda sem retorno da área ou região | Menor é melhor |
| Atualizados | Chamados que já receberam retorno | Maior é melhor |
| Idade | Dias entre a data de criação e a data de corte | — |
| Abertos até 7 dias | Chamados com idade ≤ 7 dias | Entrada recente |
| Acima de 30 dias | Chamados com idade > 30 dias | Acúmulo; menor é melhor |
| Saldo | Valor de hoje − valor da base de comparação | ↓ verde = redução |

Faixas de idade: até 7 dias · 8 a 15 dias · 16 a 30 dias · acima de 30 dias.

Dimensões de análise: plataforma, região, origem (chat, protocolo, e-mail), assunto e área responsável.

## Área responsável

| Métrica | Definição |
|---|---|
| Chamados por área | Chamados atribuídos a cada área pela tabela de-para de tratativas |
| % do total | Chamados da área ÷ total de chamados |
| Variação no dia | Valor de hoje − valor do dia anterior |

Áreas: Logística · Logística/Atendimento · Produção · Atendimento · Planejamento · Cadastro.

## Indicadores dos sellers

Cada plataforma tem seus próprios indicadores. O painel padroniza a leitura em três colunas de comparação (**D-30 · D-7 · Hoje**) e avalia cada valor contra a meta.

| Tipo de meta | Exemplos | Dentro da meta |
|---|---|---|
| Teto (máximo) | Cancelamento, envios com atraso, protocolos ÷ vendas | Valor ≤ meta |
| Piso (mínimo) | Entrega no prazo, avaliação, nota da loja | Valor ≥ meta |
| Qualitativa | Nível da loja | Conforme a escala da plataforma |

A regra de cores está em [`regras.md`](regras.md).
