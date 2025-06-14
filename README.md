# 🌎 Análise Espacial de Municípios e Focos de Desmatamento em Minas Gerais

Este repositório contém dois scripts para processar dados geográficos do estado de Minas Gerais, Brasil. O projeto faz o download, reprojeção e análise de áreas dos **municípios mineiros**, além do pré-processamento dos **focos de desmatamento** para agosto e setembro de 2022. Os resultados são exportados em formatos GeoJSON e Excel, prontos para visualização ou uso em análises geoespaciais.

---

## 📦 Requisitos

- Python 3.7+
- Bibliotecas:
  - `geopandas`
  - `pandas`
  - `openpyxl`
  - `fiona`
  - `shapely`
  - `requests`
  - `IPython` (opcional, para notebooks)

Instale os pacotes com:

```bash
pip install geopandas pandas openpyxl fiona shapely requests ipython
