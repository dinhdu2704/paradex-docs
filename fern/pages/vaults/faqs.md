---
icon: question
---

# FAQs

<details>

<summary><strong>Can anyone create a Vault?</strong></summary>

Currently, individual users are not able to create a vault or become a vault owner on Paradex. This feature will be coming soon, so stay tuned for more information!

</details>

<details>

<summary>What is the difference between a vault owner and a vault operator?</summary>

A vault owner is the account that controls the vault and receives a share of the profits. A vault operator is a specialized account that has access to the deposited funds and is responsible for trading to generate returns.

</details>

<details>

<summary>How are profits distributed in a vault?</summary>

Profits are distributed based on the vault's profit share structure. A percentage goes to the vault owner, while the rest is distributed among depositors proportional to their share in the vault.

</details>

<details>

<summary>What is the minimum owner share?</summary>

The minimum owner share is the percentage of the vault that must be maintained by the vault owner. This ensures the owner has "skin in the game" and aligns their interests with other depositors.

</details>

<details>

<summary>How long after my deposit can I withdraw my funds?</summary>

Because withdrawal transactions cannot be performed in the same block as a deposit, there is currently around a **5 minute** window where you will not be able to withdraw fund immediately after deposit. This is the time that is required to created this new block for the withdrawal transaction.\
\
Otherwise, the time is also limited by the [Lockup Period](https://docs.paradex.trade/vaults/tutorials/withdrawal#note-you-will-not-be-able-to-withdraw-from-the-vault-if-your-minimum-lockup-period-of-not-over-yet) that is configured for the Vault. This can be found just above the Deposit button with the other Vault status.

</details>

<details>

<summary>How is the performance of a vault calculated?</summary>

Vault performance is calculated based on the change in the vault's total value over time. This includes trading profits, losses, and any fees incurred.

</details>

<details>

<summary>Are there any fees associated with using vaults?</summary>

Fees may vary depending on the specific vault. Typically, there's a profit share for the vault owner. Always check the vault's details for specific fee information.

</details>

<details>

<summary>How secure are Paradex Vaults?</summary>

Paradex Vaults are built with robust security measures, including role-based access control and multi-signature approvals. However, as with any DeFi product, there are inherent risks, and users should do their own research before participating.

</details>

<details>

<summary>How can I monitor my vault's performance?</summary>

Paradex provides detailed analytics for vault operations. You can see an overview from your Portfolio and also get a more detailed analysis by clicking on the vault from the [main vaults page](https://app.paradex.trade/vaults).

</details>

<details>

<summary>Will I gain any points from depositing funds into Vaults?</summary>

Yes, points will be awarded to your account on a Weekly basis. Deposit in Vaults with an active points boost for higher points earn.

</details>

<details>

<summary>How can my vault's PnL be positive but its ROI is negative? (or vice-versa)</summary>

This can happen since the value calculated for the return is independent from TVL for vaults since you can modify the size of your investment.  If, for example, the vault performs very well when you have a small amount invested and then performs poorly when you have a large amount invested, the resulting ROI and PnL would not necessarily both be positive or both negative.\
\
If  V is equal the vault value at a given time, the return between the start and end of the day (R) is calculated by the following formula:

$$R=(V_{end} - V_{start})/V_{start}$$ &#x20;

For multiple caluculated returns, we can calculate the cumulative return (C) after a givne number of evaluations (x):

$$C= (1+R_1)*(1+R_2)*\dots(1+R_x) -1$$



**Example:**

Let's say that you decide to invest $100 in some vault (Day 0).&#x20;

* On Day 1 it goes up to $110 :
  * PnL is $10
  * ROI for Day 1: $$(110 - 100)/100 = .1$$ or +10%
* On Day 2 it goes up by another $10 to $120:
  * PnL is now $20
  * ROI for Day 2: $$(120 - 110)/110 = 0.091$$ or + 9%
  *   **Cumulative ROI:** $$(1+0.1)*(1+0.091)-1\approx 0.2$$ or 20%


* On Day 3 we add $900 to the portfolio and it ends the day with a $150 **loss** :scream:
  * PnL drops to -$130
  * ROI for Day 3: $$(870 - 1020)/1020 = -0.15$$ or -15%
  * **Cumulative ROI:** $$(1+0.1)*(1+0.091)*(1+(-0.15)) -1\approx0.02$$ or 2%

So, after Day 3, you would see a negative PnL of <mark style="color:red;">-$130</mark> but a positive ROI of 2%

</details>