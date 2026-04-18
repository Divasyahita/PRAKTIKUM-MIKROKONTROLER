

## 1. Cara Kerja Komunikasi I2C antara Arduino dan LCD

Komunikasi I2C bekerja menggunakan dua jalur utama yaitu SDA (data) dan SCL (clock). Pada rangkaian ini, Arduino bertindak sebagai master sedangkan LCD I2C sebagai slave. Arduino mengirimkan data berupa perintah atau karakter ke LCD melalui jalur SDA, sedangkan SCL digunakan untuk sinkronisasi pengiriman data.

Setiap perangkat I2C memiliki alamat unik, misalnya LCD biasanya menggunakan alamat 0x27 atau 0x20. Arduino akan mengirim data ke alamat tersebut sehingga hanya LCD yang dituju yang merespon. Dengan metode ini, komunikasi menjadi lebih efisien karena hanya membutuhkan dua kabel meskipun terdapat banyak perangkat.

---

## 2. Konfigurasi Pin Potensiometer

Konfigurasi pin potensiometer tidak boleh sembarangan karena akan mempengaruhi pembacaan nilai analog. Kaki kiri dihubungkan ke GND, kaki kanan ke 5V, dan kaki tengah ke pin analog (A0).

Jika pin kiri dan kanan tertukar, sebenarnya potensiometer tetap dapat bekerja, tetapi arah pembacaan akan terbalik. Artinya, ketika diputar ke kanan nilai akan mengecil, dan ketika diputar ke kiri nilai akan membesar. Hal ini tidak merusak rangkaian, tetapi dapat membingungkan dalam interpretasi data.

---

## 3. Program Gabungan UART dan I2C

### Kode Program

```cpp
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

// Inisialisasi LCD (alamat 0x27, 16 kolom, 2 baris)
LiquidCrystal_I2C lcd(0x27, 16, 2);

int potPin = A0;  // Pin potensiometer

void setup() {
  Serial.begin(9600); // Memulai komunikasi serial
  lcd.init();         // Inisialisasi LCD
  lcd.backlight();    // nyalain backlight LCD
}

void loop() {

  int adcValue = analogRead(potPin); // Membaca nilai ADC (0-1023)

  float voltage = adcValue * (5.0 / 1023.0); // Konversi ke volt
  int percent = map(adcValue, 0, 1023, 0, 100); // Konversi ke persen

  // INI OUTPUT KE SERIAL MONITOR
  Serial.print("ADC: ");
  Serial.print(adcValue);
  Serial.print(" Volt: ");
  Serial.print(voltage);
  Serial.print(" V Persen: ");
  Serial.print(percent);
  Serial.println("%");

  // KALAU INI OUTPUT KE LCD 
  lcd.clear();

  // Baris 1
  lcd.setCursor(0, 0);
  lcd.print("ADC:");
  lcd.print(adcValue);

  // Baris 2 (Bar level)
  lcd.setCursor(0, 1);
  int barLength = map(adcValue, 0, 1023, 0, 16);

  for (int i = 0; i < barLength; i++) {
    lcd.print((char)255); // karakter blok
  }

  delay(500);
}

```

## 4. Tabel Hasil Pengamatan

Berikut merupakan hasil pengamatan berdasarkan data yang ditampilkan pada Serial Monitor:

| ADC | Volt (V) | Persen (%) |
|-----|----------|------------|
| 1   | 0.00     | 0%         |
| 21  | 0.10     | 2%         |
| 49  | 0.24     | 4%         |
| 74  | 0.36     | 7%         |
| 96  | 0.47     | 9%         |

Nilai tegangan (Volt) diperoleh dari hasil konversi nilai ADC menggunakan rumus:

V = ADC × (5 / 1023)

Sedangkan nilai persen (%) diperoleh dari perbandingan nilai ADC terhadap nilai maksimum (1023), kemudian dikonversi ke dalam bentuk persentase.
