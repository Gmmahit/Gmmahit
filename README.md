#include <stdio.h>
#include <wiringPi.h>

#define PIR_SENSOR_PIN 7   // Pin where the PIR sensor is connected (GPIO 7)
#define LIGHT_PIN 0        // Pin where the light (LED) is connected (GPIO 0)

int main() {
    // Initialize wiringPi library
    if (wiringPiSetup() == -1) {
        printf("wiringPi setup failed!\n");
        return -1;
    }

    // Set the PIR_SENSOR_PIN as an input (for motion detection)
    pinMode(PIR_SENSOR_PIN, INPUT);

    // Set the LIGHT_PIN as an output (for controlling the light)
    pinMode(LIGHT_PIN, OUTPUT);

    while (1) {
        // Read the PIR sensor value
        int motionDetected = digitalRead(PIR_SENSOR_PIN);

        if (motionDetected == HIGH) {
            // If motion is detected, turn the light ON
            digitalWrite(LIGHT_PIN, HIGH);
            printf("Motion detected! Light ON.\n");
        } else {
            // If no motion, turn the light OFF
            digitalWrite(LIGHT_PIN, LOW);
            printf("No motion. Light OFF.\n");
        }

        // No delay needed, program continuously checks motion status
    }

    return 0;
}
