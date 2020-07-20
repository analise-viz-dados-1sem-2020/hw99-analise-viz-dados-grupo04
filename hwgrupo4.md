19/07/2020

# Importando os dados

### Trazendo o .csv para dentro de um dataframe

``` r
df <- read.csv("./Dados/caso_full.csv")
df2 <- read.csv("./Dados/caso.csv")
```

### Organizando os dados

Selecionando apenas as cidades, depois selecionando apenas as colunas de
interesse e mudando o tipo da coluna de codigos do IBGE para alterarmos
os nomes das cidades posteriormente. Por fim adicionamos uma coluna com
os meses, separados das datas, pois é uma informação que usaremos para
responder nossas perguntas.

``` r
df <- df %>% filter(place_type == "city") %>% 
select(c("date",
         "city",
         "new_confirmed",
         "new_deaths",
         "state",
         "estimated_population_2019",
         "epidemiological_week",
         "city_ibge_code")) %>% 
  mutate(city_ibge_code = as.character(city_ibge_code)) %>% 
  mutate(Mes = substring(date,6,7))
```

Trazendo tabela com os códigos do IBGE e nomes certos das cidades

``` r
codes <- read_excel("./Dados/Codigo_IBGE.xls")
```

Trazendo o nome correto para o Dataframe

``` r
dfarrumado <- left_join(df,codes,by = c("city_ibge_code"="Código"))
```

Excluindo a coluna com os nomes mal formatados

``` r
dfarrumado$city <- NULL
```

Arrumando a ordem e o nome das colunas

``` r
df <- dfarrumado[,c(1,8,7,9,4,5,2,3)]
colnames(df) <- c("data","mes","codigo","municipio","estado","popest2019","novoscasos","novasmortes")
```

### Tabela gerada

Apenas as 6 primeiras linhas

<table>

<thead>

<tr>

<th style="text-align:left;">

data

</th>

<th style="text-align:left;">

mes

</th>

<th style="text-align:left;">

codigo

</th>

<th style="text-align:left;">

municipio

</th>

<th style="text-align:left;">

estado

</th>

<th style="text-align:right;">

popest2019

</th>

<th style="text-align:right;">

novoscasos

</th>

<th style="text-align:right;">

novasmortes

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

2020-02-25

</td>

<td style="text-align:left;">

02

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2020-02-26

</td>

<td style="text-align:left;">

02

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2020-02-27

</td>

<td style="text-align:left;">

02

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2020-02-28

</td>

<td style="text-align:left;">

02

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2020-02-29

</td>

<td style="text-align:left;">

02

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2020-03-01

</td>

<td style="text-align:left;">

03

</td>

<td style="text-align:left;">

3550308

</td>

<td style="text-align:left;">

São Paulo

</td>

<td style="text-align:left;">

SP

</td>

<td style="text-align:right;">

12252023

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

</tbody>

</table>
