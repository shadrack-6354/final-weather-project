# final-weather-project

import requests

# Function to fetch the weather data
def get_weather(city_name, api_key):
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
    
    # Complete URL
    complete_url = f"{base_url}q={city_name}&appid={api_key}&units=metric"
    
    # Send a GET request to the OpenWeatherMap API
    response = requests.get(complete_url)
    
    # Convert the response to JSON
    data = response.json()
    
    # Check if the request was successful
    if data["cod"] == "404":
        print("City not found, please try again.")
    else:
        # Extract weather details from the JSON data
        main_data = data["main"]
        weather_data = data["weather"][0]
        
        # Get temperature, pressure, humidity
        temperature = main_data["temp"]
        pressure = main_data["pressure"]
        humidity = main_data["humidity"]
        
        # Get weather description (e.g., clear sky, rain)
        weather_description = weather_data["description"]
        
        # Print the weather information
        print(f"Weather in {city_name}:")
        print(f"Temperature: {temperature}°C")
        print(f"Pressure: {pressure} hPa")
        print(f"Humidity: {humidity}%")
        print(f"Weather Description: {weather_description.capitalize()}")

# Main function to run the application
def main():
    # API key from OpenWeatherMap (replace with your own)
    api_key = "your_api_key_here"
    
    # Ask the user to input the city name
    city_name = input("Enter the city name: ")
    
    # Call the get_weather function
    get_weather(city_name, api_key)

if __name__ == "__main__":
    main()
