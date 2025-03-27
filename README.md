# 1 - Acesso aos dados
url = 'https://github.com/alura-cursos/python-analise-chatgpt-assistente/raw/main/Dados/dados_vendas.json'
### Prompt:

Vamos atuar como cientistas de dados em uma empresa de supermercados.

Recebemos dados no formato de arquivo JSON, estruturados em listas e dicionários. O arquivo está disponibilizado em uma URL do Github.

Precisamos analisar esses dados para ajudar nas decisões da empresa. Programamos em Python e conhecemos as bibliotecas de análise de dados Numpy e Pandas. Portanto, priorize o uso dessas bibliotecas.

Por favor, nos informe como podemos fazer a leitura desses dados no formato JSON e como podemos visualizá-los em formato de tabela no Python.

import numpy as np
import pandas as pd


df = pd.read_json(url)
df.head()

item_identificador	loja_identificador	vendas_totais	item	loja
0	FDB08	OUT018	176503.58	{'item_peso': 6.055, 'item_conteudo_gordura': ...	{'loja_ano_estabelecimento': 2019, 'loja_taman...
1	DRQ35	OUT049	185758.20	{'item_peso': 9.3, 'item_conteudo_gordura': 'B...	{'loja_ano_estabelecimento': 2009, 'loja_taman...
2	FDD14	OUT018	165983.94	{'item_peso': 20.7, 'item_conteudo_gordura': '...	{'loja_ano_estabelecimento': 2019, 'loja_taman...
3	FDY37	OUT045	314923.40	{'item_peso': 17.0, 'item_conteudo_gordura': '...	{'loja_ano_estabelecimento': 2012, 'loja_taman...
4	FDY59	OUT018	64782.34	{'item_peso': 8.195, 'item_conteudo_gordura': ...	{'loja_ano_estabelecimento': 2019, 'loja_taman...

### Prompt:

O DataFrame "df" possui as colunas "item_identificador", "loja_identificador", "vendas_totais", "item" e "loja".

As colunas "item" e "loja" contêm dicionários aninhados dentro de cada uma das linhas. Como posso transformar os dados dos dicionários e colunas para torná-los mais acessíveis no meu DataFrame?


.# Importe a função json_normalize
from pandas import json_normalize

.# Normalize os dados da coluna "item"
df_item_normalized = json_normalize(df['item'])

.# Normalize os dados da coluna "loja"
df_loja_normalized = json_normalize(df['loja'])

.# Combine os DataFrames normalizados com o DataFrame original
df = pd.concat([df, df_item_normalized, df_loja_normalized], axis=1)

.# Exclua as colunas originais de "item" e "loja" se necessário
df.drop(['item', 'loja'], axis=1, inplace=True)
df

item_identificador	loja_identificador	vendas_totais	item_peso	item_conteudo_gordura	item_visibilidade	item_tipo	item_preco	item_quantidade_venda	loja_ano_estabelecimento	loja_tamanho	loja_tipo_localizacao	loja_tipo
0	FDB08	OUT018	176503.58	6.055	Baixo Teor de Gordura	0.031230	Frutas e Vegetais	160.36	None	2019	Médio	Nível 3	Supermercado Tipo 2
1	DRQ35	OUT049	185758.20	9.300	Baixo Teor de Gordura	0.042357	Bebidas Alcoólicas	123.24	None	2009	Médio	Nível 1	Supermercado Tipo 1
2	FDD14	OUT018	165983.94	20.700	Baixo Teor de Gordura	0.170500	Enlatados	184.13	None	2019	Médio	Nível 3	Supermercado Tipo 2
3	FDY37	OUT045	314923.40	17.000	Regular	0.026623	Enlatados	144.25	None	2012	None	Nível 2	Supermercado Tipo 1
4	FDY59	OUT018	64782.34	8.195	Baixo Teor de Gordura	0.000000	Confeitaria	93.15	None	2019	Médio	Nível 3	Supermercado Tipo 2
...	...	...	...	...	...	...	...	...	...	...	...	...	...
8545	FDY08	OUT010	28096.76	9.395	Regular	0.286345	Frutas e Vegetais	139.18	None	2008	None	Nível 3	Mercado
8546	FDC41	OUT017	130163.90	15.600	Baixo Teor de Gordura	0.117575	Alimentos Congelados	75.67	None	2017	None	Nível 2	Supermercado Tipo 1
8547	NCQ53	OUT045	614533.40	17.600	Baixo Teor de Gordura	0.018944	Mercearia	237.36	None	2012	None	Nível 2	Supermercado Tipo 1
8548	FDL46	OUT017	164985.24	20.350	baixo teor de gordura	0.054363	Lanches	117.95	None	2017	None	Nível 2	Supermercado Tipo 1
8549	NCN30	OUT046	96541.00	16.350	BTG	0.016993	Cereais	95.74	None	2007	Pequeno	Nível 1	Supermercado Tipo 1






















































































