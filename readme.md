# Analisis Sentimen Ulasan Aplikasi Wonder

Proyek ini melakukan analisis sentimen terhadap ulasan pengguna aplikasi Wonder menggunakan tahapan *preprocessing* teks, pelabelan berbasis leksikon InSet, ekstraksi fitur TF-IDF, dan klasifikasi menggunakan Linear Support Vector Machine (Linear SVM).


## Alur Proses

1. **Memuat data ulasan** dari file CSV.
2. **Pembersihan data**, termasuk menghapus baris dengan nilai kosong.
3. **Preprocessing teks**, yang mencakup pembersihan teks, case folding, normalisasi kata slang, tokenisasi, penghapusan stopword, dan tahapan preprocessing lain yang tersedia di notebook.
4. **Pelabelan sentimen** menggunakan leksikon InSet positif dan negatif. Skor leksikon dijumlahkan untuk menentukan label `positive`, `neutral`, atau `negative`.
5. **Menyimpan dataset hasil preprocessing** ke `data_cleaned_final.csv`.
6. **Membagi data** secara stratified menjadi 70% data latih, 15% data validasi, dan 15% data uji.
7. **Membangun pipeline** TF-IDF dan Linear SVM. TF-IDF di-fit melalui pipeline pada data latih agar informasi dari data validasi dan data uji tidak digunakan saat pembentukan kosakata.
8. **Memilih konfigurasi model** berdasarkan Macro-F1 pada data validasi.
9. **Evaluasi akhir** menggunakan data uji, termasuk Accuracy, Macro Precision, Macro Recall, Macro-F1, Weighted-F1, classification report, confusion matrix, serta kurva ROC dan Precision-Recall.

## Persiapan dan Instalasi

Disarankan menjalankan notebook di Google Colab karena notebook menggunakan akses Google Drive dan beberapa perintah instalasi khusus Colab.

Jika dijalankan di lingkungan Python lokal, instal dependensi utama:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn nltk Sastrawi wordcloud gdown
```

Beberapa sel mungkin membutuhkan penyesuaian jika dijalankan di luar Google Colab, khususnya bagian `google.colab`, unggah/unduh file, dan path dataset.

## Cara Menjalankan

### 1. Jalankan preprocessing

1. Buka notebook `Preprocesing_AnalsisiSentimenWonder.ipynb`.
2. Jalankan sel dari atas ke bawah.
3. Pastikan file sumber `wond.csv` dapat diunduh dan seluruh proses preprocessing selesai.
4. Notebook menyimpan hasil ke `data_cleaned_final.csv`.

### 2. Siapkan input untuk pemodelan

Letakkan `data_cleaned_final.csv` di direktori kerja notebook pemodelan. Untuk memastikan notebook pemodelan menggunakan hasil preprocessing yang sama, ubah sel pemuatan dataset menjadi:

```python
app_reviews_df = pd.read_csv("data_cleaned_final.csv")
```

Pastikan kolom berikut tersedia:
- `text_stopword`: teks yang sudah melalui preprocessing dan digunakan sebagai fitur.
- `polarity`: label sentimen yang digunakan sebagai target.

Jika notebook dijalankan di Google Colab, unggah file tersebut atau simpan di Google Drive dan sesuaikan path-nya.

### 3. Jalankan pemodelan

1. Buka notebook `Pembentukan_Model_Analisis_Sentimen_TFIDF_LinearSVM (2)(1).ipynb`.
2. Pastikan sumber data pada sel pemuatan sudah menunjuk ke dataset hasil preprocessing yang benar.
3. Jalankan semua sel secara berurutan.
4. Periksa distribusi label, hasil pemilihan parameter pada data validasi, dan metrik evaluasi pada data uji.

## Struktur Repositori yang Disarankan

data/
 - data_cleaned_final.csv
 - wond.csv

models/
- tfidf_linear_svm_balanced (1).joblib

notebooks/
- Pembentukan_Model_Analisis_Sentimen_TFIDF_LinearSVM (2).ipynb
- Preprocesing_AnalsisiSentimenWonder.ipynb

reports/
- Laporan UTS

src/
- 0dc13b49e34226b184efaa3a44da44a37d72.pdf
- Analisis+Sentimen+Pengguna+Aplikasi+Roblox+Berdasarkan+Ulasan+Menggunakan+Metode+Machine+Learning.pdf
- wahyuni,+9.+JE+-+Production+42-53.pdf

Nama file dapat dirapikan saat diunggah ke repositori, misalnya:
- `preprocessing_sentimen_wonder.ipynb`
- `modeling_tfidf_linear_svm.ipynb`
