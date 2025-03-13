# Power BI Stock Market Analysis Dashboard

## 📌 Project Overview
The **Stock Market Analysis Dashboard** is a Power BI project designed to visualize stock market trends, analyze historical data, and provide actionable insights for investors. The dashboard integrates multiple data sources to track stock performance, compare indices, and analyze financial indicators over time.

## 🚀 Features
- 📊 **Stock Performance Tracking**: Monitor daily, weekly, and monthly trends.
- 📈 **Historical Data Analysis**: Evaluate stock prices over time with dynamic filtering.
- 📉 **Technical Indicators**: Moving averages, RSI, and MACD for investment insights.
- 🌍 **Market Index Comparison**: Compare multiple stock indices in a single view.
- 📅 **Custom Date Selection**: Flexible date filtering for trend analysis.
- 🏆 **Top Gainers & Losers**: Identify best and worst-performing stocks.

## 📂 Data Sources
This dashboard is powered by multiple datasets, including:
- **Stock Price Data**: Open, Close, High, Low, Volume
- **Market Indices**: S&P 500, NASDAQ, Dow Jones
- **Financial Indicators**: RSI, MACD, Moving Averages
- **Economic Data**: Inflation, Interest Rates, GDP Growth

## 📊 Power BI Data Model
The data model consists of the following key tables:
```plaintext
1. Stocks: Ticker, Date, Open, High, Low, Close, Volume
2. Indices: Index Name, Date, Open, Close, Change (%)
3. Technical Indicators: Ticker, RSI, MACD, Moving Averages
4. Economic Data: Date, GDP Growth, Inflation Rate, Interest Rate
```

## 🔍 Power Query (M Language) Snippet
Below is an example Power Query transformation for importing and cleaning stock data:
```powerquery
let
    Source = Csv.Document(File.Contents("StockData.csv"),[Delimiter=",", Columns=6, Encoding=1252, QuoteStyle=QuoteStyle.None]),
    PromoteHeaders = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    ChangeTypes = Table.TransformColumnTypes(PromoteHeaders,{{"Date", type date}, {"Open", type number}, {"High", type number}, {"Low", type number}, {"Close", type number}, {"Volume", Int64.Type}})
 in
    ChangeTypes
```

## 📝 DAX Measures for KPI Calculation
### Total Trading Volume
```DAX
Total Volume = SUM(Stocks[Volume])
```

### 50-Day Moving Average
```DAX
Moving Avg 50 = CALCULATE(AVERAGE(Stocks[Close]), DATESINPERIOD(Stocks[Date], MAX(Stocks[Date]), -50, DAY))
```

### Daily Price Change (%)
```DAX
Price Change % =
VAR PrevClose = LOOKUPVALUE(Stocks[Close], Stocks[Date], MAX(Stocks[Date])-1)
RETURN
IF(NOT(ISBLANK(PrevClose)), (MAX(Stocks[Close]) - PrevClose) / PrevClose * 100, BLANK())
```

## 📌 How to Use the Dashboard
1. **Select a Stock or Index**: Use filters to choose a specific stock or market index.
2. **Analyze Trends**: Observe historical price trends and key indicators.
3. **Compare Performance**: Utilize comparative charts to track multiple stocks.
4. **Identify Market Patterns**: Use moving averages and technical indicators for insights.

## 🛠️ Requirements
- **Power BI Desktop** (Latest Version)
- **Stock Market Dataset** (CSV, API, or Database Connection)
- **Basic Knowledge of Power BI, DAX & Power Query**


---

