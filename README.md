# 🚴 London Bike Sharing Analysis & Visualization

A comprehensive data analysis project exploring London's bike-sharing patterns from 2015-2017, featuring interactive Tableau visualizations that reveal insights into how weather conditions and temporal factors influence bike usage.

[![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=Tableau&logoColor=white)](https://public.tableau.com/views/LondonBikesRidesVisualization/Dashboard1)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)

## 📊 Live Demo

**[View Interactive Dashboard on Tableau Public](https://public.tableau.com/views/LondonBikesRidesVisualization/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)**

The dashboard provides interactive visualizations showing:
- Bike ride trends over time with moving average analysis
- Temperature vs. wind speed correlation heatmaps
- Seasonal and weather-based usage patterns
- Hour-by-hour demand analysis

## 📑 Table of Contents

- [About the Project](#about-the-project)
- [Dataset Information](#dataset-information)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Data Processing Workflow](#data-processing-workflow)
- [Key Features](#key-features)
- [Technologies Used](#technologies-used)
- [Visualizations](#visualizations)

## 🎯 About the Project

This project analyzes bike-sharing data from London to uncover patterns and insights about urban mobility. The analysis focuses on:

- **Temporal Patterns**: How bike usage varies by hour, day, season, and year
- **Weather Impact**: The relationship between weather conditions (temperature, humidity, wind speed) and bike rides
- **Seasonal Trends**: Identifying peak and off-peak seasons for bike sharing
- **Holiday & Weekend Effects**: Understanding how special days affect bike usage

The project demonstrates end-to-end data analysis workflow from data acquisition through Kaggle API, data cleaning and transformation with Python/Pandas, to creating interactive visualizations in Tableau.

## 📦 Dataset Information

**Source**: [London Bike Sharing Dataset on Kaggle](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset)

**Time Period**: January 4, 2015 - January 3, 2017 (2 years)

**Records**: 17,414 hourly observations

### Data Dictionary

| Column | Description | Type | Values |
|--------|-------------|------|--------|
| `time` | Timestamp of the observation | datetime | Hourly intervals |
| `count` | Number of bike rides | integer | 0 - 7,860 |
| `temp_real_C` | Actual temperature in Celsius | float | -1.5 to 34.0°C |
| `temp_feels_like_C` | Perceived temperature in Celsius | float | -6.0 to 34.0°C |
| `humidity_percent` | Relative humidity | float | 0.0 - 1.0 (0-100%) |
| `wind_speed_kph` | Wind speed in km/h | float | 0.0 - 56.5 km/h |
| `weather` | Weather condition | string | Clear, Scattered clouds, Broken clouds, Cloudy, Rain, Rain with thunderstorm, Snowfall |
| `is_holiday` | Whether the day is a holiday | float | 0.0 (No), 1.0 (Yes) |
| `is_weekend` | Whether the day is a weekend | float | 0.0 (No), 1.0 (Yes) |
| `season` | Season of the year | string | spring, summer, autumn, winter |

### Weather Code Mapping

The original dataset uses numeric codes for weather conditions:
- `1.0` → Clear
- `2.0` → Scattered clouds
- `3.0` → Broken clouds
- `4.0` → Cloudy
- `7.0` → Rain
- `10.0` → Rain with thunderstorm
- `26.0` → Snowfall

### Season Code Mapping

- `0.0` → spring
- `1.0` → summer
- `2.0` → autumn
- `3.0` → winter

## 📁 Project Structure

```
twb-london-bikes/
│
├── london_bikes.ipynb              # Jupyter notebook with data analysis
├── london_merged.csv               # Raw dataset (extracted from zip)
├── london_bikes_final.xlsx         # Cleaned and transformed data
├── london-bike-sharing-dataset.zip # Original dataset from Kaggle
├── London Bikes Visualization.twb  # Tableau workbook file
└── README.md                       # Project documentation
```

## 🔧 Prerequisites

Before running this project, ensure you have the following installed:

- **Python 3.7+** (tested with Python 3.11.4)
- **Jupyter Notebook** or **JupyterLab**
- **Tableau Desktop** or **Tableau Public** (for viewing/editing visualizations)
- **Kaggle Account** (for dataset download via API)

### Required Python Libraries

- `pandas` - Data manipulation and analysis
- `kaggle` - Kaggle API for dataset download
- `zipfile` - Extract compressed files (built-in)
- `openpyxl` - Excel file handling (for pandas Excel export)

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/twb-london-bikes.git
cd twb-london-bikes
```

### 2. Set Up Python Environment (Optional but Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Required Libraries

```bash
pip install pandas kaggle openpyxl jupyter
```

### 4. Configure Kaggle API

To download the dataset programmatically:

1. Create a Kaggle account at [kaggle.com](https://www.kaggle.com)
2. Go to Account Settings → API → Create New API Token
3. Download the `kaggle.json` file
4. Place it in the appropriate location:
   - **Windows**: `C:\Users\<YourUsername>\.kaggle\kaggle.json`
   - **macOS/Linux**: `~/.kaggle/kaggle.json`
5. Set permissions (macOS/Linux only):
   ```bash
   chmod 600 ~/.kaggle/kaggle.json
   ```

## 💻 Usage

### Running the Data Analysis

1. **Open Jupyter Notebook**:
   ```bash
   jupyter notebook london_bikes.ipynb
   ```

2. **Execute the notebook cells** to:
   - Download the dataset from Kaggle
   - Extract the zip file
   - Load and explore the data
   - Clean and transform the data
   - Export the processed data to Excel

3. **Output**: The notebook generates `london_bikes_final.xlsx` ready for Tableau visualization

### Viewing the Tableau Dashboard

**Option 1: Online (No Installation Required)**
- Visit the [live dashboard](https://public.tableau.com/views/LondonBikesRidesVisualization/Dashboard1) on Tableau Public

**Option 2: Local (Requires Tableau Desktop/Public)**
1. Open Tableau Desktop or Tableau Public
2. Open `London Bikes Visualization.twb`
3. If prompted, connect to `london_bikes_final.xlsx`
4. Explore the interactive visualizations

## 🔄 Data Processing Workflow

The data processing pipeline consists of the following steps:

### 1. Data Acquisition
```python
# Download dataset from Kaggle
!kaggle datasets download -d hmavrodiev/london-bike-sharing-dataset
```

### 2. Data Extraction
```python
# Extract CSV from zip file
with zipfile.ZipFile('london-bike-sharing-dataset.zip', 'r') as file:
    file.extractall()
```

### 3. Data Loading
```python
# Load data into pandas DataFrame
bikes = pd.read_csv("london_merged.csv")
```

### 4. Data Exploration
- Check data types and null values
- Examine data shape (17,414 rows × 10 columns)
- Analyze value distributions

### 5. Data Transformation

**Column Renaming**: Improve readability
```python
bikes.rename({
    'timestamp': 'time',
    'cnt': 'count',
    't1': 'temp_real_C',
    't2': 'temp_feels_like_C',
    'hum': 'humidity_percent',
    'wind_speed': 'wind_speed_kph',
    'weather_code': 'weather',
    'is_holiday': 'is_holiday',
    'is_weekend': 'is_weekend',
    'season': 'season'
}, axis=1, inplace=True)
```

**Humidity Normalization**: Convert to 0-1 scale
```python
bikes.humidity_percent = bikes.humidity_percent / 100
```

**Categorical Mapping**: Convert codes to readable labels
```python
# Map season codes to names
season_dict = {'0.0': 'spring', '1.0': 'summer', '2.0': 'autumn', '3.0': 'winter'}
bikes.season = bikes.season.astype('str').map(season_dict)

# Map weather codes to descriptions
weather_dict = {
    '1.0': 'Clear',
    '2.0': 'Scattered clouds',
    '3.0': 'Broken clouds',
    '4.0': 'Cloudy',
    '7.0': 'Rain',
    '10.0': 'Rain with thunderstorm',
    '26.0': 'Snowfall'
}
bikes.weather = bikes.weather.astype('str').map(weather_dict)
```

### 6. Data Export
```python
# Export cleaned data to Excel for Tableau
bikes.to_excel('london_bikes_final.xlsx', sheet_name='Data')
```

## ✨ Key Features

- **Automated Data Pipeline**: Kaggle API integration for seamless data acquisition
- **Comprehensive Data Cleaning**: Handles missing values, type conversions, and categorical mappings
- **Interactive Visualizations**: Tableau dashboard with filters and drill-down capabilities
- **Weather Analysis**: Correlation between meteorological factors and bike usage
- **Temporal Analysis**: Hourly, daily, and seasonal trend identification
- **Reproducible Workflow**: Jupyter notebook documents every step of the analysis

## 🛠️ Technologies Used

### Data Processing
- **Python 3.11.4** - Core programming language
- **Pandas 2.x** - Data manipulation and analysis
- **Kaggle API** - Dataset acquisition
- **Jupyter Notebook** - Interactive development environment

### Data Visualization
- **Tableau Public/Desktop** - Interactive dashboard creation
- **Excel (xlsx)** - Data exchange format

### Development Tools
- **Git** - Version control
- **GitHub** - Code repository hosting

## 📈 Visualizations

The Tableau dashboard includes the following key visualizations:

### 1. Total Bike Rides Over Time
- Line chart showing hourly bike ride counts
- Moving average trend line to smooth fluctuations
- Interactive date range selector

### 2. Temperature vs. Wind Speed Heatmap
- Color-coded matrix showing the relationship between temperature and wind speed
- Reveals optimal conditions for bike sharing

### 3. Weather Condition Distribution
- Bar chart showing ride counts by weather type
- Highlights the impact of weather on bike usage

### 4. Seasonal Patterns
- Comparative analysis across spring, summer, autumn, and winter
- Identifies peak usage seasons

### 5. Hour-of-Day Analysis
- Heatmap showing bike usage patterns throughout the day
- Reveals commute-time peaks and off-peak hours

### 6. Holiday & Weekend Effects
- Comparison of usage patterns between regular days, weekends, and holidays

## 📝 License

This project is open source and available for educational and personal use.

**Dataset License**: The original dataset is provided by Kaggle user [hmavrodiev](https://www.kaggle.com/hmavrodiev) and is subject to Kaggle's terms of use.

## 👤 Author

Created as part of a data visualization portfolio project.

---

**⭐ If you found this project helpful, please consider giving it a star!**
