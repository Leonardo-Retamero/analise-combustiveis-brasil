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

---

### Medidas DAX

As medidas DAX foram desenvolvidas no Power BI para consolidar os indicadores de produção, perdas e comercialização de combustíveis, além de permitir a análise da evolução anual dos resultados.

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

```sql
Taxa Queia/Perda YoY = 
VAR Atual = [Taxa de Queima/Perda de Gás Natural]
VAR Anterior = CALCULATE([Taxa de Queima/Perda de Gás Natural], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

```sql
Combustíveis YoY = 
VAR Atual = [Vendas de Combustíveis m³]
VAR Anterior = CALCULATE([Vendas de Combustíveis m³], SAMEPERIODLASTYEAR(DimCalendario[Date]))
RETURN
DIVIDE(Atual - Anterior, Anterior, 0)
```

```sql
Venda de Etanol m³ = 
CALCULATE(
    [Vendas de Combustíveis m³],
    vendas_combustiveis[PRODUTO] = "ETANOL HIDRATADO"
)
```
