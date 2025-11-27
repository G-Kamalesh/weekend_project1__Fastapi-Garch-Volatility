# ⚡ GARCH Volatility Forecasting API 📉

**An MLOps Microservice for Financial Risk Analysis built with FastAPI and Python.**

## 🎯 Project Overview

This project implements a scalable, production-ready REST API to perform advanced timeseries analysis, specifically **Financial Volatility Forecasting**, using the **Generalized Autoregressive Conditional Heteroskedasticity (GARCH)** model.

The API demonstrates an end-to-end MLOps pipeline, handling data sourcing, model training, persistence, and low-latency serving.

### Key Features:
* **GARCH Implementation:** Deploys the GARCH model to analyze and forecast volatility clustering, essential for risk management and options pricing in FinTech.
* **Intelligent Data Pipeline:** The `/fit` endpoint intelligently sources data either live from the **AlphaVantage API** or from a local **SQLite** cache based on user parameters.
* **MLOps Ready:** Utilizes model persistence (`.pkl` / `.pk1`) to save and version trained models, ensuring fast serving without retraining.
* **FastAPI Backend:** Built on **FastAPI** for high performance and automatic interactive documentation (Swagger UI).

## 🛠️ Technology Stack

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend Framework** | FastAPI | High-performance API server. |
| **Model** | GARCH (via `arch` or similar library) | Volatility modeling. |
| **Data Sourcing** | AlphaVantage API | Live stock market data. |
| **Database** | SQLite | Local caching of historical data. |
| **Language** | Python 3.9+ | Core programming language. |
| **MLOps** | Python `Joblib` / File System | Model persistence and versioning. |

## 🚀 Getting Started

Follow these steps to set up and run the API locally.

### Prerequisites
* Python 3.9+
* A code editor (VS Code recommended)
* An API key for **AlphaVantage** (for live data fetching)

### .env file
```
ALPHA_VANTAGE_API_KEY="YOUR_API_KEY_HERE"
DB_NAME = "SQLITE DB NAME",
MODEL_DIRECTORY = "FOLDER NAME (for versioning and saveing the persisted model)"
```

### 1. Clone the Repository

```bash
git clone [YOUR-REPOSITORY-URL]
cd [your-project-folder]
```
### 2. Set Up Environment
It is highly recommended to use a virtual environment (venv).

```
# Create and activate environment

python -m venv venv
source venv/bin/activate  # On Windows, use: .\venv\Scripts\activate
```
### 3. Install Dependencies
Install all required Python libraries.

```
pip install -r requirements.txt
```
### 4. Run the Server
Start the FastAPI application using Uvicorn.

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8008
```

The API documentation will be available at: http://localhost:8008/docs

## 🌐 API Endpoints

The service exposes three main endpoints for functionality and health checks.

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/hello` | `GET` | Service health check and status confirmation. |
| `/fit` | `POST` | Trains a new GARCH model for a specified stock and saves the artifact. |
| `/predict`| `POST` | Loads the latest trained GARCH model and provides volatility forecasts. |


### Example 1: Training a Model (/fit)

This endpoint trains a GARCH(1,1) model for the specified ticker, using 1000 observations from the historical data cache.

Request Body (JSON):
```

{
  "ticker": "AMBUJACEM.BSE",        # ticker symbol of the company
  "use_new_data": false,            # 'false' - will fetch data from sqlite db, 'true' - will fetch data from alphavantage api
  "n_observations": 1000,           # 'None' - fetches all available data, 'int' - specify the no of data you need
  "p": 1,                           # model parameter
  "q": 1                            # model parameter
}
```

### Example 2: Forecasting Volatility (/predict)
This endpoint loads the pre-trained model for the ticker and predicts volatility for the next 7 days.

Request Body (JSON):

```

{
  "ticker": "AMBUJACEM.BSE",
  "days": 7
}

```

# ✍️ Contribution and Contact

This project was developed by " Kamaleashwar G ".

Feel free to reach out with questions or suggestions!

On [LinkedIn](https://www.linkedin.com/in/g-kamaleashwar-28a2802ba/)
