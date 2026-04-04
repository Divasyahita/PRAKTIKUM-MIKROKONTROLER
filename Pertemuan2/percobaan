int timer = 100; 
// Delay. Semakin tinggi angkanya, semakin lambat pergerakan LED.

void setup() {
  // Inisialisasi pin 2 sampai 7 sebagai OUTPUT
  for (int ledPin = 2; ledPin < 8; ledPin++) {
    pinMode(ledPin, OUTPUT);
  }
}

void loop() {
  // Loop dari pin rendah ke tinggi (2 → 7)
  for (int ledPin = 2; ledPin < 8; ledPin++) {
    digitalWrite(ledPin, HIGH); // Nyalakan LED
    delay(timer);
    digitalWrite(ledPin, LOW);  // Matikan LED
  }

  // Loop dari pin tinggi ke rendah (7 → 2)
  for (int ledPin = 7; ledPin >= 2; ledPin--) {
    digitalWrite(ledPin, HIGH); // Nyalakan LED
    delay(timer);
    digitalWrite(ledPin, LOW);  // Matikan LED
  }
}
