# Tradingview scripts

- Documentation: https://www.tradingview.com/pine-script-docs/en/v4

# Long-term investor
Based on [this bitcoin investor tool](https://lookintobitcoin.com/charts/bitcoin-investor-tool/) script.

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

```
//@version=5
indicator(title="Trend prediction signals", shorttitle="Signals", overlay=true, timeframe="1D")

short = input.int(7, minval=3, title="Short after")
long = input.int(7, minval=3, title="Long after")

TD = 0
TD := close > close[4] ? nz(TD[1]) + 1 : 0
TDUp = TD - ta.valuewhen(TD < TD[1], TD, 1 )
plotshape(TDUp == short ? true : na, style=shape.triangledown, color=color.red, text="Short", textcolor=color.red, location=location.abovebar)

TS = 0
TS := close < close[4] ? nz(TS[1]) + 1 : 0
TDDn = TS - ta.valuewhen(TS < TS[1], TS, 1 )
plotshape(TDDn == long ? true : na, style=shape.triangleup, color=color.green, text="Long", textcolor=color.green, location=location.belowbar)
```
