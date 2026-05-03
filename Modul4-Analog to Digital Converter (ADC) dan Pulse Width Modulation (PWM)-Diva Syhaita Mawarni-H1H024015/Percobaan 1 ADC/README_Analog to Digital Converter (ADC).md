#### 1. Apa fungsi perintah `analogRead()` pada rangkaian praktikum ini?

Perintah `analogRead()` digunakan untuk membaca nilai tegangan analog dari pin input (misalnya dari potensiometer). Nilai yang dibaca akan dikonversi oleh ADC (Analog to Digital Converter) menjadi data digital dengan rentang 0–1023.

---

#### 2. Mengapa diperlukan fungsi `map()` dalam program tersebut?

Fungsi `map()` digunakan untuk mengubah (mengonversi) rentang nilai dari satu skala ke skala lain.  

Pada praktikum ini:
- Nilai dari `analogRead()` berada pada rentang **0–1023**
- Sedangkan sudut servo berada pada rentang **0–180 derajat**

Sehingga diperlukan fungsi `map()` untuk menyesuaikan nilai input agar sesuai dengan kebutuhan output servo.

Contoh:
```cpp
int sudut = map(nilaiADC, 0, 1023, 0, 180);
