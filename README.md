# SaringID — Indonesian SMS Scam Triage

**Track:** AI + Finance  
**Status:** Hackathon prototype / research demonstration

SaringID is a prototype that analyses an Indonesian SMS and assigns class scores for:
- **Normal**
- **Potential fraud**
- **Promotion**

It uses TF-IDF text features and a class-weighted logistic-regression classifier. A fraud-alert threshold is selected using validation data. The notebook also includes a held-out test evaluation, error inspection, a small synthetic stress-test set, influential text-feature inspection, and a Gradio demo.

## Important safety note

SaringID is an experimental prototype, not a financial-security product or a guarantee that a message is safe. A model score is not proof of fraud or legitimacy. Never use this tool as the sole reason to click a link, transfer money, disclose an OTP/PIN/password, or block a legitimate sender. Verify unexpected claims through the organisation's official app or a phone number you already trust.

**Privacy:** Do not paste private messages or personal information into a public demo. Use synthetic examples for demonstrations.

## Repository contents

- `SaringID_Hackathon_Starter.ipynb` — end-to-end notebook: data loading, preprocessing, model training, threshold selection, evaluation, error analysis, synthetic stress test, and Gradio demo.
- `WRITEUP_TEMPLATE.md` — editable project write-up template.

## Run the notebook

### Option A: Google Colab (easiest)
1. Open the notebook file in this repository.
2. In GitHub, select **Open in Colab** if available, or download the notebook and upload it to [Google Colab](https://colab.research.google.com/).
3. Run the cells from top to bottom.
4. Review the outputs and replace any placeholders in the write-up with results from your own run.

### Option B: Local Jupyter
Use Python 3.10 or newer, then install the dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook with Jupyter Notebook or JupyterLab and run all cells from top to bottom.

## Data and reproducibility

The notebook currently loads the Indonesian SMS dataset from the raw CSV URL embedded in the notebook. Inspect the source and its terms before redistribution or public deployment. The notebook expects columns named `teks` and `label`, with the documented mapping `0 = Normal`, `1 = Fraud`, and `2 = Promotion`; it checks the column names before training.

The notebook uses a stratified random train/validation/test split. The fraud-alert threshold is tuned on the validation set, and the held-out test set is reserved for final evaluation. The hand-written stress-test examples are synthetic and are not a representative national benchmark.

## Before presenting or submitting

- Run the notebook from top to bottom and save the real outputs.
- Report baseline and model metrics, especially fraud precision and recall.
- Include examples of false positives and false negatives, without exposing personal data.
- Expand the synthetic stress test with your team's own examples and label them clearly.
- Verify dataset usage terms and cite the dataset, libraries, and AI assistance used.
- Do not claim that the prototype detects every scam or proves that a message is safe.

## Credits

- Dataset source: [Indonesian SMS spam classification project](https://github.com/ksnugroho/klasifikasi-spam-sms) — verify original usage terms before submission.
- Related project documentation and label mapping: [Indonesian SMS spam detection](https://github.com/okeypeeps/indonesian-sms-spam-detection).
- Libraries: pandas, NumPy, scikit-learn, matplotlib, and Gradio.
- AI assistance: disclose ChatGPT (OpenAI) and any other AI tools used to draft, explain, or debug the project.
