Gold Sniper AI: XAU/USD ML Trading System 

An end-to-end algorithmic trading pipeline for Gold (XAU/USD) on the 1-Minute (M1) timeframe. This project utilizes an XGBoost classifier integrated into MetaTrader 5 via the ONNX runtime to execute high-confidence "Sniper" entries based on market microstructure.

* The Strategy

The "Gold Sniper" is a Price Pressure Classifier. Unlike standard indicators, it analyzes tick-level data to calculate statistical anomalies (Skewness/Kurtosis) and momentum distribution within a single candle to predict the next minute's direction.

Timeframe: M1 (Gold/XAUUSD)

Confidence Filter: The "Sniper" only executes trades when the model probability exceeds 65%, effectively filtering out low-probability market noise.

* Feature Intelligence

The model's "edge" comes from its custom feature engineering. Instead of just OHLC data, the AI looks at the internal "microstructure" of price action.

* Model Performance (Out-of-Sample Results)

Important: All results below are generated from a 20% Hold-out Test Set (Out-of-Sample). The model was trained on the first 80% of the historical data and evaluated on the final 20% to ensure the metrics reflect real-world scenario

*SECTION 1: RAW PERFORMANCE (ALL DATA)

Includes high-noise periods where the model has low confidence.

              precision    recall  f1-score   support

           0       0.50      0.48      0.49    109765
           1       0.51      0.53      0.52    111321

    accuracy                           0.51    221086
   macro avg       0.51      0.51      0.51    221086
weighted avg       0.51      0.51      0.51    221086


* SECTION 2: SNIPER METRICS (65% THRESHOLD)

The results of the actual high-confidence trading logic on unseen data.

Metric

Value

* Total High-Confidence Trades

962

Overall Sniper Accuracy

55.61%

BUY Precision (Win Rate)

55.69%

SELL Precision (Win Rate)

55.50%

* Repository Structure

feature_extractor.mq5: Extracts intra-bar pressure and statistical features from raw ticks.

XAUUSD_AI_MODEL.ipynb: The Python training pipeline using an 80/20 time-series split.

Gold_Pressure_Sniper_M1.mq5: The MT5 Expert Advisor (Execution Engine).

gold_sniper_v1.onnx: The trained XGBoost model file for MT5.

feature_importance_plot.png: Visual breakdown of the model's top predictors.

* Setup & Installation

Place gold_sniper_v1.onnx in the /MQL5/Files/ folder of your MT5 directory.

Place Gold_Pressure_Sniper_M1.mq5 in the /MQL5/Experts/ folder.

Enable "Allow DLL imports" in your MT5 Terminal settings.

Attach the EA to a Gold (XAUUSD) M1 chart and ensure the 65% threshold is active.

Disclaimer: Algorithmic trading involves significant risk. These Out-of-Sample results do not guarantee future performance. Always test on a demo account first.
