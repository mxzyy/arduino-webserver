//Web Server dengan sensor suhu & Humadity DHT
//Library yang dipakai
#include <ESP8266WiFi.h> //Library Wifi untuk ESP8266
#include <ESP8266WebServer.h> //Library Web Server ESP8266
#include <DHT.h> //Library Sensor suhu & Kelembapan DHT
//Pilih salah satu type DHT yang di gunakan
#define DHTTYPE DHT11 // DHT 11
//#define DHTTYPE DHT21 // DHT 21 (AM2301)
//#define DHTTYPE DHT22 // DHT 22 (AM2302), AM2321
/*Masukan SSID & Password WiFi*/
const char* ssid = "SMK N 2 YOGYAKARTA"; //SSID WiFi
const char* password = "amsangaji47"; //Password WiFi
ESP8266WebServer server(80); //Port Web Server
// DHT Sensor
uint8_t DHTPin = 16; //Pin input pada D1 = Pin 1 Digital 
// Initialize DHT sensor.
DHT dht(DHTPin, DHTTYPE); 
float Temperature;
float Humidity;
void setup() {
Serial.begin(9600); //Kecepatan serial port (COM)
delay(100);
pinMode(DHTPin, INPUT);
dht.begin(); 
Serial.println("Tersambung ke ");
Serial.println(ssid);
//Koneksi ke Lokal WiFi
WiFi.begin(ssid, password);
//Check WiFi terkoneksi ke Jaringan
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}
Serial.println("");
Serial.println("WiFi sudah terkoneksi..!");
Serial.print("Got IP: "); Serial.println(WiFi.localIP()); //Menampilkan IP pada 
server.on("/", handle_OnConnect);
server.onNotFound(handle_NotFound);
server.begin();
Serial.println("HTTP server started");
}
void loop() {
server.handleClient();
}
void handle_OnConnect() {
//Temperature = dht.readTemperature(); // Mendapatkan nilai suhu
//Humidity = dht.readHumidity(); // Mendapatkan nilai Hudity
server.send(200, "text/html", SendHTML(Temperature,Humidity)); 
}
void handle_NotFound(){
server.send(404, "text/plain", "Not found");
}
String SendHTML(float Temperaturestat,float Humiditystat){
String ptr = "<!DOCTYPE html> <html>\n";
ptr +="<head><meta name=\"viewport\" content=\"width=device-width, initial scale=1.0, user-scalable=no\">\n";
ptr +="<title>Laporan Cuaca dengan Web Server ESP8266 </title>\n";
ptr +="<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}\n";
ptr +="body{margin-top: 50px;} h1 {color: #444444;margin: 50px auto 30px;}\n";
ptr +="p {font-size: 24px;color: #444444;margin-bottom: 10px;}\n";
ptr +="</style>\n";
ptr +="</head>\n";
ptr +="<body>\n";
ptr +="<div id=\"webpage\">\n";
ptr +="<h1>Laporan Cuaca dengan Web Server ESP8266</h1>\n";
ptr +="<p>Temperature: ";
//ptr +=(int)Temperaturestat;
ptr +=" °C</p>";
ptr +="<p>Humidity: ";
//ptr +=(int)Humiditystat;
ptr +="%</p>";
ptr +="</div>\n";
ptr +="</body>\n";
ptr +="</html>\n";
return ptr;
}
