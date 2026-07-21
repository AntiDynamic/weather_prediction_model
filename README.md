# Weather Prediction Model

## Project Overview

This project aims to provide accurate weather predictions, with a special focus on serving farmers in various locations, including small villages across India. It combines a custom-trained local weather model (for Pune) with real-time data from the OpenWeather API. The system is designed to be user-friendly, allowing natural language queries, and leverages the Gemini API for intelligent query parsing and enhanced location accuracy through Google Search.

## Features

-   **Natural Language Understanding:** Utilizes the Gemini API to parse user queries in a conversational manner, extracting city, date, and desired information type.
-   **Enhanced Location Accuracy:** Integrates Google Search via the Gemini API to accurately pinpoint locations, including specific addresses or sub-locations (e.g., "wadgaonsheri pune"), and retrieve precise coordinates.
-   **Hybrid Forecasting Model:**
    -   For **Pune**: Combines a local machine learning model (trained on historical Pune weather data) with OpenWeather API forecasts using a weighted averaging approach.
    -   For **Other Locations**: Fetches forecasts directly from the OpenWeather API, providing reliable data for areas without a dedicated local model.
-   **Efficient Model Retraining:** The local prediction model (`weather_model_enhanced.py`) is designed to retrain only when the source data (`pune_weather_cleaned.csv`) is newer than the saved model (`weather_model_enhanced.pkl`), optimizing resource usage.
-   **Modular and Robust Design:** The codebase is structured into distinct modules for API interaction, configuration, and application logic, promoting maintainability and scalability.
-   **API Key Management:** Securely handles API keys using environment variables (`.env` file).

## Setup Instructions

Follow these steps to set up and run the project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/AntiDynamic/weather_prediction_model.git
cd weather_prediction_model
```

### 2. Create and Activate a Virtual Environment

It's recommended to use a virtual environment to manage dependencies.

```bash
python -m venv venv
# On Windows
.\venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies

Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt
```

### 4. Configure API Keys

This project requires API keys for OpenWeatherMap and Google Gemini.

-   **OpenWeatherMap API Key:**
    1.  Sign up for a free account at [OpenWeatherMap](https://openweathermap.org/api).
    2.  Generate an API key.
-   **Google Gemini API Key:**
    1.  Go to [Google AI Studio](https://aistudio.google.com/app/apikey).
    2.  Create an API key.

Create a `.env` file in the root directory of the project (`weather_prediction_model/`) and add your API keys as follows:

```
OPENWEATHER_API_KEY=YOUR_OPENWEATHER_API_KEY
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
```

**Note:** A `.env.example` file is provided for reference. **Do not commit your actual `.env` file to version control.**

### 5. Prepare the Local Weather Model (for Pune)

The project includes a local model for Pune. You need to ensure the `pune_weather_cleaned.csv` data is present and the model is trained. The `weather_model_enhanced.py` script handles this automatically on its first run or when data is updated.

## Usage

To run the weather assistant, execute the `weather_assistant.py` script:

```bash
python weather_assistant.py
```

The assistant will prompt you to enter your weather query. You can ask questions in natural language, specifying the city, date (e.g., "tomorrow", "10th nov"), and type of information (e.g., "temperature", "rain", "wind", or general "weather").

**Example Queries:**

-   "What is the weather in Mumbai tomorrow?"
-   "Temperature in Delhi on 10th nov"
-   "Rain in Chennai"
-   "Wind in Bangalore today"
-   "Weather in Pune"
-   "Weather in Wadgaonsheri Pune tomorrow"

## Project Structure

```
weather_prediction_model/
├── .env                     # Environment variables (API keys) - NOT committed
├── .env.example             # Example for .env file
├── .gitignore               # Specifies intentionally untracked files to ignore
├── api_client.py            # Handles all interactions with the OpenWeather API
├── combined_forecast.py     # Logic for combining local model and API forecasts
├── config.py                # Configuration settings and API key loading
├── gemini_client.py         # Handles interactions with the Google Gemini API for NLU and Google Search
├── last_update.txt          # Stores the last update date for the local model
├── pune_weather_cleaned.csv # Cleaned historical weather data for Pune
├── requirements.txt         # Python dependencies
├── weather_assistant.py     # Main script for the conversational weather assistant
├── weather_model_enhanced.pkl # Trained enhanced weather model (pickle file)
├── weather_model_enhanced.py# Script for training and forecasting with the local model
└── __pycache__/             # Python cache files
```

## Future Enhancements

-   **More Robust Date Parsing:** Implement more sophisticated date parsing to handle a wider variety of natural language date expressions.
-   **Multi-day Forecast Display:** Enhance the display to show a summary of the 5-day forecast rather than just a single day.
-   **User Preferences:** Allow users to set preferences (e.g., preferred units, default location).
-   **Voice Interface:** Integrate a voice recognition system for hands-free interaction.
-   **Deployment:** Deploy the assistant as a web application or a chatbot.
-   **Error Handling:** Implement more granular error handling and user feedback for API failures or invalid queries.
-   **Internationalization:** Expand language support beyond Hindi/Marathi phrases.
