# KAVACH Dataset Guide

Add your labeled images and URLs to these folders to test the detection accuracy of KAVACH.

## Screenshots (`data/screenshots/`)
- `real/`: Put genuine payment screenshots here (PNG/JPG).
- `fake/`: Put edited or fake payment screenshots here.

## QR Codes (`data/qr/`)
- `safe/`: Put legitimate merchant QR codes here.
- `fake/`: Put fraudulent or malicious QR codes here.

## URLs (`data/urls/`)
- `safe.txt`: List of legitimate URLs, one per line.
- `fake.txt`: List of phishing/scam URLs, one per line.

## Running Evaluation
Once you have added data, run:
```bash
python evaluate.py
```
This will print accuracy, precision, recall, and F1-score for each detector.
