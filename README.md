# PID-Control-for-Brushless-Motor-with-Arduino
Implement PID control for precise speed regulation of a brushless motor.
#include <PID_v1.h>

#define MOTOR_PIN 9
#define ENCODER_PIN A0

double setpoint, input, output;
PID pid(&input, &output, &setpoint, 1, 0, 0, DIRECT);

void setup() {
    pinMode(MOTOR_PIN, OUTPUT);
    pid.SetMode(AUTOMATIC);
    pid.SetSampleTime(100);
}

void loop() {
    // Read motor speed from encoder or sensor
    input = analogRead(ENCODER_PIN);

    // Adjust setpoint for desired speed
    setpoint = 100;

    pid.Compute();
    analogWrite(MOTOR_PIN, output);
}
