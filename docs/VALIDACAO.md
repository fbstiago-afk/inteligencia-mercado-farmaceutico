# Validação

Feita com o modelo novo aberto no Power BI Desktop, por consulta DAX, contra os totais calculados direto dos arquivos (arquivo de controle).

| Teste | Resultado |
|---|---|
| Linhas carregadas | fVendas 11.495.254 · dProduto 84.912 · fEstoque 19.707 — iguais à fonte |
| Venda Vitalis total | R$ 2.366.487.796,51 — igual ao controle |
| Mercado total | R$ 123.013.935.290,67 — igual ao controle |
| Quantidade Vitalis | 108.840.006 — igual ao controle |
| Venda, outros e quantidade por UF × tipo de farmácia (BA, ES, RJ × 3 tipos) | 9 de 9 células iguais ao centavo |
| Estoque total | 11.498.821 = BA 424.397 + ES 3.062.529 + RJ 8.011.895 |
| Share = Venda ÷ (Venda + Outros) | Conferido em todas as células; ex.: ES Assoc./Franq. 14,95% |
| Δ Share em p.p. | MAT Fev/23, área de atuação: 6,02% − 7,20% = −1,18 p.p. |
| Ranking independente das colunas do visual | Top 6 produtos com posições 1 a 6 mesmo com Categoria na tabela |
| 114 medidas | Todas avaliadas sem erro no contexto padrão |
| Páginas | 9 visíveis + 4 tooltips + 3 drillthroughs abertos no Desktop; tooltip HTML de produto conferido por hover; opção de drill-through presente |

Os valores acima já estão na escala do portfólio (venda e estoque da empresa multiplicados por um fator fixo); o mercado dos outros distribuidores não foi alterado.

Não validado: tempos no Performance Analyzer; navegação por drillthrough até o destino; comportamento publicado no serviço.
