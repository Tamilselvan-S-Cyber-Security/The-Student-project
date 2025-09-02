# 🕸️ Networking Projects Guide

## Basic Projects

### 1. Paper Cup Telephone
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Paper Cups | 2 | Sound transmission |
| String | 10-15 ft | Medium for sound waves |
| Nails/Clips | 2 | Secure string |
| Scissors | 1 | Cut string |

---

### 2. LAN Cable Model
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Colored Papers | 8 | Wire representation |
| Cardboard Base | 1 | Mounting surface |
| Glue | 1 | Secure wires |
| Labels | 8 | Pin identification |

---

### 3. Wi-Fi Range Test
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Smartphone | 1 | Wi-Fi receiver |
| Toy Car | 1 | Mobile platform |
| Measuring Tape | 1 | Distance measurement |
| Wi-Fi App | 1 | Signal analyzer |

---

### 4. Ping Pong Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Students | 2 | Network nodes |
| Message Cards | 10+ | Data packets |
| Timer | 1 | Transmission timing |
| Scoreboard | 1 | Success tracking |

---

### 5. Internet Map Drawing
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Large Paper | 1 | Network diagram |
| Colored Markers | 5+ | Visual representation |
| Device Stickers | 10+ | Network devices |
| Ruler | 1 | Straight lines |

---

## Intermediate Projects

### 6. Mini Switch with LEDs
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LEDs (Red, Green, Blue, Yellow) | 4 | Data routing indicators |
| Resistors (220Ω) | 4 | Current limiting |
| Breadboard | 1 | Circuit mounting |
| Jumper Wires | 10+ | Connections |
| Push Button | 1 | Input trigger |

**Arduino Code**:
```cpp
const int buttonPin = 2;
const int ledPins[] = {3, 4, 5, 6};
const int numLeds = 4;
int buttonState = 0;
int currentLed = 0;

void setup() {
  pinMode(buttonPin, INPUT);
  for(int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  if (buttonState == HIGH) {
    // Turn off all LEDs
    for(int i = 0; i < numLeds; i++) {
      digitalWrite(ledPins[i], LOW);
    }
    
    // Light next LED in sequence
    digitalWrite(ledPins[currentLed], HIGH);
    currentLed = (currentLed + 1) % numLeds;
    
    delay(500); // Prevent multiple triggers
  }
}
```

---

### 7. Chat with Walkie-Talkie
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Walkie-Talkies | 2 | Communication devices |
| Timer | 1 | Message timing |
| Message List | 1 | Test messages |
| Paper | 5+ | Notes |

---

### 8. Wi-Fi Interference Test
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Wi-Fi Router | 1 | Signal source |
| Smartphone | 1 | Signal receiver |
| Bluetooth Speaker | 1 | Interference source |
| Microwave | 1 | Additional interference |
| Wi-Fi Analyzer App | 1 | Signal measurement |

---

### 9. IP Address Cards Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Number Cards (0-255) | 256 | IP addresses |
| Network Mask Cards | 10+ | Subnet masks |
| Routing Table | 1 | Network paths |
| Students | 5+ | Network routers |

---

### 10. Create a Mini Home Network
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Laptop with Hotspot | 1 | Network source |
| Smartphone | 1 | Connected device |
| Smart Toy/Device | 1 | IoT device |
| Ethernet Cable | 1 | Wired connection |

---

## Advanced Projects

### 11. Build a Router in Simulation
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Cisco Packet Tracer | 1 | Network simulator |
| Network Files | 5+ | Configuration templates |
| Computer | 1 | Simulation platform |

---

### 12. Design a Smart Classroom Network
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Network Diagram Software | 1 | Design tool |
| Device Inventory | 1 | Equipment list |
| Bandwidth Calculator | 1 | Capacity planning |

---

### 13. Data Packet Race Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Students | 10+ | Network nodes |
| Data Envelopes | 20+ | Data packets |
| Network Topology Map | 1 | Route planning |

---

### 14. Firewall Model with Switches
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Network Switches | 2+ | Data routing |
| Firewall Rules | 10+ | Security policies |
| Data Packets | 20+ | Test messages |

---

### 15. Cloud Storage Simulation
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Google Drive Account | 1 | Cloud storage |
| Shared Folders | 5+ | Data sharing |
| Multiple Devices | 3+ | Access points |

---

## Arduino Code for Network Projects

### Basic Network Monitor
```cpp
#include <WiFi.h>

const char* ssid = "YourWiFi";
const char* password = "YourPassword";

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  
  Serial.println("WiFi connected!");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  if (WiFi.status() == WL_CONNECTED) {
    Serial.println("WiFi: Connected");
  } else {
    Serial.println("WiFi: Disconnected");
  }
  delay(1000);
}
```

### Network Traffic Light
```cpp
const int redPin = 13;
const int yellowPin = 12;
const int greenPin = 11;
const int buttonPin = 2;

int currentState = 0; // 0=Red, 1=Yellow, 2=Green

void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(yellowPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    changeLight();
    delay(500);
  }
}

void changeLight() {
  // Turn off all lights
  digitalWrite(redPin, LOW);
  digitalWrite(yellowPin, LOW);
  digitalWrite(greenPin, LOW);
  
  // Turn on next light
  switch(currentState) {
    case 0: // Red
      digitalWrite(greenPin, HIGH);
      currentState = 2;
      break;
    case 1: // Yellow
      digitalWrite(redPin, HIGH);
      currentState = 0;
      break;
    case 2: // Green
      digitalWrite(yellowPin, HIGH);
      currentState = 1;
      break;
  }
}
```

### Simple Network Switch
```cpp
const int inputPins[] = {2, 3, 4, 5};
const int outputPins[] = {6, 7, 8, 9};
const int numPorts = 4;

void setup() {
  for(int i = 0; i < numPorts; i++) {
    pinMode(inputPins[i], INPUT_PULLUP);
    pinMode(outputPins[i], OUTPUT);
  }
}

void loop() {
  for(int i = 0; i < numPorts; i++) {
    if(digitalRead(inputPins[i]) == LOW) {
      // Route signal to corresponding output
      digitalWrite(outputPins[i], HIGH);
      delay(100);
      digitalWrite(outputPins[i], LOW);
    }
  }
}
```
# 🤖 Robotics Projects Guide

## Basic Projects

### 1. Brush Bot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Toothbrush Head | 1 | Robot body |
| DC Motor (3V) | 1 | Movement power |
| Coin Cell Battery (3V) | 1 | Power source |
| Double-sided Tape | 1 | Mounting |
| Small Wires | 2 | Electrical connection |

---

### 2. Line Follower with Black Tape
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Toy Car Chassis | 1 | Robot base |
| Black Electrical Tape | 1 | Track lines |
| White Surface | 1 | Track background |
| Markers | 1 | Track design |

---

### 3. Balloon Powered Car
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Plastic Bottle | 1 | Car body |
| Balloon | 1 | Propulsion |
| Straw | 1 | Air direction |
| Cardboard Wheels | 4 | Movement |
| Glue | 1 | Assembly |

---

### 4. Dancing Robot (LEGO or DIY kit)
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| LEGO Mindstorms Kit | 1 | Robot platform |
| Servo Motors | 2-4 | Joint movement |
| Controller | 1 | Movement commands |
| Battery Pack | 1 | Power source |

---

### 5. Handmade Robotic Arm (Cardboard + String)
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Cardboard | 1 | Arm structure |
| String | 2 | Movement control |
| Straws | 3 | Joints |
| Glue | 1 | Assembly |
| Scissors | 1 | Cutting |

---

## Intermediate Projects

### 6. Obstacle Avoider Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Ultrasonic Sensor (HC-SR04) | 1 | Distance detection |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 10+ | Connections |

**Arduino Code**:
```cpp
#include <NewPing.h>

#define TRIGGER_PIN 12
#define ECHO_PIN 11
#define MAX_DISTANCE 200
#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10

NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE);

void setup() {
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int distance = sonar.ping_cm();
  
  if (distance == 0) distance = 200;
  
  if (distance < 20) {
    // Obstacle detected - turn right
    turnRight();
    delay(500);
  } else {
    // No obstacle - move forward
    moveForward();
  }
  
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}
```

---

### 7. Light Follower Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LDR Sensors | 2 | Light detection |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 10+ | Connections |

**Arduino Code**:
```cpp
#define LEFT_LDR A0
#define RIGHT_LDR A1
#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10

void setup() {
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int leftLight = analogRead(LEFT_LDR);
  int rightLight = analogRead(RIGHT_LDR);
  
  Serial.print("Left: "); Serial.print(leftLight);
  Serial.print(" Right: "); Serial.println(rightLight);
  
  if (leftLight > rightLight + 50) {
    // More light on left - turn left
    turnLeft();
  } else if (rightLight > leftLight + 50) {
    // More light on right - turn right
    turnRight();
  } else {
    // Equal light - move forward
    moveForward();
  }
  
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnLeft() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}
```

---

### 8. Clapping Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Sound Sensor | 1 | Clap detection |
| Servo Motor | 1 | Movement |
| LED | 1 | Status indicator |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 5+ | Connections |

**Arduino Code**:
```cpp
#define SOUND_SENSOR A0
#define SERVO_PIN 9
#define LED_PIN 13

#include <Servo.h>
Servo myServo;

int soundThreshold = 500;
int servoPos = 0;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  myServo.attach(SERVO_PIN);
  Serial.begin(9600);
}

void loop() {
  int soundLevel = analogRead(SOUND_SENSOR);
  
  if (soundLevel > soundThreshold) {
    // Clap detected
    digitalWrite(LED_PIN, HIGH);
    moveServo();
    delay(1000);
    digitalWrite(LED_PIN, LOW);
  }
  
  delay(100);
}

void moveServo() {
  for (int pos = 0; pos <= 180; pos += 10) {
    myServo.write(pos);
    delay(15);
  }
  for (int pos = 180; pos >= 0; pos -= 10) {
    myServo.write(pos);
    delay(15);
  }
}
```

---

### 9. Maze Solver Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| IR Sensors | 3 | Line detection |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 15+ | Connections |

**Arduino Code**:
```cpp
#define LEFT_IR 2
#define CENTER_IR 3
#define RIGHT_IR 4
#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10

void setup() {
  pinMode(LEFT_IR, INPUT);
  pinMode(CENTER_IR, INPUT);
  pinMode(RIGHT_IR, INPUT);
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
}

void loop() {
  int leftIR = digitalRead(LEFT_IR);
  int centerIR = digitalRead(CENTER_IR);
  int rightIR = digitalRead(RIGHT_IR);
  
  if (centerIR == LOW) {
    // Line detected in center - move forward
    moveForward();
  } else if (leftIR == LOW) {
    // Line detected on left - turn left
    turnLeft();
  } else if (rightIR == LOW) {
    // Line detected on right - turn right
    turnRight();
  } else {
    // No line detected - search
    searchLine();
  }
  
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnLeft() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void searchLine() {
  // Turn left to search for line
  turnLeft();
  delay(200);
}
```

---

### 10. Voice-Controlled Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Bluetooth Module (HC-05) | 1 | Wireless control |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 15+ | Connections |

**Arduino Code**:
```cpp
#include <SoftwareSerial.h>

#define BT_RX 2
#define BT_TX 3
#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10

SoftwareSerial bluetooth(BT_RX, BT_TX);
char command;

void setup() {
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
  
  bluetooth.begin(9600);
  Serial.begin(9600);
}

void loop() {
  if (bluetooth.available()) {
    command = bluetooth.read();
    Serial.println(command);
    
    switch(command) {
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
        stopRobot();
        break;
    }
  }
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void moveBackward() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void turnLeft() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void stopRobot() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}
```

---

## Advanced Projects

### 11. Smart Dustbin Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Ultrasonic Sensor | 1 | Proximity detection |
| Servo Motor | 1 | Lid control |
| LED | 1 | Status indicator |
| Buzzer | 1 | Sound alert |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 8+ | Connections |

**Arduino Code**:
```cpp
#include <Servo.h>

#define TRIGGER_PIN 12
#define ECHO_PIN 11
#define SERVO_PIN 9
#define LED_PIN 13
#define BUZZER_PIN 8

Servo lidServo;
int lidOpen = false;

void setup() {
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  
  lidServo.attach(SERVO_PIN);
  lidServo.write(0); // Close lid
  
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);
  
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2;
  
  if (distance < 20 && !lidOpen) {
    // Person detected - open lid
    openLid();
  } else if (distance >= 20 && lidOpen) {
    // Person left - close lid
    closeLid();
  }
  
  delay(100);
}

void openLid() {
  lidServo.write(90);
  digitalWrite(LED_PIN, HIGH);
  tone(BUZZER_PIN, 1000, 200);
  lidOpen = true;
}

void closeLid() {
  lidServo.write(0);
  digitalWrite(LED_PIN, LOW);
  lidOpen = false;
}
```

---

### 12. Fire Fighting Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Flame Sensors | 3 | Fire detection |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Water Pump | 1 | Fire extinguishing |
| Relay Module | 1 | Pump control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (12V) | 1 | Power source |
| Jumper Wires | 20+ | Connections |

**Arduino Code**:
```cpp
#define LEFT_FLAME A0
#define CENTER_FLAME A1
#define RIGHT_FLAME A2
#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10
#define PUMP_PIN 7

void setup() {
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
  pinMode(PUMP_PIN, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  int leftFlame = analogRead(LEFT_FLAME);
  int centerFlame = analogRead(CENTER_FLAME);
  int rightFlame = analogRead(RIGHT_FLAME);
  
  Serial.print("Left: "); Serial.print(leftFlame);
  Serial.print(" Center: "); Serial.print(centerFlame);
  Serial.print(" Right: "); Serial.println(rightFlame);
  
  if (centerFlame < 100) {
    // Fire detected in center - move forward and spray
    moveForward();
    activatePump();
  } else if (leftFlame < 100) {
    // Fire detected on left - turn left
    turnLeft();
  } else if (rightFlame < 100) {
    // Fire detected on right - turn right
    turnRight();
  } else {
    // No fire detected - stop
    stopRobot();
    deactivatePump();
  }
  
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnLeft() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void stopRobot() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void activatePump() {
  digitalWrite(PUMP_PIN, HIGH);
}

void deactivatePump() {
  digitalWrite(PUMP_PIN, LOW);
}
```

---

### 13. Gesture-Controlled Robot
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Accelerometer (MPU6050) | 1 | Hand gesture detection |
| DC Motors | 2 | Wheel movement |
| Motor Driver (L298N) | 1 | Motor control |
| Chassis | 1 | Robot body |
| Wheels | 2 | Movement |
| Battery (9V) | 1 | Power source |
| Jumper Wires | 15+ | Connections |

**Arduino Code**:
```cpp
#include <Wire.h>

#define LEFT_MOTOR_FWD 5
#define LEFT_MOTOR_BWD 6
#define RIGHT_MOTOR_FWD 9
#define RIGHT_MOTOR_BWD 10

int16_t AcX, AcY, AcZ;

void setup() {
  Wire.begin();
  Wire.beginTransmission(0x68);
  Wire.write(0x6B);
  Wire.write(0);
  Wire.endTransmission(true);
  
  pinMode(LEFT_MOTOR_FWD, OUTPUT);
  pinMode(LEFT_MOTOR_BWD, OUTPUT);
  pinMode(RIGHT_MOTOR_FWD, OUTPUT);
  pinMode(RIGHT_MOTOR_BWD, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  Wire.beginTransmission(0x68);
  Wire.write(0x3B);
  Wire.endTransmission(false);
  Wire.requestFrom(0x68, 6, true);
  
  AcX = Wire.read() << 8 | Wire.read();
  AcY = Wire.read() << 8 | Wire.read();
  AcZ = Wire.read() << 8 | Wire.read();
  
  // Gesture control based on accelerometer values
  if (AcY > 5000) {
    // Tilt forward - move forward
    moveForward();
  } else if (AcY < -5000) {
    // Tilt backward - move backward
    moveBackward();
  } else if (AcX > 5000) {
    // Tilt right - turn right
    turnRight();
  } else if (AcX < -5000) {
    // Tilt left - turn left
    turnLeft();
  } else {
    // Level - stop
    stopRobot();
  }
  
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void moveBackward() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void turnLeft() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, HIGH);
  digitalWrite(RIGHT_MOTOR_FWD, HIGH);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}

void turnRight() {
  digitalWrite(LEFT_MOTOR_FWD, HIGH);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, HIGH);
}

void stopRobot() {
  digitalWrite(LEFT_MOTOR_FWD, LOW);
  digitalWrite(LEFT_MOTOR_BWD, LOW);
  digitalWrite(RIGHT_MOTOR_FWD, LOW);
  digitalWrite(RIGHT_MOTOR_BWD, LOW);
}
```

---

### 14. Humanoid Robot (DIY)
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Mega | 1 | Microcontroller |
| Servo Motors | 8+ | Joint movement |
| Servo Controller | 1 | Servo management |
| Chassis Parts | 1 | Robot body |
| Battery (12V) | 1 | Power source |
| Jumper Wires | 25+ | Connections |

**Arduino Code**:
```cpp
#include <Servo.h>

Servo headServo;
Servo leftArmServo;
Servo rightArmServo;
Servo leftLegServo;
Servo rightLegServo;

int headPos = 90;
int armPos = 90;
int legPos = 90;

void setup() {
  headServo.attach(2);
  leftArmServo.attach(3);
  rightArmServo.attach(4);
  leftLegServo.attach(5);
  rightLegServo.attach(6);
  
  // Initialize positions
  headServo.write(headPos);
  leftArmServo.write(armPos);
  rightArmServo.write(armPos);
  leftLegServo.write(legPos);
  rightLegServo.write(legPos);
  
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) {
    char command = Serial.read();
    
    switch(command) {
      case 'H': // Head movement
        moveHead();
        break;
      case 'A': // Arm movement
        moveArms();
        break;
      case 'L': // Leg movement
        moveLegs();
        break;
      case 'W': // Wave
        wave();
        break;
      case 'D': // Dance
        dance();
        break;
    }
  }
}

void moveHead() {
  for (int i = 0; i <= 180; i += 10) {
    headServo.write(i);
    delay(100);
  }
  for (int i = 180; i >= 0; i -= 10) {
    headServo.write(i);
    delay(100);
  }
  headServo.write(90);
}

void moveArms() {
  leftArmServo.write(0);
  rightArmServo.write(180);
  delay(1000);
  leftArmServo.write(180);
  rightArmServo.write(0);
  delay(1000);
  leftArmServo.write(90);
  rightArmServo.write(90);
}

void moveLegs() {
  leftLegServo.write(45);
  rightLegServo.write(135);
  delay(500);
  leftLegServo.write(135);
  rightLegServo.write(45);
  delay(500);
  leftLegServo.write(90);
  rightLegServo.write(90);
}

void wave() {
  for (int i = 0; i < 3; i++) {
    rightArmServo.write(0);
    delay(500);
    rightArmServo.write(180);
    delay(500);
  }
  rightArmServo.write(90);
}

void dance() {
  for (int i = 0; i < 4; i++) {
    moveArms();
    moveLegs();
    delay(500);
  }
}
```

---

### 15. Drone Project (Basic Coding)
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Nano | 1 | Flight controller |
| MPU6050 | 1 | Orientation sensor |
| Brushless Motors | 4 | Propulsion |
| ESC Controllers | 4 | Motor control |
| Frame | 1 | Drone structure |
| Propellers | 4 | Lift generation |
| Battery (3S LiPo) | 1 | Power source |
| Radio Receiver | 1 | Remote control |
| Jumper Wires | 20+ | Connections |

**Arduino Code**:
```cpp
#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;

// Motor pins
#define MOTOR1 3
#define MOTOR2 5
#define MOTOR3 6
#define MOTOR4 9

// PID variables
float Kp = 2.0;
float Ki = 0.1;
float Kd = 0.5;

float error, lastError, integral;
float setpoint = 0;

void setup() {
  Wire.begin();
  mpu.initialize();
  
  pinMode(MOTOR1, OUTPUT);
  pinMode(MOTOR2, OUTPUT);
  pinMode(MOTOR3, OUTPUT);
  pinMode(MOTOR4, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  int16_t ax, ay, az;
  int16_t gx, gy, gz;
  
  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
  
  // Calculate roll angle
  float roll = atan2(ay, az) * 180/PI;
  
  // PID control
  error = setpoint - roll;
  integral += error;
  float derivative = error - lastError;
  
  float output = Kp * error + Ki * integral + Kd * derivative;
  
  // Apply to motors
  int baseSpeed = 150;
  int leftSpeed = baseSpeed + output;
  int rightSpeed = baseSpeed - output;
  
  // Constrain speeds
  leftSpeed = constrain(leftSpeed, 0, 255);
  rightSpeed = constrain(rightSpeed, 0, 255);
  
  // Set motor speeds
  analogWrite(MOTOR1, leftSpeed);
  analogWrite(MOTOR2, leftSpeed);
  analogWrite(MOTOR3, rightSpeed);
  analogWrite(MOTOR4, rightSpeed);
  
  lastError = error;
  
  Serial.print("Roll: "); Serial.print(roll);
  Serial.print(" Output: "); Serial.println(output);
  
  delay(50);
}
```

---

## Arduino Code for Basic Robot Functions

### Motor Control Library
```cpp
class RobotMotors {
  private:
    int leftMotorFwd, leftMotorBwd;
    int rightMotorFwd, rightMotorBwd;
    
  public:
    RobotMotors(int lf, int lb, int rf, int rb) {
      leftMotorFwd = lf;
      leftMotorBwd = lb;
      rightMotorFwd = rf;
      rightMotorBwd = rb;
      
      pinMode(leftMotorFwd, OUTPUT);
      pinMode(leftMotorBwd, OUTPUT);
      pinMode(rightMotorFwd, OUTPUT);
      pinMode(rightMotorBwd, OUTPUT);
    }
    
    void forward() {
      digitalWrite(leftMotorFwd, HIGH);
      digitalWrite(leftMotorBwd, LOW);
      digitalWrite(rightMotorFwd, HIGH);
      digitalWrite(rightMotorBwd, LOW);
    }
    
    void backward() {
      digitalWrite(leftMotorFwd, LOW);
      digitalWrite(leftMotorBwd, HIGH);
      digitalWrite(rightMotorFwd, LOW);
      digitalWrite(rightMotorBwd, HIGH);
    }
    
    void turnLeft() {
      digitalWrite(leftMotorFwd, LOW);
      digitalWrite(leftMotorBwd, HIGH);
      digitalWrite(rightMotorFwd, HIGH);
      digitalWrite(rightMotorBwd, LOW);
    }
    
    void turnRight() {
      digitalWrite(leftMotorFwd, HIGH);
      digitalWrite(leftMotorBwd, LOW);
      digitalWrite(rightMotorFwd, LOW);
      digitalWrite(rightMotorBwd, HIGH);
    }
    
    void stop() {
      digitalWrite(leftMotorFwd, LOW);
      digitalWrite(leftMotorBwd, LOW);
      digitalWrite(rightMotorFwd, LOW);
      digitalWrite(rightMotorBwd, LOW);
    }
};
```
# 🔐 Cybersecurity Projects Guide

## Basic Projects

### 1. Secret Code Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display (16x2) | 1 | Code display |
| Keypad (4x4) | 1 | Code input |
| LED | 1 | Status indicator |
| Buzzer | 1 | Sound feedback |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>
#include <Keypad.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const byte ROWS = 4;
const byte COLS = 4;
char hexaKeys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};
byte rowPins[ROWS] = {9, 8, 7, 6};
byte colPins[COLS] = {A0, A1, A2, A3};
Keypad customKeypad = Keypad(makeKeymap(hexaKeys), rowPins, colPins, ROWS, COLS);

const int ledPin = 13;
const int buzzerPin = 10;
String secretCode = "1234";
String inputCode = "";

void setup() {
  lcd.begin(16, 2);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  lcd.print("Enter Code:");
}

void loop() {
  char key = customKeypad.getKey();
  if (key) {
    if (key == '#') {
      checkCode();
    } else if (key == '*') {
      inputCode = "";
      lcd.clear();
      lcd.print("Code Reset");
      delay(1000);
      lcd.clear();
      lcd.print("Enter Code:");
    } else {
      inputCode += key;
      lcd.setCursor(0, 1);
      lcd.print(inputCode);
    }
  }
}

void checkCode() {
  if (inputCode == secretCode) {
    lcd.clear();
    lcd.print("Access Granted!");
    digitalWrite(ledPin, HIGH);
    tone(buzzerPin, 1000, 500);
    delay(2000);
    digitalWrite(ledPin, LOW);
  } else {
    lcd.clear();
    lcd.print("Access Denied!");
    tone(buzzerPin, 200, 1000);
    delay(2000);
  }
  inputCode = "";
  lcd.clear();
  lcd.print("Enter Code:");
}
```

---

### 2. Caesar Cipher Wheel
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Rotary Encoder | 1 | Shift selection |
| LCD Display | 1 | Text output |
| Button | 1 | Input trigger |
| LED | 1 | Status indicator |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int encoderPin = 2;
const int buttonPin = 8;
const int ledPin = 13;

int shift = 0;
String message = "HELLO WORLD";
String encrypted = "";

void setup() {
  lcd.begin(16, 2);
  pinMode(encoderPin, INPUT);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  attachInterrupt(digitalPinToInterrupt(encoderPin), encoderISR, RISING);
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    encryptMessage();
    delay(500);
  }
  
  lcd.setCursor(0, 0);
  lcd.print("Shift: " + String(shift));
  lcd.setCursor(0, 1);
  lcd.print(message);
}

void encoderISR() {
  shift = (shift + 1) % 26;
}

void encryptMessage() {
  encrypted = "";
  for (int i = 0; i < message.length(); i++) {
    char c = message[i];
    if (c >= 'A' && c <= 'Z') {
      c = ((c - 'A' + shift) % 26) + 'A';
    }
    encrypted += c;
  }
  
  lcd.clear();
  lcd.print("Encrypted:");
  lcd.setCursor(0, 1);
  lcd.print(encrypted);
  digitalWrite(ledPin, HIGH);
  delay(2000);
  digitalWrite(ledPin, LOW);
}
```

---

### 3. Password Strength Test
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Password display |
| Keypad | 1 | Password input |
| LED (3) | 3 | Strength indicators |
| Buzzer | 1 | Sound feedback |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>
#include <Keypad.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int redLed = 13;
const int yellowLed = 12;
const int greenLed = 11;
const int buzzerPin = 10;

String password = "";
int strength = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(redLed, OUTPUT);
  pinMode(yellowLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  lcd.print("Enter Password:");
}

void loop() {
  char key = getKey();
  if (key) {
    if (key == '#') {
      testPasswordStrength();
    } else if (key == '*') {
      password = "";
      lcd.clear();
      lcd.print("Password Reset");
      delay(1000);
      lcd.clear();
      lcd.print("Enter Password:");
    } else {
      password += key;
      lcd.setCursor(0, 1);
      lcd.print(password);
    }
  }
}

void testPasswordStrength() {
  strength = 0;
  
  // Length check
  if (password.length() >= 8) strength += 2;
  else if (password.length() >= 6) strength += 1;
  
  // Complexity checks
  if (hasUpperCase(password)) strength += 1;
  if (hasLowerCase(password)) strength += 1;
  if (hasNumbers(password)) strength += 1;
  if (hasSpecialChars(password)) strength += 1;
  
  displayStrength();
}

void displayStrength() {
  lcd.clear();
  lcd.print("Strength: " + String(strength) + "/5");
  
  if (strength <= 2) {
    digitalWrite(redLed, HIGH);
    tone(buzzerPin, 200, 1000);
  } else if (strength <= 3) {
    digitalWrite(yellowLed, HIGH);
    tone(buzzerPin, 500, 500);
  } else {
    digitalWrite(greenLed, HIGH);
    tone(buzzerPin, 1000, 200);
  }
  
  delay(2000);
  digitalWrite(redLed, LOW);
  digitalWrite(yellowLed, LOW);
  digitalWrite(greenLed, LOW);
}
```

---

### 4. Treasure Hunt with Clues
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Clue display |
| RFID Reader | 1 | Tag detection |
| RFID Tags | 5+ | Clue triggers |
| LED | 1 | Status indicator |
| Buzzer | 1 | Sound feedback |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>
#include <SPI.h>
#include <MFRC522.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
MFRC522 rfid(10, 9);
const int ledPin = 13;
const int buzzerPin = 8;

String clues[] = {
  "Find the red door",
  "Look under the table",
  "Check the bookshelf",
  "Behind the curtain",
  "Final treasure found!"
};

int currentClue = 0;

void setup() {
  lcd.begin(16, 2);
  SPI.begin();
  rfid.PCD_Init();
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  lcd.print("Find RFID Tags!");
  lcd.setCursor(0, 1);
  lcd.print("Clue: " + String(currentClue + 1));
}

void loop() {
  if (rfid.PICC_IsNewCardPresent() && rfid.PICC_ReadCardSerial()) {
    processRFID();
    delay(1000);
  }
}

void processRFID() {
  currentClue++;
  if (currentClue < 5) {
    lcd.clear();
    lcd.print("Clue " + String(currentClue + 1) + ":");
    lcd.setCursor(0, 1);
    lcd.print(clues[currentClue]);
    
    digitalWrite(ledPin, HIGH);
    tone(buzzerPin, 1000, 500);
    delay(2000);
    digitalWrite(ledPin, LOW);
  } else {
    lcd.clear();
    lcd.print("Congratulations!");
    lcd.setCursor(0, 1);
    lcd.print("You found it!");
    
    digitalWrite(ledPin, HIGH);
    tone(buzzerPin, 2000, 2000);
    delay(3000);
    digitalWrite(ledPin, LOW);
  }
}
```

---

### 5. Digital Safety Poster
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Computer | 1 | Design tool |
| Design Software | 1 | Poster creation |
| Printer | 1 | Output device |
| Paper | 1 | Print medium |
| Markers | 5+ | Decoration |

---

## Intermediate Projects

### 6. Build a Simple Login Page
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Ethernet Shield | 1 | Network connection |
| LCD Display | 1 | Status display |
| LED | 1 | Connection status |
| SD Card | 1 | Web page storage |
| Battery (12V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <SPI.h>
#include <Ethernet.h>
#include <SD.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
IPAddress ip(192, 168, 1, 177);
EthernetServer server(80);

const int ledPin = 13;
String username = "admin";
String password = "password123";

void setup() {
  lcd.begin(16, 2);
  pinMode(ledPin, OUTPUT);
  
  if (Ethernet.begin(mac) == 0) {
    lcd.print("Failed to configure");
    lcd.setCursor(0, 1);
    lcd.print("Ethernet using DHCP");
    return;
  }
  
  server.begin();
  lcd.print("Server at:");
  lcd.setCursor(0, 1);
  lcd.print(Ethernet.localIP());
  digitalWrite(ledPin, HIGH);
}

void loop() {
  EthernetClient client = server.available();
  if (client) {
    String currentLine = "";
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        if (c == '\n') {
          if (currentLine.length() == 0) {
            sendLoginPage(client);
            break;
          } else {
            currentLine = "";
          }
        } else if (c != '\r') {
          currentLine += c;
        }
      }
    }
    client.stop();
  }
}

void sendLoginPage(EthernetClient client) {
  client.println("HTTP/1.1 200 OK");
  client.println("Content-Type: text/html");
  client.println();
  client.println("<html><body>");
  client.println("<h1>Login Page</h1>");
  client.println("<form method='post'>");
  client.println("Username: <input type='text' name='username'><br>");
  client.println("Password: <input type='password' name='password'><br>");
  client.println("<input type='submit' value='Login'>");
  client.println("</form></body></html>");
}
```

---

### 7. Encryption with Colors
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| RGB LED | 1 | Color output |
| Light Sensor | 1 | Color detection |
| LCD Display | 1 | Message display |
| Button | 1 | Input trigger |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;
const int lightSensorPin = A0;
const int buttonPin = 8;

String message = "HELLO";
String encrypted = "";

void setup() {
  lcd.begin(16, 2);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
  
  lcd.print("Color Encryption");
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    encryptMessage();
    delay(2000);
  }
}

void encryptMessage() {
  lcd.clear();
  lcd.print("Encrypting...");
  
  for (int i = 0; i < message.length(); i++) {
    char c = message[i];
    int ascii = (int)c;
    
    // Convert ASCII to RGB values
    int red = (ascii * 7) % 256;
    int green = (ascii * 11) % 256;
    int blue = (ascii * 13) % 256;
    
    analogWrite(redPin, red);
    analogWrite(greenPin, green);
    analogWrite(bluePin, blue);
    
    delay(1000);
  }
  
  // Turn off LED
  analogWrite(redPin, 0);
  analogWrite(greenPin, 0);
  analogWrite(bluePin, 0);
  
  lcd.clear();
  lcd.print("Message Encrypted!");
  lcd.setCursor(0, 1);
  lcd.print("Check RGB LED");
}
```

---

### 8. Phishing Awareness Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Game display |
| Buttons (2) | 2 | Answer selection |
| LED (2) | 2 | Result indicators |
| Buzzer | 1 | Sound feedback |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int button1Pin = 2;
const int button2Pin = 3;
const int greenLed = 13;
const int redLed = 12;
const int buzzerPin = 8;

String questions[] = {
  "Is this email safe?",
  "Click this link?",
  "Share password?",
  "Download file?",
  "Verify account?"
};

bool answers[] = {false, false, false, false, false};
int currentQuestion = 0;
int score = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(button1Pin, INPUT_PULLUP);
  pinMode(button2Pin, INPUT_PULLUP);
  pinMode(greenLed, OUTPUT);
  pinMode(redLed, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  displayQuestion();
}

void loop() {
  if (digitalRead(button1Pin) == LOW) {
    checkAnswer(true);
  } else if (digitalRead(button2Pin) == LOW) {
    checkAnswer(false);
  }
}

void displayQuestion() {
  lcd.clear();
  lcd.print(questions[currentQuestion]);
  lcd.setCursor(0, 1);
  lcd.print("Yes(1) No(2)");
}

void checkAnswer(bool answer) {
  if (answer == answers[currentQuestion]) {
    score++;
    digitalWrite(greenLed, HIGH);
    tone(buzzerPin, 1000, 500);
    lcd.setCursor(0, 1);
    lcd.print("Correct! Score: " + String(score));
  } else {
    digitalWrite(redLed, HIGH);
    tone(buzzerPin, 200, 1000);
    lcd.setCursor(0, 1);
    lcd.print("Wrong! Score: " + String(score));
  }
  
  delay(2000);
  digitalWrite(greenLed, LOW);
  digitalWrite(redLed, LOW);
  
  currentQuestion++;
  if (currentQuestion < 5) {
    displayQuestion();
  } else {
    gameOver();
  }
}

void gameOver() {
  lcd.clear();
  lcd.print("Game Over!");
  lcd.setCursor(0, 1);
  lcd.print("Final Score: " + String(score) + "/5");
}
```

---

### 9. Firewall Simulation with Cards
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Status display |
| Buttons (3) | 3 | Rule selection |
| LED (3) | 3 | Rule indicators |
| Buzzer | 1 | Alert sound |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int allowButton = 2;
const int blockButton = 3;
const int resetButton = 4;
const int allowLed = 13;
const int blockLed = 12;
const int alertLed = 11;
const int buzzerPin = 8;

String requests[] = {
  "HTTP Request",
  "FTP Connection",
  "Email Download",
  "File Upload",
  "Database Query"
};

bool allowed[] = {true, false, true, false, true};
int currentRequest = 0;
int correctDecisions = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(allowButton, INPUT_PULLUP);
  pinMode(blockButton, INPUT_PULLUP);
  pinMode(resetButton, INPUT_PULLUP);
  pinMode(allowLed, OUTPUT);
  pinMode(blockLed, OUTPUT);
  pinMode(alertLed, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  displayRequest();
}

void loop() {
  if (digitalRead(allowButton) == LOW) {
    makeDecision(true);
  } else if (digitalRead(blockButton) == LOW) {
    makeDecision(false);
  } else if (digitalRead(resetButton) == LOW) {
    resetGame();
  }
}

void displayRequest() {
  lcd.clear();
  lcd.print("Request: " + String(currentRequest + 1));
  lcd.setCursor(0, 1);
  lcd.print(requests[currentRequest]);
}

void makeDecision(bool allow) {
  if (allow == allowed[currentRequest]) {
    correctDecisions++;
    digitalWrite(allowLed, HIGH);
    tone(buzzerPin, 1000, 200);
    lcd.setCursor(0, 1);
    lcd.print("Correct! Score: " + String(correctDecisions));
  } else {
    digitalWrite(blockLed, HIGH);
    digitalWrite(alertLed, HIGH);
    tone(buzzerPin, 200, 1000);
    lcd.setCursor(0, 1);
    lcd.print("Wrong! Score: " + String(correctDecisions));
  }
  
  delay(2000);
  digitalWrite(allowLed, LOW);
  digitalWrite(blockLed, LOW);
  digitalWrite(alertLed, LOW);
  
  currentRequest++;
  if (currentRequest < 5) {
    displayRequest();
  } else {
    gameOver();
  }
}

void resetGame() {
  currentRequest = 0;
  correctDecisions = 0;
  displayRequest();
}

void gameOver() {
  lcd.clear();
  lcd.print("Firewall Test Done!");
  lcd.setCursor(0, 1);
  lcd.print("Score: " + String(correctDecisions) + "/5");
}
```

---

### 10. QR Code Secret Message
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Message display |
| Button | 1 | Generate trigger |
| LED | 1 | Status indicator |
| Computer | 1 | QR generation |
| QR Code Library | 1 | Code creation |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int buttonPin = 8;
const int ledPin = 13;

String messages[] = {
  "Hello World!",
  "Secret Message",
  "Arduino Rocks!",
  "Cybersecurity",
  "QR Code Test"
};

int currentMessage = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  
  lcd.print("QR Code Generator");
  lcd.setCursor(0, 1);
  lcd.print("Press Button");
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    generateQRMessage();
    delay(1000);
  }
}

void generateQRMessage() {
  digitalWrite(ledPin, HIGH);
  
  lcd.clear();
  lcd.print("Message " + String(currentMessage + 1));
  lcd.setCursor(0, 1);
  lcd.print(messages[currentMessage]);
  
  // Send to serial for QR generation
  Serial.println("QR:" + messages[currentMessage]);
  
  currentMessage = (currentMessage + 1) % 5;
  
  delay(2000);
  digitalWrite(ledPin, LOW);
  
  lcd.clear();
  lcd.print("QR Code Generated!");
  lcd.setCursor(0, 1);
  lcd.print("Check Serial");
}
```

---

## Advanced Projects

### 11. Simple Ethical Hacking Lab
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Computer | 1 | Testing platform |
| Kali Linux | 1 | Penetration testing |
| Network Switch | 1 | Network testing |
| Target Devices | 2+ | Vulnerability testing |
| Ethernet Cables | 3+ | Network connections |
| USB Drive | 1 | Bootable media |

---

### 12. Network Sniffing Demo
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Ethernet Shield | 1 | Network interface |
| LCD Display | 1 | Packet display |
| LED | 1 | Activity indicator |
| SD Card | 1 | Log storage |
| Battery (12V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <SPI.h>
#include <Ethernet.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
IPAddress ip(192, 168, 1, 100);
EthernetClient client;

const int ledPin = 13;
int packetCount = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(ledPin, OUTPUT);
  
  if (Ethernet.begin(mac) == 0) {
    lcd.print("DHCP Failed");
    return;
  }
  
  lcd.print("Network Monitor");
  lcd.setCursor(0, 1);
  lcd.print("IP: " + String(Ethernet.localIP()[0]));
}

void loop() {
  // Simulate packet monitoring
  if (millis() % 5000 == 0) {
    packetCount++;
    displayPacketInfo();
    digitalWrite(ledPin, HIGH);
    delay(100);
    digitalWrite(ledPin, LOW);
  }
}

void displayPacketInfo() {
  lcd.clear();
  lcd.print("Packets: " + String(packetCount));
  lcd.setCursor(0, 1);
  lcd.print("Time: " + String(millis()/1000) + "s");
}
```

---

### 13. Build Your Own Captcha System
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| Touch Screen | 1 | User interface |
| SD Card Module | 1 | Image storage |
| Speaker | 1 | Audio output |
| LED | 1 | Status indicator |
| Battery (12V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <SD.h>
#include <SPI.h>
#include <TFT.h>

TFT screen = TFT(9, 8, 7);
TouchScreen ts = TouchScreen(10, 6, A1, A2);

const int ledPin = 13;
const int speakerPin = 11;
int captchaAttempts = 0;
bool captchaPassed = false;

void setup() {
  screen.begin();
  screen.background(0, 0, 0);
  pinMode(ledPin, OUTPUT);
  pinMode(speakerPin, OUTPUT);
  
  generateCaptcha();
}

void loop() {
  TSPoint p = ts.getPoint();
  if (p.z > MINPRESSURE && p.z < MAXPRESSURE) {
    checkCaptcha(p.x, p.y);
  }
}

void generateCaptcha() {
  screen.fill(0, 0, 0);
  screen.setTextColor(255, 255, 255);
  screen.setTextSize(2);
  screen.setCursor(20, 50);
  screen.print("CAPTCHA");
  
  // Generate random pattern
  for(int i = 0; i < 10; i++) {
    int x = random(50, 200);
    int y = random(50, 150);
    screen.circle(x, y, random(2, 5));
  }
}

void checkCaptcha(int x, int y) {
  captchaAttempts++;
  
  if (captchaAttempts <= 3) {
    if (validateCaptcha(x, y)) {
      captchaPassed = true;
      screen.fill(0, 255, 0);
      screen.setTextColor(0, 0, 0);
      screen.setCursor(50, 100);
      screen.print("PASSED!");
      tone(speakerPin, 1000, 1000);
      digitalWrite(ledPin, HIGH);
    } else {
      screen.fill(255, 0, 0);
      screen.setTextColor(255, 255, 255);
      screen.setCursor(50, 100);
      screen.print("FAILED!");
      tone(speakerPin, 200, 500);
    }
  } else {
    screen.fill(255, 0, 0);
    screen.setCursor(20, 100);
    screen.print("Too Many Attempts!");
  }
}

bool validateCaptcha(int x, int y) {
  // Simple validation logic
  return (x > 100 && x < 200 && y > 80 && y < 120);
}
```

---

### 14. Ransomware Simulation Game
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| LCD Display | 1 | Game display |
| Buttons (3) | 3 | Game controls |
| LED (3) | 3 | Status indicators |
| Buzzer | 1 | Sound effects |
| Battery (9V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int button1Pin = 2;
const int button2Pin = 3;
const int button3Pin = 4;
const int redLed = 13;
const int yellowLed = 12;
const int greenLed = 11;
const int buzzerPin = 8;

bool filesLocked = false;
int timeRemaining = 60;
int score = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(button1Pin, INPUT_PULLUP);
  pinMode(button2Pin, INPUT_PULLUP);
  pinMode(button3Pin, INPUT_PULLUP);
  pinMode(redLed, OUTPUT);
  pinMode(yellowLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  startGame();
}

void loop() {
  if (filesLocked) {
    handleLockedState();
  } else {
    handleNormalState();
  }
  
  delay(1000);
}

void startGame() {
  lcd.clear();
  lcd.print("Ransomware Sim");
  lcd.setCursor(0, 1);
  lcd.print("Protect Files!");
  delay(2000);
}

void handleNormalState() {
  if (digitalRead(button1Pin) == LOW) {
    // Backup files
    score += 10;
    lcd.clear();
    lcd.print("Files Backed Up!");
    lcd.setCursor(0, 1);
    lcd.print("Score: " + String(score));
    digitalWrite(greenLed, HIGH);
    delay(1000);
    digitalWrite(greenLed, LOW);
  }
  
  if (digitalRead(button2Pin) == LOW) {
    // Update security
    score += 5;
    lcd.clear();
    lcd.print("Security Updated!");
    lcd.setCursor(0, 1);
    lcd.print("Score: " + String(score));
    digitalWrite(yellowLed, HIGH);
    delay(1000);
    digitalWrite(yellowLed, LOW);
  }
  
  if (digitalRead(button3Pin) == LOW) {
    // Simulate attack
    simulateAttack();
  }
}

void simulateAttack() {
  filesLocked = true;
  timeRemaining = 60;
  
  lcd.clear();
  lcd.print("FILES LOCKED!");
  lcd.setCursor(0, 1);
  lcd.print("Pay ransom or solve!");
  
  digitalWrite(redLed, HIGH);
  tone(buzzerPin, 200, 2000);
}

void handleLockedState() {
  timeRemaining--;
  
  lcd.clear();
  lcd.print("Files Locked!");
  lcd.setCursor(0, 1);
  lcd.print("Time: " + String(timeRemaining) + "s");
  
  if (timeRemaining <= 0) {
    gameOver();
  }
  
  if (digitalRead(button1Pin) == LOW) {
    // Try to decrypt
    if (random(100) < 30) {
      unlockFiles();
    } else {
      lcd.clear();
      lcd.print("Decryption Failed!");
      lcd.setCursor(0, 1);
      lcd.print("Try Again!");
      delay(2000);
    }
  }
}

void unlockFiles() {
  filesLocked = false;
  score += 50;
  
  lcd.clear();
  lcd.print("Files Unlocked!");
  lcd.setCursor(0, 1);
  lcd.print("Score: " + String(score));
  
  digitalWrite(redLed, LOW);
  digitalWrite(greenLed, HIGH);
  tone(buzzerPin, 1000, 1000);
  delay(2000);
  digitalWrite(greenLed, LOW);
}

void gameOver() {
  lcd.clear();
  lcd.print("Game Over!");
  lcd.setCursor(0, 1);
  lcd.print("Final Score: " + String(score));
  
  digitalWrite(redLed, HIGH);
  tone(buzzerPin, 100, 3000);
  delay(3000);
  digitalWrite(redLed, LOW);
}
```

---

### 15. IoT Security Demo
**Components Table**:
| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno | 1 | Microcontroller |
| WiFi Module | 1 | Wireless connection |
| LCD Display | 1 | Status display |
| LED (2) | 2 | Security indicators |
| Buzzer | 1 | Alert sound |
| Motion Sensor | 1 | Intrusion detection |
| Battery (12V) | 1 | Power source |

**Arduino Code**:
```cpp
#include <WiFi.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int motionPin = 2;
const int secureLed = 13;
const int alertLed = 12;
const int buzzerPin = 8;

const char* ssid = "SecureNetwork";
const char* password = "StrongPassword123";
bool isSecure = true;
int failedAttempts = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(motionPin, INPUT);
  pinMode(secureLed, OUTPUT);
  pinMode(alertLed, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  WiFi.begin(ssid, password);
  
  lcd.print("IoT Security Demo");
  lcd.setCursor(0, 1);
  lcd.print("Connecting...");
  
  if (WiFi.status() == WL_CONNECTED) {
    lcd.clear();
    lcd.print("Connected!");
    lcd.setCursor(0, 1);
    lcd.print("IP: " + WiFi.localIP().toString());
    digitalWrite(secureLed, HIGH);
  }
}

void loop() {
  if (WiFi.status() != WL_CONNECTED) {
    handleDisconnection();
  }
  
  if (digitalRead(motionPin) == HIGH) {
    handleMotionDetected();
  }
  
  // Simulate security checks
  if (millis() % 10000 == 0) {
    performSecurityCheck();
  }
  
  delay(100);
}

void handleDisconnection() {
  isSecure = false;
  digitalWrite(secureLed, LOW);
  digitalWrite(alertLed, HIGH);
  
  lcd.clear();
  lcd.print("SECURITY BREACH!");
  lcd.setCursor(0, 1);
  lcd.print("WiFi Disconnected");
  
  tone(buzzerPin, 200, 1000);
}

void handleMotionDetected() {
  if (!isSecure) {
    failedAttempts++;
    
    lcd.clear();
    lcd.print("Intrusion Alert!");
    lcd.setCursor(0, 1);
    lcd.print("Attempts: " + String(failedAttempts));
    
    digitalWrite(alertLed, HIGH);
    tone(buzzerPin, 500, 2000);
    
    if (failedAttempts >= 3) {
      activateLockdown();
    }
  }
}

void performSecurityCheck() {
  if (WiFi.status() == WL_CONNECTED && isSecure) {
    lcd.clear();
    lcd.print("Security Check OK");
    lcd.setCursor(0, 1);
    lcd.print("System Secure");
    digitalWrite(secureLed, HIGH);
    digitalWrite(alertLed, LOW);
  }
}

void activateLockdown() {
  lcd.clear();
  lcd.print("LOCKDOWN ACTIVATED!");
  lcd.setCursor(0, 1);
  lcd.print("All Access Denied");
  
  digitalWrite(alertLed, HIGH);
  tone(buzzerPin, 100, 5000);
  
  // Simulate system shutdown
  delay(5000);
  lcd.clear();
  lcd.print("System Shutdown");
}
```

---

## Arduino Code for Security Functions

### Basic Encryption Library
```cpp
class SimpleEncryption {
  private:
    int key;
    
  public:
    SimpleEncryption(int encryptionKey) {
      key = encryptionKey;
    }
    
    String encrypt(String message) {
      String encrypted = "";
      for (int i = 0; i < message.length(); i++) {
        char c = message[i];
        encrypted += (char)(c ^ key);
      }
      return encrypted;
    }
    
    String decrypt(String encrypted) {
      return encrypt(encrypted); // XOR is symmetric
    }
};
```

### Password Validator
```cpp
class PasswordValidator {
  public:
    bool validatePassword(String password) {
      bool hasUpper = false;
      bool hasLower = false;
      bool hasNumber = false;
      bool hasSpecial = false;
      
      if (password.length() < 8) return false;
      
      for (int i = 0; i < password.length(); i++) {
        char c = password[i];
        if (c >= 'A' && c <= 'Z') hasUpper = true;
        else if (c >= 'a' && c <= 'z') hasLower = true;
        else if (c >= '0' && c <= '9') hasNumber = true;
        else hasSpecial = true;
      }
      
      return hasUpper && hasLower && hasNumber && hasSpecial;
    }
};
```
