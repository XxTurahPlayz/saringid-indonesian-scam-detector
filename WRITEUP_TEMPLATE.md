# SaringID — one-page write-up template

> Replace every bracketed item with your team's real information and actual measured results. Do not invent numbers.

**Track:** AI + Finance  
**Team:** [names]  
**Project:** SaringID — Indonesian SMS Scam Triage

## The problem
An Indonesian phone user may receive unexpected messages about prizes, account problems, delivery fees, loans, or promotions. They need a quick way to decide whether a message deserves extra caution, without assuming every promotion is a scam or every ordinary-looking message is safe.

## What we built
SaringID classifies a message into **Normal**, **Potential fraud**, or **Promotion**. It returns model scores, influential text features, and a safety-oriented next step. The primary user is [specific user/persona], who would use the tool when [specific moment].

## What we added
We extended the suggested scam-filter idea in three ways: (1) an Indonesian three-class distinction between normal messages, fraud-like messages, and promotions; (2) a fraud-alert threshold selected on validation data to emphasise recall; and (3) a separate synthetic challenge set written by our team to probe modern message patterns. The challenge set was not used for training and is not a representative national dataset.

## How it works
**Data:** [dataset title and link], [number of rows after cleaning], labels 0=Normal, 1=Fraud, 2=Promotion. We removed blank messages, ambiguous conflicting duplicates, and exact duplicates. We split data into [train count] training, [validation count] validation, and [test count] held-out test examples, stratified by class.

**Model:** TF-IDF word unigrams and bigrams plus class-weighted logistic regression. We tuned the fraud-score threshold using F2 on the validation set. The final test set was not used for tuning.

## Results
On the held-out test data:
- Majority-class baseline: accuracy [ ], macro-F1 [ ], fraud precision [ ], fraud recall [ ].
- SaringID: accuracy [ ], macro-F1 [ ], fraud precision [ ], fraud recall [ ].
- Synthetic stress test: [report separately; do not combine with the held-out test score].

**Where it fails:** [show one false negative and one false positive from the held-out test set]. A likely reason is [careful hypothesis]. The dataset is older and may not represent current scam language; the model can also mistake legitimate promotions for fraud or miss new scam formats.

## What we'd do next
1. Obtain a larger, recent, human-labelled Indonesian dataset with clear permission and more diverse message sources.
2. Test performance across SMS, WhatsApp-style text, regional language mixing, and evolving scam tactics, with a human review step for uncertain messages.

## Sources
- Dataset: [exact link and licence/permission evidence]
- Model: scikit-learn TF-IDF + LogisticRegression documentation
- Libraries: pandas, scikit-learn, matplotlib, Gradio
- AI tools used: [list all tools, including ChatGPT if used]

**This project is a prototype and is not financial advice.**
