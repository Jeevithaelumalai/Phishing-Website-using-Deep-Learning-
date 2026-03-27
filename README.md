# 🛡️ PhishGuard — AI-Powered Phishing Detection

A real-time phishing website detector using Deep Learning + Browser Extension.

## GitHub Repo
https://github.com/Jeevithaelumalai/Phishing-Website-using-Deep-Learning-.git

## Project Structure

```
phishguard/
├── data/                        # Datasets (auto-downloaded)
├── models/                      # Saved model weights & plots
├── src/
    ├── feature_extractor.py     # 30-feature URL analyzer
    ├── model.py                 # CNN + LSTM dual-input model
    └── train.py                 # Full training pipeline
├── requirements.txt
└── README.md
```

## Phase 1 — Model Training

### Setup
```bash
pip install -r requirements.txt
```

### Train the model
```bash
# Default (20 epochs, batch size 32)
python src/train.py

# Custom
python src/train.py --epochs 30 --batch-size 64
```

### What happens:
1. Downloads phishing dataset automatically (or generates synthetic data)
2. Extracts 30 URL features per sample
3. Tokenizes URLs character-by-character
4. Trains dual-input CNN+LSTM model
5. Saves best model to `models/phishguard_model.keras`
6. Outputs training plots and confusion matrix

## Model Architecture

```
URL String ──► Char Embedding ──► Multi-Scale CNN (3,5,7) ──┐
                                ► BiLSTM ──────────────────────┤
                                                               ├──► Dense ──► Sigmoid
30 Features ──► Dense(64) ──► BatchNorm ──────────────────────┘
```

## Features Extracted (30 total)

| Category | Features |
|---|---|
| URL Structure | length, dots, hyphens, slashes, port, query params |
| Security | HTTPS, IP address, hex encoding, obfuscation |
| Domain | shorteners, suspicious TLD, subdomain depth |
| Brand Impersonation | brand in subdomain/path, suspicious keywords |
| Character Analysis | special chars, digit ratio, entropy |

## Expected Performance
- Accuracy: ~96%+
- AUC: ~0.98+
- Precision/Recall: ~95%+

## Next Phases
- **Phase 2**: FastAPI server wrapping the model
- **Phase 3**: Chrome extension for real-time detection
- **Phase 4**: Visual screenshot detection + PhishTank live feed
