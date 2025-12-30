# Forecasting Production using Recurrent Neural Networks

This repository contains implementations of Long Short-Term Memory (LSTM) networks for forecasting oil, gas, and water production from offshore wells using real-world historical data from Equinor's Volve field in the Norwegian North Sea. 

## Overview

This project contains two implementations, both of which use a sliding window approach for temporal pattern learning:

**singleouput**

This model implements a single output LSTM model to estimate oil production on day t using:
- operatiional features from t-(window_size-1) to t (previous window_size days including day t)
- production features t-window_size to t-1 (previous window_size days excluding day t)

Here, window_size = 8, meaning that the model is estimating today's oil production using the previous 8 days of operational data (t-7 to t) and the previous 8 days of lagging production data (t-8 to t-1).

**multioutput**

This model implements a multi-output LSTM model to forecast oil, gas, and water production on day t+horizon using:
- operatiional features from t-window_size to t (previous 4 days including day t)
- production features from t-window_size to t (previous 4 days including day t)

Here, window_size = 4 and horizon = 3, meanig that the model is forecasting production 3 days ahead (t+1 to t+3) using 4 days of past (t-3 to t) operational and production data.

**NOTE:** The model architecture supports the multi-out implementation mentioned above to prediction BORE_OIL_VOL, BORE_GAS_VOL, and BORE_WAT_VOL simu simultaneously, though gas and water are currently commented out in the implementation.

### Dataset

The project uses real data from the [**Volve field dataset**](https://www.equinor.com/energy/volve-data-sharing), publicly released by [Equinor](https://www.equinor.com/). This dataset contains historical data from wells in the field spanning 2008-2016:
- 6 production wells
- 3 daily production volumes (oil, gas, and water) and 9 operational parameters (pressure, temperature, choke size, etc.)
- 15,600+ data points

## Project Structure
```
production-forecast/
├── data/
│   └── production_volve_data.xlsx
├── notebooks/
│   ├── production_forecast_singleoutput.ipynb
│   └── production_forecast_multioutput.ipynb
├── .gitignore
├── requirements.txt
├── LICENSE
└── README.md
```

## Tech Stack

- Python 3.x
- TensorFlow/Keras
- Pandas & NumPy
- Scikit-learn
- Matplotlib & Seaborn

## Installation

1. Clone this repository:

```bash
git clone https://github.com/yourusername/production-forecast.git
cd production-forecast
```
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Place your `volve_production_data.xlsx` file in the project directory

## Usage

### Running the Notebook

Open and run the Jupyter notebook:

**singleouput**
```bash
jupyter notebook production_forecast_singleoutput.ipynb
```

**multioutput**
```bash
jupyter notebook production_forecast_multioutput.ipynb
```

## Future Work

- [ ] adding well-specific metadata or embeddings
- [ ] training multiple wells simultaneously
- [ ] further hyperparameter tuning (random search/systematic grid)
- [ ] using temporal cross-validation
- [ ] explore architectures (e.g. atttention mechanisms)
- [ ] refactoring + congfiguration
