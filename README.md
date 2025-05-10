# Weather-app

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="weather-container">
    <h1>Weather App</h1>
    <input type="text" id="cityInput" placeholder="Enter city name">
    <button onclick="getWeather()">Get Weather</button>
    <div id="weatherResult"></div>
  </div>
  <script src="script.js"></script>
</body>
</html>



body {
  font-family: Arial, sans-serif;
  background: linear-gradient(to right, #74ebd5, #9face6);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.weather-container {
  background: white;
  padding: 20px 30px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

input {
  padding: 8px;
  width: 200px;
  margin-right: 10px;
}

button {
  padding: 8px 12px;
  background-color: #4285f4;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

#weatherResult {
  margin-top: 20px;
}
const apiKey = 'YOUR_API_KEY'; // Replace with your actual API key

function getWeather() {
  const city = document.getElementById('cityInput').value;
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

  fetch(url)
    .then(response => {
      if (!response.ok) throw new Error("City not found");
      return response.json();
    })
    .then(data => {
      const weatherDiv = document.getElementById('weatherResult');
      const temp = data.main.temp;
      const description = data.weather[0].description;
      const icon = data.weather[0].icon;

      weatherDiv.innerHTML = `
        <h2>${data.name}</h2>
        <img src="http://openweathermap.org/img/wn/${icon}@2x.png" alt="weather icon">
        <p><strong>${temp}°C</strong></p>
        <p>${description}</p>
      `;
    })
    .catch(error => {
      document.getElementById('weatherResult').innerHTML = `<p>${error.message}</p>`;
    });
}
