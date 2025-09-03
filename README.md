This project is a simple Python script that fetches and displays real-time currency exchange rates using the FreeCurrencyAPI
.
It’s perfect for beginners to learn how to make API requests and work with JSON data in Python.

import requests  # Importing the requests library to make API calls

# Your unique API key for FreeCurrencyAPI
API_KEY = 'fca_live_cu6JgBBXFeFq3VwlSlVsoFLniP'

# Base URL for the API endpoint, with your API key added
BASE_URL = f"https://api.freecurrencyapi.com/v1/latest?apikey={API_KEY}"

# List of currencies you want conversion rates for
CURRENCIES = ["USD", "CAD", "EUR", "AUD", "INR", "CNY"]

# Function to fetch conversion rates for the given base currency
def convert_currency(base):
    currencies = ",".join(CURRENCIES)  # Join the list into a comma-separated string
    url = f"{BASE_URL}&base_currency={base}&currencies={currencies}"  # Complete API URL
    try:
        response = requests.get(url)  # Make the API request
        data = response.json()        # Convert the response to JSON format
        return data["data"]           # Return the 'data' portion of the JSON response
    except:
        print("Invalid Currency")     # Error message if the currency is invalid or API call fails
        return None

# Main loop to interact with the user
while True:   
    base = input("Enter the base currency (q for quit):").upper()  # Get currency from user and convert to uppercase

    if base == "Q":  # Quit the program if user enters 'q'
        break
      
    data = convert_currency(base)  # Call the function to get rates
    if not data:                   # Skip if the API call failed
        continue

    del data[base]  # Remove the base currency from the results

    # Print conversion rates for each currency
    for ticker, value in data.items():
        print(f"{ticker}: {value}")
