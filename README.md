# hxc3-indicator 股票技术指标库（JavaScript）

A javascript technical indicators.

包含  asi, bias, boll, kdj, macd, rsi, vr, wr 

# Demo 

```javascript

    // 阿里巴巴 月k线 上市后的40个交易日的数据
    // usa.BABA month kline
    // t --> time
    // o --> openPrice 开盘价
    // a --> maxPrice 最高价
    // i --> minPrice 最低价
    // c --> closePrice 收盘价
    // n --> volume 成交量
    // np --> turnover 成交金额
    // n, np字段根据技术指标需要传入，有些技术指标不需要这两个字段

    var data = [
    {"t": "20150721", "o": 76.58, "a": 83.25, "i": 76.22, "c": 82.54, "n": 28291511 },
    {"t": "20150831", "o": 79.59, "a": 80.99, "i": 58, "c": 66.12, "n": 349649240 },
    {"t": "20150929", "o": 64.38, "a": 68.08, "i": 57.2, "c": 57.82, "n": 401172600 },
    {"t": "20151030", "o": 66.04, "a": 84.44, "i": 65.96, "c": 83.83, "n": 314092650 },
    {"t": "20151130", "o": 83.52, "a": 86.42, "i": 75.64, "c": 84.08, "n": 424712910 },
    {"t": "20151224", "o": 83.77, "a": 85.82, "i": 80.9, "c": 83.71, "n": 239338910 },
    {"t": "20160129", "o": 71.29, "a": 73.34, "i": 65.34, "c": 67.4, "n": 230766290 },
    {"t": "20160229", "o": 66.5, "a": 70.58, "i": 59.25, "c": 68.81, "n": 276400040 },
    {"t": "20160331", "o": 70.02, "a": 79.84, "i": 69.86, "c": 79.15, "n": 196736540 },
    {"t": "20160429", "o": 78.2, "a": 85.89, "i": 75.66, "c": 76.94, "n": 180592400 },
    {"t": "20160531", "o": 76.89, "a": 82.03, "i": 74.12, "c": 82, "n": 372797840 },
    {"t": "20160630", "o": 79.15, "a": 80.14, "i": 74.85, "c": 79.598, "n": 347040840 },
    {"t": "20160729", "o": null, "a": 85, "i": null, "c": 82.48, "n": 160246260 },
    {"t": "20160826", "o": 82.79, "a": 98.86, "i": 82.59, "c": 95.06, "n": 399044690 },
    {"t": "20160930", "o": 97.97, "a": 109.87, "i": 97, "c": 105.79, "n": 354603350 },
    {"t": "20161031", "o": 105.45, "a": 106.29, "i": 99, "c": 101.69, "n": 174483980 },
    {"t": "20161130", "o": 100.43, "a": 104.1, "i": 87.88, "c": 94.02, "n": 304165390 },
    {"t": "20161230", "o": 94, "a": 94.055, "i": 86.01, "c": 87.81, "n": 218070200 },
    {"t": "20170131", "o": 89, "a": 104.57, "i": 88.08, "c": 101.31, "n": 239146180 },
    {"t": "20170228", "o": 102.07, "a": 105.2, "i": 100.02, "c": 102.9, "n": 160471730 },
    {"t": "20170331", "o": 103.68, "a": 110.45, "i": 102.1, "c": 107.83, "n": 205398600 },
    {"t": "20170428", "o": 108.85, "a": 115.99, "i": 106.76, "c": 115.5, "n": 171981650 },
    {"t": "20170531", "o": 115.63, "a": 126.4, "i": 114, "c": 122.46, "n": 267264690 },
    {"t": "20170630", "o": 122.82, "a": 148.29, "i": 122.26, "c": 140.9, "n": 516459720 },
    {"t": "20170731", "o": 141.75, "a": 160.39, "i": 139.495, "c": 154.95, "n": 273387640 },
    {"t": "20170831", "o": 156.25, "a": 177, "i": 147.5, "c": 171.74, "n": 472763820 },
    {"t": "20170929", "o": 171.99, "a": 180.87, "i": 166.79, "c": 172.71, "n": 363734620 },
    {"t": "20171031", "o": 174.57, "a": 185.12, "i": 168.58, "c": 184.89, "n": 337680200 },
    {"t": "20171130", "o": 187.88, "a": 191.75, "i": 173.62, "c": 177.08, "n": 402499560 },
    {"t": "20171229", "o": 175.27, "a": 180.68, "i": 164.25, "c": 172.43, "n": 416245890 },
    {"t": "20180131", "o": 176.399, "a": 206.2, "i": 175.7, "c": 204.29, "n": 423672800 },
    {"t": "20180228", "o": 192.75, "a": 199.49, "i": 168.88, "c": 186.14, "n": 445029520 },
    {"t": "20180329", "o": 186.18, "a": 201.5, "i": 175.46, "c": 183.54, "n": 375865040 },
    {"t": "20180430", "o": 182.81, "a": 183.63, "i": 166.13, "c": 178.54, "n": 288314560 },
    {"t": "20180531", "o": 177.58, "a": 202.28, "i": 175.77, "c": 198.01, "n": 412790740 },
    {"t": "20180629", "o": 199.5, "a": 211.7, "i": 182.04, "c": 185.53, "n": 408902150 },
    {"t": "20180731", "o": 181.66, "a": 198.35, "i": 181.06, "c": 187.23, "n": 321804400 },
    {"t": "20180831", "o": 186, "a": 189.06, "i": 165.39, "c": 175.01, "n": 453444360 },
    {"t": "20180928", "o": 173.5, "a": 173.95, "i": 152.85, "c": 164.76, "n": 433332330 },
    {"t": "20181031", "o": 165.92, "a": 165.95, "i": 130.06, "c": 142.28, "n": 544315530 }
    
]
     
    var KDJ = hxc3.IndicatorFormula.getClass('kdj');
    var kdjIndicator = new KDJ();
    var result = kdjIndicator.calculate(data);
    console.log(result)

```

# scan all Indicators 查看所有指标计算公式
```javascript

    console.log(hxc3.IndicatorFormula.getAllClass())


# scan Indicators configs 查看某个指标的配置项
```javascript

    var KDJ = hxc3.IndicatorFormula.getClass('kdj');
    
    console.log(KDJ.defaultOption)

```

# Adding new indicators 添加新的指标计算

```javascript

    registerIndicatorFormula(NewIndicator, NewIndicator.type)

```