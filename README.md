## PERTEMUAN 1
Percobaan 1A: Percabangan

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

Percobaan 2A: Perulangan

Pertanyaan Praktikum:
1.Gambarkan rangkaian schematic 5 LED running yang digunakan pada percobaan!
![Uploading image.png…]()
2. Jelaskan bagaimana program membuat efek LED berjalan dari kiri ke kanan!
   Efek LED berjalan dari kiri ke kanan dibuat menggunakan perulangan for dengan nilai pin yang naik (increment):
   for (int ledPin = 2; ledPin < 8; ledPin++) {
   Perulangan dimulai dari pin 2 hingga pin 7. Setiap iterasi: LED dinyalakan (HIGH) - Delay sebentar - LED dimatikan (LOW).
   Karena pin bertambah (2 → 3 → 4 → ...), maka LED menyala berurutan dari kiri ke kanan
3. Jelaskan bagaimana program membuat LED kembali dari kanan ke kiri!
   Efek sebaliknya dibuat dengan perulangan for yang menurun (decrement): for (int ledPin = 7; ledPin >= 2; ledPin--) {
   Perulangan dimulai dari pin dengan nilai terbesar, yaitu pin 7, kemudian berkurang hingga pin 2. Pada setiap iterasi,
   LED pada pin yang sedang diproses akan dinyalakan, diberi jeda waktu menggunakan delay, lalu dimatikan kembali sebelum
   berpindah ke pin berikutnya. Karena urutan pin berjalan dari angka besar ke kecil, maka LED terlihat menyala dari arah
   kanan ke kiri secara berurutan.
4. Buatkan program agar LED menyala tiga LED kanan dan tiga LED kiri secara bergantian dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!
   int timer = 500; // Waktu delay

void setup() {
  // Inisialisasi semua pin LED sebagai OUTPUT
  for (int pin = 2; pin <= 7; pin++) {
    pinMode(pin, OUTPUT);
  }
}

void loop() {
  // Nyalakan 3 LED kiri (pin 2, 3, 4)
  digitalWrite(2, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(4, HIGH);

  // Matikan 3 LED kanan (pin 5, 6, 7)
  digitalWrite(5, LOW);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);

  delay(timer);

  // Matikan semua LED
  for (int pin = 2; pin <= 7; pin++) {
    digitalWrite(pin, LOW);
  }

  // Nyalakan 3 LED kanan (pin 5, 6, 7)
  digitalWrite(5, HIGH);
  digitalWrite(6, HIGH);
  digitalWrite(7, HIGH);

  // Matikan 3 LED kiri (pin 2, 3, 4)
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);

  delay(timer);

  // Matikan semua LED sebelum mengulang
  for (int pin = 2; pin <= 7; pin++) {
    digitalWrite(pin, LOW);
  }
}
   
