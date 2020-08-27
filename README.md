//# Simple-EEPROM-program
//This is an example Arduino program for EEPROM.

#include <EEPROM.h>

bool flag = false;
int x =0;

int eunice;

void setup() {
  pinMode (A0, INPUT); //button
  pinMode (2, OUTPUT); //LED

  digitalWrite(A0, LOW);

  eunice = EEPROM.read(0);

  if( eunice == 0){
    digitalWrite(2, LOW);
  }
  else if(eunice == 1){
    digitalWrite(2, HIGH);
  }
}

void loop() {
   if(x == 0){
     if( digitalRead(A0) == HIGH){
        flag = true;
     }  
     if( digitalRead(A0) == LOW and flag == true){
        digitalWrite(2, HIGH);
        x++;
        flag = false;

        EEPROM.write(0, 1);
      }
   }// if x ==0

   
   if (x == 1){
     if( digitalRead(A0) == HIGH){
        flag = true;
     }  
  
     if( digitalRead(A0) == LOW and flag == true){
        digitalWrite(2, LOW);
        x = 0;
        flag = false;

        EEPROM.write(0, 0);
      }
   }// if x ==1
  
}//end void loop
