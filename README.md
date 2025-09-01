# Predict The Introverts From The Extroverts

Proyek ini bertujuan untuk membangun model machine learning yang mampu memprediksi kepribadian seseorang (Introvert atau Ekstrovert) berdasarkan kebiasaan sosial dan personal mereka. Analisis data eksplorasi (EDA) dilakukan untuk memahami karakteristik data dan merumuskan hipotesis awal.

## 🗂️ Daftar Isi

  - [Analisis Data Eksplorasi (EDA)](https://www.google.com/search?q=%23-analisis-data-eksplorasi-eda)
      - [Hipotesis Awal](https://www.google.com/search?q=%23-hipotesis-awal)
      - [Observasi Utama](https://www.google.com/search?q=%23-observasi-utama)
      - [Rekomendasi Penanganan Data](https://www.google.com/search?q=%23-rekomendasi-penanganan-data)

-----

## 🔬 Analisis Data Eksplorasi (EDA)

Tahap ini berfokus pada pemahaman mendalam terhadap dataset, termasuk distribusi data, identifikasi anomali, dan hubungan antar variabel.

### ❓ Hipotesis Awal

Berikut adalah beberapa hipotesis yang dirumuskan sebelum analisis mendalam:

1.  **Hubungan `Time_spent_Alone` dengan `Personality`**

      * **H₁**: Semakin **tinggi** jumlah waktu yang dihabiskan sendirian, semakin besar kemungkinan seseorang memiliki kepribadian **introvert**.

2.  **Hubungan `Stage_fear` dengan `Personality`**

      * **H₁**: Seseorang yang **memiliki** demam panggung (`Stage_fear` = Yes) lebih cenderung memiliki kepribadian **introvert**.

3.  **Hubungan `Social_event_attendance` dengan `Personality`**

      * **H₁**: Semakin **rendah** frekuensi kehadiran di acara sosial, semakin besar kemungkinan seseorang memiliki kepribadian **introvert**.

4.  **Hubungan `Going_outside` dengan `Personality`**

      * **H₁**: Semakin **rendah** frekuensi keluar rumah, semakin besar kemungkinan seseorang memiliki kepribadian **introvert**.

5.  **Hubungan `Drained_after_socializing` dengan `Personality`** 🔋

      * **H₁**: Seseorang yang **merasa lelah** setelah bersosialisasi (`Drained_after_socializing` = Yes) sangat cenderung memiliki kepribadian **introvert**.

6.  **Hubungan `Friends_circle_size` dengan `Personality`** 👥

      * **H₁**: Semakin **kecil** ukuran lingkaran pertemanan, semakin besar kemungkinan seseorang memiliki kepribadian **introvert**.

7.  **Hubungan `Post_frequency` dengan `Personality`**

      * **H₁**: Semakin **rendah** frekuensi posting di media sosial, semakin besar kemungkinan seseorang memiliki kepribadian **introvert**.

### 📊 Observasi Utama

#### Ringkasan Umum

Secara umum, dataset cenderung mengarah ke profil ekstrovert. Hal ini terlihat dari rata-rata waktu yang dihabiskan sendirian yang relatif rendah (sekitar 3 jam), frekuensi kehadiran di acara sosial dan keluar rumah yang tinggi (masing-masing 5 dan 4 kali seminggu), serta ukuran lingkaran pertemanan dan frekuensi posting yang besar.

#### Analisis Variabel Kunci

  * **`Personality` (Variabel Target)**

      * **Ketidakseimbangan Kelas (Class Imbalance):** Observasi paling krusial. Dataset sangat tidak seimbang dengan proporsi **74% Ekstrovert (13.699)** dan **26% Introvert (4.825)**. Hal ini perlu ditangani agar model tidak bias.
      * **Kualitas Data:** Kolom ini menjadi referensi utama karena tidak memiliki *missing values*.

  * **Variabel Kategorikal (`Drained_after_socializing` & `Stage_fear`)**

      * **Distribusi:** Mayoritas responden menjawab **'No'** untuk kedua variabel ini (tidak lelah setelah bersosialisasi dan tidak punya demam panggung), yang konsisten dengan dominasi kelas ekstrovert.
      * **Kualitas Data:** Terdapat *missing values* pada kedua kolom ini (`Drained_after_socializing`: 1.149; `Stage_fear`: 1.893) yang perlu ditangani.

#### Analisis Outlier

  * **Sumber Outlier:** Outlier hanya ditemukan pada kolom `Time_spent_Alone` sebanyak **2.843 titik data**.
  * **Dampak:** Keberadaan outlier ini memengaruhi 2.843 baris data. Menghapus baris-baris ini akan mengurangi ukuran dataset secara signifikan dan berpotensi menghilangkan informasi berharga dari kolom lain.

#### Analisis Distribusi Data Numerik

  * **Distribusi Normal:**
      * `Friends_circle_size` (Sangat Simetris)
      * `Post_frequency` (Sangat Simetris)
      * `Social_event_attendance` (Cukup Simetris)
      * `Going_outside` (Cukup Simetris)
  * **Distribusi Miring ke Kanan (Positively Skewed):**
      * `Time_spent_Alone` (Sangat Miring)

### ✅ Rekomendasi Penanganan Data

Berdasarkan temuan di atas, berikut adalah rekomendasi untuk tahap pre-processing data:

1.  **Penanganan Outlier pada `Time_spent_Alone`:**

      * **Rekomendasi Terkuat: *Capping (Winsorization)*.** Ganti nilai yang lebih besar dari batas atas (misalnya, \> 8.5) dengan nilai batas atas itu sendiri. Pendekatan ini memperbaiki anomali **tanpa kehilangan data**.
      * **Alternatif Lain:**
          * **Transformasi Data:** Terapkan transformasi log atau akar kuadrat untuk mengurangi dampak nilai ekstrem.
          * **Gunakan Model yang Robust:** Manfaatkan model seperti **Random Forest** atau **Gradient Boosting** yang secara inheren lebih tahan terhadap outlier.

2.  **Penanganan Distribusi Miring pada `Time_spent_Alone`:**

      * **Tindakan:** Terapkan **Log Transformation** atau **Square Root Transformation**. Tujuannya adalah membuat distribusi lebih mendekati normal untuk meningkatkan performa model, terutama model linear.

3.  **Penanganan *Missing Values*:**

      * Terapkan strategi imputasi (misalnya, menggunakan modus untuk data kategorikal) pada kolom `Drained_after_socializing` dan `Stage_fear`.

4.  **Penanganan Ketidakseimbangan Kelas:**

      * Gunakan teknik seperti **SMOTE (Synthetic Minority Over-sampling Technique)** untuk menyeimbangkan jumlah kelas introvert dan ekstrovert pada data training.
