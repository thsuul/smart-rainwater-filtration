# Smart Rainwater Filtration System — ML Predictions

> Machine Learning model that predicts rainwater quality using weather data — no lab testing required.

---

## Problem

In urban areas, rainwater is treated as waste and sent to sewers — but it could be reused for irrigation, car washing, and technical purposes. The barrier? We don't know if it's safe.

Traditional lab testing costs **$50+ and takes days**. This project replaces that with instant, free ML predictions.

---

## Solution

```
Weather Data → Feature Engineering → ML Model → Water Quality Prediction
```

**Example:**
- Input: Light rain, 15°C, 5 dry days
- Output: TDS ≈ 121 mg/L, Turbidity ≈ 107 NTU →  Safe for irrigation

---

## Model Performance

| Model | R² Score | MAE | RMSE |
|-------|----------|-----|------|
| TDS Prediction | 0.915 | 12.4 mg/L | 18.7 mg/L |
| Turbidity Prediction | 0.923 | 45.2 NTU | 67.8 NTU |

Both models use **Random Forest Regressor** — chosen for its ability to handle nonlinear relationships and provide feature importance analysis.

---

## Key Findings

**1. Rain type is the dominant factor**
- Snow: TDS ≈ 250 mg/L (road salts) #Snowmelt shows significantly higher TDS levels due to de-icing road salt accumulation.
- Heavy rain: TDS ≈ 144 mg/L (first flush effect)
- Light rain: TDS ≈ 122 mg/L (cleanest)

**2. First flush effect is real**
- After 10+ dry days, first rainfall is ~40% dirtier
- Recommendation: discard first 10–15 minutes after long dry periods

**3. DIY filter effectiveness**

| Parameter | Before | After | Reduction |
|-----------|--------|-------|-----------|
| TDS | 121.8 mg/L | 115.7 mg/L | 5% |
| Turbidity | 107.3 NTU | 26.8 NTU | 75% |

Filter: Sieve → Magnets → Sand/Gravel → Activated Carbon
- Excellent at removing particles
- Limited effect on dissolved salts
- → Safe for irrigation, **not** for drinking

---

## Dataset Limitations

Training dataset includes 16 rain events.
Data is physics-simulated based on environmental assumptions.

This project demonstrates methodology and modeling approach, not production-grade deployment.

---
## Repository Structure

```
├── data/
│   ├── archive.csv                        # Raw weather data (104 days)
│   ├── smart_rainwater_system_full.csv    # Feature-engineered dataset
│   └── smart_rainwater_system_training.csv # Rain-events only (ML training)
├── models/
│   ├── tds_model.pkl                      # Trained TDS model
│   └── turbidity_model.pkl                # Trained Turbidity model
├── visualizations/                        # 5 result graphs
├── train_model.ipynb                      # Full training notebook
├── requirements.txt
└── README.md
```

---

## Quick Start

```bash
git clone https://github.com/thsuul/smart-rainwater-filtration.git
cd smart-rainwater-filtration
pip install -r requirements.txt
jupyter notebook train_model.ipynb
```

---

## Feature Engineering

| Feature | Why It Matters |
|---------|---------------|
| Rain_Intensity | Light rain vs storm vs snow have different contamination |
| ADP_Days | Days since last rain = accumulated dirt |
| ADP_Days_squared | Nonlinear accumulation effect |
| Wind_Squared | Strong wind mobilizes dust exponentially |
| Temp_Wind_Interaction | Hot + windy = maximum airborne particles |
| Wind_Rolling_7d | Weekly weather trend |

---

## Future Development

- Real sensor integration (Raspberry Pi Pico + TDS/turbidity sensors)
- LSTM time-series forecasting
- Web dashboard with real-time monitoring
- Full-year seasonal dataset
- Air quality data (PM2.5, PM10)

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![pandas](https://img.shields.io/badge/pandas-Data-green)

---

## License

MIT License — free to use, modify, and learn from.

---

*Built as an independent applied ML research project by [@thsuul](https://github.com/thsuul)*
