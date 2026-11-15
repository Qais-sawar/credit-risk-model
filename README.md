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
| Default rate (all loans) | [ ]% |
| AUC / Gini (full model) | [ ] / [ ] |
| AUC / Gini (current account only) | [ ] / [ ] |
| Default rate, safest band A | [ ]% |
| Default rate, riskiest band E | [ ]% |
| Expected loss (test loans) | [ ] DM ([ ]% of exposure) |
| Lowest-cost cut-off | approve if PD < [ ], approving [ ]% of applicants |

## What I found

- [ ]
- [ ]
- [ ]

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
