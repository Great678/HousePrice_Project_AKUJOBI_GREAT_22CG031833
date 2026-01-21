# House Price Prediction System

A complete machine learning project that predicts house prices using a trained Random Forest Regressor model and a Flask web interface.

## Project Overview

This project demonstrates a complete ML pipeline with two main components:
- **Part A**: Model Development (model_development.py)
- **Part B**: Web GUI Application (app.py with Flask)

## Dataset

The project uses the **House Prices: Advanced Regression Techniques** dataset from Kaggle.

### Selected Features (6 of 9)
1. **OverallQual** - Overall material and finish rating (1-10)
2. **GrLivArea** - Above grade living area (sq ft)
3. **TotalBsmtSF** - Total basement square footage
4. **GarageCars** - Size of garage in car capacity (0-5)
5. **YearBuilt** - Original construction year
6. **Neighborhood** - Physical location within Ames city limits

### Target Variable
- **SalePrice** - The sale price of the house (in dollars)

## Algorithm

**Random Forest Regressor** with the following configuration:
- Number of trees: 100
- Max depth: 20
- Train-test split: 80-20

## Installation

1. **Download the dataset:**
   - Visit: https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data
   - Download `train.csv` and place it in the project root directory

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Step 1: Train the Model

Run the model development script to train and save the model:

```bash
python model_development.py
```

This will:
- Load and preprocess the dataset
- Handle missing values
- Encode categorical variables
- Scale features
- Train the Random Forest model
- Evaluate using MAE, MSE, RMSE, and R² metrics
- Save the model and preprocessing artifacts to the `models/` directory

**Output files created:**
- `models/price_model.joblib` - Trained model
- `models/scaler.joblib` - Feature scaler
- `models/label_encoders.joblib` - Categorical encoders
- `models/feature_names.joblib` - Feature names
- `models/model_metrics.joblib` - Evaluation metrics

### Step 2: Run the Web Application

Start the Flask web server:

```bash
python app.py
```

The application will start at `http://localhost:5000`

Open your browser and navigate to the URL to access the prediction interface.

## Project Structure

```
House_Price_Prediction/
├── model_development.py      # Model training script
├── app.py                    # Flask web application
├── requirements.txt          # Python dependencies
├── README.md                 # This file
├── models/                   # Saved model files
│   ├── price_model.joblib
│   ├── scaler.joblib
│   ├── label_encoders.joblib
│   ├── feature_names.joblib
│   └── model_metrics.joblib
├── templates/               # HTML templates
│   └── index.html           # Main prediction interface
└── static/                  # Static files
    ├── styles.css           # CSS styling
    └── script.js            # JavaScript functionality
```

## Model Performance

The model is evaluated on the test set using:

- **MAE (Mean Absolute Error)** - Average prediction error in dollars
- **MSE (Mean Squared Error)** - Squared average error
- **RMSE (Root Mean Squared Error)** - Square root of MSE
- **R² Score** - Coefficient of determination (0-1, higher is better)

See console output from `model_development.py` for specific metrics on your dataset.

## Data Preprocessing

1. **Missing Values Handling:**
   - Numerical features: Filled with median values
   - Categorical features: Filled with mode values
   - Target variable: Rows with missing values removed

2. **Feature Encoding:**
   - Categorical variables (Neighborhood) encoded using LabelEncoder

3. **Feature Scaling:**
   - All features standardized using StandardScaler (mean=0, std=1)

## Web Interface Features

- **Input Form**: Easy-to-use form for entering house features
- **Real-time Validation**: Client-side and server-side input validation
- **Live Predictions**: Instant predictions as you submit
- **Model Metrics**: Display of model performance metrics
- **Responsive Design**: Works on desktop and mobile devices
- **Error Handling**: Clear error messages for invalid inputs

## Technical Stack

### Backend
- Python 3.7+
- Flask 2.3.3 - Web framework
- scikit-learn 1.3.0 - ML algorithms
- pandas 2.0.3 - Data manipulation
- numpy 1.24.3 - Numerical computing
- joblib 1.3.1 - Model serialization

### Frontend
- HTML5
- CSS3 (with responsive design)
- Vanilla JavaScript (ES6+)

## API Endpoints

### GET `/`
- Renders the main prediction interface

### POST `/predict`
- **Request body (JSON):**
  ```json
  {
    "overall_qual": 7,
    "gr_liv_area": 2500,
    "total_bsmt_sf": 1500,
    "garage_cars": 2,
    "year_built": 2005,
    "neighborhood": "NridgHt"
  }
  ```
- **Response (JSON):**
  ```json
  {
    "success": true,
    "prediction": 315000.50,
    "formatted_price": "$315,000.50"
  }
  ```

### GET `/neighborhoods`
- Returns list of available neighborhoods

### GET `/metrics`
- Returns model performance metrics (MAE, RMSE, R²)

## Troubleshooting

### Dataset Not Found
If you see "ERROR: Dataset not found!":
1. Download `train.csv` from Kaggle
2. Place it in the project root directory (same level as `model_development.py`)

### Model Not Found
If the web app says "Model not loaded":
1. Ensure you've run `python model_development.py` first
2. Check that the `models/` directory contains all required files

### Port Already in Use
If port 5000 is already in use:
1. Edit `app.py` and change `port=5000` to a different port
2. Or kill the process using port 5000

## Sample Input Values

For testing the application, try these typical values:

**Example House:**
- Overall Quality: 7
- Living Area: 2500 sq ft
- Basement: 1500 sq ft
- Garage: 2 cars
- Year Built: 2005
- Neighborhood: NridgHt

## License

This project is created for educational purposes as part of CSC415 course project.

## Author

House Price Prediction System - CSC415 Project

## References

- Dataset: https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques
- Flask Documentation: https://flask.palletsprojects.com/
- scikit-learn Documentation: https://scikit-learn.org/
