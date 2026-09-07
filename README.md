# Mobile Money Fraud Detection

A machine learning model that detects fraudulent transactions in a mobile money system — the kind of platform MTN MoMo, Airtel Money, and similar services run across Rwanda and much of Africa, where mobile money often handles more transaction volume than traditional banking.

## Why this matters

Mobile money fraud is a real, high-stakes problem that's underrepresented in typical machine learning portfolios, most of which default to Western financial datasets (credit cards, bank transfers). Mobile money transactions are often instant and difficult to reverse, making fraud detection especially valuable in this context.

## Why synthetic data

Real mobile money transaction data is never publicly released, for obvious privacy and security reasons — this is standard practice across fraud detection research. Even well-known published fraud detection datasets (such as PaySim) are synthetic simulations designed to mirror real transaction behavior rather than real logs. This project follows the same approach: a synthetic dataset was generated with a realistic fraud pattern deliberately built in — compromised accounts being rapidly drained through transfers or cash-outs — while keeping the overall fraud rate low (~1.5%), matching the heavy class imbalance seen in real-world fraud detection.

## What it does

The model classifies each transaction as fraudulent or normal based on features including transaction type, amount, balance before and after the transaction, and time of day. A key engineered feature, the balance-drained ratio (how much of an account's balance was emptied in a single transaction), turned out to be the strongest predictor of fraud.

## Results

The model achieves approximately 88% recall (catching most actual fraud) with 32% precision, and a ROC-AUC of 0.98. The precision/recall trade-off here is deliberate and realistic: in fraud detection, missing real fraud is typically far more costly than investigating a false alarm, so the model is tuned to prioritize catching fraud even at the cost of some false positives.

## Tech stack

Python, scikit-learn (Random Forest), pandas, NumPy, matplotlib, seaborn, Jupyter Notebook.

## Files

- `mobile_money_fraud_detection.ipynb` — full pipeline: synthetic data generation, feature engineering, model training, evaluation, and a transaction-scoring function

## Next steps

Real-world extensions include incorporating velocity features (transaction frequency and volume per account over time, which require transaction history this simplified dataset doesn't model), wrapping the scoring function in a real-time API for live transaction pipelines, and — if paired with the explainable credit risk classifier's SHAP approach — adding per-transaction explanations to help fraud investigators understand exactly why a transaction was flagged. This also has direct relevance to HURO Africa, should the platform ever process payments directly.
