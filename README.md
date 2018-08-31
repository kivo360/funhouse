# Funhouse - Funguana's Time Series Pre-processing library for our crypto trading bot

`Funhouse` is a simple small library that is created to easily standardize pre-processing for our trading bot. It's based on TA-Lib and Pandas.

The entire goal we have for this library is to modularize the processing for Funguana's Bot. It allows us to organize better.

Funhouse currently only supports price and TA data. In the future it'll support text data as well.



## What makes `Funhouse` better?
Currently it's only the simpler interface and modular library available for what we need.


## How does it work?
It's a simple builder pattern to extract the information we need given a data set. 



### Example:
---
```python
from funtime import Store, Converter
from funpicker import Query
from funhouse import TA, index_time

# Create a library and access the store you want
store = Store().create_lib("ticker.Price").get_store()
tickstore = store["ticker.Price"]


# Get the bittrex price
hourly_bittrex_eth = Query().set_crypto("ETH").set_fiat("USD").set_exchange("bittrex").set_period("hour").set_limit(500).get()

# Get the price dataframe
bittrex_frame_hr = Converter.to_dataframe(hourly_bittrex_eth)

# Get the newly indexed time
bittrex_frame_hr = index_time(bittrex_frame)

tframe = TA(bittrex_frame_hr)

# We're getting all of the necessary TA indicators
tframe.SMA().SMA(100).RSI().RSI(window=30).BOLL().ATR().FIBBB()

# Get the main indicators
tframe.main

# Get the fibbonaci indicator
tframe.fib


# can store the TA indicators here
# Note: This part isnt tested yet


```

## How to install

Make sure to install mongodb at the very beginning. The instructions are different for different operating systems. Then run:

```
pip install funhouse
```

Or you can use `pipenv` for it:

```
pipenv install funhouse
```