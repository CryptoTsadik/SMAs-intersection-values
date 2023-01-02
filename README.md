# SMAs-intersection-values

![Image](https://user-images.githubusercontent.com/103097327/210254304-f9ecd232-e798-45e0-8dc7-69f49abc3f40.png)



The Bitstamp API.ipynb download daily OHLC data from bitstamp public API using request library and stores it in csv file.
Parameters used are from Bitstamp API, no custom parameters added:
  - start: date from which data would be retrieved
  - end: last date to download
  - pair: chosen pair to download
  - step:	Timeframe in seconds. Default 86400 - 1 Day
  - limit: Limit OHLC results. Deafult: 1000)

Retrieved data is written to csv file for futher usage.

SMAs intersection.ipynb display periods where the price difference from Simple Moving Avarages matches with price difference values in the near past. 
For this, the following steps are used:
  - Lodaing csv file, converting epoch time to datetime format, set columns with timestamps as index, removing unwanted columns. 
  - Creating Simple Moving Averages using Close column values
  - Creating columns and filling them with value of difference (we'll call it: price_diff_) between "Close" and "Moving Averages".
  - Scale data with StandardScaler to make it uninform.
  - Define bounds of min and max values of difference of price from SMAs in time range defined by user (we'll call it: researched period).
  - Compare values recieved from previous step with historical values to see if the price_diff_ had been aat the same levels and when.
  - Plot periods which correspond to intersection of multiple price_diff_ values, mening that researched period is similar to previous ones, which you can see on chart.
    (yellow - researched period, green - periods with similar price_diff_ values.)
  
Parametres to set by user: 
  - period_to_compare: days from today backwords to include in comparison with historical data (researched period). 
        For example: if set for 30, then previous 30 days from today would be included in analysis.
  - level_of_intersection: value in % which represents how many of intersections are needed to "signal" an intersection. 
        For example if the value is set to 60, it means that in case of 60 out 100 "sma_diff_" values are in the bounds of min and max values from researched period 
        it would be displayd by programm. 
        
Next improvements might me implemented:
- adding "weights" accroding to length of SMA
- adding implied return adjusted for capitalization based on historical returns data at "similar points".
- store data for altcoins to SQLlite DB to use this code.
  
