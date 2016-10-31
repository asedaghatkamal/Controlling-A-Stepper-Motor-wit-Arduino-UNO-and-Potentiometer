# Controlling-A-Stepper-Motor-wit-Arduino-UNO-and-Potentiometer
/*
   MotorKnob

   A stepper motor follows the turns of a potentiometer
   (or other sensor) on analog input 0.

   http://www.arduino.cc/en/Reference/Stepper
   This example code is in the public domain.
*/

#include <Stepper.h>

// change this to the number of steps on your motor
#define STEPS 400

// create an instance of the stepper class, specifying
// the number of steps of the motor and the pins it's
// attached to
Stepper stepper(STEPS, 2, 3, 4, 5);

// the previous reading from the analog input
int previous = 0;

void setup() {
  // set the speed of the motor to 30 RPMs
  stepper.setSpeed(30);
  Serial.begin(9600);
}

void loop() {
  // get the sensor value
  int val = analogRead(A4);

  // move a number of steps equal to the change in the
  // sensor reading
  Serial.println(val );
  val = map(val, 0, 1023, 0, 800);
  if ((val > previous + 6) || (val < previous - 6)) {
    stepper.step(val - previous);
 Serial.println("!");
    // remember the previous value of the sensor
    previous = val;
  }
}
