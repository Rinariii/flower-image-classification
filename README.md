# 🌸 Flower Classification using Custom CNN

Repositori ini berisi implementasi model *Deep Learning* untuk klasifikasi 5 jenis bunga menggunakan arsitektur **Convolutional Neural Network (CNN)** kustom berbasis **TensorFlow/Keras**. Model dirancang secara efisien untuk menangani dataset terbatas dengan performa tinggi.

---

## 📂 Struktur Proyek
```text
├── saved_model/          # Model dalam format TensorFlow SavedModel (.pb)
│   ├── saved_model.pb
│   └── variables/
├── tflite/               # Model teroptimasi untuk Mobile & IoT
│   ├── model.tflite
│   └── label.txt
├── tfjs_model/           # Model untuk deployment di Browser (JS)
│   ├── model.json
│   └── group1-shard1of1.bin
├── notebook.ipynb        # Eksperimen dan proses training
├── requirements.txt      # Daftar dependensi library
└── README.md             # Dokumentasi proyek

```

---

## 📊 Dataset

Dataset yang digunakan berasal dari Kaggle: **[Custom Flower Dataset: 5-Class Image Dataset](https://www.kaggle.com/datasets/kausthubkannan/5-flower-types-classification-dataset)**.

**Daftar Kelas:**

* 🌹 **Rose**
* 🌼 **Marigold**
* 🌸 **Petunia**
* 🌺 **Hibiscus**
* 🌻 **Chrysanthemum**

> **Preprocessing:** Semua gambar di-resize menjadi **224 × 224** piksel untuk menjaga konsistensi input model.

---

## 🏗️ Arsitektur Model

Model dikembangkan dengan fokus pada efisiensi (ringan) dan pencegahan *overfitting* menggunakan teknik regularisasi, mengingat rata-rata jumlah data hanya ~200 gambar per kelas.

**Detail Arsitektur:**

* **Block 1-4:** `Conv2D` → `Batch Normalization` → `ReLU` → `MaxPooling` → `Dropout` (0.15 - 0.30).
* **Global Layer:** `GlobalAveragePooling2D` (mengurangi jumlah parameter secara signifikan).
* **Classifier:** `Dense(128)` dengan `BatchNorm` & `Dropout(0.4)`.
* **Output:** `Dense(5, Softmax)` untuk klasifikasi multi-kelas.

**Mekanisme Optimasi (Callbacks):**

* 📉 `ReduceLROnPlateau`: Menurunkan *learning rate* saat performa mulai stagnan.
* 🛑 `EarlyStopping`: Menghentikan training otomatis jika tidak ada peningkatan untuk mencegah *overfitting*.

---

## ⚙️ Konfigurasi Training

| Parameter | Nilai |
| --- | --- |
| **Optimizer** | Adam |
| **Loss Function** | Sparse Categorical Crossentropy |
| **Input Shape** | 224 × 224 × 3 (RGB) |
| **Epochs** | 20 |

---

## 🚀 Model Exports

Untuk mendukung berbagai skenario deployment, model telah diekspor ke beberapa format:

1. **SavedModel:** Terletak di `submission/saved_model/` (untuk penggunaan server/Python).
2. **TFLite:** Terletak di `submission/tflite/` (untuk aplikasi Android/iOS atau Edge Devices).
3. **TFJS:** Terletak di `submission/tfjs_model/` (untuk integrasi di aplikasi web).

---

## 🛠️ Instalasi & Penggunaan

1. **Clone Repositori:**
```bash
git clone [https://github.com/username/flower-classification.git](https://github.com/username/flower-classification.git)
cd flower-classification

```


2. **Install Dependensi:**
```bash
pip install -r requirements.txt

```



---

## 🏆 Ringkasan Hasil

Model menunjukkan performa yang sangat impresif:

* ✅ **Akurasi Training:** 97% - 98%
* ✅ **Akurasi Test Set:** 98%
