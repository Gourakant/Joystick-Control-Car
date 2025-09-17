# Code 2
# Joystick-Control-Car-with-Obstacle-Avoiding
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

// === Ultrasonic Sensor Pins ===
int trigPin = 11;
int echoPin = 12;

// === Setup ===
void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ENApin, OUTPUT);
  pinMode(IN1pin, OUTPUT);
  pinMode(IN2pin, OUTPUT);
  pinMode(IN3pin, OUTPUT);
  pinMode(IN4pin, OUTPUT);
  pinMode(ENBpin, OUTPUT);

  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

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

// === Ultrasonic Distance Function ===
long getDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH);
  long distance = duration * 0.034 / 2;  // Convert to cm
  return distance;
}

// === Loop ===
void loop() {
  xVal = analogRead(joyXPin);
  yVal = analogRead(joyYPin);
  buttonState = digitalRead(buttonPin);

  long distance = getDistance();

  Serial.print("X: "); Serial.print(xVal);
  Serial.print(" | Y: "); Serial.print(yVal);
  Serial.print(" | Distance: "); Serial.print(distance); Serial.println(" cm");

  // Joystick directions with obstacle check
  if (yVal < 400 && distance > 10) {
    moveForward();
  } else if (yVal > 600) {
    moveBackward();
  } else if (xVal > 600) {
    moveLeft();
  } else if (xVal < 400) {
    moveRight();
  } else {
    stopCar();
  }
}


# Code 1
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
  if (yVal < 400 && distance > 10) {
    moveForward();
  } else if (yVal > 600) {
    moveBackward();
  } else if (xVal > 600) {
    moveLeft();
  } else if (xVal < 400) {
    moveRight();
  } else {
    stopCar();
  }
}

