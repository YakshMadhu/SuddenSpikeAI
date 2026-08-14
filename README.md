# SuddenSpikeAI


### The prognosis: 

The stock market has always been a source of curiosity for me because of its inherent unpredictability. There is no perfect formula that can consistently explain what a stock will do next. At the simplest level, a price can rise, fall, or remain relatively unchanged, yet behind those movements are countless interacting variables: price and volume behavior, volatility, liquidity, short interest, options activity, market sentiment, company fundamentals, macroeconomic conditions, news, human behavior, and more. Many of these factors can be measured, while others may be difficult to observe, poorly understood, or hidden within complex relationships between variables. Even when two market situations appear almost identical according to everything we can measure, their outcomes can still be completely different. This led me to a broader hypothesis: **there may be patterns, interactions, or sources of uncertainty within market data that we have not yet discovered or learned how to represent.**

One particularly interesting example of this unpredictability is the sudden extreme price spike, especially in low-float and small-cap stocks. Within a very short period of time, a stock can experience an unusually large upward movement. Within a very short period of time, a stock can experience an unusually large upward movement. Such spikes may be associated with short squeezes, news, momentum, options activity, liquidity changes, shifts in market attention, combinations of several factors, or mechanisms that are not immediately obvious. For this project, however, the exact human-defined explanation behind the spike is not the primary focus. A spike is treated as a spike regardless of what ultimately caused it. 

But these known indicators raise a more interesting possibility: **what if there are combinations, sequences, relationships, or precursor structures hidden within market data that repeatedly appear before these extreme movements but have never been explicitly identified by humans?** Rather than manually defining what a pre-spike setup should look like, through this project I want to explore whether a machine can search historical market behavior itself, discover statistically meaningful nonlinear and complex hidden patterns preceding sudden price spikes, determine which of those patterns generalize beyond the data in which they were discovered, and recognize similar or evolving structures as they begin forming in real time.

### Research Question

**Can an AI system autonomously discover previously unknown/very complex patterns in market data that precede short squeezes and use those patterns to estimate, in real time, the probability that a short squeeze is developing?**

### Tools 

The project will primarily use:

- **Python** — machine learning, deep learning, statistical analysis, experimentation, and data processing
- **C++** — performance-critical market-data processing and computation
- **SQL** — storing, querying, and analyzing large amounts of historical market data
- **PyTorch** — developing and experimenting with deep-learning models
- **NumPy/Pandas/Polars** — numerical and market-data processing
- **Scikit-learn** — statistical modeling, clustering, anomaly detection, and baseline models
- **FastAPI** — exposing the prediction and discovery system through an API
- **TypeScript (React)** — building a real-time interface for viewing discovered patterns and model predictions
- **Git (GitHub)** — version control, experiments, documentation, and project development

**This is fluid and is likely to change as the research progresses**

### Project Breakdown

- **1. Market data**: My first step would be to build a reliable dataset containing the basic observable building blocks of the market. Instead of giving SuddenSpikeAI hundreds of human-made rules or indicators, I want to give it the market's alphabet through which it discovers the words, sentences, and grammar. The goal is for the model to gradually discover relationships, sequences, and hidden patterns on its own rather than being told what to look for. This way, its approach remains fluid and dynamic, allowing it to adapt as new relationships and patterns emerge rather than being limited by fixed human-defined rules. At its absolute core, the market is surprisingly small:

* **Identity**

  * **Ticker / Security ID:** Unique identifier for the stock or security
  * **Company:** Business the security belongs to
  * **Security type:** Type of asset being traded
  * **Exchange:** Exchange where the security is listed
  * **Trading venue:** Place where the actual trade occurs
  * **Currency:** Currency used to price the security

* **Time**

  * **Date:** Calendar day of the observation
  * **Timestamp:** Exact time something happened
  * **Trading session:** Pre-market, regular market, or after-hours
  * **Market state:** Whether trading is open, closed, halted, or in auction

* **Trade**

  * **Trade price:** Price at which shares actually traded
  * **Trade size:** Number of shares traded
  * **Trade side / condition:** Information about how the trade occurred
  * **Trade venue:** Where the trade was executed

* **Quote**

  * **Bid price:** Highest price a buyer currently offers
  * **Bid size:** Shares buyers currently want at the bid
  * **Ask price:** Lowest price a seller currently accepts
  * **Ask size:** Shares sellers currently offer at the ask
  * **Quote timestamp:** Exact time the quote was recorded

* **Order Book**

  * **Order side:** Whether the order is to buy or sell
  * **Order price:** Price requested by the order
  * **Order quantity:** Number of shares requested
  * **Order timestamp:** Time the order entered or changed
  * **Order added:** New order entered the market
  * **Order modified:** Existing order was changed
  * **Order cancelled:** Order was removed without completion
  * **Order executed:** Order resulted in a trade

* **Share Supply**

  * **Shares outstanding:** Total shares the company has issued
  * **Public / tradable float:** Shares available for public trading
  * **Restricted shares:** Shares that currently cannot freely trade
  * **Insider-held shares:** Shares owned by company insiders

* **Short Selling**

  * **Shares sold short:** Shares borrowed and sold by short sellers
  * **Short interest:** Shares currently remaining short
  * **Short-sale transaction price:** Price of a short-sale trade
  * **Short-sale transaction size:** Number of shares sold short
  * **Short-sale timestamp:** Time the short sale occurred

* **Securities Lending**

  * **Shares available to borrow:** Shares currently available for shorting
  * **Shares borrowed:** Shares currently taken on loan
  * **Shares returned:** Borrowed shares given back
  * **Borrow fee / rate:** Cost of borrowing the shares
  * **Stock-loan recalls:** Lender requests borrowed shares back
  * **Failures to deliver:** Shares not delivered by settlement deadline

* **Options**

  * **Call/put:** Whether the option relates to buying or selling rights
  * **Strike price:** Price specified by the option contract
  * **Expiration date:** Date the option expires
  * **Contract multiplier:** Number of shares represented by one contract
  * **Option trade price:** Price at which the option traded
  * **Option trade size:** Number of option contracts traded
  * **Option bid price:** Highest current offer to buy the option
  * **Option bid size:** Contracts wanted at the bid
  * **Option ask price:** Lowest current offer to sell the option
  * **Option ask size:** Contracts offered at the ask
  * **Open interest:** Option contracts currently still open
  * **Trading venue:** Where the option was traded

* **Corporate Information**

  * **Financial statement values:** Reported company financial numbers
  * **Regulatory filings:** Official documents submitted to regulators
  * **Corporate announcements:** Information publicly announced by the company
  * **Earnings releases:** Reported company financial results
  * **Dividends:** Money distributed to shareholders
  * **Stock splits:** Shares divided into a different number of shares
  * **Share issuances / offerings:** New shares introduced into the market
  * **Share buybacks:** Company purchases its own shares
  * **Mergers / acquisitions:** Companies combining or purchasing one another
  * **Management changes:** Changes in company leadership

* **External Information**

  * **News text + timestamp:** Published news and when it appeared
  * **Social-media activity + timestamp:** Public online discussion and when it occurred
  * **Related-stock raw data:** Market data from connected companies
  * **ETF raw data:** Market data from relevant ETFs
  * **Market-index raw data:** Data describing the broader market
  * **Interest rates:** Current cost of borrowing money
  * **Economic releases:** Official economic data announcements
  * **Currency prices:** Exchange values between currencies
  * **Commodity prices:** Prices of resources such as oil or gold

* **Data Integrity**

  * **Data source:** Where the information came from
  * **Original event timestamp:** When the market event actually happened
  * **Data-received timestamp:** When the system received the information
  * **Missing-data flag:** Indicates information is unavailable
  * **Correction flag:** Indicates previously reported data was corrected
  * **Cancellation flag:** Indicates an event or trade was cancelled
  * **Data-quality status:** Indicates reliability of the observation
  
* **2. Extreme Spike Identification**: The system will establish a clear, objective definition of an extreme upward price spike in low-float and small-cap stocks using measurable price movement and time criteria. The cause of the movement does not matter, be it a short squeeze, news event, momentum rally, liquidity shock, options activity, or an unknown mechanism; all treated simply as spikes to help keep the target objective and prevent human explanations from influencing what the model learns.

* **3. Pattern Discovery**: The model will search historical market behavior for recurring structures that appeared before extreme spikes, but with a strict restriction: the model will not be told what a pre-spike pattern should look like. Instead, it must independently discover useful relationships, sequences, time delays, nonlinear interactions, changes in relationships, and latent representations among the market's basic observable variables. The goal is to allow the model to discover structures that may already be known, completely unknown, or too complex to have a human-defined name.

* **4. Pattern Validation**: A discovered pattern is meaningless if it only fits the data in which it was discovered. Every candidate pattern must therefore be tested against completely unseen stocks and future market periods. The system will then undergo live testing for a fixed period, in which every prediction is permanently recorded before its outcome is known. Patterns that fail to generalize will be rejected. On the other hand, patterns that remain predictive across different stocks, periods, and market conditions will be retained and used by the model to improve its predictions over time.

* **5. Extreme Spike Prediction**: Rather than producing a simple **BUY / SELL** signal, SuddenSpikeAI will describe what it believes may happen and how uncertain that belief is. Its output will include:

  * **Probability of an extreme upward spike**
  * **Likely time window**
  * **Expected magnitude range**
  * **Confidence/uncertainty**
  * **Detected hidden patterns currently forming**
  * **Strength of similarity to historically validated pre-spike states**

  The prediction should continuously change as new evidence arrives rather than remain a fixed one-time decision.

* **6. Real-Time Detection & Learning**: SuddenSpikeAI will continuously receive new market information and evaluate the evolving market state against the structures it has discovered. As relationships strengthen, disappear, or evolve, its probability estimates should update in real time. New observations will later be incorporated through controlled retraining or continual-learning cycles, allowing the system to adapt to changing market behavior while protecting previously validated knowledge from being blindly overwritten.

* **7. Evaluation**: Every prediction will be recorded before the outcome is known and later compared against what actually happened. Because extreme spikes are rare, simple overall accuracy would be misleading; a model that always predicts "no spike" could appear accurate while being useless. Evaluation will therefore focus on:

  * **Precision:** Of all predicted spikes, how many actually occurred?
  * **Recall:** Of all actual spikes, how many did the model detect?
  * **False-positive rate:** How often was a spike predicted that never occurred?
  * **False-negative rate:** How many real spikes were completely missed?
  * **Probability calibration:** When the model predicts a 70% probability, does the event occur roughly 70% of the time across many predictions?
  * **Lead time:** How early before the movement can meaningful evidence be detected?
  * **Time-window accuracy:** Did the spike occur within the predicted period?
  * **Magnitude error:** How close was the predicted price-movement range to the actual move?
  * **Out-of-sample performance:** Does the discovered knowledge work on data never used during discovery or training?
  * **Cross-stock generalization:** Can patterns learned from some stocks successfully transfer to completely unseen stocks?
  * **Regime robustness:** Do the relationships remain useful across different market environments?
  * **Pattern stability:** Do discovered patterns continue working over time or quickly disappear?
  * **Baseline comparison:** Does SuddenSpikeAI outperform simple statistical models, conventional ML approaches, and traditional human-designed indicators?
  * **Discovery value:** Does removing a newly discovered relationship measurably reduce prediction performance, providing evidence that the model found something genuinely useful?

The objective is not to prove that every extreme spike can be predicted. 

SuddenSpikeAI is ultimately an experiment built around a deeper question: **Can an AI autonomously discover hidden relationships and structures in market data that precede extreme price spikes, without being explicitly taught what patterns to look for?**

