# Tradingview scripts

Pine script documentation: https://www.tradingview.com/pine-script-docs/en/v5

## Long-term investor
Based on [this bitcoin investor tool](https://lookintobitcoin.com/charts/bitcoin-investor-tool/) script.

### inputs
```
Baseline   (int)   default 100 weeks
Multiplier (float) default 3.2
```

### script
```
//@version=5
indicator(title="Long-term investor", shorttitle="Investor", overlay=true, timeframe="1W")

base = input.int(100, minval=1, title="Baseline")
multiplier = input.float(3.2, minval=.1, title="Multiplier")

output = ta.ema(close, base)

plot(output, title="EMA", color=color.green, linewidth=2, offset=0)
plot(output * multiplier, title="EMA", color=color.red, linewidth=2, offset=0)
```

# Trend prediction signals
Base on DeMark9 indicator from [demark.com](https://demark.com/indicators-list/).

### inputs
```
Short (int) default 7 sequential days
Long  (int) default 7 sequential days
```

### script
```
//@version=5
indicator(title="Trend prediction signals", shorttitle="Signals", overlay=true, timeframe="1D")

short = input.int(7, minval=3, title="Short")
long = input.int(7, minval=3, title="Long")

display = false

down = 0
down := close > close[4] ? nz(down[1]) + 1 : 0

display := down - ta.valuewhen(down < down[1], down, 1 ) == short
plotshape(display, style=shape.triangledown, color=color.red, text="Short", textcolor=color.red, location=location.abovebar)

up = 0
up := close < close[4] ? nz(up[1]) + 1 : 0
display := up - ta.valuewhen(up < up[1], up, 1 ) == long
plotshape(display, style=shape.triangleup, color=color.green, text="Long", textcolor=color.green, location=location.belowbar)
```
