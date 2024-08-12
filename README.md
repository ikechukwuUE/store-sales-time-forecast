# Store Sales Time Series Forecasting

This repository contains a time series forecasting model implemented using Python. The project leverages various libraries, including `pmdarima`, `pandas`, and `matplotlib`, to build and evaluate forecasting models.

## Table of Contents
- [Installation](#installation)
- [Data Description](#data-description)
- [Model Implementation](#model-implementation)
- [Model Usage](#model-usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

To use the code in this repository, you need to have Python installed along with several dependencies. You can install the required packages using:

```bash
pip install -r requirements.txt
```

## Data Description

The dataset used in this project contains time series data that spans multiple years. The data includes various columns with numerical values representing different metrics recorded over time.

### Data Types:
- `float16`
- `float32`
- `int64`

### Handling Null Values:
Null values in the dataset are filled using appropriate methods to ensure no important dates are missed.

## Model Implementation

The model implementation involves the following steps:

1. **Loading the Data:** The dataset is loaded and preprocessed to handle any missing values and ensure the data types are correctly formatted.

2. **DeterministicProcess:** The `DeterministicProcess` from the `pmdarima` package is used to create trend features for the time series data. This process is applied to both the training and test datasets to ensure consistency.

3. **Trend Feature Creation:** Trend features are generated for the dataset to capture the underlying patterns in the data.

4. **Model Training:** The model is trained using the trend features and other relevant columns from the dataset.

5. **Model Evaluation:** The trained model is evaluated using appropriate metrics to assess its performance on the test data.

## Model Usage

### 1. Generating Trend Features:

The `DeterministicProcess` from the `pmdarima` package is used to generate trend features for the dataset. This involves creating features that capture the deterministic trends in the data. The trend features are generated for both the training and test datasets to ensure that the shape of the test dataset's trend features matches that of the training dataset.

### 2. Handling Data Types:

The dataset contains numerical columns of types `float16`, `float32`, and `int64`. These data types are preserved throughout the modeling process to ensure that the model works efficiently with the available resources.

### 3. Filling Null Values:

To avoid missing important dates, null values in the dataset are filled instead of dropped. This ensures that all time points are accounted for in the forecasting model.

### 4. Visualization:

Plots are generated starting from specific dates, such as June 2017, to provide clear and meaningful visualizations of the forecasted trends.

### Example Usage:

```python
from pmdarima import auto_arima
from pmdarima.preprocessing import DeterministicProcess
import pandas as pd

# Load the dataset
data = pd.read_csv('your_dataset.csv')

# Create trend features
dp = DeterministicProcess(index=data.index, order=1)
trend = dp.in_sample()

# Add trend features to the data
data = data.join(trend)

# Train the model
model = auto_arima(data['target_column'], exogenous=trend)

# Forecast using the model
forecast = model.predict(n_periods=12, exogenous=trend[-12:])
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an issue for any bug reports or feature requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
