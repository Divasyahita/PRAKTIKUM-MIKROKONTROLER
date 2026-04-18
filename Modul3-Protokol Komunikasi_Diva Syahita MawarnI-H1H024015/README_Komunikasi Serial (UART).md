
## 1. Jelaskan proses dari input keyboard hingga LED menyala/mati! 

Proses yang terjadi adalah sebagai berikut:

1. User mengetik karakter pada **keyboard** di Serial Monitor Arduino IDE  
2. Data dikirim melalui komunikasi **Serial (UART)** ke Arduino  
3. Arduino menerima data melalui fungsi `Serial.read()`  
4. Sebelum membaca, Arduino mengecek apakah data tersedia dengan `Serial.available()`  
5. Data yang diterima dibandingkan menggunakan kondisi `if`  
6. Jika:
   - `'1'` → LED menyala  
   - `'0'` → LED mati  
7. Arduino mengirim sinyal HIGH/LOW ke pin digital (misalnya pin 8)  
8. LED merespon:
   - HIGH → LED menyala  
   - LOW → LED mati  

Gambar Rangkaian Tinkercad
<img width="793" height="562" alt="image" src="https://github.com/user-attachments/assets/0f1c5d3f-80cc-45a3-90fc-80ee9af44fc3" />
<img width="793" height="562" alt="WhatsApp Image 2026-04-14 at 09 27 11" src="https://github.com/user-attachments/assets/e59545c1-5ce8-43e7-8587-18796d520c02" />


Link Tinkercad : https://www.tinkercad.com/things/0FkEHcdi3NA-modul-3-praktikum-sismik?sharecode=MlJSKxaL2hCwFRMVfXawMzO-SujGVEcE5-GCEDpsMuQ

---

## 2. Mengapa digunakan Serial.available() sebelum membaca data? Apa yang terjadi jika baris tersebut dihilangkan?

### Fungsi:
`Serial.available()` digunakan untuk mengecek apakah ada data yang masuk ke buffer serial.

### Alasan digunakan:
Agar Arduino tidak membaca data kosong dan menghindari error atau pembacaan data tidak valid

### Jika dihapus:

Jika `Serial.available()` dihilangkan, Arduino akan tetap menjalankan fungsi `Serial.read()` tanpa memastikan apakah data benar-benar tersedia atau tidak. Hal ini dapat menyebabkan Arduino membaca data kosong (null) atau data yang tidak valid. Akibatnya, program bisa berjalan tidak stabil dan respon terhadap input menjadi tidak sesuai dengan yang diharapkan.

---

## 3. Modifikasi program agar LED berkedip (blink) ketika menerima input '2' dengan kondisi jika ‘2’ aktif maka LED akan terus berkedip sampai perintah selanjutnya diberikan dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!

### 📌 Kode Program

```cpp
int ledPin = 8;          
char data;               // ini variabel untuk menyimpan data dari serial
bool blinkMode = false;  

void setup() {
  pinMode(ledPin, OUTPUT);  
  Serial.begin(9600);       // ini mulai komunikasi serial
}

void loop() {

  // nah ini mengecek apakah ada data masuk
  if (Serial.available() > 0) {
    data = Serial.read();   

    if (data == '1') {
      digitalWrite(ledPin, HIGH); // LED nyala
      blinkMode = false;          // mode blink mati
    }
    else if (data == '0') {
      digitalWrite(ledPin, LOW);  // LED mati
      blinkMode = false;          // mode blink mati
    }
    else if (data == '2') {
      blinkMode = true;           // mode blink aktif
    }
  }

  // Jika mode blink aktif
  if (blinkMode) {
    digitalWrite(ledPin, HIGH); // LED nyala
    delay(500);                 // Delay 500ms
    digitalWrite(ledPin, LOW);  // LED mati
    delay(500);                 // Delay 500ms
  }
}
```
Link Tinkercad : https://www.tinkercad.com/things/0FkEHcdi3NA-modul-3-praktikum-sismik?sharecode=MlJSKxaL2hCwFRMVfXawMzO-SujGVEcE5-GCEDpsMuQ

---
## 4. Pemilihan `delay()` atau `millis()`

Pada program ini digunakan fungsi `millis()` sebagai pengganti `delay()` karena sifatnya non-blocking. Artinya, Arduino tetap dapat menjalankan proses lain seperti membaca input dari Serial Monitor tanpa harus menunggu proses jeda waktu selesai.

Jika menggunakan `delay()`, maka selama waktu delay berlangsung, seluruh proses dalam program akan berhenti sementara. Hal ini menyebabkan Arduino tidak dapat menerima atau memproses input baru, sehingga sistem menjadi kurang responsif.

Sebaliknya, dengan menggunakan `millis()`, LED tetap dapat berkedip secara periodik tanpa menghentikan jalannya program utama. Arduino tetap bisa membaca data serial secara real-time, sehingga sistem menjadi lebih efisien dan responsif.

Dengan demikian, penggunaan `millis()` lebih disarankan untuk sistem yang membutuhkan multitasking atau respon cepat terhadap input.
