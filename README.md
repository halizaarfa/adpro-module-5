# Adpro - Profiling
Haliza N. S. Arfa | 2306211401 | Adpro A

---

## Reflection
### Perbedaan JMeter dan Intellij Profiler
Perbedaan pendekatan performance testing dengan JMeter dan profiling dengan Intellij Profiler
dalam konteks optimisasi performa aplikasi yaitu:
- **JMeter** digunakan untuk mengukur performa aplikasi dengan cara mensimulasikan beban kerja yang tinggi
  pada aplikasi (aplikasi digunakan oleh banyak orang pada saat yang bersamaan), sedangkan
- **Intellij Profiler** digunakan untuk mencari tahu bottleneck pada aplikasi yang menyebabkan
  performa aplikasi menjadi buruk atau lambat.

### Proses Profiling
Proses profiling sangat berguna untuk menemukan bottleneck pada aplikasi yang menyebabkan performa
aplikasi menjadi lambat. Selama proses ini, profiler akan mengumpulkan data serta menganalisis bagian-bagian
yang menjadi bottleneck. Informasi yang kita peroleh bisa berupa CPU usage, memory allocation,
garbage collection activity, dan thread concurrency.

### Efektivitas IntelliJ Profiler
Menurut saya, Intellij Profiler sudah efektif dalam menemukan bottleneck pada aplikasi. Dengan flame graph
yang disediakan oleh Intellij Profiler, kita bisa melihat bagian mana yang memakan waktu eksekusi yang lama.
Selain itu, tab Method List memberikan kita informasi mengenai Execution time. Jika terdapat method yang
kita optimisasi, kita bisa melihat perubahan (Diff execution time) dari method tersebut sehingga saya
tidak perlu menghitung manual seberapa persen peningkatan performa yang saya dapatkan.

### Tantangan dalam Performance Testing dan Profiling
Tantangan yang saya hadapi dalam melakukan performance testing dan profiling adalah:
- **Memahami Hasil Profiling**: Saya harus paham dalam melihat hasil profiling agar dapat melakukan refactoring
  pada bottleneck yang saya temukan.
- **Melakukan Optimisasi**: Setelah menemukan bottleneck, saya harus melakukan refactoring pada bottleneck
  tersebut agar performa aplikasi menjadi lebih baik dan bagi saya ini merupakan tantangan yang besar.

### Manfaat IntelliJ Profiler
Selain yang sudah saya sebutkan pada poin refleksi sebelumnya, saya tidak perlu menggunakan
third party app lainnya untuk melakukan profiling karena sudah disediakan dalam satu IDE yang saya gunakan
yaitu Intellij IDEA. Dengan begitu, saya tidak perlu melakukan setup yang rumit untuk profiling.

### Inkonsistensi IntelliJ Profiler dan JMeter
Saya tidak mengalami hasil yang tidak konsisten dari dua alat tersebut. Namun, jika saya mengalami hal tersebut,
hal yang saya lakukan adalah memeriksa kembali konfigurasi yang saya lakukan pada JMeter dan memeriksa kembali
hasil profiling yang saya dapatkan dari Intellij Profiler. Jika masih inkonsisten, saya akan mencari tahu
penyebabnya melalui search engine atau bertanya kepada dosen, kakak asdos, atau teman saya.

### Implementasi Optimisasi Kode Aplikasi
Strategi yang saya lakukan untuk melakukan refactoring pada aplikasi adalah:
- **Mengurangi Jumlah Pemanggilan Database**:

Hal ini saya lakukan pada method `getAllStudentsWithCourses()`. Sebelumnya, setiap kali mengakses daftar mahasiswa,
kode melakukan panggilan database terpisah untuk setiap mahasiswa dengan mata kuliah yang diambil. Setelah di-refactor,
saya menggunakan `studentCourseRepository.findAll()` untuk langsung mendapatkan semua data hubungan antara mahasiswa
dan kursus dari database dalam satu pemanggilan. Lalu, saya memanfaatkan `HashMap` untuk ID mahasiswa.
Dengan begitu, cukup iterasi `StudentCourse` untuk mencari mahasiswa yang sesuai dalam `HashMap`.

- **Perbaiki Struktur Data untuk Alokasi Memori**:

Diterapkan dalam optimisasi method `joinStudentNames()`. Operasi `concatenation` atau `+=` pada String memerlukan alokasi
memori tambahan karena String bersifat immutable dan membuat objek baru setiap kali konkatensi dilakukan. Dengan begitu,
sebaiknya menggunakan `StringBuilder` untuk mengurangi alokasi memori yang tidak perlu.

- **Optimisasi Query**:

Saya lakukan pada method `findStudentWithHighestGpa()`. Sebelumnya, untuk mendapatkan mahasiswa dengan IPK tertinggi, kita
melakukan iterasi semua mahasiswa dan melakukan compare IPK satu per satu. Untuk mengoptimalkannya, saya menggunakan query
`SELECT * FROM students ORDER BY gpa DESC LIMIT 1` yang diterapkan pada `StudentRepository`. Query ini mengambil
mahasiswa dengan IPK tertinggi dengan mengurutkan secara menurun dan ambil satu anggota pertama.

Untuk memastikan bahwa optimisasi yang saya lakukan tidak mempengaruhi fungsionalitas aplikasi, saya dapat membuat sebuah
unit test sebelumnya seperti yang sudah diajarkan pada minggu-minggu sebelumnya. Namun, pada latihan kali ini saya tidak
melakukannya.


## JMeter Report and Test Results
### **Endpoint** `/all-student`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/de7a37d2-4083-4e1f-87e7-3fc014bf63a2)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/a4a52334-8d93-49fc-9e6d-ed5fff9889f9)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/d76d74f3-3b0d-4680-9989-144f15ecdda8)

Execution Time `getAllStudentWithCourses()` from Intellij Profiler:

| Before | After | Diff Percentage |
| -- | -- | -- |
| 17,542 ms | 1,466 ms | 91.65% |


### **Endpoint** `/all-student-name`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/0c741dd9-2ec3-49ab-8703-d1f3ab4f3618)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/6ff7a8a6-16cb-477c-b73a-bc753bc065a9)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/80af6fc8-2059-4420-8a0a-977bab4e4436)

Execution Time `joinStudentNames()` from Intellij Profiler:

| Before | After  | Diff Percentage |
|--------|--------| -- |
| 979 ms | 230 ms | 76.5% |


### **Endpoint** `/highest-gpa`

**a) Before Optimization**

GUI Test Result:
![image](https://github.com/user-attachments/assets/b439d40a-782a-4c66-8c87-7a5f03f98e55)

Command Line Test Result:
![image](https://github.com/user-attachments/assets/cf6c3c02-f0f3-4e32-8d4b-421259da86d8)

**b) After Optimization**
![image](https://github.com/user-attachments/assets/02038e8b-1b72-45c1-87ef-42715adbc427)

Execution Time `findStudentWithHighestGpa()` from Intellij Profiler:

| Before | After | Diff Percentage |
|--------|-------| -- |
| 180 ms | 40 ms | 77.7% |

### Kesimpulan
Berdasarkan gambar Test Result, terlihat adanya peningkatan performa berdasarkan hasil sample time yang diperoleh.
Waktu eksekusi sebelum optimisasi lebih lama dibandingkan setelah optimisasi.
Dari sini, saya menyimpulkan bahwa optimisasi yang dilakukan berhasil, dengan bantuan alat JMeter dan IntelliJ Profiler.
