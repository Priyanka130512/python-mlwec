Smart Cold Storage Monitoring System
📌 Description

An IoT-based system that monitors temperature, humidity, gas leakage, fire detection, and RFID-based tracking in cold storage units. It sends real-time data and alerts to a cloud dashboard.

🛠️ Technologies Used
ESP32
DHT11 Sensor
Gas Sensor (Analog)
Fire Sensor
RFID Module
WiFi (HTTP requests)
C++ (Arduino IDE)
⚙️ Key Features
Real-time temperature & humidity monitoring
Fire and gas leak detection
RFID-based tag tracking system
Automatic alert system via API
Buzzer alarm for emergency situations
1. WiFi + Sensor Initialization
#include <WiFi.h>
#include <HTTPClient.h>
#include <DHT.h>

DHT dht(23, DHT11);

const int firePin = 12;
const int gasPin = 13;
const int buzzerPin = 14;

WiFi.begin(ssid, password);
2. Sensor Reading + Alert Logic
float temperature = dht.readTemperature();
float humidity = dht.readHumidity();

int fireValue = digitalRead(firePin);
int gasValue = analogRead(gasPin);

if (fireValue == LOW || gasValue > 400) {
  digitalWrite(buzzerPin, HIGH);
}
3. API Alert Sending Function
void sendAlert(String tagID) {
  HTTPClient http;
  String url = alertRoute + "&tagID=" + tagID;
  http.begin(url);
  http.GET();
  http.end();
}
📁 Project Structure (Recommended)
Smart-Cold-Storage/
│── main.ino
│── README.md
│── sensors.h
│── api.cpp
