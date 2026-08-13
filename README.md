# SuddenSpikeAI


### The prognosis: 

The stock market has always been a source of curiosity for me because of its inherent unpredictability. There is no perfect formula that can consistently explain what a stock will do next. At the simplest level, a price can rise, fall, or remain relatively unchanged, yet behind those movements are countless interacting variables: price and volume behavior, volatility, liquidity, short interest, options activity, market sentiment, company fundamentals, macroeconomic conditions, news, human behavior, etc... Many of these factors can be measured, but others may be difficult to observe, poorly understood, or hidden within complex relationships between variables. Even when two market situations appear almost identical according to the information we can measure, their outcomes can still be completely different. This led me to a broader hypothesis: **there may be patterns, interactions, or sources of uncertainty within market data that we have not yet discovered or learned how to represent.**

One particularly interesting example of this unpredictability is the **short squeeze**. A short squeeze occurs when a heavily shorted stock begins rising rapidly, forcing some short sellers to buy shares back to close their positions. That buying can create additional upward pressure, which may force even more short sellers to exit, sometimes producing an extremely rapid and nonlinear price increase. We already know several conditions commonly associated with short squeezes, such as high short interest, limited share availability, unusual volume, increasing volatility, and strong buying pressure. 

But these known indicators raise a more interesting possibility: **what if there are additional combinations, sequences, relationships, or precursor patterns hidden within market data that humans have never explicitly identified?** Rather than manually defining what a short-squeeze setup should look like, through the project I want to explore whether a machine can search historical market behavior itself, discover statistically meaningful nonlinear/complex hidden patterns preceding past squeezes, determine which of those patterns generalize beyond the data in which they were discovered, and recognize similar or evolving structures as they begin forming in real time.

### Research Question

**Can an AI system autonomously discover previously unknown/very complex patterns in market data that precede short squeezes and use those patterns to estimate, in real time, the probability that a short squeeze is developing?**.
