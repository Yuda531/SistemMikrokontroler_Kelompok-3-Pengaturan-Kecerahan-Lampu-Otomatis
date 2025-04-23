#include <LiquidCrystal_I2C.h> // Jika I2C
// #include <LiquidCrystal.h>  // Jika non-I2C

LiquidCrystal_I2C lcd(0x27, 16, 2);
const int ledPin = 3;                // PWM output ke LED
int state = 0;                       // 0=off, 1=dim, 2=bright
unsigned long lastChange = 0;
const unsigned long interval = 2000; // 2 detik per mode

void setup() {
  lcd.init();
  lcd.backlight();
  pinMode(ledPin, OUTPUT);

  // Pastikan LED mati sebelum apa-apa
  analogWrite(ledPin, 0);

  // --- Pesan Startup ---
  lcd.setCursor(0, 0);
  lcd.print("Sietem Kecerahan");
  lcd.setCursor(0, 1);
  lcd.print("Otomatis");
  delay(2000);
  lcd.clear();
  // ----------------------

  // Mulai hitung interval
  lastChange = millis();
}

void loop() {
  unsigned long now = millis();
  if (now - lastChange >= interval) {
    state = (state + 1) % 3;  // berganti 0->1->2->0
    lastChange = now;
  }

  int brightness;
  lcd.clear();
  lcd.setCursor(0, 0);

  switch (state) {
    case 0:
      brightness = 0;           // Mati
      lcd.print("Mode: Mati");
      break;
    case 1:
      brightness = 128;         // Redup (~50%)
      lcd.print("Mode: Redup");
      break;
    case 2:
      brightness = 255;         // Terang (100%)
      lcd.print("Mode: Terang");
      break;
  }

  analogWrite(ledPin, brightness);

  // Baris kedua dibiarkan kosong
  delay(50);  // debounce kecil
}
