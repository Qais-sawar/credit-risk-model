# Credit Risk Model: Predicting Loan Defaults

In my Standard Chartered credit analyst simulation I assessed one company's credit risk by hand. Banks also have to do this for thousands of borrowers at once, so this project builds a simple credit scoring model in Python on the German Credit dataset: 1,000 real loans from a German bank, each labelled as repaid or defaulted.

## What the notebook covers

1. Default rates for different types of borrower (current account balance, credit history, savings, loan length, age)
2. A logistic regression model giving each borrower a probability of default (PD), trained on 70% of loans and tested on the other 30%
3. Model accuracy: AUC and Gini, compared with a simple model using only the current account balance
4. Score bands: whether higher-risk bands actually defaulted more
5. Expected loss on the portfolio: PD × LGD × EAD, with a 45% LGD
6. Choosing an approval cut-off when approving a bad loan costs 5 times as much as rejecting a good one

I left out sex and foreign worker status, because UK lenders can't base decisions on protected characteristics.

## Results

| Measure | Value |
|---|---|
| Default rate (all loans) | 30.0% |
| AUC / Gini (full model) | 0.80 / 0.59 |
| AUC / Gini (current account only) | 0.72 / 0.45 |
| Default rate, two safest bands (A, B) | 11.7%, 8.3% |
| Default rate, riskiest band E | 66.7% |
| Expected loss (300 test loans) | 166,273 DM (16.1% of 1,030,647 DM exposure) |
| Lowest-cost cut-off | approve if PD < 0.20: approves 44% of applicants, 9.8% of whom default |

## What I found

- The model separated good and bad borrowers well: an AUC of 0.80 on loans it had never seen, compared with 0.72 using the current account balance alone.
- The risk bands mostly ranked correctly. The riskiest band defaulted 66.7% of the time against about 10% for the two safest, though band A (11.7%) defaulted slightly more than band B (8.3%), probably because each band only has 60 loans.
- The riskiest band held 29% of the money lent but 56% of the expected loss, so a small group of loans carries most of the risk.
- Because a bad loan costs 5 times a rejected good one, the cheapest cut-off was strict: approving only 44% of applicants, but cutting the default rate among approved loans from 30% to 9.8%.
- Some results looked backwards: borrowers with no current account and with a "critical" credit history were rated safer. This is likely because the bank only approved those people when other things about them were strong, which shows the bias of only seeing approved loans.

## Limitations

- 1,000 loans from one German bank, collected decades ago
- The bank only knows the outcome of loans it approved, so the model learns from a biased sample
- The 45% LGD is a regulatory assumption, not measured from the data
- No information about the economy, so the PDs don't rise in a recession
- Only 300 test loans, so the results would move a little with a different split
- Other features (like age or job) can still be linked to protected characteristics

## How to run

Open `Credit_Risk_Model.ipynb` in Google Colab and click Runtime > Run all. It downloads the data from OpenML automatically.

Data: Statlog (German Credit Data), UCI Machine Learning Repository, via OpenML (`credit-g`).

Python, pandas, scikit-learn, matplotlib.
