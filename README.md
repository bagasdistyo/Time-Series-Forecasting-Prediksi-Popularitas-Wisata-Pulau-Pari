# 🏝️ Time Series Forecasting: Prediksi Popularitas Wisata Pulau Pari

## 📌 Project Overview

Proyek ini bertujuan untuk **memprediksi popularitas wisata Pulau Pari** selama satu tahun ke depan menggunakan data Google Trends. Data ini mencerminkan seberapa sering kata kunci "Pulau Pari" dicari dalam mesin pencari Google setiap minggunya.

Model yang digunakan adalah **ARIMA** dan **SARIMA**, dengan fokus pada perbandingan performa keduanya dalam memprediksi data time series dengan potensi musiman mingguan.

---

## 📊 Dataset

- **Sumber**: Google Trends
- **Frekuensi**: Mingguan
- **Periode**: Maret 2022 – Agustus 2024
- **Target kolom**: `Popularity` (indeks pencarian mingguan)

---

## 🎯 Objective

- Melakukan analisis time series pada popularitas Pulau Pari.
- Mengidentifikasi pola tren, musiman, dan noise dalam data.
- Melatih model ARIMA dan SARIMA untuk memprediksi popularitas 1 tahun ke depan.
- Mengevaluasi performa model menggunakan MAE dan MAPE.
- Menentukan model terbaik berdasarkan akurasi prediksi.

---

## 🧪 EDA (Exploratory Data Analysis)

### ✅ Temuan Utama:

- **Tren meningkat** dari tahun 2022 hingga 2024 dengan 5 lonjakan besar.
- **Lonjakan popularitas** umumnya terjadi saat **libur nasional**, seperti:
  - 1 Mei 2022 (Hari Buruh)
  - 23 April 2023 (Libur Lebaran)
  - 24 Desember 2023 (Natal)
  - 14 April 2024 (Ramadan)
  - 30 Juni 2024 (Liburan sekolah)
- **Model Decomposition** menunjukkan pola musiman yang kuat → cocok untuk SARIMA.
- **Periodisitas musiman**: 52 minggu (1 tahun).
- **Uji stasioner (ADF Test)** menunjukkan bahwa data sudah **stationary** tanpa differencing → `d = 0`.

---

## 🔧 Model Development

### ARIMA
- Parameter optimal berdasarkan AIC: **(1, 0, 2)**
- MAE (Train): 6.69
- MAPE (Train): 21%
- MAE (Test): 10.07
- MAPE (Test): 24%

### SARIMA
- Parameter optimal: **(1, 0, 2)(1, 0, 2, 52)**
- MAE (Train): 6.5
- MAPE (Train): 19%
- MAE (Test): 10.3
- MAPE (Test): 25%

---

## 🧠 Model Comparison

| Model  | MAE (Test) | MAPE (Test) | Seasonal Support | Catatan |
|--------|------------|-------------|------------------|---------|
| ARIMA  | **10.07**  | **24%**     | ❌               | Akurasi lebih baik, tapi prediksi flat |
| SARIMA | 10.30      | 25%         | ✅               | Lebih mengikuti pola musiman, tetapi sedikit lebih error |

🔎 **Kesimpulan**:
- **ARIMA dipilih sebagai model terbaik** karena memiliki error prediksi lebih kecil.
- Namun, SARIMA lebih baik dalam menangkap pola musiman → bisa dieksplorasi lebih lanjut jika data lebih panjang atau jika musiman menjadi fokus utama.

---

## 📈 Inference (Forecasting)

- Dilakukan prediksi **52 minggu ke depan** (1 tahun).
- Visualisasi menunjukkan bahwa **ARIMA menghasilkan garis prediksi datar**, sedangkan **SARIMA mengikuti pola musiman** dari data historis.

---

## 🧾 Evaluation Metrics

- **MAE (Mean Absolute Error)**: Digunakan karena mudah diinterpretasi dan tidak sensitif terhadap outlier.
- **MAPE (Mean Absolute Percentage Error)**: Memberikan insight dalam bentuk persentase kesalahan prediksi.

---

## 💡 Kesimpulan Akhir

- Data popularitas wisata Pulau Pari memiliki pola musiman yang kuat.
- Model ARIMA memberikan hasil prediksi yang **lebih akurat secara numerik**, meskipun tidak menangkap pola musiman.
- **SARIMA** cocok untuk digunakan dalam prediksi yang membutuhkan representasi pola musiman seperti peak saat libur panjang.
- **Rekomendasi bisnis**: Fokus promosi pada momen liburan (Mei, Desember, April) yang menunjukkan lonjakan pencarian signifikan.

---

## 🧠 Tools & Libraries

- Python
- Pandas
- Matplotlib
- Statsmodels (ARIMA & SARIMA)
- Scikit-learn (for evaluation metrics)
