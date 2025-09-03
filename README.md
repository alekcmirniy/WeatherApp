🌤️ WeatherApp
A weather application with an update widget built on Vue.js that allows you to check current weather in any city. The project includes a widget with a countdown timer until the scheduled website update.

✨ Features
Weather search by city name using OpenWeatherMap API

Display of temperature, weather conditions, and descriptions

Countdown widget with toggleable display formats (full time or days only)

Modern, clean design using Vue 3 and TypeScript

Responsive interface

🚀 Quick Start
Clone and Install

# Clone the repository
  -git clone https://github.com/alekcmirniy/weather-app.git
  -cd weather-app

# Install dependencies
  -npm install
  
Development

# Start local development server
  -npm run serve

Production Build

# Build for production
  -npm run build
📖 How to Use
Enter a city name (minimum 2 characters) in the input field

Click the "Check Weather" button

The application will display current weather with detailed information

🛠️ Technologies
Vue 3 + Options API

TypeScript - type safety and enhanced development

Axios - HTTP requests to APIs

SCSS - CSS preprocessor for styling

OpenWeatherMap API - weather data

⚙️ Configuration
OpenWeatherMap API Key
Get a free API key from openweathermap.org

Replace the key in src/App.vue:

appid=YOUR_API_KEY
Update Date
Modify the update date for the widget in src/assets/UpdateDate.ts:

export const updateDate = new Date('2024-01-01T00:00:00'); // Your date here

📁 Project Structure
text
src/
├── assets/
│   ├── UpdateDate.ts          # Update date configuration
│   └── main.scss              # SCSS styles (added for organization)
├── components/
│   ├── UpdateWidget.vue       # Countdown widget component
├── App.vue                  # Main application component
└── main.ts                 # Application entry point

📝 Available Scripts
npm run serve - start development server

npm run build - build for production


🌐 Live Demo
Application Demo (if deployed to GitHub Pages)

🤝 Contributing
Contributions are welcome! Feel free to fork this project and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

📄 License
This project is distributed under the MIT License. See the LICENSE file for details.

👨‍💻 Author
Alexey Miroshnichenko

GitHub: alekcmirniy

Project: WeatherApp

An OpenWeatherMap API key is required for the application to function. Get a free key at openweathermap.org.
