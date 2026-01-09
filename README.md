# 🌍 Wanderly - AI Trip Planner

**Wanderly** is a next-generation travel planning application that leverages the power of AI to create personalized, day-by-day itineraries for any destination in the world.

**Live (Azure Static Web Apps):** https://gentle-sea-09cc45f00.2.azurestaticapps.net

![Wanderly Banner](https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?q=80&w=2070&auto=format&fit=crop)

## ✨ Features

*   **🤖 AI-Powered Itineraries**: Generates detailed daily schedules based on your travel style, budget, and preferences using Google's Gemini AI.
*   **☀️ Real-Time Weather**: Fetches current weather conditions for your destination using OpenWeatherMap.
*   **💼 Budget-First Search**: Enter budget, days, starting city, and travel type to get 3 destination options with transparent cost breakdowns.
*   **🏨 Smart Recommendations**: Suggests activities and logistics tailored to your trip style.
*   **💰 Cost Estimation**: Breaks down transport, food, local transport, and activities (backed by seeded city cost data).
*   **💱 Currency Converter**: Instantly convert costs between major global currencies (USD, EUR, GBP, JPY, etc.).
*   **🗺️ Interactive Map**: Search exact locations with Leaflet + OpenStreetMap integration. Select destinations via map click or search.
*   **📍 Location Database**: Stores searched locations in MongoDB for analytics and improved recommendations.
*   **🔔 Smart Alerts System**: Get notified when trip prices drop by 5% or more. Seasonal event alerts for festivals and best times to visit.
*   **📊 Price Tracking**: Historical price data with trends, min/max pricing, and savings calculations.
*   **🕐 Search History**: Track all searches (budget, planner, locations) with statistics and one-click re-run.
*   **🧭 Nearby Suggestions**: Discover popular destinations near your selected location with smart ranking (proximity + popularity + preferences).
*   **💬 Community Testimonials**: Share travel experiences, edit/delete testimonials, like others' stories, approval system.
*   **📱 Responsive Design**: Beautiful, glassmorphism-inspired UI that works perfectly on desktop and mobile.

## 🛠️ Tech Stack

*   **Frontend**: HTML5, CSS3 (Custom Properties, Glassmorphism), JavaScript (ES6+)
*   **AI Engine**: Google Gemini 2.0 Flash
*   **Database**: MongoDB (Atlas or local)
*   **APIs**:
    *   OpenWeatherMap (Weather & Geocoding)
    *   OpenTripMap (Attractions)
    *   Unsplash (Dynamic Images)
    *   Leaflet + OpenStreetMap (Interactive Maps)
*   **Backend / Serverless**: Netlify Functions (Node.js)

## 🚀 Getting Started

### Prerequisites

*   Node.js installed (for local development with Netlify CLI)
*   API Keys for:
    *   Google Gemini
    *   OpenWeatherMap

### Local Development

1.  **Clone the repository**
    ```bash
    git clone https://github.com/Pakeeza1508/imagine-cup-project.git
    cd imagine-cup-project
    ```

2.  **Install Netlify CLI** (Required for serverless functions)
    ```bash
    npm install -g netlify-cli
    ```

3.  **Run the development server**
    ```bash
    netlify dev
    ```
    This will start a local server (usually at `http://localhost:8888`) where the frontend and backend functions work together.

### Seed the Database (Required for Budget Search & Currency Conversion)

The budget search uses seeded city cost data, and currency conversion uses exchange rates stored in MongoDB.

1.  Create a `.env` in the project root (do **not** commit this file):
    ```bash
    MONGODB_URI=mongodb://localhost:27017
    MONGODB_DB=wanderly
    GOOGLE_API_KEY=your_gemini_key
    OPENWEATHER_KEY=your_openweather_key
    ```
    Alternatively, use your MongoDB Atlas connection string for `MONGODB_URI`.

2.  With `netlify dev` running, open these URLs **once** to seed:
    - Seed cities: `http://localhost:8888/.netlify/functions/seedCityCosts`
    - Seed trending destinations: `http://localhost:8888/.netlify/functions/seedTrendingDestinations`
    - **Seed exchange rates**: `http://localhost:8888/.netlify/functions/seedExchangeRates`
    - **Seed seasonal events**: `http://localhost:8888/.netlify/functions/seedSeasonalEvents` (NEW)

If you see a message like "Cities already seeded", your database is ready.

**Note**: Exchange rates are stored in MongoDB for easy management. You can update them anytime via:
   - Manual update: `POST` to `/.netlify/functions/updateExchangeRates` with JSON payload
   - Fetch current: `GET` `/.netlify/functions/getExchangeRates`

## ☁️ Deployment (Azure Static Web Apps)

This project now deploys via **Azure Static Web Apps** using the GitHub Actions workflow in `.github/workflows/azure-static-web-apps-gentle-sea-09cc45f00.yml`.

1. Push to `main` → GitHub Actions will build and publish to Azure Static Web Apps.
2. In the Azure Static Web App resource, set environment variables (Configuration > Application settings):
    * `GOOGLE_API_KEY`: Your Gemini API key
    * `OPENWEATHER_KEY`: Your OpenWeatherMap API key
    * `MONGODB_URI`: Your MongoDB connection string (Atlas recommended)
    * `MONGODB_DB`: Database name (e.g., `wanderly`)
3. After deployment, seed once using your production domain:
    - `https://gentle-sea-09cc45f00.2.azurestaticapps.net/.netlify/functions/seedCityCosts`
    - `https://gentle-sea-09cc45f00.2.azurestaticapps.net/.netlify/functions/seedTrendingDestinations`
    - `https://gentle-sea-09cc45f00.2.azurestaticapps.net/.netlify/functions/seedExchangeRates`
    - `https://gentle-sea-09cc45f00.2.azurestaticapps.net/.netlify/functions/seedSeasonalEvents`
4. Scheduled price-drop checks: ensure the Azure Static Web Apps instance allows the scheduled Netlify-style function or run manually as needed.

## 🔒 Security

Serverless functions keep API keys server-side. Store secrets only in `.env` locally and in Azure Static Web Apps application settings in production; never commit them.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

