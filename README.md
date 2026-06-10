# Machine-Learning
# 🌧️ Rain Prediction in Indonesia — Machine Learning Project

Projekt klasyfikacji binarnej przewidujący wystąpienie opadów deszczu w ciągu najbliższych 6 godzin na podstawie danych meteorologicznych z Indonezji.

---

## 📌 Cel projektu

Zbudowanie i porównanie modeli uczenia maszynowego odpowiadających na pytanie:

> **Czy w ciągu najbliższych 6 godzin wystąpią opady deszczu?**

Zmienna docelowa: `rain_next_6h` (0 = brak opadów, 1 = opady)

---

## 📂 Źródło danych

Zbiór danych pochodzi z platformy Kaggle:
[Indonesia Hourly Weather for Rain Prediction](https://www.kaggle.com/datasets/karanroyka/indonesia-hourly-weather-for-rain-prediction)

- **Liczba rekordów:** ~210 000
- **Liczba cech:** 15
- **Rozkład klas:** 54% opady (1), 46% brak opadów (0)

---

## 🔧 Technologie

- Python 3
- Google Colab
- pandas, numpy
- scikit-learn
- matplotlib, seaborn

---

## 🗂️ Struktura projektu

```
Machine-Learning/
│
├── RAIN_PREDICTION_INDONESIA.ipynb   # Główny notebook z całą analizą
├── ml_dataset.csv                    # Zbiór danych (pobrany z Kaggle)
└── README.md
```

---

## 🔍 Metodologia

### 1. Eksploracja danych (EDA)
- Analiza rozkładu zmiennej docelowej
- Wizualizacje: histogramy, macierz korelacji, scatter matrix, mapa geograficzna
- Wykrycie silnej korelacji zmiennych `rain` i `rain_sum_next_6h` ze zmienną docelową → usunięcie jako **data leakage**

### 2. Przygotowanie danych
- Stratyfikowany podział na zbiór treningowy (80%) i testowy (20%) z użyciem `StratifiedShuffleSplit` po zmiennej `precipitation` (najsilniej niezbalansowana cecha)
- Selekcja cech — usunięcie kolumn tekstowych (`city`, `timestamp`) oraz kolumn z data leakage (`rain`, `rain_sum_next_6h`)
- Skalowanie danych dla Regresji Logistycznej (`StandardScaler`)

### 3. Modele

| Model | Metoda optymalizacji | Najlepsze hiperparametry |
|---|---|---|
| Regresja Logistyczna | — | max_iter=1000 |
| Drzewo Decyzyjne | GridSearchCV (cv=5) | max_depth=15, min_samples_split=50 |
| Las Losowy | RandomizedSearchCV (cv=5) | max_depth=20, min_samples_split=37, n_estimators=238 |

---

## 📊 Wyniki

Główna metryka oceny: **F1-score** (odporna na niezbalansowane klasy)

| Model | F1-Score (klasa 1) | Accuracy |
|---|---|---|
| Regresja Logistyczna | 0.80 | 80% |
| Drzewo Decyzyjne | 0.81 | 80% |
| **Las Losowy** | **0.82** | **81%** |

### 🥇 Najlepszy model: Las Losowy

```
--- Raport klasyfikacji: Las Losowy (Optymalny) ---
              precision    recall  f1-score   support

           0       0.76      0.87      0.81     19103
           1       0.88      0.77      0.82     22974

    accuracy                           0.81     42077
   macro avg       0.82      0.82      0.81     42077
weighted avg       0.82      0.81      0.81     42077
```

---

## 🚀 Jak uruchomić projekt

1. Pobierz zbiór danych z [Kaggle](https://www.kaggle.com/datasets/karanroyka/indonesia-hourly-weather-for-rain-prediction)
2. Wgraj plik `ml_dataset.csv` do Google Colab (zakładka Pliki → `/content/`)
3. Otwórz `RAIN_PREDICTION_INDONESIA.ipynb` w Google Colab
4. Uruchom wszystkie komórki: **Runtime → Run all**

---

## 👩‍💻 Autor

**Barbara Tylkowska**
[GitHub](https://github.com/TylkowskaBarbara/Machine-Learning)
