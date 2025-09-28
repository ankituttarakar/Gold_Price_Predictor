

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestRegressor
import joblib
from flask import Flask, request, jsonify
import numpy as np
import threading
import time
import os
from dotenv import load_dotenv


# TRAIN AND SAVE THE MODEL


# Load the data
try:
    gold_data = pd.read_csv('C:\\Users\\ankit\\Downloads\\gld_price_data.csv')
except FileNotFoundError:
    print("Error: dataset file not found. Please upload the file to your Colab session before running.")
    exit()

# Prepare the data for training
X = gold_data.drop(['Date','GLD'], axis=1)
Y = gold_data['GLD']

# Split the data
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=2)

# Initialize and train the model
regressor = RandomForestRegressor(n_estimators=100, random_state=2)
regressor.fit(X_train, Y_train)

# Save the trained model to a file
joblib.dump(regressor, 'gold_price_model.joblib')

print("Model trained and saved successfully.")



# HTML FRONTEND TEMPLATE

html_template = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gold Price Predictor</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f4f9; color: #333; margin: 0; padding: 20px; display: flex; justify-content: center; align-items: center; min-height: 90vh; }

        .container { background: #fff; max-width: 500px; margin: auto; padding: 30px; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); text-align: center; }
        
        input { width: calc(100% - 22px); padding: 10px; margin-bottom: 20px; border: 1px solid #ddd; border-radius: 5px; }
        button { width: 100%; padding: 12px; background-color: #ffd700; color: #333; font-weight: bold; border: none; border-radius: 5px; cursor: pointer; transition: background-color 0.3s; font-size: 1em; }
        button:hover { background-color: #e6c300; }
        h2 { color: #333; }
        #result { font-size: 1.5em; margin-top: 25px; color: #28a745; font-weight: bold; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Gold Price Predictor ⚜️</h2>
        <form id="prediction-form">
            <input type="number" step="any" id="spx" name="spx" placeholder="SPX (S&P 500 Index)" required>
            <input type="number" step="any" id="uso" name="uso" placeholder="USO (US Oil Fund)" required>
            <input type="number" step="any" id="slv" name="slv" placeholder="SLV (Silver Price)" required>
            <input type="number" step="any" id="eur_usd" name="eur_usd" placeholder="EUR/USD Exchange Rate" required>
            <button type="submit">Predict Price</button>
        </form>
        <div id="result"></div>
    </div>

    <script>
        document.getElementById('prediction-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            let data = {
                spx: parseFloat(document.getElementById('spx').value),
                uso: parseFloat(document.getElementById('uso').value),
                slv: parseFloat(document.getElementById('slv').value),
                eur_usd: parseFloat(document.getElementById('eur_usd').value)
            };

            fetch('/predict', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(data)
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('result').innerText = 'Predicted GLD Price: $' + data.prediction;
            })
            .catch(error => console.error('Error:', error));
        });
    </script>
</body>
</html>
"""

# CREATE AND RUN THE FLASK APP

load_dotenv()

app = Flask(__name__)

model = joblib.load('gold_price_model.joblib')

@app.route('/')
def home():
    return html_template

@app.route('/predict', methods=['POST'])
def predict():
    data = request.get_json(force=True)
    features = [np.array(list(data.values()))]
    prediction = model.predict(features)
    return jsonify(prediction=round(prediction[0], 2))


def run_app():
    import logging
    log = logging.getLogger('werkzeug')
    log.setLevel(logging.ERROR)  
    app.run(host="0.0.0.0", port=5000)


flask_thread = threading.Thread(target=run_app)
flask_thread.start()


time.sleep(2)

print(" Your Gold Price Predictor is live at http://127.0.0.1:5000/")
