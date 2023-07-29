# Weather Data Retrieval.
This Python program allows users to retrieve weather data, wind speed, and pressure for a specific date using the OpenWeatherMap API.


import requests

def get_weather_data(location):
    api_url = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=b6907d289e10d714a6e88b30761fae22"
    response = requests.get(api_url)
    return response.json()

def get_temperature(data, date):
    for forecast in data['list']:
        if date in forecast['dt_txt']:
            return forecast['main']['temp']
    return None

def get_wind_speed(data, date):
    for forecast in data['list']:
        if date in forecast['dt_txt']:
            return forecast['wind']['speed']
    return None

def get_pressure(data, date):
    for forecast in data['list']:
        if date in forecast['dt_txt']:
            return forecast['main']['pressure']
    return None

def main():
    location = "London,us"
    weather_data = get_weather_data(location)

    while True:
        print("\nOptions:")
        print("1. Get weather")
        print("2. Get Wind Speed")
        print("3. Get Pressure")
        print("0. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            date = input("Enter the date (yyyy-mm-dd HH:MM:SS): ")
            temperature = get_temperature(weather_data, date)
            if temperature is not None:
                print(f"The temperature at {date} is {temperature}°C.")
            else:
                print("No data available for the given date.")
        elif choice == '2':
            date = input("Enter the date (yyyy-mm-dd HH:MM:SS): ")
            wind_speed = get_wind_speed(weather_data, date)
            if wind_speed is not None:
                print(f"The wind speed at {date} is {wind_speed} m/s.")
            else:
                print("No data available for the given date.")
        elif choice == '3':
            date = input("Enter the date (yyyy-mm-dd HH:MM:SS): ")
            pressure = get_pressure(weather_data, date)
            if pressure is not None:
                print(f"The pressure at {date} is {pressure} hPa.")
            else:
                print("No data available for the given date.")
        elif choice == '0':
            print("Exiting the program.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

