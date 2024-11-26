---
description: An overview of how Paradex's unique continuous funding mechanism works
---

# 💰 Funding Mechanism

## Mechanism

The funding mechanism calculates the funding PnL for each open perpetual position. This PnL is realised when the position size changes after a trade.

The accrued funding contributes to the total unrealized PnL (hence to the account value). The accrued funding PnL is calculated in USDC (settlement asset).\
\
In order to reduce on-chain transaction spikes, Paradex has a continuous accrual mechanism. Funding is continuously accrued on an account with a perpetual futures position and the entire unrealized funding PnL of that account's position is settles every time the position is adjusted on-chain.

### Funding Premium

At a given time **t**, the **Funding Premium** represents the 8h amount paid by long positions to short positions. This value expressed in the settlement asset of the instrument (**USDC**) and depends on the Funding Rate using the relationship :

$$
\small \text{Funding~Premium}=\text{Funding~Rate}*\frac{\text{Spot Oracle Price}}{\text{USDC Oracle Price}}
$$

### Funding Rate

The **Funding Rate** is derived from [**Fair Basis**](mark-price-calculation.md#steps-to-calculate-the-fair-basis-and-the-mark-price) by applying interest rate clamping and by constraining the resulting value to the interval \[ − 𝑀 , + 𝑀 ] where M is the Maximum Funding Rate.

$$
\text{Funding Rate}=\text{capped}\big(\text{Fair Basis} + \text{clamp}\big(\text{Interest Rate}, \text{Fair Basis}, \text{Clamp Rate}\big)\big)
$$

and

$$
\text{clamp}\big(\text{Interest Rate}, \text{Fair Basis}, \text{Clamp Rate}\big) =\\~~~~~~~~~\min\big(\max\big(\text{Interest Rate}-\text{Fair Basis},~-\text{Clamp Rate}\big),~~+\text{Clamp Rate}\big)
$$

$$
\text{capped}\big(x\big) = \text{max}(−\text{Maximum Funding Rate}, \text{min}(x, \text{Maximum Funding Rate}))
$$

Current values for the above settings are:

* Interest Rate = 0.01%
* Clamp Rate = 0.05%
* Maximum Funding Rate = 0.05

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

### Funding Index

At a global level, a **Funding Index** calculates accrued funding for 1 unit of the asset since launch and is calculated as a time-weighted sum of the Funding Premium :

$$
\text{Funding Index (current timestamp)}=\int_{\text{launch timestamp}}^{\text{current timestamp}}\text{Funding Premium(t) dt}
$$

The **Funding Premium** is updated along with the mark price (every 5 seconds). This triggers an update of the funding index. The Funding Premium corresponds to the USDC amount paid by 1 unit of the contract continuously after **8h** if the prices remain unchanged.

At any point in time, the **Current Funding Index** can be calculated as :

$$
\text{Current Funding Index}=\text{Last Cached Funding Index}\\+\text{Funding Premium}*\frac{\text{current timestamp}-\text{cached timestamp}}{8*3600}
$$

where timestamps are expressed in seconds.

### Accrued Funding

The **Accrued (Unrealized) Funding** of an open perpetual position depends on the change in the funding index since its last cached value (from last trade) :

$$
\text{Accrued Funding PnL}=-\text{Perpetual Position Size}\\*~(\text{Current Funding Index - Cached Funding Index})*\text{USDC Oracle Price}
$$

where **Perpetual Position Size** is a signed position size (positive in case of a long position, negative in case of short position)

Whenever the account updates an existing perpetual position, accrued funding is realised :

$$
\text{Funding Realized PnL}=-\text{Previous Perpetual Position Size}\\*~(\text{Current Funding Index - Cached Funding Index})
$$

## **Example**

* Initial market data at time $$t_0$$ :

$$\text{Funding Index}_\text{ XYZ-USD-PERP}(t_0)=1'000~\text{USDC}$$

$$\text{Mark Price}_\text{ XYZ-USD-PERP}(t_0)=112$$

$$\text{XYZ Oracle Price}(t_0)=100$$

$$\text{USDC Oracle Price}=1$$

Therefore : $$\text{Funding Premium}_\text{ XYZ-USD-PERP}(t_0)=\frac{\text{Mark~Price}~-~\text{Spot~Oracle~Price}}{\text{USDC Oracle Price}}=12~\text{USDC}$$

* Alice enters a long position of size 50 XYZ-USD-PERP at $$t_0$$
* For example simplicity, we assume prices stay unchanged for 1 hour, i.e. the Funding Premium remains the same :

$$
\begin{split} \text{Funding Index}_\text{ XYZ-USD-PERP}(t_0+1~\text{hour} )&=\text{Funding Index}_\text{ XYZ-USD-PERP}(t_0 )\\ &~+\frac{1}{8}*\text{Funding Premium}_\text{ XYZ-USD-PERP}(t_0)\\ &=1’000+\frac{12}{8}\\ &=1’001.5~\text{USDC} \end{split}
$$

Within the past hour, Alice accrued a **Funding Loss** equal to : $$50*(1'001.5-1'000.0)=75~\text{USDC}$$

Note that this negative PnL affects Alice's account value but is not reflected in the USDC balance until Alice's next $$\text{XYZ-USD-PERP}$$ trade.

* Exactly at $$t_0+1~\text{hour}$$, XYZ-USD-PERP Mark Price jumps to $$118$$. However, XYZ Spot Oracle Price remains unchanged. The funding premium now increases to $$18~\text{USDC}$$
*   Assuming prices do not change during the next 2 hours (i.e. until $$t_0+3~\text{hours}$$), the funding index becomes : $$\text{Funding Index}_\text{XYZ-USD-PERP}(t_0+3~\text{hours})=1'001.5+\frac{2*18}{8}=1'006~\text{USDC}$$

    Alice's funding loss increases to $$50*(1'006-1'000.0)=300~\text{USDC}$$
* Alice decides to increase the long position size by successfully submitting a market order. This results in the previous accrued funding loss of 300 USDC to be realized (i.e. USDC balance is debited by 300) and accrued funding to be reset to zero.