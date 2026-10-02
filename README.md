# Inteligência de Mercado Farmacêutico

Dashboard em Power BI que cruza as vendas de uma distribuidora farmacêutica com dados de auditoria de mercado. Mostra participação, ganho e perda de share, oportunidades por produto e laboratório e alinhamento do estoque.

Projeto de portfólio. O nome da empresa é fictício (**Vitalis**) e os valores de venda e estoque foram escalados para preservar a confidencialidade.

## O problema

A distribuidora acompanhava o faturamento todo mês, mas o número sozinho não dizia se o resultado era bom. O painel responde:

- Qual o tamanho do mercado e quanto dele é nosso?
- Estamos ganhando ou perdendo espaço, e onde?
- Quais produtos e laboratórios concentram a maior oportunidade?
- O estoque acompanha o que vende?

## O que o painel revelou (últimos 12 meses, área de atuação)

- O mercado cresceu 11,5% e a venda da distribuidora caiu 6,8%; o share foi de 7,2% para 6,0% (−1,18 p.p.).
- Nove das dez categorias perderam ou apenas mantiveram share.
- Share de 12,5% em um estado, 7,5% em outro e menos de 1% no terceiro.
- Nas grandes redes o share é de 3%, menos da metade do obtido em farmácias independentes.
- Cinco laboratórios respondem por 62% da venda; a empresa vende 29% dos produtos do seu mercado.
- Cada ponto de share vale cerca de R$ 190 milhões por ano.
- 267 produtos têm saldo em estoque e nenhuma venda em seis meses.

## Páginas

| Página | Pergunta |
|---|---|
| Visão Executiva | Como estamos, em 30 segundos? |
| Mercado & Share | Ganhamos ou perdemos share, e onde? |
| Produtos | O que vende, ganha e perde? |
| Laboratórios | Quem concentra a venda e onde há espaço? |
| Canal & Geografia | Onde somos fortes e fracos? |
| Estoque & Cobertura | O estoque acompanha a venda? |
| Oportunidades | Onde está o próximo ponto de share? |
| Diagnóstico | De onde vem a variação? |
| Definições | O que significa cada termo? |

Mais 4 tooltips em HTML (produto, laboratório, estoque, período) e 3 páginas de detalhe por drillthrough.

## Como foi construído

- **Modelo em estrela:** 2 fatos (mercado e estoque) e 5 dimensões, sem filtros bidirecionais nem colunas calculadas.
- **114 medidas DAX** em 13 pastas, todas com descrição: share, variação em p.p., market gap, índice de evolução, ranking com mudança de posição, Pareto, cobertura de estoque e potencial.
- **Calendário mensal com índice contínuo** para comparar qualquer seleção com o período anterior equivalente.
- **Cards, resumo executivo e tooltips em HTML**, gerados por medidas (visual HTML Content).
- **Tema central** (`theme.json`): paleta, tipografia, bordas e tabelas definidos uma única vez.
- **Formato PBIP (PBIR + TMDL):** todo o projeto em texto, versionável.

Detalhes em [`docs/`](docs): plano, changelog, performance e validação.

## Estrutura

```
Analise Varejo Mercado Farmaceutico.pbip
Analise Varejo Mercado Farmaceutico.Report/         relatório (PBIR)
Analise Varejo Mercado Farmaceutico.SemanticModel/  modelo (TMDL)
theme.json                                          tema do relatório
docs/                                               documentação
```

## Dados

A base não está no repositório: os dados de mercado são licenciados e os da empresa são confidenciais. O projeto abre no Power BI Desktop com a estrutura completa (modelo, medidas e páginas), mas sem dados carregados. O modelo lê CSVs da pasta indicada no parâmetro `PastaDados`.

## Requisitos

Power BI Desktop (versão com suporte a PBIP/PBIR) e o visual **HTML Content**, do AppSource.

## Autor

Tiago — [github.com/fbstiago-afk](https://github.com/fbstiago-afk)
