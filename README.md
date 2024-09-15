```
// Define motor driver pins
#define IN1 7  // Motor 1 direction pin
#define IN2 6  // Motor 1 direction pin
#define IN3 5  // Motor 2 direction pin
#define IN4 4  // Motor 2 direction pin
#define ENA 9  // Motor 1 speed (PWM pin)
#define ENB 10 // Motor 2 speed (PWM pin)

char command; // Variable to store Bluetooth command

void setup() {
  // Set motor control pins as outputs
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);

  // Start serial communication for Bluetooth module at 9600 baud rate
  Serial.begin(9600);
}

void loop() {
  // Check if there's a command received via Bluetooth
  if (Serial.available() > 0) {
    command = Serial.read(); // Read the incoming data

    switch (command) {
      case 'F': // Forward
        moveForward();
        break;

      case 'B': // Backward
        moveBackward();
        break;

      case 'L': // Left
        turnLeft();
        break;

      case 'R': // Right
        turnRight();
        break;

      case 'S': // Stop
        stopCar();
        break;

      default:
        stopCar(); // Stop if no valid command is received
        break;
    }
  }
}

void moveForward() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
  analogWrite(ENA, 255); // Full speed
  analogWrite(ENB, 255); // Full speed
}

void moveBackward() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
  analogWrite(ENA, 255); // Full speed
  analogWrite(ENB, 255); // Full speed
}

void turnLeft() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
  analogWrite(ENA, 150); // Reduced speed for smooth turning
  analogWrite(ENB, 255); // Full speed
}

void turnRight() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
  analogWrite(ENA, 255); // Full speed
  analogWrite(ENB, 150); // Reduced speed for smooth turning
}

void stopCar() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
  analogWrite(ENA, 0);   // Stop motor 1
  analogWrite(ENB, 0);   // Stop motor 2
}
```
