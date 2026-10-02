# Plano de modernização

Projeto novo: `Analise Varejo Mercado Farmaceutico.pbip` .

## Decisões tomadas com o usuário

| Tema | Decisão |
|---|---|
| Nome da distribuidora | Fictício: **Vitalis** (dados, medidas e títulos) |
| Dados do portfólio | Venda e estoque da empresa multiplicados por um fator fixo; laboratórios e produtos reais; códigos internos trocados |
| Mercado de referência | Relatório abre em BA, ES e RJ (área de atuação) e no MAT mais recente; os outros estados continuam no filtro |

## Arquitetura do modelo (estrela)

```
dCalendario ─┐
dProduto ────┤
dEstado ─────┼──► fVendas (mês × distribuidor × FCC × UF × tipo de farmácia)
dTipoFarmacia┤
dDistribuidor┘
dProduto, dEstado ──► fEstoque (UF × SKU, foto de 03/04/2023)
```

- A ponte `auxEan` e os dois filtros bidirecionais saem: o EAN do estoque é resolvido para o FCC na carga, e o estoque liga direto ao produto.
- `dProduto` passa de 368.960 para 84.912 linhas (apenas itens com venda ou estoque), com textos aparados e nomes de coluna legíveis.
- Laboratório, categoria e canal ficam como atributos das dimensões existentes. Tabelas separadas criariam snowflake sem ganho.
- Calendário mensal com índice contínuo de meses; comparações de período usam o índice, não texto nem data/hora automática.
- Tabelas de apoio: `dGlossario` (digitada), `Meta Share` (what-if), `Dimensão de Análise` e `Indicador` (parâmetros de campo), `_Medidas`.
- Parâmetro `PastaDados` e função `fnLerCsv` centralizam a leitura.

## Medidas

114 medidas em `_Medidas`, em pastas: 00 Base · 01 Receita · 02 Mercado · 03 Share · 04 Quantidade · 05 Crescimento · 06 Ranking · 07 Estoque · 08 Preço · 09 Benchmark · 10 Inteligência · 90 HTML · 99 Auxiliares. Todas com descrição.

Regras preservadas: `Venda Vitalis` e `Venda Outros` continuam filtrando o distribuidor; a base de valor continua sendo o campo `RS_PR`.
Regras corrigidas: share (÷ mercado total) e crescimento (base = período anterior). A razão antiga fica disponível como `Razão Vitalis/Outros (legado)`.

## Páginas

| Página | Pergunta que responde | Componentes |
|---|---|---|
| Visão Executiva | Como estamos, em 30 segundos? | 6 KPIs HTML, venda × share mensal, resumo em texto, Δ share por categoria, top 5 laboratórios, maior oportunidade |
| Mercado & Share | Ganhamos ou perdemos share, e onde? | Leitura do share, share × ano anterior × média móvel, tabela por dimensão escolhida, crescimento Vitalis × mercado |
| Produtos | O que vende, ganha e perde? | Top 15, tabela de ranking com Δ posição, Pareto, concentração |
| Laboratórios | Quem concentra a venda e onde há espaço? | Top 15, ranking com potencial, dispersão share × crescimento, concentração |
| Canal & Geografia | Onde somos fortes e fracos? | Tipo de farmácia, market gap por estado, tabela por estado, mapa de calor categoria × canal |
| Estoque & Cobertura | O estoque acompanha a venda? | Cards, alerta de itens sem cadastro e sem giro, estoque por laboratório, cobertura por produto, itens sem cadastro |
| Oportunidades | Onde está o próximo ponto de share? | Card de oportunidade, meta de share, matriz de crescimento, top 30 por potencial com estoque |
| Diagnóstico | De onde vem a variação? | Árvore de decomposição da variação de venda, evolução do indicador escolhido |
| Definições | O que significa cada termo? | Glossário em cards |
| Ocultas | — | 4 tooltips HTML (produto, laboratório, estoque, período) e 3 drillthroughs (produto, laboratório, estado) |

Eliminadas: "Página 1" (rascunho de 3.300 px), "Produtos que mais crescem" (tabela estática do PDF), a coluna lateral de 8 slicers e o infográfico customizado.

## Design system

`theme.json` (também registrado no relatório) define paleta, tipografia, raio de 14 px, sombra suave, eixos, tabelas e slicers. Os visuais só carregam o que é específico deles.
Canvas 1600 × 900, margem 24 px, espaçamento 16 px. Navy `#172B4D`, azul `#2563EB`, teal `#0F9D8A`, verde `#16A36A`, laranja `#F59E0B`, vermelho `#D64545`, fundo `#F5F7FA`.

## Índice de oportunidade: avaliado e simplificado

Um score ponderado (tamanho + crescimento + share baixo + tendência + estoque) foi considerado e descartado: os pesos seriam arbitrários e o número final não teria unidade. No lugar ficou uma medida em reais, verificável à mão:

`Potencial até Share Médio = mercado da linha × (share de referência − share da linha)`

e uma classificação com regras explícitas (`Classe de Oportunidade`), descritas no README.
