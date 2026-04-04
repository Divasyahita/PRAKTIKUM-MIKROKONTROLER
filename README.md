## PERTEMUAN 1
Percobaan 1A:Percabangan

Pertanyaan Praktikum:
1. Pada kondisi apa program masuk ke blok if?
   Program akan masuk ke blok if ketika kondisi:
   timeDelay <= 100
   Artinya, saat nilai timeDelay sudah sangat kecil (LED berkedip sangat cepat), maka program akan:
   Memberikan jeda (delay(3000)) dan Mengembalikan nilai timeDelay ke 1000 (reset).
2. Pada kondisi apa program masuk ke blok else?
   Program akan masuk ke blok else ketika kondisi if tidak terpenuhi, yaitu:
   timeDelay > 100
   Pada kondisi ini, program akan:
   Mengurangi nilai timeDelay sebesar 100 dan Membuat LED berkedip semakin cepat secara bertahap.
3. Apa fungsi dari perintah delay(timeDelay)?
   Fungsi delay(timeDelay) adalah untuk:
   Memberikan jeda waktu (delay) dalam satuan milidetik dan Mengatur kecepatan kedipan LED
   Semakin besar nilai delay → LED berkedip lebih lambat, Semakin kecil nilai delay → LED berkedip lebih cepat.
4. Jika program yang dibuat memiliki alur mati → lambat → cepat → reset (mati), ubah menjadi LED tidak langsung reset → tetapi berubah dari cepat → sedang → mati dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!

const int ledPin = 6;      // Menentukan pin LED pada pin 6
int timeDelay = 1000;      // Nilai awal delay (kedip lambat)
bool faseTurun = true;     // Penanda arah perubahan (cepat atau lambat kembali)

void setup() {
  pinMode(ledPin, OUTPUT); // Mengatur pin LED sebagai output
}

void loop() {
  // Menyalakan LED
  digitalWrite(ledPin, HIGH);
  delay(timeDelay);

  // Mematikan LED
  digitalWrite(ledPin, LOW);
  delay(timeDelay);

  // Logika percabangan untuk perubahan delay
  if (faseTurun) {
    timeDelay -= 100;  // Mempercepat kedipan

    // Jika sudah terlalu cepat
    if (timeDelay <= 100) {
      faseTurun = false; // Ubah arah menjadi melambat
    }
  } else {
    timeDelay += 100;  // Memperlambat kembali

    // Jika sudah kembali lambat
    if (timeDelay >= 1000) {
      delay(2000);      // Jeda sebelum mati
      timeDelay = 1000; // Reset ke awal
      faseTurun = true; // Ulangi siklus
    }
  }
}
