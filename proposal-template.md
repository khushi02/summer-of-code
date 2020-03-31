#  Khushi Wadhwa 

## Project

Write examples for official libraries.

## Abstract

This project is designed to create a comprehensive set of examples for the official Arduino libraries. Projects will range from beginner-friendy to advanced, with code and diagrams that are easy to replicate. These examples will integrate various different libraries and leverage external components in order to facilitate an in-depth understanding of the library's functions and the Arduino as a whole.

## Technical Details

In order to accomplish this project, I will code multiple examples using a variety of Arduino libraries. Examples that involve circuits and hardware will be accompanied by both fritzing diagrams and images. The examples will not be limited to using only one library, rather I will focus on implementing multiple libraries into the examples in order to create complex projects. This will demonstrate diversity in the use of libraries and their interactions with other libraries.

Previously, I have submitted a pull request to add an example to the servo library. This is example records sensory data through a potentiometer and saves it to EEPROM. The Arduino accesses the saved data and replays the actions on a servo. This example is useful for repeated actions on a servo that do not require precise measurements, simply general motions. This demonstrates how I plan to blend multiple libraries together into one project, just as is done in practice. The pull request can be found here: [Servo Example](https://github.com/arduino-libraries/Servo/pull/46). I have also attached the code below.

```
int potPin = 0;       // analog pin used to connect the potentiometer
int buttonPin = 13;   // digital pin used to connect the button
int servoPin = 9;     // digital pin used to connect the servo
int val;              // variable to read the value from the analog pin
int read;             // variable to read the data from memory

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // configure the button's pin
  myServo.attach(servoPin);   // attaches the servo pin to the Servo object
}

void loop() {
  // begin recording on potentiometer if button is pressed 
  if (record == true) {
    for (int i = 1; i < EEPROM.length(); i++) {
      val = analogRead(potPin);            // reads the value of the potentiometer (value between 0 and 1023)
      val = map(val, 0, 1023, 0, 180);     // scales it to use it with the servo (value between 0 and 180)
      
      EEPROM.write(i, val);                // stores data in memory
      myServo.write(val);                  // sets the servo position according to the scaled value
      delay(15);                           // waits for the servo to get there
    }
    delay(1000);                           // pause before replay
    record = false;                        // sets record to false in order to go to replay
  }
  // begin replay on servo
  else {
    for (int i = 1; i < EEPROM.length(); i++) {
      // returns to record if button is pressed
      if (digitalRead(buttonPin) == LOW) {
        record = true;                    // sets record to true in order to go to rerecord the data
        break;                            
      }
      read = EEPROM.read(i);              // sets the value of read to the value from memory
      myServo.write(read);                // servo repeats the values collected from the potentiometer during record
      delay(15);                          
    }
  }
}
```

## Schedule of Deliverables

### **Community Bonding Period**

* Familiarize myself with my mentors and the other GSoC participants 
* Discuss my ideas with the team/mentors
* Adjust my ideas with the feedback that I receive 
* Finalize the projects and obtain approval

### **Phase 1 (June 1 - June 29)**

* Deliverable 1
  * Week 1 - Draft 3-5 examples for the **servo** library. This includes hardware images and fritzing schematics.
    * Ideas:
      * Implement examples with ultrasonic sensors and photresisters
      * Demonstrate uses of common objects such as buttons, switches, joysticks, and potentiometers (already included)
  * Week 2 - Implement suggestions from mentors and ensure that code is clean. Finalize examples.
* Deliverable 2
  * Week 3 - Draft 3-5 examples (may change based on time analysis from previous week) for the **capacitive sensor** library. This includes hardware images and fritzing schematics
    * Ideas:
      * Simple dispenser system
      * Touch sensing grid
      * Mini keyboard
  * Week 4 - Implement suggestions from mentors and ensure that code is clean. Finalize examples.

### **Phase 2 (July 3 - July 27)**

* Deliverable 1
  * Week 5 - Draft 2-3 examples (these projects take longer) for the **keyboard** library. This includes hardware images and fritzing schematics. 
    * Ideas:
      * Mini musical keyboard
      * 4x3 (or another dimension) keypad
   * Week 6 - Implement suggestions from mentors and ensure that code is clean. Finalize examples.
* Deliverable 2
  * Week 7 - Draft 2-3 examples for the **mouse** library. This includes hardware images and fritzing schematics. Use extra time to clean up old code, double-check fritzing and hardware images, and ensure all deliverables have been met so far.
    * Ideas:
      * Integrate the Arduino and a USB mouse
      * Create a touchpad tracker
  * Week 8 - Implement suggestions from mentors and ensure that code is clean. Finalize examples.

### **Phase 3 (July 31 - August 24)**

* Deliverable 1
  * Week 9 - Draft 2-3 examples (these projects take longer) for the **serial peripheral interface (SPI)** library. This includes hardware images and fritzing schematics.
    * Ideas:
      *  
* Deliverable 2

### **Final Week (August 24 - August 31)**

* Go back and review all code for hidden errors, redundancies, and unprofessional coding practices
* Make sure all code is clean and easy to read with plentiful comments
* Check that diagrams and documentation are provided where necessary 

## Development Experience

_Do you have code on GitHub? Can you show previous contributions to other projects?
Did you do other code related projects or university courses?_

_Do you have experience with Arduino?_

## Other Experiences

...


## Why this project?

_Why you want to do this project?_

## Do you have any other commitments during the GSoC period?

_Provide dates, such as holidays, when you will not be available._

