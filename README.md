---
tags:
- machine-learning
- regression
- sports-analytics
- formula1
- streamlit
- huggingface
---

# 🏎️ F1 Team Points Predictor

Bu proje, 1950–2020 yılları arasındaki Formula 1 yarış verilerini kullanarak bir takımın bir yarışta alacağı puanı tahmin etmeye yönelik bir regresyon modeli içerir. Takım adı, yarış yılı ve pist bilgileri modele verilerek tahmini puan çıktısı elde edilir.

## 📌 Kullanılan Veri Seti

- Kaggle → [Formula 1 World Championship (1950 - 2020)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)

Kullanılan dosyalar:
- `constructor_results.csv`
- `constructors.csv`
- `races.csv`

## 🧪 Proje Adımları

1. Veriler birleştirildi ve her yarış için takım, yıl, pist bilgileri çıkarıldı.
2. `LabelEncoder` ile kategorik veriler sayısal hale getirildi.
3. Model girdisi: `year`, `team_encoded`, `circuit_encoded`
4. Model hedefi: `points` (takımın o yarışta aldığı puan)
5. `RandomForestRegressor` eğitildi ve RMSE ≈ 4.42, R² ≈ 0.65 başarı elde edildi.
6. Model ve encoder’lar `.pkl` olarak kaydedildi.
7. Kullanıcı arayüzü Streamlit ile geliştirildi.

## 🖥️ Streamlit Arayüzü

Kullanıcı:
- Yıl (slider ile)
- Takım (seçim kutusu)
- Pist ID (seçim kutusu)

seçerek puan tahmini alabilir.

## 📦 Gereksinimler

```bash
pip install -r requirements.txt


▶ Uygulamayı Çalıştır
streamlit run app.py


🔍 Model Dosyaları
team_points_predictor.pkl → Eğitimli regresyon modeli

team_encoder.pkl → Takım adlarını sayıya çeviren etiketleyici

circuit_encoder.pkl → Pist ID’lerini sayıya çeviren etiketleyici


🧠 Kullanım Örneği
import joblib

model = joblib.load('team_points_predictor.pkl')
team_encoder = joblib.load('team_encoder.pkl')
circuit_encoder = joblib.load('circuit_encoder.pkl')

input_data = [[2020, team_encoder.transform(['Mercedes'])[0], circuit_encoder.transform(['monza'])[0]]]
predicted_points = model.predict(input_data)
print(f"Tahmin Edilen Puan: {predicted_points[0]:.2f}")



🚀 Model Yüklemeleri
Bu model aşağıdaki platformlara da yüklenebilir:

🤗 Hugging Face: team_points_predictor.pkl + encoder’lar

💻 GitHub: notebook, app.py, requirements.txt, README.md


👤 Geliştirici
Bu proje, yapay zekâ alanında uygulamalı portfolyo geliştirmek amacıyla oluşturulmuştur. Spor analitiği, veri mühendisliği ve makine öğrenimi alanlarının birleşimini temsil eder.


