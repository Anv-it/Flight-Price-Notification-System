
# Flight Price Notification System

This project is a Python application that monitors flight prices for specified destinations and sends an SMS notification when a cheaper flight is available. The program integrates several APIs (Sheety, Amadeus, and Twilio) to retrieve, manage, and notify users of flight data.

## Features
- **Data Management**: The app uses the Sheety API to store and update destination city data, including IATA codes and lowest recorded prices.
- **Flight Search**: The Amadeus Flight Search API checks for the lowest flights from a specified origin city to each destination over the next 6 months.
- **Notifications**: When a flight is found below the recorded threshold, an SMS notification is sent with details about the flight using the Twilio API.
- **APIs Used**:
  - Sheety API for Google Sheets management
  - Amadeus Flight Search API for flight data
  - Twilio API for sending SMS notifications

## Files

### `data_manager.py`
Handles interactions with the Google Sheet, including retrieving destination data and updating IATA codes for each city.

### `flight_data.py`
Defines the `FlightData` class, which stores details of a flight, including price, origin and destination cities, airport codes, and travel dates.

### `flight_search.py`
Handles requests to the Amadeus API to retrieve IATA codes for cities and search for flights based on origin and destination IATA codes.

### `main.py`
The main script that orchestrates the entire workflow:
- Retrieves data from the Google Sheet
- Checks flight prices for each destination
- Sends a notification if a flight price is below the threshold

### `notification_manager.py`
Contains the logic for sending SMS messages using the Twilio API. For this setup, make sure you have Twilio account credentials and a verified phone number.

## Setup and Configuration

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/flight-price-notification-system.git
   cd flight-price-notification-system
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Create a `.env` file** with the following environment variables:
   ```plaintext
   SHEETY_API_KEY="your_sheety_api_key"
   TEQUILA_API_KEY="your_tequila_api_key"
   TWILIO_SID="your_twilio_sid"
   TWILIO_AUTH_TOKEN="your_twilio_auth_token"
   TWILIO_VIRTUAL_NUMBER="your_twilio_virtual_number"
   TWILIO_VERIFIED_NUMBER="your_twilio_verified_number"
   ```

4. **Run the program**:
   ```bash
   python main.py
   ```

## Usage

- **Flight Search**: The program retrieves flights for each destination from the next day up to six months in advance.
- **SMS Notifications**: An SMS alert will be sent if a flight is found for less than the recorded lowest price.
- **Updating Destination Data**: The Sheety API is used to automatically update IATA codes if they’re missing in the Google Sheet.

## Notes
- Be mindful of **API rate limits**, especially with free-tier accounts.
- Ensure you use city IATA codes, not specific airport codes, for destinations.
- Twilio requires a verified phone number to send messages on free accounts.