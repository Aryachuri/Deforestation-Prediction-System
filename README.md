# Deforestation Prediction and Analysis System

## Overview

The Deforestation Prediction and Analysis System is a Python-based web application built using Flask to analyze changes in forest cover and forecast tree-cover loss.

The application combines image processing techniques with time-series forecasting to help users explore deforestation patterns through a web interface.

## Features

- **Satellite Image Comparison:** Upload past and current images to identify potential changes between them.
- **Image Processing:** Use OpenCV to convert images to grayscale, calculate pixel differences, and apply thresholding.
- **Deforestation Region Detection:** Use connected-component labeling to count detected regions in the thresholded difference image.
- **Time-Series Forecasting:** Use an LSTM neural network to forecast tree-cover-loss values from historical data.
- **Interactive Data Filtering:** Select country, subnational region, and tree-cover-loss threshold.
- **Prediction Visualization:** Display actual and predicted values in a graph using Matplotlib.
- **Image Preprocessing:** Convert uploaded images and masks to grayscale.
- **Web Interface:** Navigate through login, signup, home, features, analysis, prediction, and map pages.

## Technologies Used

- **Programming Language:** Python
- **Web Framework:** Flask
- **Image Processing:** OpenCV, Pillow, scikit-image
- **Data Processing:** Pandas, NumPy
- **Machine Learning:** Scikit-learn
- **Deep Learning:** TensorFlow, Keras, LSTM
- **Visualization:** Matplotlib
- **Frontend:** HTML, CSS, JavaScript
- **Data Format:** CSV

## How It Works

### 1. Satellite Image Analysis

The application accepts two images representing different points in time.

1. Upload the past and current images.
2. Convert both images to grayscale.
3. Resize the current image to match the dimensions of the past image.
4. Calculate the absolute pixel-wise difference.
5. Apply thresholding to identify significant pixel differences.
6. Label connected components and count the detected regions.

The resulting count is displayed through the Flask web interface.

**Note:** The current implementation detects image differences, not confirmed deforestation. Differences in lighting, season, image alignment, or other surface changes can also affect the result.

### 2. Deforestation Trend Forecasting

The prediction module uses historical tree-cover-loss data stored in a CSV file.

1. Load the dataset using Pandas.
2. Filter records by country, subnational region, and threshold.
3. Extract the tree-cover-loss time-series columns.
4. Scale the data using MinMaxScaler.
5. Prepare sequential input windows containing ten time steps.
6. Train an LSTM neural network with 50 units and a Dense output layer.
7. Compare predicted values with held-out actual values.
8. Plot the results using Matplotlib and display the graph in the web application.

The current implementation uses an 80/20 sequential train-test split and trains the model for 200 epochs.

## Project Structure

```text
Deforestation-Prediction-System/
├── app.py
├── Subnational 1 tree cover loss.csv
├── analysis.html
├── features.html
├── index.html
├── login.html
├── signup.html
├── predict.html
├── map.html
├── outcome.html
├── result1.html
├── login_script.js
├── signup_script.js
├── style.css
└── Other page-specific CSS files
```

*Adjust this structure to match the actual directory layout in your repository. Flask templates are normally stored in a `templates/` folder, and static files such as CSS, JavaScript, and uploaded images are normally stored in `static/`.*

## Installation and Setup

### Prerequisites

- Python 3.10 or another Python version compatible with your selected TensorFlow release
- pip
- Git

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd YOUR_PROJECT_FOLDER
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
```

On Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

Install the libraries used by the application:

```bash
pip install Flask opencv-python numpy matplotlib scikit-learn pandas scikit-image tensorflow Pillow
```

### 4. Configure the dataset path

Update the CSV file path in `app.py` to point to the dataset location on your computer.

For example, replace the machine-specific path with a path based on the project directory.

### 5. Run the application

```bash
python app.py
```

Open the local URL shown in the terminal, usually:

`http://127.0.0.1:5000`

## Limitations

- Image comparison relies on grayscale pixel differences and thresholding.
- Detected regions are not a direct measurement of deforested area.
- LSTM forecasts depend on the quality and length of the historical time series.
- The current prediction route trains the model when a prediction request is submitted, which can increase response time.
- Prediction quality should be assessed using appropriate time-series evaluation metrics.

## Future Improvements

- Integrate a trained image-segmentation model for more robust forest-cover analysis.
- Improve image alignment and preprocessing.
- Evaluate forecasting performance using MAE, RMSE, or other appropriate metrics.
- Load a previously trained forecasting model rather than retraining it for every request.
- Improve dataset-path configuration and error handling.
- Add deployment instructions and screenshots.

## Author

**Arya Churi**

GitHub: https://github.com/Aryachuri
