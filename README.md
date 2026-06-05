# ChronoSales — Store Sales Forecasting

A time-series sales forecasting system using LSTM neural networks, served as a Flask REST API. Predicts future sales for a given store and date using historical sales data.

## Features

- LSTM-based deep learning model trained on multi-store sales data
- Sequence modeling with a 7-day sliding window
- REST API endpoint for real-time sales prediction by store and date
- **Web UI** — Bootstrap frontend to enter store number and date, displays predicted sales instantly
- MinMaxScaler normalization for stable training and inference

## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat&logo=keras&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat&logo=flask&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)

## Setup

```bash
pip install flask keras tensorflow pandas numpy scikit-learn
```

## Running the App

```bash
python stores.py
```

The server starts on `http://localhost:5004`. Open `index.html` in your browser (or serve it statically) to use the web interface — enter a store number and date, click **Check**, and the predicted sales appear instantly.

## API Usage

**POST** `/predict`

| Field | Type | Description |
|-------|------|-------------|
| `storeNumber` | int | Store ID |
| `day` | int | Day of month |
| `month` | int | Month (1–12) |
| `year` | int | Year |

**Response:** Predicted sales value (integer)

**Example:**
```bash
curl -X POST http://localhost:5004/predict \
  -d "storeNumber=1&day=15&month=6&year=2024"
```

## How It Works

1. Historical sales for the requested store are retrieved from the training data
2. The last 7 days of sales (sequence length) are used as input features
3. The pre-trained LSTM model (`model.json` + `model_weights.h5`) predicts the next sales value
4. The output is inverse-transformed from normalized space back to actual sales units

## Project Structure

```
ChronoSales/
├── stores.py          # Flask API server + prediction logic
├── index.html         # Bootstrap web UI (store number + date input)
├── model.json         # Saved LSTM architecture
├── model_weights.h5   # Trained model weights
├── con_train.zip      # Preprocessed training dataset
└── ChronoSales.pptx   # Project presentation
```
