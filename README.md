# KAVACH – Real Time Scam Shield for Rural India

KAVACH is an advanced fraud detection system designed to protect users against UPI payment scams, QR code fraud, and phishing URLs.

## Features
- **Enhanced Screenshot Analysis**: Multi-stage OCR preprocessing with OpenCV and 10+ weighted rule-based fraud scoring.
- **Layout Validation**: Region-based layout checks for PhonePe, Google Pay, and Paytm screenshots.
- **QR Fraud Shield**: Robust UPI URI decoding and safety validation (malformed URI, personal-as-merchant, suspicious handles).
- **Phishing Protection**: Heuristic-based URL analysis with homograph detection, brand mimicry checks, and WHOIS integration.

## Backend Architecture
- **FastAPI**: High-performance Python backend.
- **OpenCV + Pytesseract**: Image processing and text extraction.
- **Unified Scoring Engine**: Standardized risk levels (Safe, Suspicious, Blocked).

## Evaluation & Dataset Tuning
KAVACH includes a built-in evaluation pipeline to tune detection accuracy for demo usage.

### 1. Prepare Dataset
Add labeled data to the `data/` folder:
- **Screenshots**: Place genuine images in `data/screenshots/real/` and fake/edited ones in `data/screenshots/fake/`.
- **QR Codes**: Place safe QRs in `data/qr/safe/` and fraudulent ones in `data/qr/fake/`.
- **URLs**: Add one URL per line in `data/urls/safe.txt` and `data/urls/fake.txt`.

### 2. Run Evaluation
Execute the evaluation script to see accuracy metrics:
```bash
python evaluate.py
```
This prints Accuracy, Precision, Recall, and F1-score per detector.

### 3. Tuning Rules
You can adjust the weights of fraud rules and thresholds in:
- `backend/services/screenshot_service.py`
- `backend/services/qrcode_service.py`
- `backend/services/url_service.py`
- `backend/utils/scoring.py`

## Installation & Running
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Start the server:
   ```bash
   python -m uvicorn backend.main:app --reload
   ```
3. Access the dashboard: `http://localhost:8000/`

## API Reference
Standardized output for all analysis endpoints:
```json
{
  "risk_score": 75,
  "status": "blocked",
  "confidence": "high",
  "reasons": ["Suspicious UTR pattern", "Low OCR confidence"],
  "extracted_fields": {"upi_id": "...", "amount": "100.00"},
  "evidence_summary": "2 indicator(s) identified."
}
```
## Hosting & Deployment
KAVACH is production-ready and can be hosted on platforms like **Render**, **Railway**, or **DigitalOcean**. 

1. **Deployment via Procfile**: The included `Procfile` allows for one-click deployment on Render/Heroku.
2. **Environment Variables**:
   - `PORT`: The port the server will run on (default: 8000).

### Deploying to Render:
1. Connect your GitHub repository to Render.
2. Choose **Web Service**.
3. Set the **Runtime** to `Python 3`.
4. The **Build Command** should be `pip install -r requirements.txt`.
5. The **Start Command** should be `uvicorn backend.main:app --host 0.0.0.0 --port $PORT`.

## PWA Support (Progressive Web App)
KAVACH can be installed as a standalone app on your smartphone or desktop:

1. **On Android (Chrome)**: Open the URL, tap the three dots (⋮), and select **"Install App"** or **"Add to Home Screen"**.
2. **On iOS (Safari)**: Open the URL, tap the **Share** button (Square with arrow), then select **"Add to Home Screen"**.
3. **On Desktop (Chrome/Edge)**: Click the **Install** icon in the address bar.

### PWA Features:
- **Offline Shell**: Access the dashboard even without an internet connection.
- **Premium Dark UI**: Optimized for mobile and desktop screens.
- **Biometric Ready**: Integrates with device camera for instant scans.

---
*Created for the safety of Rural India.* 🛡️
