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

On the held-out test data (229 messages):

- Majority-class baseline: accuracy 0.498, macro-F1 0.222, fraud precision 0.000, fraud recall 0.000.
- Always-normal baseline: accuracy 0.498, macro-F1 0.222, fraud precision 0.000, fraud recall 0.000.
- SaringID: accuracy 0.917, macro-F1 0.903, fraud precision 0.831, fraud recall 0.955.

The detailed classification report shows a Fraud F1-score of 0.89. The confusion matrix shows that SaringID correctly identified 64 of 67 fraud messages. It incorrectly classified 13 non-fraud messages as fraud.

**Synthetic stress test:** [Add the actual results from the synthetic challenge set separately.]

**Where it fails:** [Add one real false positive and one real false negative from the held-out test set.] A likely limitation is that legitimate promotional messages can resemble scam messages. The dataset may also not represent current scam language.

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
