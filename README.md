# Lung Sound Classification using Convolutional Neural Network

**Dataset : International Conference on Biomedical and Health Informatics 2017 (ICBHI 2017)**

Klasifikasi suara paru dilakukan dengan mempersiapkan data terlebih dahulu. Data berupa file audio (rekaman suara paru), file teks (berisi pembagian siklus pernafasan dan label dari setiap siklus pernafasan), dan file yang berisi asal pengambilan suara paru (contoh : trakea). Langkah awal yang dilakukan adalah dengan memisahkan suara paru menjadi persiklus pernafasan berdasarkan file teks yang ada. Setelah melakukan pemisahan audio menjadi persiklus pernafasan, maka dilakukan proses encode label. Proses encode label digunakan karena label masih terbagi menjadi dua kolom, yaitu crackle dan wheeze. Label diencode menjadi :

0 = Normal,
1 = Crackle,
2 = Wheeze,
3 = Crackle and Wheeze.

Setelah itu mulailah dilakukan pembuatan spektogram dengan menggunakan algoritma STFT (Short-Time Fourier Transform). Spektogram yang telah dibuat kemudian digunakan untuk melakukan klasifikasi dengan menggunakan CNN. Sebelum melakukan klasifikasi, dilakukan beberapa augmentasi seperti mempercepat audio, memperlambat audio, dan lainnya. Augmentasi tersebut kemudian juga diubah menjadi spektogram dengan menggunakan STFT. Ketika seluruh data sudah siap untuk klasifikasi, maka dilakukanlah penentuan untuk melakukan validasi model terlebih dahulu. Sebagai validasi model digunakan K-Fold Cross-Validation karena jumlah data spektogram yang akan diklasifikasi (tanpa augmentasi) hanya terdapat 2369 data, maka K-Fold Cross-Validation adalah pilihan yang tepat daripada menggunakan Hold-Out. K-Fold Cross-Validation digunakan untuk mencegah terjadinya overfitting pada model yang akan kita buat. Selain dengan menggunakan Cross-Validation, beberapa regularisasi juga dilakukan untuk mencegah terjadinya overfitting (contoh : augmentasi dan dropout).

Secara garis besar, proses yang dilakukan pada pembuatan model kali ini adalah
1. Membersihkan dan mempersiapkan data
2. Modelling dan Cross-Validation untuk mencari hyperparameter yang baik
3. Train ulang model dengan menggunakan hyperparameter yang didapatkan dari hasil validasi dengan Cross-Validation
4. Test model yang telah dilatih
