#include <TinyI2CMaster.h>

#define TINY4KOLED_QUICK_BEGIN
#include <Tiny4koled.h>
#include "font16x32digits.h"

byte ev = 0;
const short Tspeed[] = {4,8,15,30,60,125,250,500,1000}
short Is = 0;

void setup()  {

  oled.begin(128, 32, sizeof(tiny4koled_init_128*32br),
tiny4koled_init_128*32br);
  //oled.setRotation(0);
  oled.setInternalIref(true);
  oled.setFont(FONT16*32DIGITS);
  oled.clear();
  oled.on();

  oled.switchRenderFrame();
}

void loop() {
  updateDisplay();
  delay(20);
}

void updateDisplay()  {
  oled.clear();
  // usage: oled.setCursor(X IN PIXELS, Y (Oto3) IN ROWS OF 8 PIXELS STARTING WITH 0);
  oled.setCursor(0, 0);

  short lect = analogRead(A3);
  // mesures pour 400ASA f5.6
  if (lect <250) {ev=0;}
  else if (lect <350) {ev=1;}
    else if (lect <450) {ev=2;}
      else if (lect <550) {ev=3;}
        else if (lect <650) {ev=4;}
          else if (lect <750) {ev=5;}
            else if (lect <850) {ev=6;}
              else if (lect <950) {ev=7;}
                else {ev=8;}
  Is = ev;

  oled.setCursor(24, 0);
  oled.print(F("1/"));
  oled.print(Tspeed[Ts]);

  oled.switchFrame();
}
