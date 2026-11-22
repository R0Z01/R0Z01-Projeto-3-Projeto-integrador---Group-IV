# Projeto-3-Projeto-integrador---Group-IV
# Projeto Integrador — Group IV

Este repositório será utilizado para armazenar a documentção e o código do projeto.

## Organização do trabalho

- As sprints serão definidas e acompanhadas em um quadro Kanban no Trello.
- A documentação escrita do projeto ficará armazenada neste repositório.

## Ferramentas utilizadas

- Python
- Notebooks (`.ipynb`)
- Streamlit
- Biblia Sagrada
- Monster Ultra
  
## Pipeline SRAG Medallion

Pipeline de dados baseado na arquitetura Medallion (Bronze, Silver e Gold) utilizando os registos públicos de Síndrome Respiratória Aguda Grave (SRAG) do Ministério da Saúde (2019 a 2026).
---

Camada Bronze — Coleta e Ingestão de Dados Brutos

A etapa Bronze consulta e transfere os CSVs oficiais de SRAG diretamente do armazenamento do Ministério da Saúde para a pasta local `data/bronze/`, preservando os ficheiros originais sem qualquer alteração de conteúdo ou esquema, além de gerar metadados de integridade e diagnóstico em `metadata/`.

### 1. Origem dos Dados
* **Fonte:** Portal de Dados Abertos do SUS (OpenDataSUS) — Ministério da Saúde (`https://dadosabertos.saude.gov.br/dataset/srag-2019-a-2026`).
* **Método de coleta:** O notebook `notebooks/01_bronze.ipynb` utiliza URLs diretas verificadas manualmente (`FONTES_REFERENCIA` hospedadas em `s3.sa-east-1.amazonaws.com/ckan.saude.gov.br/SRAG/`) via Python + `requests`.
* **Sem API CKAN:** O pipeline **não** consulta endpoints de catálogo CKAN automaticamente; caso o portal publique novas versões anuais, a URL correspondente deve ser atualizada manualmente no dicionário `FONTES_REFERENCIA`.

### 2. Configuração do Ambiente (Linux e Windows)

Com o Python 3.10+ instalado, clone o repositório e crie o ambiente virtual na raiz do projeto:

**Linux / macOS:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
