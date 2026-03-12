# 📊 Análise Estatística com Python — PNAD 2015 (IBGE)

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-yellow)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

Projeto de **Análise Exploratória de Dados (EDA)** e **Estatística Descritiva** utilizando Python, baseado nos microdados da **Pesquisa Nacional por Amostra de Domicílios (PNAD) 2015** do IBGE.

O objetivo do projeto é aplicar conceitos de **estatística aplicada à análise de dados**, explorando padrões socioeconômicos da população brasileira.

---

# 📚 Dataset

Os dados utilizados são provenientes da **Pesquisa Nacional por Amostra de Domicílios (PNAD 2015)**.

A PNAD investiga características da população brasileira como:

- renda
- educação
- idade
- trabalho
- demografia

Fonte oficial:

https://ww2.ibge.gov.br/home/estatistica/populacao/trabalhoerendimento/pnad2015/microdados.shtm

---

# 🧰 Tecnologias Utilizadas

- Python  
- Pandas  
- NumPy  
- Seaborn  
- Matplotlib  
- SciPy  
- Google Colab  

---

# 📂 Estrutura do Projeto


analise-estatistica-pnad/

│
├── notebook
│ └── analise_estatistica_pnad.ipynb
│
├── data
│ └── dados.csv
│
└── README.md


---

# 📊 Processo de Análise

O projeto seguiu as seguintes etapas.

---

## 1️⃣ Importação das bibliotecas

```python
import pandas as pd
import numpy as np
import seaborn as sns
```

2️⃣ Carregamento do dataset

```python
dados = pd.read_csv('/content/sample_data/dados.csv')
```
Os dados foram carregados utilizando Pandas e armazenados em um DataFrame.

3️⃣ Construção de classes de renda

Para analisar a distribuição da renda, os valores foram agrupados em faixas baseadas em salários mínimos.

O salário mínimo em 2015 era R$ 788.

Classe	Faixa
A	Acima de 25 salários mínimos
B	15 a 25 salários mínimos
C	5 a 15 salários mínimos
D	2 a 5 salários mínimos
E	Até 2 salários mínimos

```python
classes = [
    dados.Renda.min(),
    2 * 788,
    5 * 788,
    15 * 788,
    25 * 788,
    dados.Renda.max()
]

```
4️⃣ Tabela de frequência da renda

Foi construída uma tabela de frequência utilizando pd.cut() e value_counts().

```python
frequencia = pd.value_counts(
    pd.cut(
        x=dados.Renda,
        bins=classes,
        labels=labels,
        include_lowest=True
    )
)
```
Também foi calculado o percentual de cada classe.
```python
percentual = pd.value_counts(
    pd.cut(
        x=dados.Renda,
        bins=classes,
        labels=labels,
        include_lowest=True
    ),
    normalize=True
) * 100

```
5️⃣ Gráfico de barras da distribuição de renda

```python
dist_freq_quantitativas_personalizadas['Frequência'].plot.bar(
    width=1,
    color='blue',
    alpha=0.2,
    figsize=(12,6)
)

```
6️⃣ Histogramas das variáveis

Foram criados histogramas para:

Idade

Altura

Renda

Exemplo:
```python
sns.distplot(dados['Idade'])
```
Esses gráficos permitem identificar distribuição, concentração de valores e possíveis outliers.

7️⃣ Histograma de renda filtrado

Para melhorar a visualização da renda, foi criado um histograma considerando apenas valores abaixo de R$ 20.000.
```python
sns.histplot(dados.query('Renda < 20000').Renda)
8️⃣ Tabela cruzada entre Sexo e Cor
frequencia = pd.crosstab(dados.Sexo, dados.Cor)
```
Tabela percentual:
```python
percentual = pd.crosstab(
    dados.Sexo,
    dados.Cor,
    normalize=True
) * 100
```
9️⃣ Estatísticas descritivas da renda
Métrica	Valor
Média	R$ 2000
Mediana	R$ 1200
Desvio padrão	R$ 3323

A média maior que a mediana indica assimetria positiva na distribuição da renda.

🔟 Estatísticas de renda por sexo e cor
```python
pd.crosstab(
    dados.Cor,
    dados.Sexo,
    values=dados.Renda,
    aggfunc={'mean','median','max'}
)
```
1️⃣1️⃣ Medidas de dispersão

Foram analisadas:

desvio médio absoluto

variância

desvio padrão

Essas métricas mostram o nível de desigualdade na distribuição da renda.

1️⃣2️⃣ Boxplot de renda
```python
sns.boxplot(
    x='Renda',
    y='Cor',
    hue='Sexo',
    data=dados.query('Renda < 10000')
)
```
1️⃣3️⃣ Percentual de pessoas que ganham até 1 salário mínimo
```python
from scipy import stats

stats.percentileofscore(dados.Renda, 788, kind='weak')
```

Resultado:

28.87% da população ganha até um salário mínimo.

1️⃣4️⃣ Valor máximo recebido por 99% da população
```python
dados.Renda.quantile(.99)
```
Resultado:

R$ 15.000

🧠 Insights Encontrados

Durante a análise foi possível observar:

A maior parte da população possui renda inferior a 5 salários mínimos

A distribuição de renda apresenta alta desigualdade

Pessoas com maior escolaridade possuem maior renda

Existem diferenças de renda entre estados brasileiros

▶️ Como Executar o Projeto

Clone o repositório:

git clone https://github.com/GabrielSbarbosa/seu-repositorio.git

Instale as dependências:

pip install pandas numpy seaborn scipy

Abra o notebook em:

Jupyter Notebook

Google Colab

👨‍💻 Autor

Gabriel Barbosa

GitHub
https://github.com/GabrielSbarbosa

Área de interesse
Data Analysis • Python • SQL • Estatística
