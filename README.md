### Análise da Produção e Comercialização de Combustíveis no Brasil

Projeto de análise de dados desenvolvido com Python, Pandas e Power BI, com o objetivo de explorar a evolução da produção de petróleo e gás natural, a queima/perda de gás natural e a comercialização de combustíveis no Brasil.

A análise contempla dados históricos de produção, localização da produção, volumes comercializados e segmentos de clientes, utilizando técnicas de tratamento, agregação e visualização de dados para identificar tendências e padrões.

### Objetivos

- Analisar a evolução histórica da produção de petróleo e gás natural;
- Avaliar a quantidade de gás natural queimado ou perdido;
- Identificar os combustíveis com maior volume de vendas;
- Analisar a distribuição das vendas por segmento de cliente;
- Comparar a produção realizada em mar e terra;
- Avaliar a variação anual dos principais indicadores por meio do YoY.

### Ferramentas utilizadas

- Python
- Pandas
- Matplotlib
- Power BI
- DAX

---

### Perguntas Respondidas

- Como evoluíram a produção de petróleo e de gás natural ao longo do período analisado?
- Qual foi o volume total de gás natural queimado ou perdido e qual sua representatividade em relação à produção?
- Qual foi o volume total de combustíveis comercializados?
- Como a produção de petróleo e Gás Natural evoluiu ano a ano?
- Quais combustíveis apresentam os maiores volumes de vendas?
- Quais segmentos de clientes concentram as vendas de combustíveis?
- Como a produção de petróleo e gás natural se distribui entre as operações em mar e terra?
- Produção de Petróleo e Gás Natural por Estado e Região.
- Produção de Gás Natural por Região.
- Tipos de Combustíveis mais vendidos.
- Vendas de Combustíveis por Ano.
- Vendas de Combustíveis por Estado e Região.
- Vendas de Combustíveis por segmento de clientes.
- Como os principais indicadores variaram em relação ao ano anterior (YoY)?

---

### Principais Insights

### 1. Crescimento da produção

> A produção de petróleo e gás natural apresenta tendência de crescimento ao longo do período analisado. Em 2025, o petróleo apresentou crescimento de **11,97%**, enquanto o gás natural cresceu **16,68%** em relação a 2024.

### 2. Queima e perda de gás natural

> Em 2025, o volume de gás natural queimado ou perdido apresentou crescimento de 16,72%. Apesar disso, a taxa de queima/perda subiu apenas 0,04% em relação ao ano anterior, indicando que o volume queimado/perdido cresceu abaixo do ritmo da produção.

### 3. Concentração das vendas

> Óleo Diesel e Gasolina C apresentaram os maiores volumes de vendas, com aproximadamente 1,66 bilhão de m³ e 1,08 bilhão de m³, respectivamente.

### 4. Perfil dos compradores

> O segmento Posto Revendedor concentra o maior volume de vendas, representando aproximadamente 1,36 bilhão de m³, significativamente acima dos demais segmentos.

### 5. Predominância da produção offshore

> A produção está concentrada em operações em mar. O petróleo apresenta aproximadamente 92% de sua produção em mar, enquanto o gás natural apresenta cerca de 77%.

### 6. Variação nas vendas de etanol

> As vendas de etanol hidratado apresentam oscilações expressivas ao longo do período analisado, com períodos de retração e recuperação. Essa variação pode estar associada a fatores como a competitividade do etanol em relação à gasolina, a disponibilidade do produto e as condições da safra de cana-de-açúcar. Entretanto, essas relações não podem ser confirmadas apenas com os dados de vendas utilizados neste projeto.

### 7. Concentração da produção na região Sudeste

> A região Sudeste concentra a maior parcela da produção de petróleo e gás natural entre as regiões analisadas. Esse resultado está associado à relevância das operações offshore brasileiras, incluindo os campos do pré-sal, especialmente nas bacias de Santos e Campos.

### 8. Queima e perda de gás natural no Rio de Janeiro

> O Rio de Janeiro apresenta o maior volume de queima/perda de gás natural entre os estados analisados, com aproximadamente 35 milhões de m³, superando significativamente os demais. Desse total, cerca de 34 milhões de m³ estão associados à produção em mar, indicando forte concentração das ocorrências em operações offshore.

---

### Medidas DAX

As medidas DAX foram desenvolvidas no Power BI para consolidar os indicadores de produção, perdas e comercialização de combustíveis, além de permitir a análise da evolução anual dos resultados.

### 1. Indicadores de volume

Medidas utilizadas para calcular os volumes totais de petróleo produzido, gás natural produzido, gás natural queimado ou perdido e combustíveis comercializados.

### Produção Barris Petróleo

Calcula o volume total de petróleo produzido, em barris

```sql
Produção Barris Petróleo = SUM(producao_petroleo[PRODUÇÃO_BARRIS])
```

### Produção Gás Natural m³

Calcula o volume total de gás natural produzido, em metros cúbicos.

```sql
Produção Gás Natural m³ = SUM(producao_gn[PRODUÇÃO])
```

### Queima/Perda Gás Natural m³

Calcula o volume total de gás natural queimado ou perdido, em metros cúbicos.

```sql
Queima/Perda Gás Natural m³ = SUM(queima_perda_gn[QUEIMADO]) 
```

### Vendas de Combustíveis m³

Calcula o volume total de combustíveis comercializados, em metros cúbicos.

```sql
Vendas de Combustíveis m³ = SUM(vendas_combustiveis[VENDAS])
```

### 2. Indicador de queima e perda de gás natural

### Taxa de Queima/Perda de Gás Natural

Calcula a proporção entre o volume de gás natural queimado ou perdido e o volume total produzido. O resultado permite acompanhar a representatividade dessas perdas em relação à produção.

```sql
Taxa de Queima/Perda de Gás Natural = 
DIVIDE(
    [Queima/Perda Gás Natural m³],
    [Produção Gás Natural m³],
    0
)
```

### 3. Indicadores de variação anual (YoY)

O indicador YoY (Year over Year) calcula a variação percentual de um indicador em relação ao mesmo período do ano anterior. Neste projeto, as medidas utilizam SAMEPERIODLASTYEAR() para recuperar o período correspondente do ano anterior e DIVIDE() para calcular a variação relativa.

### Petróleo YoY

Calcula a variação percentual anual do volume de petróleo produzido.

```sql
Petróleo YoY = 
VAR Atual = [Produção Barris Petróleo]
VAR Anterior = CALCULATE([Produção Barris Petróleo], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

### Gás Natural YoY

Calcula a variação percentual anual do volume de gás natural produzido.

```sql
Gás Natural YoY = 
VAR Atual = [Produção Gás Natural m³]
VAR Anterior = CALCULATE([Produção Gás Natural m³], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

### Queima/Perda YoY

Calcula a variação percentual anual do volume de gás natural queimado ou perdido, permitindo acompanhar a evolução desse indicador ao longo do tempo.

```sql
Queima/Perda YoY = 
VAR Atual = [Queima/Perda Gás Natural m³]
VAR Anterior = CALCULATE([Queima/Perda Gás Natural m³], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

### Taxa Queima/Perda YoY

Calcula a variação percentual da taxa de queima/perda em relação ao mesmo período do ano anterior, permitindo avaliar se a participação do gás queimado ou perdido aumentou ou diminuiu proporcionalmente à produção.

```sql
Taxa Queia/Perda YoY = 
VAR Atual = [Taxa de Queima/Perda de Gás Natural]
VAR Anterior = CALCULATE([Taxa de Queima/Perda de Gás Natural], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

### Combustíveis YoY

Calcula a variação percentual anual do volume de combustíveis comercializados.

```sql
Combustíveis YoY = 
VAR Atual = [Vendas de Combustíveis m³]
VAR Anterior = CALCULATE([Vendas de Combustíveis m³], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

### 4. Indicador de vendas por produto

### Venda de Etanol m³

Calcula o volume comercializado de etanol hidratado, reutilizando a medida de vendas totais e aplicando um filtro específico ao produto. Essa abordagem permite analisar um combustível individual sem precisar criar uma nova soma diretamente sobre a coluna de vendas.

```sql
Venda de Etanol m³ = 
CALCULATE(
    [Vendas de Combustíveis m³],
    vendas_combustiveis[PRODUTO] = "ETANOL HIDRATADO"
)
```

### Dimensões do Modelo de Dados

As dimensões foram desenvolvidas para organizar atributos descritivos e facilitar a análise dos dados por período, produto e localização geográfica. Elas permitem centralizar informações compartilhadas entre as tabelas e simplificar a construção de filtros, segmentações e visualizações no Power BI.

### 1. DimCalendario

A DimCalendario é responsável por centralizar as informações temporais utilizadas na análise. Ela contém atributos como data, ano, mês, ano-mês e trimestre, permitindo explorar os indicadores em diferentes granularidades e realizar comparações entre períodos.

Objetivo: padronizar a análise temporal e possibilitar comparações anuais, mensais e trimestrais, incluindo os indicadores YoY (Year over Year).

```sql
DimCalendario = 
ADDCOLUMNS(
    CALENDAR(
        DATE(1990, 1, 1),
        DATE(2025, 12, 31)
    ),
    "ANO", YEAR([Date]),
    "MÊS", FORMAT([Date], "MMM"),
    "MÊS_NUM", MONTH([Date]),
    "ANO_MES", FORMAT([Date], "YYYY-MM")
)
```

### 2. DimProduto

A DimProduto centraliza os nomes dos produtos analisados e permite aplicar filtros consistentes entre as tabelas relacionadas a diferentes indicadores.

Objetivo: facilitar a comparação entre produtos e permitir análises segmentadas por categoria de produto.

```sql
DimProduto = 
DISTINCT(
    UNION(
        SELECTCOLUMNS(producao_petroleo, "PRODUTO", producao_petroleo[PRODUTO]),
        SELECTCOLUMNS(producao_gn, "PRODUTO", producao_gn[PRODUTO]),
        SELECTCOLUMNS(queima_perda_gn, "PRODUTO", queima_perda_gn[PRODUTO]),
        SELECTCOLUMNS(vendas_combustiveis, "PRODUTO", vendas_combustiveis[PRODUTO]),
        SELECTCOLUMNS(vendas_combustiveis_segmento, "PRODUTO", vendas_combustiveis_segmento[PRODUTO])
    )
)
```

### 3. DimGeografia

A DimGeografia reúne os atributos geográficos utilizados na análise, permitindo explorar a distribuição regional dos dados.

Objetivo: permitir a análise dos indicadores por região e estado, facilitando a identificação de diferenças geográficas na produção e na comercialização de combustíveis.

```sql
DimGeografia = 
DISTINCT(
    SELECTCOLUMNS(
        vendas_combustiveis,
        "UF", vendas_combustiveis[UNIDADE DA FEDERAÇÃO],
        "REGIAO", vendas_combustiveis[GRANDE REGIÃO]
    )
)
```
