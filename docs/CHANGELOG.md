# Changelog — 02/10/2026

[CRIADO] Base de dados de portfólio (`dados_portfolio\`) — empresa renomeada para Vitalis, venda e estoque escalados, códigos internos substituídos.
[CRIADO] Parâmetro `PastaDados` e função `fnLerCsv`.
[CRIADO] `fEstoque` ligado diretamente a `dProduto` e `dEstado`.
[CRIADO] `dGlossario` digitado.
[CRIADO] `Meta Share`, `Dimensão de Análise`, `Indicador`.
[CRIADO] 114 medidas em `_Medidas`, com pastas e descrições.
[CRIADO] Tema `MarketIntelligencePharma.json` / `theme.json`.
[CRIADO] Páginas Visão Executiva, Mercado & Share, Produtos, Laboratórios, Canal & Geografia, Estoque & Cobertura, Oportunidades, Diagnóstico, Definições.
[CRIADO] Tooltips Produto, Laboratório, Estoque, Período.
[CRIADO] Drillthrough Produto, Laboratório, Estado.

[ALTERADO] Share — denominador passa a ser o mercado total.
[MOTIVO] A fórmula anterior dividia pela venda dos concorrentes.

[ALTERADO] Crescimento mensal — base passa a ser o período anterior.
[MOTIVO] `% PM` usava o período atual como base e invertia o sinal.

[ALTERADO] Tipagem de valores — lidos como inteiro em centavos e convertidos para decimal fixo.
[MOTIVO] Conversão de texto com ponto decimal em cultura pt-BR.

[OTIMIZADO] `dProduto` — 368.960 → 84.912 linhas; 3 colunas calculadas eliminadas.
[OTIMIZADO] Estoque — 6 leituras do Excel → 1 CSV; ponte e filtros bidirecionais removidos.
[OTIMIZADO] Ranking e Pareto — iteram a coluna do item, não a tabela de produto inteira.

[REMOVIDO] Tabelas `Estoque`, `auxEan`, `auxCrescimento`, `Legenda`, `Preços/Definições`, `Top Apresentações`, tabelas de data automática.
[MOTIVO] Órfãs, duplicadas ou dependentes de PDF.

[REMOVIDO] Página "Página 1".
[MOTIVO] Rascunho de 3.300 px que abria como página inicial.

[REMOVIDO] Página "Produtos que mais crescem".
[MOTIVO] Tabela estática copiada de PDF, sem ligação com o modelo.

[REMOVIDO] Página "Arvore Hierarquica" isolada.
[MOTIVO] Substituída pela árvore da página Diagnóstico, com medida e contexto definidos.

[REMOVIDO] Coluna lateral de 8 slicers e visual `pureVizInfographic`.
[MOTIVO] Cinco filtros globais sincronizados cobrem o uso; o infográfico não agregava leitura.

[REMOVIDO] Medidas `ACUMULADO TESTE`, `Total Acumulado`, `Faturamento Acumulado`.
[MOTIVO] Sem uso em nenhum visual.
