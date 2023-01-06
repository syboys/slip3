# slip3
slip3

Q.1 Write a JAVA Program to implement built-in support (java.util.Observable) Weather
station with members temperature, humidity, pressure and methods
mesurmentsChanged(), setMesurment(), getTemperature(), getHumidity(),
getPressure() 
Q. 2. Write a python program to make Categorical values in numeric format for a given
dataset 
Q. 3. Create an HTML form for Login and write a JavaScript to validate email ID
using Regular Expression. 








Q.1 Write a JAVA Program to implement built-in support (java.util.Observable) Weather
station with members temperature, humidity, pressure and methods
mesurmentsChanged(), setMesurment(), getTemperature(), getHumidity(),
getPressure()

:
import java.util.Observable;
import java.util.Observer;
class CurrentConditionsDisplay implements Observer, DisplayElement {
 Observable observable;
 private float temperature;
 private float humidity; 
public CurrentConditionsDisplay(Observable observable) {
 this.observable = observable;
 observable.addObserver(this);
 }
 public void update(Observable obs, Object arg) {
 if (obs instanceof WeatherData) {
 WeatherData weatherData = (WeatherData)obs;
 this.temperature = weatherData.getTemperature();
 this.humidity = weatherData.getHumidity();
 display();
 }
 }
 public void display() {
 System.out.println("Current conditions: " + temperature
 + "F degrees and " + humidity + "% humidity");
 }
}
interface DisplayElement {
 public void display();
}
class ForecastDisplay implements Observer, DisplayElement {
 private float currentPressure = 29.92f;
 private float lastPressure;
 public ForecastDisplay(Observable observable) {
 observable.addObserver(this);
 } 
public void update(Observable observable, Object arg) {
 if (observable instanceof WeatherData) {
 WeatherData weatherData = (WeatherData)observable;
 lastPressure = currentPressure;
 currentPressure = weatherData.getPressure();
 display();
 }
 }
 public void display() {
 System.out.print("Forecast: ");
 if (currentPressure > lastPressure) {
 System.out.println("Improving weather on the way!");
 } else if (currentPressure == lastPressure) {
 System.out.println("More of the same");
 } else if (currentPressure < lastPressure) {
 System.out.println("Watch out for cooler, rainy weather");
 }
 }
}
 class HeatIndexDisplay implements Observer, DisplayElement {
 float heatIndex = 0.0f;

 public HeatIndexDisplay(Observable observable) {
 observable.addObserver(this);
 } 
public void update(Observable observable, Object arg) {
 if (observable instanceof WeatherData) {
 WeatherData weatherData = (WeatherData)observable;
 float t = weatherData.getTemperature();
 float rh = weatherData.getHumidity();
 heatIndex = (float)
 (
 (16.923 + (0.185212 * t)) +
 (5.37941 * rh) -
 (0.100254 * t * rh) +
 (0.00941695 * (t * t)) +
 (0.00728898 * (rh * rh)) +
 (0.000345372 * (t * t * rh)) -
 (0.000814971 * (t * rh * rh)) +
 (0.0000102102 * (t * t * rh * rh)) -
 (0.000038646 * (t * t * t)) +
 (0.0000291583 * (rh * rh * rh)) +
 (0.00000142721 * (t * t * t * rh)) +
 (0.000000197483 * (t * rh * rh * rh)) -
 (0.0000000218429 * (t * t * t * rh * rh)) +
 (0.000000000843296 * (t * t * rh * rh * rh)) -
 (0.0000000000481975 * (t * t * t * rh * rh * rh)));
 display();
 }
 }
 public void display() {
 System.out.println("Heat index is " + heatIndex);
 }
}
 class StatisticsDisplay implements Observer, DisplayElement {
 private float maxTemp = 0.0f;
 private float minTemp = 200;
 private float tempSum= 0.0f; 
private int numReadings;
 public StatisticsDisplay(Observable observable) {
 observable.addObserver(this);
 }

 public void update(Observable observable, Object arg) {
 if (observable instanceof WeatherData) {
 WeatherData weatherData = (WeatherData)observable;
 float temp = weatherData.getTemperature();
 tempSum += temp;
 numReadings++;
 if (temp > maxTemp) {
 maxTemp = temp;
 }
 if (temp < minTemp) {
 minTemp = temp;
 }
 display();
 }
 }
 public void display() {
 System.out.println("Avg/Max/Min temperature = " + (tempSum / numReadings)+ "/"
+ maxTemp + "/" + minTemp);
 }
}

 class WeatherData extends Observable { 
private float temperature;
 private float humidity;
 private float pressure;
 public WeatherData() { }
 public void measurementsChanged() {
 setChanged();
 notifyObservers();
 }
 public void setMeasurements(float temperature, float humidity, float pressure) {
 this.temperature = temperature;
 this.humidity = humidity;
 this.pressure = pressure;
 measurementsChanged();
 }
 public float getTemperature() {
 return temperature;
 }
 public float getHumidity() {
 return humidity;
 }

 public float getPressure() {
 return pressure;
 }
}
public class Main {
 public static void main(String[] args) {
 WeatherData weatherData = new WeatherData(); 
CurrentConditionsDisplay currentConditions = new
CurrentConditionsDisplay(weatherData);
 StatisticsDisplay statisticsDisplay = new
StatisticsDisplay(weatherData);
 ForecastDisplay forecastDisplay = new ForecastDisplay(weatherData);
 weatherData.setMeasurements(80, 65, 30.4f);
 weatherData.setMeasurements(82, 70, 29.2f);
 weatherData.setMeasurements(78, 90, 29.2f);
 }
} 


Q. 2. Write a python program to make Categorical values in numeric format for a given
dataset
:

from sklearn.preprocessing import LabelEncoder
label_encoder = LabelEncoder()
x = ['Apple', 'Orange', 'Apple', 'Pear']
y = label_encoder.fit_transform(x)
print(y)

array([0, 1, 0, 2])


from numpy import array
from numpy import argmax
from sklearn.preprocessing import OneHotEncoder
onehot_encoder = OneHotEncoder(sparse=False)
y = y.reshape(len(y), 1)
onehot_encoded = onehot_encoder.fit_transform(y)
print(onehot_encoded)

[[1. 0. 0.]
[0. 1. 0.]
[1. 0. 0.]
[0. 0. 1.]]


Q. 3. Create an HTML form for Login and write a JavaScript to validate email ID
using Regular Expression.

:

<html>
 <head>
 <title>Slip 3 Email Validation</title>
 <script>
 function validateform(){
 var email = document.getElementById("email").value;
 var pass = document.getElementById("pass").value;
 var regEmail = /^([a-zA-Z0-9\._]+)@([a-z]+)(.[a-z]+)?$/;

 //if Fields are empty
 if(email.length == 0){
 alert("All Fields are Mandatory");
 return false;
 }
 else if(pass.length == 0){
 alert("All Fields are Mandatory");
 return false;
 }
 else if(!regEmail.test(email)){
 alert("Enter Name Format Correctly \"First Name Last Name\"");
 return false;
 }
 else{
 alert("Validation Successfull");
 return true;
 }
}
 </script>
 </head>
 <body>
 <form>
 Email: <input type="text" id="email"></input></br></br>
 Password: <input type="password" id="pass"></input></br></br>
 <button type="submit" onclick="validateform()">Submit</button>
 </form>
 </body>
</html>
