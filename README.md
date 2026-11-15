# SaringID — Indonesian SMS Scam Triage

**Track:** AI + Finance  
**Status:** Hackathon prototype / research demonstration

SaringID is an experimental prototype that analyses Indonesian SMS messages and classifies them into three categories:

- **Normal**
- **Potential fraud**
- **Promotion**

It uses TF-IDF text features and a class-weighted Logistic Regression classifier. A fraud-alert threshold is selected using validation data.

The notebook includes model training, held-out testing, baseline comparison, error analysis, a synthetic stress test, influential text-feature inspection, and a Gradio demonstration.

## Important safety note

SaringID is an experimental prototype, not a financial-security product or a guarantee that a message is safe. A model score is not proof of fraud or legitimacy.

Never use this tool as the sole reason to click a link, transfer money, disclose an OTP/PIN/password, or block a legitimate sender. Verify unexpected claims through the organisation's official app or a phone number you already trust.

**Privacy:** Do not paste private messages or personal information into a public demo. Use synthetic examples for demonstrations.

## Repository contents

- `SaringID_Hackathon.ipynb` — End-to-end notebook containing data loading, preprocessing, model training, threshold selection, evaluation, error analysis, synthetic stress testing, and the Gradio demo.
- `WRITEUP.md` — Project write-up, methodology, results, limitations, and sources.
- `requirements.txt` — Python dependencies.
- `LICENSE_NOTE.txt` — Dataset licensing and usage notice.

## Run the notebook

### Option A: Google Colab (easiest)

1. Open `SaringID_Hackathon.ipynb` in this repository.
2. Download the notebook or use the available Open in Colab option.
3. Upload it to [Google Colab](https://colab.research.google.com/) if necessary.
4. Run the cells from top to bottom.

### Option B: Local Jupyter

Use Python 3.10 or newer and install the dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook with Jupyter Notebook or JupyterLab and run all cells from top to bottom.

## Data and reproducibility

The notebook loads the Indonesian SMS dataset from the raw CSV URL embedded in the notebook. The dataset source is [ksnugroho/klasifikasi-spam-sms](https://github.com/ksnugroho/klasifikasi-spam-sms).

The notebook expects columns named `teks` and `label`, with the mapping `0 = Normal`, `1 = Fraud`, and `2 = Promotion`.

The notebook uses stratified train, validation, and test splits. The fraud-alert threshold is tuned using validation data, while the held-out test set is reserved for final evaluation.

The hand-written stress-test examples are synthetic and are not a representative national benchmark. Check the original dataset's usage terms before redistribution or public deployment.

## Evaluation results

On the held-out test set of 229 messages:

- **Accuracy:** 91.7%
- **Macro F1-score:** 0.903
- **Fraud precision:** 83.1%
- **Fraud recall:** 95.5%

On the separate 12-message synthetic stress test:

- **Accuracy:** 66.7%
- **Macro F1-score:** 0.68

These results are limited to the evaluated datasets and do not establish real-world scam-detection performance.

## Credits

- **Dataset:** [Indonesian SMS Spam Dataset](https://github.com/ksnugroho/klasifikasi-spam-sms). Verify original usage terms before redistribution.
- **Machine learning:** Scikit-learn TF-IDF Vectorizer and Logistic Regression.
- **Libraries:** pandas, NumPy, scikit-learn, matplotlib, and Gradio.
- **Development environment:** Google Colab.
- **AI assistance:** ChatGPT (OpenAI), used for project planning, coding guidance, debugging support, and write-up assistance.

**SaringID is an educational prototype and is not financial advice.**
