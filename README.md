# AmropaliNet — Amropali Mango Fruit Disease Classifier

AI-powered classification of **7 Amropali mango fruit diseases** using **AA-ENet** (EfficientNet-B0 + CBAM + Transformer), deployed on [Streamlit Community Cloud](https://share.streamlit.io).

**Live deploy repo:** [Arpon-30/LastUpdatedmango](https://github.com/Arpon-30/LastUpdatedmango)

## Features

- Upload & classify mango fruit/leaf images with confidence scores
- CLIP zero-shot mango validation (rejects non-mango images)
- Grad-CAM++ visualization of model attention
- Disease encyclopedia (symptoms & treatment)
- Downloadable branded PDF reports
- Dark / light theme toggle

## Disease classes

| # | Class |
|---|-------|
| 1 | Anthracnose |
| 2 | Bacterial Canker |
| 3 | Healthy |
| 4 | Powdery Mildew |
| 5 | Scab |
| 6 | Sooty Mould |
| 7 | Stem End Rot |

## Local run

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
# source .venv/bin/activate

pip install -r requirements.txt
streamlit run streamlit_app.py
```

Open http://localhost:8501

## Deploy to Streamlit Community Cloud

1. Push this project to GitHub (public repo), including `AA-ENet_proposed.pt`
2. Do **not** push `fruit_classifier.pth` (unused legacy weights)
3. Go to [share.streamlit.io](https://share.streamlit.io) → **New app**
4. Select repo / branch `main`
5. Main file path: `streamlit_app.py`
6. In **Advanced settings**, set **Python version to 3.11** (required for PyTorch)
7. Click **Deploy**

First boot downloads CLIP (`openai/clip-vit-base-patch32`) from Hugging Face and may take several minutes. Free-tier RAM is limited; if the app is killed for memory, reboot from Manage app.

### Required files for Cloud

| File | Purpose |
|------|---------|
| `streamlit_app.py` | App entrypoint |
| `model.py` / `inference.py` / `report.py` | ML + PDF logic |
| `AA-ENet_proposed.pt` | Trained weights (~18 MB) |
| `requirements.txt` | Python deps (CPU PyTorch) |
| `.streamlit/config.toml` | Theme & upload limits |

## Model

**AA-ENet** ≈ EfficientNet-B0 → 1×1 reduce → CBAM → 1-layer Transformer → classifier  

~5.8M parameters · trained on 3,500 images (500 per class)

## Attribution

AIUB R&D ICCA Research Group · License: MIT
