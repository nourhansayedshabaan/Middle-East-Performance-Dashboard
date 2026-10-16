#  Middle East Performance Dashboard

An interactive **Power BI** dashboard comparing **16 Middle East countries and territories** on economy, trade, demographics, health and development level.

> Built as **Mini Project 3** using Power Query for cleaning and DAX for the data model.

---

##  Project Goal
Help decision makers see which countries lead, which lag, and where to look deeper across:
- **Economy:** GDP, GDP growth, inflation, external debt, imports and exports, trade balance
- **Demographics and health:** population, birth and death rates, life expectancy, infant mortality
- **Development level:** countries classified as Developed, Developing or Underdeveloped

**Countries covered (16):** Bahrain, Egypt, Gaza Strip, Iran, Iraq, Jordan, Kuwait, Lebanon, Oman, Qatar, Saudi Arabia, Syria, Turkey, United Arab Emirates, West Bank, Yemen.

---

##  Dashboard Preview

### 1. Executive Overview
KPI cards (Average GDP, Average Life Expectancy, Total Population, Highest GDP Country, Lowest Inflation Country), GDP map, Average GDP by GDP Category, and a country table with growth indicators and GDP rank.

![Executive Overview]

### 2. Health & Education Analysis
Birth vs death rate, life expectancy, Development Level split, GDP vs life expectancy (bubble size = population), and infant mortality.

![Health & Education Analysis]

### 3. Economic Performance Analysis
GDP growth and trade balance cards, trade balance waterfall, Average GDP donut, imports vs exports, external debt treemap, and inflation trend.

![Economic Performance Analysis]

### 4. Country Details
Top 5 and Bottom 5 countries by GDP growth indicator, and GDP vs life expectancy scatter.

![Country Details]

### 5. Tooltip Page
Hovering over a country shows life expectancy, population, birth rate and death rate.

![Tooltip]

---

##  Features
- Synced **Country** and **GDP Category** slicers across all pages
- **Drillthrough** by Country
- Custom **tooltip** page
- Page navigator, Back button and a **Clear all slicers** button
- **Dynamic title** that changes with the selected Development Level
- Conditional colors for the GDP Growth Indicator

---

##  Data Model
- Table **`Country_Comparison`**: 16 countries
- Measures table **`Metrics`**: **15 DAX measures**
- **4 calculated columns:** Development Level, GDP Category, Growth Indicator Category and Population Category

**Development Level logic**
```DAX
Development Level =
IF(
    'Country_Comparison'[Life expectancy at birth(years)] >= 74 &&
    'Country_Comparison'[GDP - per capita] >= 15000, "Developed",
    IF(
        'Country_Comparison'[Life expectancy at birth(years)] >= 68 &&
        'Country_Comparison'[GDP - per capita] >= 3000, "Developing",
        "Underdeveloped"
    )
)
```

**GDP Category logic**
```DAX
GDP Category =
SWITCH(
    TRUE(),
    ISBLANK('Country_Comparison'[GDP]), "Unknown",
    'Country_Comparison'[GDP] >= 200000000000, "High GDP (>= $200B)",
    'Country_Comparison'[GDP] >= 30000000000, "Medium GDP ($30B - $200B)",
    "Low GDP (< $30B)"
)
```

## 🧹 Data Cleaning (Power Query)
1. Loaded the source and promoted headers
2. Removed unneeded top rows and columns
3. Filtered rows to keep only the 16 valid countries
4. Fixed data types
5. Quality check: no errors, `Country` is unique, *Current account balance* is about 12% empty (Gaza Strip and West Bank)

---

##  Key Insights
- Average birth rate is **25.9 per 1,000** against **4.6 deaths**, so births exceed deaths in all 16 countries
- **Yemen** has the highest birth rate (43.07) and death rate (8.53)
- **Saudi Arabia** has the largest current account surplus (**+$51.5B**); **Turkey** has the largest deficit (**−$15.3B**)
- Gulf economies run surpluses, while Turkey, Lebanon and Iraq run deficits

##  Recommendations
1. Prioritize health and education in Yemen, Gaza Strip and Iraq
2. Monitor external vulnerability in Turkey, Lebanon and Iraq
3. Use Saudi Arabia, Kuwait, UAE and Qatar as regional benchmarks
4. Complete the missing data for Gaza Strip and West Bank

---



## 🛠️ Tools
Power BI Desktop · Power Query · DAX
