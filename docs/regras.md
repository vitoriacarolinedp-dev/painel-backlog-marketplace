# Regras de negócio, alertas e validações

## 1. Base de comparação

- O painel usa sempre o **dia fechado**, para não misturar leituras parciais.
- Cada leitura diária é salva e vira a base de comparação das leituras seguintes, formando uma série histórica.
- Comparativos padrão: **30 dias** (tendência), **7 dias** (semana) e **dia anterior** (variação no dia, na visão por área).

## 2. Cores pela meta

As metas ficam em um **bloco de dados JSON separado da lógica** (`<script type="application/json" id="metas">` no `index.html`). Cada indicador é um registro:

```json
["Protocolos / vendas", "≤ 1%", "teto", "p2", [0.0144, 0.02, 0.0199]]
```

| Posição | Conteúdo |
|---|---|
| 1 | Nome do indicador |
| 2 | Meta em texto, com operador (`≤`, `<`, `≥`, `>`) |
| 3 | Tipo: `teto` (taxas, menor é melhor), `piso` (notas e prazos, maior é melhor) ou `txt` (escala qualitativa) |
| 4 | Formato de exibição (`p2` = percentual com 2 casas, `n1` = número com 1 casa, `h` = horas) |
| 5 | Valores de D-30, D-7 e hoje |

Uma única função (`classifica`) interpreta o operador e o valor da meta e devolve a cor. **Para revisar uma meta numérica, basta alterar o texto da meta no JSON; o código não muda.**

| Cor | Regra |
|---|---|
| 🟢 Verde | Dentro da meta |
| 🟡 Amarelo | Dentro da meta, mas a até 1 ponto do limite |
| 🔴 Vermelho | Fora da meta |

Indicadores qualitativos (`txt`), como o nível da loja, usam uma escala de status definida no código: Verde e Excelente em verde, Bom e Amarelo em amarelo, demais em vermelho.

Nas colunas de saldo, a cor mostra a direção: **verde** quando o número melhora e **vermelho** quando piora, conforme o tipo de métrica.

## 3. Alertas gerenciais

Cada alerta tem um nível de prioridade e a área responsável pela ação.

| Nível | Quando é gerado | Exemplo |
|---|---|---|
| **Crítico** | Indicador muito acima ou abaixo da meta, com risco imediato | Cancelamento 8 vezes acima da meta |
| **Atenção** | Indicador fora da meta ou acúmulo relevante de backlog | Mais de 20% dos chamados acima de 30 dias |
| **Positivo** | Melhora consistente no período | Backlog caiu em 30 dias |

Formato de cada alerta: **o que aconteceu** · **o número que sustenta** · **→ quem precisa agir**.

## 4. Atribuição de área responsável

Cada chamado interno recebe uma área a partir da tratativa pendente, por meio de uma tabela de-para:

| Tratativa | Área |
|---|---|
| Confirmar coleta · Interromper entrega · Realizar entrega | Logística |
| Confirmar entrega · Confirmar troca | Logística/Atendimento |
| Liberar produção · Produzir e liberar envio · Liberar pedido | Produção |
| Em análise | Atendimento |
| Programar pedido | Planejamento |
| Cancelar pedido | Cadastro |

## 5. Validações

Antes de publicar a leitura do dia:

- [ ] **Totais:** o total de cada visão fecha com a soma das partes.
- [ ] **Fonte x canais:** o total informado pela fonte bate com a soma dos tipos de protocolo. Divergências são sinalizadas.
- [ ] **Dados ausentes:** a plataforma sem atualização no dia mantém a última leitura disponível e fica sinalizada.
- [ ] **Datas:** a data de corte é conferida antes de qualquer comparação histórica.
- [ ] **Premissas:** mudanças de estrutura na fonte (novos tipos, colunas renomeadas) são revisadas antes de comparar.

## 6. Leitura do dia

O texto de leitura de cada plataforma é montado a partir dos próprios dados: o que subiu, o que caiu, onde está o maior volume e qual área concentra os chamados. Assim, o texto acompanha os números e não depende de digitação manual.
