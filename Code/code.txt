const int pingPin = 13; // Trigger Pin of Ultrasonic Sensor
const int echoPin = 12; // Echo Pin of Ultrasonic Sensor

const int sensorPin = A0;    // select the input pin for the potentiometer
     // select the pin for the LED
 int sensorValue = 0;
const int buzz = 9;
const int motor = 11;

void setup() {
   Serial.begin(9600); // Starting Serial Terminal
   pinMode(buzz, OUTPUT);
   pinMode(motor, OUTPUT);
}

void loop() {
  //following code together measures distance
   long duration, inches, cm;
   pinMode(pingPin, OUTPUT);
   digitalWrite(pingPin, LOW);
   delayMicroseconds(2);
   digitalWrite(pingPin, HIGH);
   delayMicroseconds(10);
   digitalWrite(pingPin, LOW);
   pinMode(echoPin, INPUT);
   pinMode(buzz, OUTPUT);
   duration = pulseIn(echoPin, HIGH);
   inches = microsecondsToInches(duration);
   cm = microsecondsToCentimeters(duration);
   Serial.print(inches);
   Serial.print("in, ");
   Serial.print(cm);
   Serial.print("cm");
   Serial.println();
   delay(100);
sensorValue = analogRead(sensorPin);
  Serial.println(sensorValue);

  
   if(cm < 35 || sensorValue > 510){  // if distance in cm is smaller than 35 or if the gas sensor value goes above 510 - buzzer and vibration motor turns on
    digitalWrite(buzz, HIGH);
    digitalWrite(motor, HIGH);
    
   }
   else{
    digitalWrite(buzz,LOW); //else they remain off
    digitalWrite(motor, LOW);
   }
}

long microsecondsToInches(long microseconds) {
   return microseconds / 74 / 2;
}

long microsecondsToCentimeters(long microseconds) {
   return microseconds / 29 / 2;
}