# Dashboard de E-commerce — Análise de Transações e Clientes

Projeto final do módulo de Aprofundamento de Analytics (Profissão Ciência de Dados). Consolida dados de transações e clientes de um e-commerce via SQL e exibe os resultados em um dashboard HTML interativo.

## Objetivo

- Unificar duas bases (transações e clientes) via JOIN SQL
- Tratar e normalizar os dados (conversão de tipos)
- Exportar dataset consolidado para consumo no dashboard
- Exibir métricas de vendas, perfil demográfico e distribuição geográfica em dashboard interativo

## Estrutura do projeto

```
ecommerce-dashboard/
├── data/
│   ├── raw/                 # Dados de origem (transações e clientes)
│   └── processed/           # Dataset consolidado (resultado do JOIN)
├── notebooks/
│   └── Profissao Cientista de Dados M26 Projeto.ipynb
├── src/
│   └── dashboard.html       # Dashboard interativo (Chart.js)
├── requirements.txt
└── README.md
```

## Stack

- Python 3.13
- pandas
- SQLite (via `sqlite3`)
- Jupyter Notebook
- Chart.js 4.4.0 (dashboard HTML)

## Como executar

### 1. Pipeline de dados

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Abra `notebooks/Profissao Cientista de Dados M26 Projeto.ipynb` e execute todas as células. O arquivo `data/processed/dados_ecommerce_final.csv` será gerado.

### 2. Dashboard

O dashboard é um arquivo HTML autocontido — os 296 registros do CSV estão embutidos diretamente no arquivo, então não é necessário executar o pipeline para visualizá-lo.

**Opção A — servidor local (recomendado):**

```bash
python3 -m http.server 8000
```

Acesse `http://localhost:8000/src/dashboard.html`.

**Opção B — abrir diretamente no navegador:**

Abra `src/dashboard.html` com duplo clique ou `File > Open` no navegador.

## Pipeline

1. **Leitura dos dados raw**: `TB_TRANSACOES_PROJETO_ECOMM.csv` e `TB_CLIENTES_PROJETO_ECOMM.csv`
2. **Normalização**: conversão da coluna `Price` (formato `72,93` → `72.93`)
3. **Carga em SQLite**: tabelas `tb_transacoes` e `tb_clientes`
4. **JOIN SQL**: `INNER JOIN` entre as tabelas via `id_client`
5. **Export**: dataset consolidado em `data/processed/dados_ecommerce_final.csv`

## Justificativa do JOIN

Foi utilizado **INNER JOIN** porque o objetivo é analisar transações vinculadas a clientes identificados (perfil demográfico, localização). Transações cujo `id_client` não possui correspondência na tabela de clientes (registros órfãos) não agregam valor às métricas demográficas/geográficas do dashboard e foram excluídas do conjunto final — resultando em 296 registros consolidados.

## Dashboard

O dashboard `src/dashboard.html` é autocontido e não depende de servidor ou conexão com banco de dados em tempo de execução. Utiliza Chart.js (CDN) para renderizar os gráficos.

**Métricas exibidas:**
- Total de vendas e ticket médio
- Número de transações e clientes únicos
- Distribuição geográfica por estado (barras)
- Perfil demográfico por gênero (rosca)
- Receita por categoria de produto (barras horizontais)
- Distribuição de preços — histograma com 10 faixas
- Top cargos por número de transações

**Filtros interativos:** gênero, estado e categoria. Todos os KPIs e gráficos atualizam ao selecionar um filtro.

## Autor

Projeto desenvolvido como parte do curso Profissão Ciência de Dados.