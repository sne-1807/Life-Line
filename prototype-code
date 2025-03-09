#include <TinyGPS++.h>
#include <HardwareSerial.h>
#include "DHT.h"
#include <Wire.h> // Include Wire library for I2C
#include <Adafruit_BMP085.h> // Include BMP180 library

// Create a TinyGPS++ object
TinyGPSPlus gps;

// Define the serial connections
HardwareSerial gpsSerial(1);

// DHT11 sensor setup
#define DHTPIN 4
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

// BMP180 sensor setup
Adafruit_BMP085 bmp;

void setup() {
  // Start the hardware serial for GPS module at 9600 baud rate
  gpsSerial.begin(9600, SERIAL_8N1, 16, 17);

  // Start the serial monitor
  Serial.begin(9600);
  Serial.println("GPS, DHT11, and BMP180 Data Parsing");

  // Initialize DHT sensor
  dht.begin();
  delay(1000); // Allow sensor to stabilize

  // Initialize BMP180 sensor
  if (!bmp.begin()) {
    Serial.println("Could not find a valid BMP085 sensor, check wiring!");
    while (1); // Stop execution if BMP180 is not found
  }
}

void loop() {
  // Read GPS data
  while (gpsSerial.available() > 0) {
    gps.encode(gpsSerial.read());

    if (gps.location.isUpdated()) {
      Serial.print("Latitude: ");
      Serial.println(gps.location.lat(), 6);
      Serial.print("Longitude: ");
      Serial.println(gps.location.lng(), 6);
    }

    if (gps.date.isUpdated()) {
      Serial.print("Date: ");
      Serial.print(gps.date.day());
      Serial.print("/");
      Serial.print(gps.date.month());
      Serial.print("/");
      Serial.println(gps.date.year());
    }

    if (gps.time.isUpdated()) {
      Serial.print("Time: ");
      Serial.print(gps.time.hour());
      Serial.print(":");
      Serial.print(gps.time.minute());
      Serial.print(":");
      Serial.println(gps.time.second());
    }

    if (gps.altitude.isUpdated()) {
      Serial.print("Altitude: ");
      Serial.println(gps.altitude.meters());
    }

    if (gps.speed.isUpdated()) {
      Serial.print("Speed: ");
      Serial.println(gps.speed.kmph());
    }

    if (gps.satellites.isUpdated()) {
      Serial.print("Satellites: ");
      Serial.println(gps.satellites.value());
    }
  }

  // Read DHT11 data
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    delay(2000);
    return;
  }

  // Read BMP180 data
  double pressure = bmp.readPressure();
  double temperatureBMP = bmp.readTemperature();
  double altitudeBMP = bmp.readAltitude();

  // Print sensor data
  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature (DHT): ");
  Serial.print(t);
  Serial.println(" *C");

  Serial.print("Temperature (BMP): ");
  Serial.print(temperatureBMP);
  Serial.print(" *C\t");
  Serial.print("Pressure: ");
  Serial.print(pressure / 100.0); // Convert Pa to hPa
  Serial.print(" hPa\t");
  Serial.print("Altitude (BMP): ");
  Serial.print(altitudeBMP);
  Serial.println(" m");

  delay(2000);
}
