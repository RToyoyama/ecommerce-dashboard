# Dashboard de E-commerce — Análise de Transações e Clientes

Projeto final do módulo de Aprofundamento de Analytics (Profissão Ciência de Dados). Consolida dados de transações e clientes de um e-commerce via SQL, exportando um dataset único pronto para visualização em Power BI / Looker Studio.

## Objetivo

- Unificar duas bases (transações e clientes) via JOIN SQL
- Tratar e normalizar os dados (conversão de tipos)
- Exportar dataset consolidado para consumo em ferramentas de BI
- Construir dashboard interativo com métricas de vendas, perfil demográfico e distribuição geográfica dos clientes

## Estrutura do projeto

```
ecommerce-dashboard/
├── data/
│   ├── raw/                 # Dados de origem (transações e clientes)
│   └── processed/           # Dataset consolidado (resultado do JOIN)
├── notebooks/
│   └── Profissao Cientista de Dados M26 Projeto.ipynb
├── requirements.txt
└── README.md
```

## Stack

- Python 3.13
- pandas
- SQLite (via `sqlite3`)
- Jupyter Notebook
- Power BI / Looker Studio (visualização)

## Como executar

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Abra `notebooks/Profissao Cientista de Dados M26 Projeto.ipynb` e execute todas as células.

## Pipeline

1. **Leitura dos dados raw**: `TB_TRANSACOES_PROJETO_ECOMM.csv` e `TB_CLIENTES_PROJETO_ECOMM.csv`
2. **Normalização**: conversão da coluna `Price` (formato `72,93` → `72.93`)
3. **Carga em SQLite**: tabelas `tb_transacoes` e `tb_clientes`
4. **JOIN SQL**: `INNER JOIN` entre as tabelas via `id_client`
5. **Export**: dataset consolidado em `data/processed/dados_ecommerce_final.csv`

## Justificativa do JOIN

Foi utilizado **INNER JOIN** porque o objetivo é analisar transações vinculadas a clientes identificados (perfil demográfico, localização). Transações cujo `id_client` não possui correspondência na tabela de clientes (registros órfãos) não agregam valor às métricas demográficas/geográficas do dashboard e foram excluídas do conjunto final — resultando em 296 registros consolidados.

## Dashboard

> Em construção. Será adicionado link e prints do dashboard (Power BI / Looker Studio) com as seguintes métricas:
> - Total de vendas e número de transações
> - Distribuição geográfica dos clientes (por estado)
> - Perfil demográfico (gênero, cargo)
> - Categorias de produtos mais vendidas
> - Distribuição por tipo de cartão

## Autor

Projeto desenvolvido como parte do curso Profissão Ciência de Dados.