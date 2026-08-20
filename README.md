# IFVG Ultimate+

By Canto Lab on TradingView.

## Disclaimer

I do not recommend trading this strategy as is. Read the rest of this README before you download the indicator for better understanding.

## What I left out and why

The original is a messy indicator with a lot of unnecessary inputs, most of which Dodgy doesn't even use himself.

I chose to leave out:

1. **Sensitivity** — he keeps this on the most sensitive setting by default, meaning every IFVG setup is shown even the small ones. So my code shows everything as well.
2. **HTF FVGs** — he never properly explains how he uses these. In practice they're treated as extra confluence at best. If a trade goes to profit without an HTF FVG lining up, **he still takes it**.
3. **TP lines** — I went with RR based targets instead of nearest liquidity. Taking Prophets, the dev of the original indicator, has said in his own videos that nearest-liquidity TP is too mechanical and in real scenarios he uses discretion and turns it off. So I built RR based TP instead, which is also just what most people requested me anyway.
4. **Setup grade box** — left out entirely. Dodgy himself has said the grading is mechanical, meaning there's a fixed set of rules generating the grade that doesn't imply actual grade.

**Outside of that, this indicator is not watered down. Any IFVG setup Dodgy sees on his chart is going to show up here too.**

One small change: the label on the IFVG line reads "IFVG" instead of "DD". If you're a fan of him and want it to say "DD", you can change it in settings.

## Does that mean the indicator is good?

Not really. I spent time watching Dodgy's videos while building this, and here's why I wouldn't take his explanations, his videos, or his indicator seriously.

**1. He hides invalidated IFVGs.** Meaning any setup that hit stoploss before reaching break even. This is in the code itself, it's not real-time quality filtering, it just removes losers after the fact it has happened.

In his videos he'll frame a specific loss as "this one failed because it was a setup I wouldn't have taken anyway" but that's not what the code is doing, it's not identifying bad setups in advance, **it's deleting the losing ones after they've already lost**. You have no way to tell that apart from a real loss when you're trading it live.

**2. He only shows 1–2 setups on chart "to keep charts clean."** Same underlying problem as above, it hides setups.

**3. He isn't consistent about where his stop actually is.** There are clear cases where a stop placed below the IFVG low would have failed, and in those videos he explains it as the stop being below structure low instead.

But on trades where the IFVG-low stop would have worked, he frames it as the stop being at the IFVG low, because it gives a higher RR. Both explanations get used depending on which one makes the trade look better after the fact, not based on a fixed rule stated up front.

You can watch these examples in his videos don't take my word for it.

**To know the true nature of the indicator, toggle to see losing setups and increase history** this shows all setups that you would see real time.

## What I noticed building this

This indicator is constantly scanning for setups, and that's a bad thing.

Price is always forming FVGs, if there's a swing, there's basically always an FVG in it. And given enough time, that FVG will always become an IFVG.

The only thing his model does to control for this is require the FVG to invert within 7–15 candles, which cuts down the number of setups shown, but doesn't meaningfully increase how often they actually work out.

I also built HTF sweep confirmation into IFVG detection (turn on in settings) expecting it to clean things up. Setup quality barely changed, if anything it looked slightly worse. So I didn't bother coding HTF FVG confluence or SMT on top of it, especially since he takes trades without them as well.

## So does the strategy have any value?

NO

## Why open source

This should not be a paid product. On top of that, Dodgy is a classic example of a hindsight trader — his own explanations contradict each other depending on how the trade played out.

## Features

- Single or Series IFVG detection
- Bullish, Bearish, or Neutral bias filtering
- HTF liquidity sweep detection and optional sweep-required filter
- Stoploss placement by wick, body, or IFVG boundary
- Break even level tracking
- RR based projections (fully configurable ratios)
- Session based alerting
- Configurable setup history depth, with option to hide invalidated setups

## Installation

1. Open TradingView and go to the Pine Editor.
2. Create a new indicator and paste in the contents of `ifvgUltimatePlus.pine`.
3. Save and add it to your chart.

## Contributing

Pull requests welcome, especially around cleaner sweep detection and any invalidation logic that's closer to how these setups actually fail in real time.

## License

MIT. Do whatever you want with it. Just don't sell it.
