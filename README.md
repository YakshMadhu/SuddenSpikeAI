# SuddenSpikeAI

### The Premise

The stock market has always been a source of curiosity for me because of its inherent unpredictability. There is no perfect formula that can consistently explain what a stock will do next. At the simplest level, a price can rise, fall, or remain relatively unchanged, yet behind those movements are countless interacting variables: price and volume behavior, liquidity, short interest, options activity, market sentiment, company fundamentals, macroeconomic conditions, news, human behavior, and more.

Many of these factors can be measured, while others may be difficult to observe, poorly understood, or hidden within complex relationships between variables. Even when two market situations appear almost identical according to everything we can measure, their outcomes can still be completely different.

This led me to a broader hypothesis:

**There may be patterns, interactions, sequences, or sources of uncertainty within market data that we have not yet discovered or learned how to represent.**

One particularly interesting example of this unpredictability is the **sudden extreme upward price spike**, especially in low-float and small-cap stocks. Within a short period of time, a stock can experience an unusually large upward movement. Such spikes may be connected to short squeezes, news, momentum, options activity, liquidity changes, shifts in market attention, combinations of several factors, or mechanisms that are not immediately obvious.

For this project, however, the human-defined explanation behind the movement is not the primary concern.

**A spike is treated as a spike regardless of what caused it.**

This raises a more interesting possibility:

 **What if there are combinations, sequences, relationships, or precursor structures hidden within market data that repeatedly appear before extreme price spikes but have never been explicitly identified by humans?**

Rather than manually defining what a pre-spike setup should look like, SuddenSpikeAI will explore whether a machine can search historical market behavior itself, discover statistically meaningful nonlinear and complex structures preceding extreme upward movements, determine which discoveries generalize beyond the data in which they were found, and recognize similar or evolving structures as they begin forming in real time.

---

## Research Question

**Can an AI system autonomously discover previously unknown or highly complex structures in market data that precede sudden extreme upward price spikes in low-float and small-cap stocks, and recognize those structures as they begin forming in real time?**

At a deeper level, the project asks:

**Can machines discover useful knowledge that we did not explicitly teach them to look for?**

---

## Tools

The project will primarily use:

* **Python** — machine learning, deep learning, statistical analysis, experimentation, and data processing
* **PyTorch** — developing and experimenting with deep-learning models
* **Scikit-learn** — baseline models, clustering, anomaly detection, and statistical experimentation
* **NumPy / Pandas / Polars** — numerical and market-data processing
* **C++** — performance-critical numerical and market-data processing
* **Go** — concurrent real-time market-data ingestion and streaming services
* **SQL** — storing, querying, and analyzing historical and processed market data
* **FastAPI** — exposing the discovery and prediction system through an API
* **JavaScript + React** — building a real-time interface for viewing predictions and discovered patterns
* **Git / GitHub** — version control, experiments, documentation, and project development

**This technology stack is fluid and may change as the research progresses.**

---

# Project Breakdown

## 1. Market Data

The first step will be to build a reliable dataset containing the basic observable building blocks of the market.

Instead of giving SuddenSpikeAI hundreds of human-made rules and indicators, I want to give it the market's **alphabet** and allow it to discover the words, sentences, and grammar itself.

The goal is for the model to gradually discover relationships, sequences, and hidden structures rather than being told exactly what to look for. This keeps its approach fluid and dynamic rather than limiting it to fixed human-defined rules.

At its absolute core, the market is surprisingly small:

### Identity

* **Ticker / Security ID:** Unique identifier for the stock or security
* **Company:** Business the security belongs to
* **Security type:** Type of asset being traded
* **Exchange:** Exchange where the security is listed
* **Trading venue:** Place where market activity occurs
* **Currency:** Currency used to price the security

### Time

* **Date:** Calendar day of the observation
* **Timestamp:** Exact time something happened
* **Trading session:** Pre-market, regular market, or after-hours
* **Market state:** Whether trading is open, closed, halted, or in auction

### Trade

* **Trade price:** Price at which shares actually traded
* **Trade size:** Number of shares traded
* **Trade side / condition:** Information about how the trade occurred
* **Trade venue:** Where the trade was executed

### Quote

* **Bid price:** Highest price a buyer currently offers
* **Bid size:** Shares buyers currently want at the bid
* **Ask price:** Lowest price a seller currently accepts
* **Ask size:** Shares sellers currently offer at the ask
* **Quote timestamp:** Exact time the quote was recorded

### Order Book

* **Order side:** Whether the order is to buy or sell
* **Order price:** Price requested by the order
* **Order quantity:** Number of shares requested
* **Order timestamp:** Time the order entered or changed
* **Order added:** New order entered the market
* **Order modified:** Existing order was changed
* **Order cancelled:** Order was removed without completion
* **Order executed:** Order resulted in a trade

### Share Supply

* **Shares outstanding:** Total shares the company has issued
* **Public / tradable float:** Shares available for public trading
* **Restricted shares:** Shares that cannot currently trade freely
* **Insider-held shares:** Shares owned by company insiders

### Short Selling

* **Shares sold short:** Shares borrowed and sold by short sellers
* **Short interest:** Shares currently remaining short
* **Short-sale transaction price:** Price of a short-sale trade
* **Short-sale transaction size:** Number of shares sold short
* **Short-sale timestamp:** Time the short sale occurred

### Securities Lending

* **Shares available to borrow:** Shares currently available for shorting
* **Shares borrowed:** Shares currently taken on loan
* **Shares returned:** Borrowed shares given back
* **Borrow fee / rate:** Cost of borrowing the shares
* **Stock-loan recalls:** Lender requests borrowed shares back
* **Failures to deliver:** Shares not delivered by the settlement deadline

### Options

* **Call / put:** Type of option contract
* **Strike price:** Price specified by the contract
* **Expiration date:** Date the option expires
* **Contract multiplier:** Shares represented by one contract
* **Option trade price:** Price at which the option traded
* **Option trade size:** Number of contracts traded
* **Option bid price:** Highest current offer to buy the option
* **Option bid size:** Contracts wanted at the bid
* **Option ask price:** Lowest current offer to sell the option
* **Option ask size:** Contracts offered at the ask
* **Open interest:** Contracts currently remaining open
* **Trading venue:** Where the option was traded

### Corporate Information

* **Financial statement values:** Reported company financial numbers
* **Regulatory filings:** Official documents submitted to regulators
* **Corporate announcements:** Information released by the company
* **Earnings releases:** Reported company financial results
* **Dividends:** Money distributed to shareholders
* **Stock splits:** Changes in the number of shares
* **Share issuances / offerings:** New shares introduced into the market
* **Share buybacks:** Company purchases its own shares
* **Mergers / acquisitions:** Companies combining or purchasing one another
* **Management changes:** Changes in company leadership

### External Information

* **News text + timestamp:** Published information and when it appeared
* **Social-media activity + timestamp:** Public online discussion and when it occurred
* **Related-stock raw data:** Market information from related companies
* **ETF raw data:** Market information from relevant ETFs
* **Market-index raw data:** Information describing the broader market
* **Interest rates:** Current borrowing rates
* **Economic releases:** Official economic announcements
* **Currency prices:** Exchange values between currencies
* **Commodity prices:** Prices of resources such as oil or gold

### Data Integrity

* **Data source:** Where the information came from
* **Original event timestamp:** When the event actually occurred
* **Data-received timestamp:** When SuddenSpikeAI received the information
* **Missing-data flag:** Indicates unavailable information
* **Correction flag:** Indicates previously reported data was corrected
* **Cancellation flag:** Indicates an event or trade was cancelled
* **Data-quality status:** Indicates reliability of the observation

Human-designed indicators such as RSI, MACD, squeeze scores, momentum scores, relative volume, days to cover, and similar derived interpretations will not form the foundation of the system when their underlying observations are available.

The philosophy is simple:

> **Give the model the letters and investigate whether it can discover the words, sentences, and grammar itself.**

---

## 2. Representation Discovery

Before discovering complete pre-spike patterns, SuddenSpikeAI must first learn useful ways of representing the raw market.

The model may discover that individual observations are less meaningful than relationships between them, their rates of change, their order through time, or combinations involving many variables simultaneously.

Rather than manually defining every useful feature, the system should be capable of learning internal representations from the market alphabet itself.

Conceptually:

**Raw observations → relationships → temporal relationships → higher-order representations**

These learned representations may correspond to concepts humans already understand, or they may represent structures that do not currently have a human-defined name.

---

## 3. Extreme Spike Identification

The system will establish a clear and objective definition of an **extreme upward price spike** using measurable price movement and time criteria.

Conceptually:

`Price increase ≥ X% within ≤ Y time`

The exact thresholds will be determined experimentally rather than chosen arbitrarily.

The cause of the movement does not matter. Whether the event resulted from a short squeeze, news, momentum, liquidity, options activity, market attention, several interacting mechanisms, or an unknown cause, it will be treated as an extreme spike.

This keeps the prediction target objective and prevents human explanations from determining what the model is allowed to discover.

---

## 4. Pattern Discovery

The model will search historical market behavior for recurring structures that appeared **before extreme spikes**.

A strict restriction will remain in place:

> **The model will not be told what a pre-spike pattern should look like.**

Instead, it must independently search for:

* Relationships between variables
* Nonlinear interactions
* Sequences of events
* Time-delayed relationships
* Changes in relationships over time
* Multi-variable interactions
* Multi-timescale structures
* Latent representations
* Recurring market states

A useful structure may look nothing like a traditional technical indicator.

For example, the important information may not simply be:

`A + B + C`

but instead something closer to:

`A changes → B responds later → relationship between C and D changes → E accelerates → spike probability increases.

The goal is to discover structures that may be known, completely unknown, or too complex to have a human-defined name.

Discovered patterns will be stored together with information about when they were discovered, which data supported them, their validation performance, and the model version that discovered them.

---

## 5. Pattern Validation

A discovered pattern is meaningless if it only happens to fit the historical data in which it was found.

Every candidate pattern must therefore be tested against **completely unseen market periods and stocks**.

Historical data will be separated chronologically so that information from the future cannot leak into the model's past.

The system will also undergo live forward-testing for a fixed period in which every prediction is recorded **before its outcome is known**.

Patterns that fail to generalize will be rejected.

Patterns that remain predictive across different stocks, time periods, and market conditions will be retained and used to improve future versions of the model.

The system must also be capable of effectively saying:

**"I previously believed this relationship mattered, but new evidence suggests that it does not."**

Rejecting false discoveries is just as important as finding new ones.

---

## 6. Cross-Stock Generalization

One of the strongest tests of whether SuddenSpikeAI has discovered useful market knowledge will be whether that knowledge transfers to stocks the model has **never encountered before**.

The experimental structure will therefore separate stocks into groups such as:

**Discovery Stocks → Validation Stocks → Completely Unseen Test Stocks**

A pattern discovered from one group of stocks should not be considered broadly useful simply because it predicts those same stocks.

SuddenSpikeAI should eventually be able to analyze a completely unseen stock, recognize whether previously discovered structures are beginning to form, and estimate the probability of an extreme upward spike.

If knowledge discovered from one part of the market successfully transfers to another, this provides stronger evidence that the model learned something about the underlying phenomenon rather than memorizing ticker-specific behavior.

---

## 7. Extreme Spike Prediction

Rather than producing a simple **BUY / SELL** signal, SuddenSpikeAI will describe what it believes may happen and how uncertain that belief is.

Its output will include:

* **Probability of an extreme upward spike**
* **Likely time window**
* **Expected magnitude range**
* **Confidence/uncertainty**
* **Detected hidden structures currently forming**
* **Similarity to historically validated pre-spike states**

Predictions should update as new evidence arrives rather than remain fixed one-time decisions.

The system is not intended to claim:

**"This stock will spike."**

Instead, it should estimate something closer to:

**"Given the information currently observable, how strongly does this market state resemble structures that historically preceded extreme spikes?"**

---

## 8. Real-Time Detection & Learning

SuddenSpikeAI will continuously receive new market information and evaluate the evolving state of each stock against the structures it has discovered.

As relationships strengthen, disappear, or evolve, its probability estimates should update in real time.

However, the production model should not blindly rewrite itself after every new observation.

Instead, learning will occur through controlled model versions:

**Model v1 → collect new data → evaluate → retrain → validate → Model v2**

This allows SuddenSpikeAI to adapt to changing market behavior while preserving reproducibility and preventing useful previously learned knowledge from being unintentionally destroyed.

Each model version and its discoveries will be tracked independently.

---

## 9. Evaluation

Every prediction will be permanently recorded **before the outcome is known** and later compared against what actually happened.

Because extreme spikes are rare, simple overall accuracy would be misleading. A model that predicts **"no spike"** every time could appear highly accurate while being completely useless.

Evaluation will therefore focus on:

* **Precision:** Of all predicted spikes, how many actually occurred?
* **Recall:** Of all actual spikes, how many did the model detect?
* **False-positive rate:** How often was a spike predicted that never occurred?
* **False-negative rate:** How many real spikes were completely missed?
* **Probability calibration:** When the model predicts a 70% probability, does the event occur roughly 70% of the time across many predictions?
* **Lead time:** How early before the movement can meaningful evidence be detected?
* **Time-window accuracy:** Did the spike occur inside the predicted period?
* **Magnitude error:** How close was the expected movement range to the actual movement?
* **Out-of-sample performance:** Does the discovered knowledge work on data never used during training or discovery?
* **Cross-stock generalization:** Does knowledge learned from some stocks transfer to completely unseen stocks?
* **Regime robustness:** Do discovered relationships survive different market environments?
* **Pattern stability:** Do discovered structures remain useful over time or quickly disappear?
* **Baseline comparison:** Does SuddenSpikeAI outperform simpler statistical models, conventional machine-learning approaches, and traditional human-designed indicators?
* **Discovery value:** Does removing a discovered representation or relationship measurably reduce prediction performance?
* **Reproducibility:** Can the same experiment be repeated and produce comparable conclusions?

Simple baseline models will be created before increasingly complex deep-learning systems are introduced. A more complicated model will only be considered an improvement if it provides measurable value beyond simpler approaches.

Live predictions will include information such as:

`Timestamp → Ticker → Model Version → Spike Probability → Time Window → Magnitude Range → Confidence`

Once recorded, predictions will not be changed after the outcome becomes known.

---

## Final Objective

The objective of SuddenSpikeAI is **not to prove that every extreme price spike can be predicted**, nor is it simply to create another stock-trading indicator.

The project is an experiment in autonomous discovery.

The immediate question is:

**Can an AI autonomously discover hidden relationships and structures in market data that precede extreme upward price spikes, without being explicitly taught what patterns to look for?**

The broader question behind the entire project is:

**Can machines discover useful knowledge that we did not explicitly teach them to look for?**
