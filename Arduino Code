#define in1 2 //L298n Motor Driver pins.
#define in2 3
#define in3 4
#define in4 5
#define buzzer 13
#define TRIG_PIN 10
#define ECHO_PIN 11
unsigned long startTime=0;
int state =0;
int command; //Int to store app command state.
int Distance;
int Speed = 204; // 0 - 255.
int Speedsec;
int buttonState = 0;
int lastButtonState = 0;
int Turnradius = 0; //Set the radius of a turn, 0 - 255
int brakeTime = 45;
int brkonoff = 1; //1 for the electronic braking system [Automatic], 0 for normal.

unsigned long start_millis;
unsigned long current_millis;


void setup() {
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  pinMode(buzzer, OUTPUT); //Set the Buzzer pin.
  pinMode(TRIG_PIN, OUTPUT); // Set the trigPin as an OUTPUT
  pinMode(ECHO_PIN, INPUT); // Set the echoPin as an INPUT
  Serial.begin(9600);  //Set the baud rate for Bluetooth module.
}
 
void loop() {
  if (Serial.available() > 0) {
    command = Serial.read();
    Stop(); //Initialize with motors stoped.
    switch (command) {
      case 'F':
        forward();
        break;
      case 'B':
        back();
        break;
      case 'L':
        left();
        break;
      case 'R':
        right();
        break;
      case 'G':
        forwardleft();
        break;
      case 'I':
        forwardright();
        break;
      case 'H':
        backleft();
        break;
      case 'J':
        backright();
        break;
      case '0':
        Speed = 0;
        break;
      case '1':
        Speed = 23;
        break;
      case '2':
        Speed = 46;
        break;
      case '3':
        Speed = 69;
        break;
      case '4':
        Speed = 92;
        break;
      case '5':
        Speed = 115;
        break;
      case '6':
        Speed = 138;
        break;
      case '7':
        Speed = 161;
        break;
      case '8':
        Speed = 184;
        break;
      case '9':
        Speed = 207;
        break;
      case 'q':
        Speed = 255;
        break;
      case 'V':
        buzzer1();
        break;
      case 'v':
        buzzer2();
        break;
    }
    Speedsec = Turnradius;
    if (brkonoff == 1) {
      brakeOn();
    } else {
      brakeOff();
    }

  }

  current_millis= millis();
  if (current_millis - start_millis > 1000) {   //So the code dosen't stay on delay (frozen) we use once every 1000
    digitalWrite(TRIG_PIN, LOW);
    delayMicroseconds(2);
    digitalWrite(TRIG_PIN, HIGH);
    delayMicroseconds(10);
    digitalWrite(TRIG_PIN, LOW);
    long duration = pulseIn(ECHO_PIN, HIGH);
    Distance = duration * 0.034 / 2; //to convert to CM
    start_millis = current_millis;
  }

    if (Distance <20 && Distance != 0){
    buzzer1();
    Distance == 0;

  }
    else {
      buzzer2();
  }

  

}


void forward() {
  analogWrite(in2, Speed);
  analogWrite(in4, Speed);

}

void back() {
  analogWrite(in1, Speed);
  analogWrite(in3, Speed);

}
void buzzer1() {
digitalWrite(buzzer,HIGH);

}
void buzzer2() {
digitalWrite(buzzer,LOW);

}
 
 
void right() {
  analogWrite(in2, Speed);
  analogWrite(in3, Speed);
}
 
void left() {
  analogWrite(in4, Speed);
  analogWrite(in1, Speed);
}
void forwardright() {
  analogWrite(in3, Speedsec);
  analogWrite(in1, Speed);
}
void forwardleft() {
  analogWrite(in3, Speed);
  analogWrite(in1, Speedsec);
}
void backleft() {
  analogWrite(in4, Speed);
  analogWrite(in2, Speedsec);
}
void backright() {
  analogWrite(in4, Speedsec);
  analogWrite(in2, Speed);
}
 
void Stop() {
  analogWrite(in1, 0);
  analogWrite(in2, 0);
  analogWrite(in3, 0);
  analogWrite(in4, 0);
}
 
void brakeOn() {
  //Braking system
  buttonState = command; //reads current command/button pressed
  // compare the buttonState to its previous state
  if (buttonState != lastButtonState) {
    // if the state has changed, increment the counter   
    if (buttonState == 'S') {
      if (lastButtonState != buttonState) {
        digitalWrite(in1, HIGH);
        digitalWrite(in2, HIGH);
        digitalWrite(in3, HIGH);
        digitalWrite(in4, HIGH);
        delay(brakeTime);
        Stop();
      }
    }
    // save the current state as the last state,
    //for next time through the loop
    lastButtonState = buttonState;
  }
}
void brakeOff() {
 
}
