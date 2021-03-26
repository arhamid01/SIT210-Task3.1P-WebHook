# SIT210-Task3.1P-WebHook
// This #include statement was automatically added by the Particle IDE.
#include <Adafruit_DHT_Particle.h>
#define DHTPIN  D5

DHT dht(DHTPIN,22);
int led = D7;

void setup() {

    pinMode(led, OUTPUT);
    digitalWrite(led, LOW);
    dht.begin();

    Particle.subscribe("hook-response/temp", myHandler, MY_DEVICES);

}

void myHandler(const char *event, const char *data) {
  digitalWrite(led, HIGH);
}


void loop() {

    double tmp = dht.getTempCelcius();
    
    Particle.publish("temp", String(tmp), PRIVATE);

    delay(30000);

}
