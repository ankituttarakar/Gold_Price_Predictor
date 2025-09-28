# Gold Price Predictor

A **machine learning–powered Flask application** that predicts gold prices (GLD) based on key financial indicators like S&P 500, US Oil Fund, Silver, and EUR/USD exchange rate. This app provides a clean, interactive web interface for local usage or deployment.

---
```
Gold_Price_Predictor/
├── GoldPriceDetector.py      # Main Flask application and model training script
├── gold_price_model.joblib   # Trained Random Forest model (generated after training)
├── gld_price_data.csv        # Historical gold price dataset
├── .gitignore                # Files to ignore for Git
├── README.md                 # Project documentation
└── requirements.txt          # Python dependencies
```

## Features

* Predict gold prices using a trained **Random Forest Regressor**.
* Interactive **HTML frontend** for inputting financial indicators.
* Runs locally with Flask without external tunneling (ngrok removed).
* Easy to extend with new features or indicators.

---

## Setup & Installation

1. **Clone the repository:**

```
git clone https://github.com/ankituttarakar/Gold_Price_Predictor.git
cd Gold_Price_Predictor
```

2. **Install dependencies:**

```
pip install -r requirements.txt
```

3. **Ensure dataset is available:**
   Place `gld_price_data.csv` in the project folder. The script expects the path:
   `C:\Users\ankit\Downloads\gld_price_data.csv` (update in code if different).

4. **Run the app:**

```
python GoldPriceDetector.py
```

5. **Access the app locally:**
   Open a browser and go to:

```
http://127.0.0.1:5000/
```

---

## Usage

1. Enter values for:

   * **SPX (S&P 500 Index)**
   * **USO (US Oil Fund)**
   * **SLV (Silver Price)**
   * **EUR/USD Exchange Rate**

2. Click **Predict Price**.

3. View predicted **GLD price** on the page.

---

## Notes

* Model is trained on historical data (`gld_price_data.csv`), predictions may vary for live market conditions.
* The app is intended for **educational and demonstration purposes**.

---

## Dependencies

* Python 3.10+
* pandas
* numpy
* scikit-learn
* joblib
* Flask
* python-dotenv

Install via:

```
pip install pandas numpy scikit-learn joblib flask python-dotenv
```

## Author

### Ankit Uttarakar
[GitHub](https://github.com/ankituttarakar)
