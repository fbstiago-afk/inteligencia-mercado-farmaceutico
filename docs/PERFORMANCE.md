# Performance

## O que foi medido

Não há medição "antes" comparável: o projeto original não atualiza (fontes em `D:\`) e o Performance Analyzer não foi executado em nenhuma das duas versões. Os números abaixo são estruturais, mais a observação do comportamento da versão nova no Desktop.

| Item | Antes | Depois |
|---|---|---|
| Linhas em dProduto | 368.960 | 84.912 (−77%) |
| Colunas de texto em dProduto | 17, com espaços à direita | 14, aparadas |
| Colunas calculadas com transição de contexto | 3 sobre 369 mil linhas | 0 |
| Relacionamentos bidirecionais | 2 | 0 |
| Tabelas de data automática | 2 | 0 |
| Colunas no fato | 9 (data + período redundantes) | 8 (chave de mês inteira) |
| Leitura do Excel de estoque | 6 vezes | 0 (CSV preparado) |
| Atualização completa | Não executa | ~2 minutos (11,5 milhões de linhas) |

## Observado na versão nova

- Uma consulta com as 26 medidas mais pesadas (Pareto, itens para 80%, HTML de resumo, oportunidade, ranking e tooltips) no contexto padrão respondeu em poucos segundos.
- Todas as páginas renderizaram no Desktop; os tempos não foram cronometrados. Oportunidades foi visivelmente a mais lenta (ranking de potencial sobre ~9 mil produtos).

## Pontos de atenção

- `Produtos p/ 80% da Venda` usa `WINDOW` sobre os produtos com venda; é a medida mais cara do modelo.
- As tabelas de produto usam filtro Top N para não calcular ranking e Pareto para milhares de linhas.
- `FORMAT` aparece só nas medidas de texto/HTML; medidas numéricas usam formato do modelo.

## Próximo passo

Rodar o Performance Analyzer página a página e registrar aqui os tempos de consulta DAX por visual.
