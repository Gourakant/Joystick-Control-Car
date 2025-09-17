# Joystick-Control-Car
// === Pin Configurations ===
int joyXPin = A0;
int joyYPin = A1;
int buttonPin = 2;

int xVal;
int yVal;
int buttonState;

int ENApin = 5;
int IN1pin = 6;
int IN2pin = 7;
int IN3pin = 8;
int IN4pin = 9;
int ENBpin = 10;

// === Setup ===
void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ENApin, OUTPUT);
  pinMode(IN1pin, OUTPUT);
  pinMode(IN2pin, OUTPUT);
  pinMode(IN3pin, OUTPUT);
  pinMode(IN4pin, OUTPUT);
  pinMode(ENBpin, OUTPUT);

  Serial.begin(9600);
}

// === Helper Functions ===
void moveForward() {
  digitalWrite(IN1pin, HIGH);
  digitalWrite(IN2pin, LOW);
  digitalWrite(IN3pin, HIGH);
  digitalWrite(IN4pin, LOW);
  analogWrite(ENApin, 200);  // Speed control (0-255)
  analogWrite(ENBpin, 200);
}

void moveBackward() {
  digitalWrite(IN1pin, LOW);
  digitalWrite(IN2pin, HIGH);
  digitalWrite(IN3pin, LOW);
  digitalWrite(IN4pin, HIGH);
  analogWrite(ENApin, 200);
  analogWrite(ENBpin, 200);
}

void moveLeft() {
  digitalWrite(IN1pin, HIGH);
  digitalWrite(IN2pin, LOW);
  digitalWrite(IN3pin, LOW);
  digitalWrite(IN4pin, HIGH);
  analogWrite(ENApin, 180);
  analogWrite(ENBpin, 180);
}

void moveRight() {
  digitalWrite(IN1pin, LOW);
  digitalWrite(IN2pin, HIGH);
  digitalWrite(IN3pin, HIGH);
  digitalWrite(IN4pin, LOW);
  analogWrite(ENApin, 180);
  analogWrite(ENBpin, 180);
}

void stopCar() {
  digitalWrite(IN1pin, LOW);
  digitalWrite(IN2pin, LOW);
  digitalWrite(IN3pin, LOW);
  digitalWrite(IN4pin, LOW);
}

// === Loop ===
void loop() {
  xVal = analogRead(joyXPin);
  yVal = analogRead(joyYPin);
  buttonState = digitalRead(buttonPin);

  Serial.print("X: "); Serial.print(xVal);
  Serial.print(" | Y: "); Serial.print(yVal);
  Serial.print(" | Button: "); Serial.println(buttonState);

  // Joystick directions
  if (yVal > 600) {
    moveForward();
  } else if (yVal < 400) {
    moveBackward();
  } else if (xVal < 400) {
    moveLeft();
  } else if (xVal > 600) {
    moveRight();
  } else {
    stopCar();
  }
}
