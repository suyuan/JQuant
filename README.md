# JQuant

# Maven依赖

```xml
<dependency>
    <groupId>quant.fans</groupId>
    <artifactId>JQuant</artifactId>
    <version>0.1</version>
</dependency>
```

# 示例

```java
package quant.fans;

import quant.fans.model.StockData;

import java.util.List;

public class Main {

    public static void main(String[] args) {
        Quants quants = new Quants();
        //获取股票列表
        List<String> list = quants.data.stockList();

        for (String stock : list) {
            //StockData代表一个时间片的数据，例如日线级别，每个StockData为一天收盘后的股票数据
            List<StockData> stockDatas = quants.data.dailyData(stock);
            //剔除交易数据小于60天的股票
            if (stockDatas == null || stockDatas.size() < 60) {
                continue;
            }
            //indicator包含常用指标的计算
            quants.indicator.macd(stockDatas);
            //获取5、10、20、30、40、60均线，也可以通过sma(stockDatas,ma)获取指定时间间隔的均线
            quants.indicator.sma(stockDatas);
            quants.indicator.boll(stockDatas);
            quants.indicator.kdj(stockDatas);
            //strategy包含简单的策略计算，例如macd金叉
            quants.strategy.macdCross(stockDatas);
            quants.strategy.kdjCross(stockDatas);
            quants.strategy.goldenSpider(stockDatas);
            quants.strategy.bollThroat(stockDatas);
            for (StockData stockData : stockDatas) {
                System.out.println(stockData);
            }
        }
    }
}
```

# API

## 初始化

> Quants quants = new Quants();

## 股票数据 quants.data

## 股票列表 quants.stocks

## 指标计算 quants.indicator

## 策略计算 quants.strategy
