# SaringID — one-page write-up template

> Replace every bracketed item with your team's real information and actual measured results. Do not invent numbers.

**Track:** AI + Finance

**Team:** I GUSTI NGURAH GANESHA KRISHNA

**Project:** SaringID — Indonesian SMS Scam Triage

## The problem
An Indonesian phone user may receive unexpected messages about prizes, account problems, delivery fees, loans, or promotions. They need a quick way to decide whether a message deserves extra caution, without assuming every promotion is a scam or every ordinary-looking message is safe.

## What we built
SaringID classifies a message into **Normal**, **Potential fraud**, or **Promotion**. It returns model scores, influential text features, and a safety-oriented next step. The primary user is an Indonesian smartphone user who receives unexpected SMS messages and wants help identifying potentially fraudulent messages. They would use SaringID when they receive a suspicious message about banking, digital wallets, prizes, delivery fees, or account verification.

## What we added
We extended the suggested scam-filter idea in three ways: (1) an Indonesian three-class distinction between normal messages, fraud-like messages, and promotions; (2) a fraud-alert threshold selected on validation data to emphasise recall; and (3) a separate synthetic challenge set written by our team to probe modern message patterns. The challenge set was not used for training and is not a representative national dataset.

## How it works
**Data:** Indonesian SMS Spam Dataset (`dataset_sms_spam_v1.csv`), sourced from [ksnugroho/klasifikasi-spam-sms](https://github.com/ksnugroho/klasifikasi-spam-sms). The original dataset contained 1,143 rows. After cleaning, 1,142 messages remained: 568 Normal, 335 Fraud, and 239 Promotion. We removed blank messages, invalid labels, conflicting duplicate messages, and exact-text duplicates. Labels are 0=Normal, 1=Fraud, and 2=Promotion. We used stratified sampling to split the data into 730 training messages, 183 validation messages, and 229 held-out test messages.

**Model:** TF-IDF word unigrams and bigrams plus class-weighted logistic regression. We tuned the fraud-score threshold using F2 on the validation set. The final test set was not used for tuning.

## Results

On the held-out test data (229 messages):

- Majority-class baseline: accuracy 0.498, macro-F1 0.222, fraud precision 0.000, fraud recall 0.000.
- Always-normal baseline: accuracy 0.498, macro-F1 0.222, fraud precision 0.000, fraud recall 0.000.
- SaringID: accuracy 0.917, macro-F1 0.903, fraud precision 0.831, fraud recall 0.955.

The detailed classification report shows a Fraud F1-score of 0.89. SaringID correctly identified 64 of 67 fraud messages. It incorrectly classified 13 non-fraud messages as fraud.

**Synthetic stress test:** We evaluated SaringID separately on 12 team-written Indonesian SMS examples (4 Normal, 4 Fraud, and 4 Promotion). The model achieved 66.7% accuracy and a macro F1-score of 0.68. For Fraud, precision was 0.50 and recall was 0.75. It correctly classified 8 of the 12 messages.

The model missed one fraud message about a digital wallet balance supposedly expiring that night. It also incorrectly flagged two normal messages and one legitimate promotional message as fraud. This small, synthetic challenge set is useful for probing model weaknesses, but it is not representative of real-world performance.

**Where it fails:**

- **False negative:** "GRATIS internetan 5MB berlaku utk 7 hari hanya..." — Actual label: Fraud; predicted: Promotion.
- **False positive:** "Baik Pak, berarti nanti Kamis kami ke kantor lagi" — Actual label: Normal; predicted: Fraud.

A likely limitation is that promotional language and unusual wording can confuse the classifier. The dataset may also not represent current scam language.
## What we'd do next
1. Obtain a larger, recent, human-labelled Indonesian dataset with clear permission and more diverse message sources.
2. Test performance across SMS, WhatsApp-style text, regional language mixing, and evolving scam tactics, with a human review step for uncertain messages.

## Sources

- **Dataset:** Indonesian SMS Spam Dataset — [ksnugroho/klasifikasi-spam-sms](https://github.com/ksnugroho/klasifikasi-spam-sms). Original dataset usage and licensing terms should be verified with the source.
- **Machine learning model:** [Scikit-learn TF-IDF Vectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) and [Logistic Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html).
- **Libraries:** pandas, NumPy, scikit-learn, matplotlib, and Gradio.
- **Development environment:** Google Colab.
- **AI assistance:** ChatGPT (OpenAI), used for project planning, coding guidance, debugging support, and write-up assistance.

**This project is a prototype and is not financial advice.**
