# **Latihan 7 – Demonstrasi Dampak Berbagi Sumber Daya pada Kinerja Sistem Multitasking**

## **Deskripsi**
Repositori ini berisi implementasi *Exercise 7 – Demonstrate that the sharing of resources in a multitasking design can lead to a deterioration in system performance*. Latihan ini bertujuan untuk menunjukkan bahwa penggunaan sumber daya bersama dalam desain multitasking dapat menurunkan kinerja sistem secara keseluruhan.

Latihan ini terdiri dari tiga tugas yang masing-masing bertanggung jawab untuk mem-flash LED tertentu. Kinerja sistem dinilai berdasarkan perubahan pola flash LED akibat kontensi sumber daya.

---

## **Tujuan Latihan**
1. Memahami bagaimana berbagi sumber daya dapat memengaruhi kinerja multitasking.
2. Mempelajari dampak kontensi sumber daya terhadap responsivitas sistem.
3. Melihat perbandingan kinerja antara sistem tanpa kontrol akses dan sistem dengan kontrol akses sumber daya.
4. Mengapresiasi pentingnya meminimalkan waktu penggunaan sumber daya bersama dalam sistem multitasking.

---

## **Implementasi**
### **Konfigurasi Tugas**
1. **Tugas Green LED**:
   - Prioritas: *Normal*.
   - Flash LED hijau dengan `osDelay` 200 ms di setiap siklus.
   - Akses sumber daya bersama di setiap siklus.

2. **Tugas Red LED**:
   - Prioritas: *Normal*.
   - Flash LED merah dengan `osDelay` 550 ms di setiap siklus.
   - Akses sumber daya bersama di setiap siklus.

3. **Tugas Orange LED**:
   - Prioritas: *Above Normal* (prioritas tertinggi).
   - Flash LED oranye dengan frekuensi 10 Hz (`osDelay` 50 ms).
   - Tidak mengakses sumber daya bersama.

4. **Akses Sumber Daya Bersama**:
   - Mengecek status *Start Flag*:
     - Jika *Up*: Set ke *Down*.
     - Jika *Down*: Nyalakan LED biru.
   - Simulasi operasi baca/tulis selama 1 detik.
   - Matikan LED biru (opsional).
   - Set *Start Flag* kembali ke *Up*.

5. **Kontrol Akses (Opsional)**:
   - Gunakan `taskENTER_CRITICAL()` untuk menonaktifkan *interrupt* sebelum mengakses sumber daya.
   - Gunakan `taskEXIT_CRITICAL()` untuk mengaktifkan kembali *interrupt* setelah selesai.

---

## **Langkah Eksperimen**
### **Exercise 7.1**: Verifikasi Waktu Eksekusi Individual  
- Jalankan satu tugas pada satu waktu.
- Periksa apakah perilaku run-time sesuai dengan nilai waktu yang diharapkan.
### **Demonstrasi 7.1**:
![Exercise7 1](https://github.com/user-attachments/assets/b75127d0-2f8f-41b6-9a92-323e8729ac68)


### **Exercise 7.2**: Pengujian Tanpa Kontrol Akses  
- Jalankan semua tugas secara bersamaan.
- Amati perubahan pola flash LED karena kontensi sumber daya.
- Catat perbedaan perilaku dibandingkan dengan *Exercise 7.1*.
### **Demonstrasi 7.2**:
![Exercise7 2](https://github.com/user-attachments/assets/2e8861c0-09d5-431b-84b3-6491447a99c0)


### **Exercise 7.3**: Pengujian dengan Kontrol Akses  
- Ulangi *Exercise 7.2* dengan menambahkan mekanisme kontrol akses menggunakan `taskENTER_CRITICAL()` dan `taskEXIT_CRITICAL()`.
- Bandingkan hasil dengan *Exercise 7.2* untuk melihat pengaruh kontrol akses pada kinerja sistem.
### **Demonstrasi 7.3**:
![Exercise7 3](https://github.com/user-attachments/assets/6ee8ca01-7315-4596-b234-48d013efb9fb)


---

## **Pelajaran yang Didapat**
1. **Kontensi Sumber Daya**:
   - Membagi sumber daya bersama tanpa kontrol dapat menyebabkan ketidakpastian waktu eksekusi.
   - Kontensi dapat mengurangi responsivitas sistem atau bahkan menyebabkan kegagalan sistem.

2. **Kontrol Akses**:
   - Menggunakan `taskENTER_CRITICAL()` dapat menghilangkan kontensi sumber daya, tetapi menghentikan multitasking sementara.
   - Waktu di dalam blok kritis harus diminimalkan untuk mengurangi dampak negatif pada sistem.

3. **Pentingnya Evaluasi Temporal**:
   - Desain multitasking membutuhkan analisis waktu yang mendalam untuk meminimalkan ketidakpastian waktu.

4. **Minimalkan Penggunaan Sumber Daya Bersama**:
   - Kurangi jumlah tugas dan sumber daya bersama untuk mengurangi risiko kontensi.

---

Dengan menyelesaikan latihan ini, Anda akan memiliki pemahaman yang lebih baik tentang tantangan desain multitasking dan pentingnya kontrol akses sumber daya bersama.
