

<h1>🌎 Análise Espacial de Municípios e Focos de Desmatamento em MG</h1>

<p>Este repositório contém dois scripts para processar dados geográficos do estado de Minas Gerais, Brasil. O projeto realiza download, reprojeção e análise de áreas dos <strong>municípios mineiros</strong>, além do pré-processamento de <strong>focos de desmatamento</strong> (agosto e setembro/2022). Os resultados são exportados em GeoJSON e Excel, prontos para visualização ou uso em SIGs.</p>

<hr>

<h2>📦 Requisitos</h2>
<ul>
  <li>Python 3.7+</li>
  <li>Bibliotecas: geopandas, pandas, openpyxl, fiona, shapely, requests, IPython</li>
</ul>

<pre><code>pip install geopandas pandas openpyxl fiona shapely requests ipython</code></pre>

<hr>

<h2>🗺️ 1. Cálculo da Área dos Municípios</h2>
<p>O script baixa o GeoJSON dos municípios mineiros, converte o CRS para EPSG:31983, calcula as áreas em km² e exporta os resultados.</p>

<pre><code>import geopandas as gpd
import requests
from IPython.display import display

url = "https://raw.githubusercontent.com/tbrugz/geodata-br/master/geojson/geojs-31-mun.json"
gdf = gpd.read_file(url)
if gdf.crs is None:
    gdf = gdf.set_crs('EPSG:4326')

gdf_31983 = gdf.to_crs('EPSG:31983')
gdf_31983['area_km2'] = gdf_31983.geometry.area / 1_000_000
gdf_31983.to_file("municipios_mg_31983.geojson", driver='GeoJSON')
gdf_31983.drop(columns='geometry').to_excel("municipios_mg_31983.xlsx", index=False)</code></pre>

<p><strong>Exemplo:</strong> maior município: 4.061,92 km² | menor município: 87,61 km²</p>

<hr>

<h2>🌳 2. Processamento de Focos de Desmatamento</h2>
<p>Este script une arquivos GPKG dos focos de desmatamento de agosto e setembro de 2022, reprojeta para EPSG:31983 e exporta os dados.</p>

<pre><code>import geopandas as gpd
import pandas as pd

gdf_ago = gpd.read_file("desmatamento_ago22.gpkg")
gdf_set = gpd.read_file("desmatamento_set22.gpkg")
gdf_unido = gpd.GeoDataFrame(pd.concat([gdf_ago, gdf_set], ignore_index=True))
gdf_unido = gdf_unido.to_crs(epsg=31983)
gdf_unido.to_file('focos-desmatamento-mg.geojson', driver='GeoJSON')
df_excel = gdf_unido.drop(columns=['geometry'])
df_excel.to_excel('focos-desmatamento-mg.xlsx', index=False)</code></pre>

<hr>

<h2>📁 Estrutura Sugerida</h2>
<pre><code>/
├── municipios_mg_31983.geojson
├── municipios_mg_31983.xlsx
├── focos-desmatamento-mg.geojson
├── focos-desmatamento-mg.xlsx
├── desmatamento_ago22.gpkg
├── desmatamento_set22.gpkg
└── README.html</code></pre>

<hr>

<h2>📚 Fontes dos Dados</h2>
<ul>
  <li><a href="https://github.com/tbrugz/geodata-br" target="_blank">tbrugz/geodata-br</a> — GeoJSON de municípios</li>
  <li>Focos de desmatamento — fornecidos localmente</li>
</ul>




</body>
</html>
