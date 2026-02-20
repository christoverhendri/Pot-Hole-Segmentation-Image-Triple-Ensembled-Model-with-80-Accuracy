# 🛣️ Pothole Segmentation: Triple Ensemble with SOTA Models

Proyek ini adalah implementasi **Deep Learning** untuk segmentasi lubang jalan (potholes) menggunakan teknik **Ensemble Stacking** dari tiga arsitektur model *State-of-the-Art* (SOTA). Dikembangkan khusus untuk akurasi tinggi dan ketahanan terhadap variasi kondisi jalan.

## 🚀 Key Features
* **Triple Model Ensemble**: Menggabungkan kekuatan **UNet**, **MAnet**, dan **Segformer**.
* **Advanced TTA (Test Time Augmentation)**: Menggunakan *Multi-scale* (0.8x, 1.0x, 1.2x) dan *Horizontal/Vertical Flips* untuk prediksi yang lebih presisi.
* **Isotonic Calibration**: Mengkalibrasi probabilitas output untuk mengurangi *False Positives*.
* **Robustness**: Dilengkapi dengan *Gradient Clipping* dan *NaN-Safety guards* untuk stabilitas model.

---

## 🏗️ Model Architectures

Kami menggunakan tiga variasi model untuk menangkap fitur yang berbeda:

| Model | Encoder / Backbone | Karakteristik |
| :--- | :--- | :--- |
| **UNet** | `ConvNeXt-Base` | Sangat kuat dalam mempertahankan detail spasial tepi lubang. |
| **MAnet** | `ConvNeXt-Base` | Menggunakan *Multi-scale Attention* untuk fokus pada lubang yang jauh (kecil). |
| **Segformer** | `MiT-B3` | Berbasis Transformer, unggul dalam menangkap konteks tekstur aspal secara global. |

---

## 🛠️ Pipeline Training
Proyek ini menggunakan **5-Fold Cross Validation** untuk memastikan model tidak *overfit* dan memiliki generalisasi yang baik.



1.  **Preprocessing**: Resize ke 512x512 dengan augmentasi berat (Albu).
2.  **Training**: Optimasi menggunakan `AdamW` dengan *Learning Rate Scheduler*.
3.  **Ensemble Strategy**: 
    * Bobot ditentukan melalui optimasi Bayesian (**Optuna**).
    * Rumus Gabungan: $Score = (w_1 \cdot UNet) + (w_2 \cdot MAnet) + (w_3 \cdot Segformer)$.
4.  **Post-Processing**: Konversi output ke format **RLE (Run-Length Encoding)** untuk submisi.

---

## 📈 Results & Visualizations

### Performance Trend (Epoch 5 Snapshot)
Model menunjukkan progres belajar yang sangat stabil di semua fold:
* **UNet**: Dice Score ~0.84
* **MAnet**: Dice Score ~0.82
* **Segformer**: Dice Score ~0.81

*Catatan: Skor akhir ditingkatkan secara signifikan menggunakan Multi-Scale TTA.*

---

## 🧑‍💻 Author
**[Nama Kamu]** *AI & Computer Vision Enthusiast*
