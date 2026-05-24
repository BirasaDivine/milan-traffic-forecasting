# Milan Mobile Network Traffic — Time Series Forecasting
A complete machine learning pipeline for analyzing and forecasting mobile internet 
traffic across the city of Milan, Italy, using the Telecom Italia Mobile (TIM) dataset.

## Project Overview
This project covers three main tasks:

- **Task 1:** Efficient handling and memory optimization of a ~19GB dataset on an 8GB RAM local machine
- **Task 2:** Exploratory data analysis including spatial, temporal, and statistical characterization of mobile traffic patterns
- **Task 3:** Design and comparison of three forecasting models (SARIMA, LSTM, Transformer) for one-step-ahead traffic prediction
## Repository Structure
```
milan-traffic-forecasting/
├── Loading_dataset.ipynb   
├── Task2.ipynb            
├── Task3.ipynb         
├── outputs/ # All generated plots               
├── requirements.txt        
├── .gitignore
└── README.md
```
## Dataset

The dataset is the Telecom Italia Mobile (TIM) Milan telecommunications activity 
dataset, available from the Harvard Dataverse:

- **Telecommunications activity data:** https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EGZHFV
- **Grid data:** https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/QJWLFU

The dataset consists of 62 plain-text files covering November 1 to January 1, 2014.
Only the `square_id`, `time_interval`, and `internet` columns are used.
Raw data files are not included in this repository due to size constraints.

## Requirements

- Python 3.10+
- 8 GB RAM minimum
- ~20 GB free disk space for raw data

Install all dependencies:

```bash
pip install -r requirements.txt
```

## Setup Instructions

### Step 1: Clone the repository

```bash
git clone https://github.com/BirasaDivine/milan-traffic-forecasting.git
cd milan-traffic-forecasting
```

### Step 2: Download the dataset

Go to the Harvard Dataverse links above and download all 62 files.
Extract all ZIP files into a single folder:
Windows: C:\Users\YOUR_USERNAME\Downloads\milan_data
Mac/Linux: ~/Downloads/milan_data/
### Step 3: Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Launch Jupyter Notebook

```bash
# Windows
python -m notebook

# Mac/Linux
jupyter notebook
```

### Step 5: Run notebooks in order

>  Notebooks must be run in this exact order

**1. `Loading_dataset.ipynb` (Task 1)**
- Loads and optimizes all 62 raw files
- Reduces memory usage by 83.3% through type downcasting and column selection
- Saves `traffic_data.parquet` and `traffic_matrix.parquet`
- First run takes approximately 5-10 minutes

**2. `Task2.ipynb` (Task 2)**
- Loads parquet files from Task 1
- Generates all 7 EDA plots saved to `outputs/`
- Saves `task2_checkpoint.pkl` with target area information

**3. `Task3.ipynb` (Task 3)**
- Trains SARIMA, LSTM, and Transformer models
- All results saved as `.pkl` checkpoints , no need to retrain on subsequent runs
- Generates all 9 prediction plots saved to `outputs/`


## Target Areas

| Area | Rank | Total Traffic 
|------|------|--------------
| 5161 | #1 | 12,730,825 
| 4159 |#424 | 2,453,775 
| 4556 |#109 | 4,573,268 

## Results

### Model Performance

| Model | Area 5161 MAE | Area 5161 MAPE | Area 4159 MAE | Area 4159 MAPE | Area 4556 MAE | Area 4556 MAPE |
|-------|--------------|----------------|--------------|----------------|--------------|----------------|
| SARIMA | 354.70 | **20.16%** | 168.30 | 66.95% | 330.47 | 68.95% |
| LSTM | 1843.35 | 436.31% | **112.31** | **35.63%** | **204.30** | **64.96%** |
| Transformer | 1155.95 | 201.38% | 113.30 | 36.10% | 252.08 | 79.04% |

**Best model per area:**
- Area 5161  → **SARIMA**
- Area 4159 → **LSTM**
- Area 4556 → **LSTM**

