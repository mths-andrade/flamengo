Todos os dados estão organizados por ano, em arquivos distintos.

2019: [lib 19.csv](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/lib%2019.csv)
2020: [lib 20.csv](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/lib%2020.csv)
2021: [lib 21.csv](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/lib%2021.csv)
2022: [lib 22.csv](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/lib%2022.csv)
2023: [lib 23.csv](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/lib%2023.csv)

Meu objetivo é verificar qual campanha teve maior eficácia em relação a finalizações realizadas e convertidas, a primeira impressão é que seja a campanha de 2022 pois o time ganhou 12 jogos e só empatou um.

Uma primeira observação importante é que o desempenho de um time no torneio é irregular, nem todo ano chega nas quartas ou na final por exemplo. Ou seja, estamos tratando de amostras de tamanhos diferentes.

Agora, começamos importando as bibliotecas, nesse caso, pandas para operar os dados, matplotlib e seaborn para a parte gráfica, numpy para cálculos e statsmodels para a estatística.

Lemos os arquivos e transformamos as colunas de datas no formato `datetime` para que os módulos assim as interpretem. Como um exemplo, temos o comando abaixo, que transforma o formato do primeiro arquivo para o padrão na biblioteca.

```python
lib19['data'] = pd.to_datetime(lib19['data'], format='%Y-%m-%d')
```
Para facilitar o processo, criei três funções, uma para os três gráficos juntos, outro para os dados dos modelos e mais outra para a regressão linear se o modelo for estatisticamente relevante.

Respectivamente:

```python
def plot_comparacao(x, y1, y2, y3, dataset, titulo):
	plt.figure(figsize=(12,6))
	ax = plt.subplot(3,1,1)
	ax.set_title(titulo,fontsize=18, loc='left')
	sns.lineplot(x=x, y=y1, data=dataset)
	plt.subplot(3,1,2)
	sns.lineplot(x=x, y=y2, data=dataset)
	plt.subplot(3,1,3)
	sns.lineplot(x=x, y=y3, data=dataset)
	ax=ax
```

```python
def sumario(formula,dataset):
  resultado=smf.ols(formula=formula, data=dataset).fit()
  print(resultado.summary())
```

```python
def regressao(x,y,dataset,titulo):
  ax=sns.lmplot(x=x,y=y,data=dataset)
  ax.fig.suptitle(titulo,y=1.05)
```

## 2019

De cara já temos um ano com o número máximo de 13 jogos e um título.

![tendência 19](https://github.com/mths-andrade/flamengo/assets/159069202/54f555b9-2ad0-44aa-afbc-e9eb41182aa6)

Não temos tanta relação entre finalizações no alvo e gols de fato como visto acima. Vamos ver com os dados estatísticos. Usei o método dos mínimos quadrados para ajustar os dados.

![modelo 19](https://github.com/mths-andrade/flamengo/assets/159069202/bb7ad0e0-9768-4836-85ba-500d6602ecb2)

Como o p-valor é menor que 0.05, o modelo é significativo. Temos um R² relativamente alto de 0.731, o que significa que há uma relação bem linear entre finalizações e gols.

![regressão 19](https://github.com/mths-andrade/flamengo/assets/159069202/004db6e7-b8c5-42a1-99c3-0cd0110e98a6)

## 2020

No ano de início da pandemia, o time foi eliminado na oitavas, então temos menos dados, oito para ser mais exato.

![tendência 20](https://github.com/mths-andrade/flamengo/assets/159069202/008e8bc9-f35b-4f84-bf9b-b64d09e361ee)

A relação entre os dados parece maior.

![modelo 20](https://github.com/mths-andrade/flamengo/assets/159069202/5fa0d103-9bfb-4b02-916a-7f044cc790f5)

O modelo é significativo pois o p-valor é menor que 0.05. R² é 0.733, ligeiramente maior do que o anterior, logo a relação linear é maior.

![regressão 20](https://github.com/mths-andrade/flamengo/assets/159069202/a0a82fbb-45ec-46bb-9965-d094760b534b)

## 2021

Mais um ano em que o time chegou à final do torneio, então teve o máximo de 13 jogos. 

![tendência 21](https://github.com/mths-andrade/flamengo/assets/159069202/de286543-7b4e-4861-b48f-fd20eee2bd28)

A diferença entre as categorias é muito grande, sinalizando baixa eficácia do time. Isso pode ser confirmado com o modelo.

![modelo 21](https://github.com/mths-andrade/flamengo/assets/159069202/370557e1-bd06-491e-9d8e-720bda0b0d7e)

p-valor menor que 0.05: modelo significativo. Temos um R² baixo de 0.488, o que confirma a baixa eficácia no time na conversão de finalizações e uma relação pouco linear.

![regressão 21](https://github.com/mths-andrade/flamengo/assets/159069202/2d87f084-1c4d-4e8d-b947-fbee557957da)

## 2022

Temos o segundo ano no nosso estudo em que o time chegou à final e ganhou o título. Portanto, outro ano com 13 dados.

![tendência 22](https://github.com/mths-andrade/flamengo/assets/159069202/f4cadd32-9df5-4c3e-9ac4-36d5ac04b8f8)

Aparentemente há grande similaridade nas duas categorias de dados.

![modelo 22](https://github.com/mths-andrade/flamengo/assets/159069202/3a370f5d-ed50-4419-b169-23abc1205a2a)

p-valor menor que 0.05: modelo significativo. Como suspeitava, temos o ano com maior eficiência até agora pois a relação linear entre finalizações realizadas e convertidas é bem forte, com R² de 0.881. 

Portanto, minha primeira impressão de que o ano mais eficaz seria esse estava correta.

![regressão 22](https://github.com/mths-andrade/flamengo/assets/159069202/2ef35221-8a53-4a59-9dd0-29edbd10080f)

## 2023

O time parou nas oitavas no ano passado, então apenas 8 jogos na amostra.

![tendência 23](https://github.com/mths-andrade/flamengo/assets/159069202/ca699a71-e680-41c0-825c-fcf14139c477)

Novamente uma eficácia apenas regular.

![modelo 23](https://github.com/mths-andrade/flamengo/assets/159069202/d124d923-6b2b-4bc7-8a7c-d58e38cc2555)

Entretanto, temos um p-valor maior que 0.05, então o modelo obtido por mínimos quadrados não é estatisticamente significativo, não podemos fazer inferências mais formais sobre ele.

## Desenvolvimento sobre 2022

Como o ano de 2022 teve uma eficácia maior, vamos ver um gráfico de dispersão desse ano.

```python
x = lib22.fin_alvo
y = lib22.gols

ax = sns.scatterplot(data=lib22, x="fin_alvo", y="gols")
ax.figure.set_size_inches(10, 6)
ax.set_title("Finalizações realizadas no alvo X gols na Libertadores de 2022")
ax.hlines(y = y.mean(), xmin = x.min(), xmax = x.max(), colors='gray', linestyles='dashed')
ax.vlines(x = x.mean(), ymin = y.min(), ymax = y.max(), colors='gray', linestyles='dashed')
```

![gráfico 22](https://github.com/mths-andrade/flamengo/assets/159069202/143dcfdf-409e-4fd8-bfb5-e227be205932)

Temos várias situações, por exemplo, 2 gols com 3, 4, 5 e 6 finalizações no alvo e quatro finalizações que resultaram em um e dois gols. As linhas tracejadas são as médias de cada categoria: 6 finalizações no alvo e 2.54 gols por jogo, na minha opinião, médias bem altas, maiores do que as médias do campeonato.

Em 2019, tivemos uma média de 5.77 de finalizações por jogo, um pouquinho menor, e 1.85 gols por jogo, bem menor que em 2022, menor do que a média de 2.35 do campeonato. Em 2021, respectivamente 6.15 e 2.54, maiores do que os dois, ainda assim, sem um título. A média dessa edição foi de impressionantes 2.73.

## Todos os jogos

Para terminar, reuni todos os jogos nacionais e internacionais do time nesses mesmos anos e com as mesmas categorias de dados. 

Dessa vez, há muita diferença entre os números de jogos, especialmente em 2020 por causa da pandemia. Em 2021 tivemos mais de uma edição do Brasileirão, então obviamente esse ano teve mais jogos.

| ano |	fin_alvo | fin_fora |	gols | jogos |
| --- | -------- | -------- | ---- | ----- |
|2019|320|305|115|57|
|2020|224|209|75|41|
|2021|436|437|139|72|
|2022|335|367|108|62|
|2023|291|282|97|61|

![tendência_final](https://github.com/mths-andrade/flamengo/assets/159069202/6411e2c8-25b7-47df-9979-cd65f1a7a252)

A similaridade entre finalizações no alvo e gols chama a atenção imediatamente, parecem idênticos.

![modelo_final](https://github.com/mths-andrade/flamengo/assets/159069202/68fbca29-0458-4c6c-9b67-c28bb75c1f89)

Temos uma excelente correlação de 0.957, então a relação entre as categorias nesse período é quase linear… 

Porém, temos um p-valor alto de 0.655, então não podemos considerar os resultados acima por não terem relevância estatística, infelizmente.

## Conclusão

1. Não podemos prever corretamente os números de gols na Libertadores pelas finalizações no alvo em cada jogo.
2. O ano mais eficaz do time nesse período, e provavelmente na história, foi de 2022. Ainda assim, sinto que não dão o destaque devido a essa campanha forte estatisticamente.
3. Se fazendo recortes de 8 a 13 jogos não conseguimos prever direito o número de gols, com 50, 60 ou 70 é impossível.

Notebook: [flamengo.ipynb](https://github.com/mths-andrade/flamengo/blob/efc526c9c390b6b7ce1f2596b0ddb48dc9f6078a/flamengo.ipynb)

Agradeço a todas as pessoas que leram até aqui, muito obrigado!

