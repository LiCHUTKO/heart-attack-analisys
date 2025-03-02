# ❤️ Heart Attack Analysis

## 📑 Spis treści
- [📋 Opis projektu](#opis-projektu)
- [📂 Struktura projektu](#struktura-projektu)
- [📦 Wymagania](#wymagania)
- [⚙️ Instalacja](#instalacja)
- [📊 Przygotowanie danych](#przygotowanie-danych)
- [🧠 Trenowanie modelu](#trenowanie-modelu)
- [📈 Ocena modelu](#ocena-modelu)
- [🔍 Wykonanie predykcji](#wykonanie-predykcji)
- [📉 Wizualizacja wyników](#wizualizacja-wyników)
- [👥 Autorzy](#autorzy)

## 📋 Opis projektu
Projekt "Heart Attack Analysis" ma na celu stworzenie modelu sieci neuronowej do przewidywania ryzyka zawału serca na podstawie danych medycznych pacjentów. Model jest trenowany, walidowany i testowany na zbiorze danych zawierającym informacje o pacjentach z różnymi cechami zdrowotnymi.

## 📂 Struktura projektu
```
heart-attack-analysis/
│
├── heart.csv
├── notebook.ipynb
├── requirements.txt
└── README.md
```

## 📦 Wymagania
- Python 3.7+
- TensorFlow 2.0+
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Pandas

## ⚙️ Instalacja
Sklonuj repozytorium:
```bash
git clone https://github.com/LiCHUTKO/heart-attack-analysis.git
cd heart-attack-analysis
```

Zainstaluj wymagane biblioteki:
```bash
pip install -r requirements.txt
```

## 📊 Przygotowanie danych
Dane są wczytywane z pliku CSV i przetwarzane w notebooku `notebook.ipynb`. Zawierają informacje takie jak wiek, płeć, ciśnienie krwi, poziom cholesterolu i inne cechy zdrowotne pacjentów.

## 🧠 Trenowanie modelu
Otwórz plik `notebook.ipynb` w Jupyter Notebook lub Jupyter Lab. Wykonaj wszystkie komórki w notebooku, aby załadować dane, przygotować je, zbudować model, przeprowadzić trening i ocenić model.

Kod do trenowania modelu:
```python
model = Sequential([
    Dense(256, activation='relu', input_shape=(13,)),
    Dense(128, activation='relu'),
    Dense(64, activation='relu'),
    Dense(32, activation='relu'),
    Dense(1, activation='sigmoid')
])

model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])

history = model.fit(X_train, y_train, epochs=100, validation_split=0.2, batch_size=4096)
```

## 📈 Ocena modelu
Model jest oceniany na zbiorze testowym za pomocą różnych metryk, takich jak dokładność, precyzja, czułość i F1-score.

Kod do oceny modelu:
```python
accuracy = accuracy_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)

print(f"Accuracy: {accuracy}")
print(f"Recall: {recall}")
print(f"Precision: {precision}")
print(f"F1: {f1}")
```

## 🔍 Wykonanie predykcji
Model może wykonywać predykcje na nowych danych pacjentów.

Kod do wykonania predykcji:
```python
data1 = pd.DataFrame([{
    'wiek': 55,
    'płeć': 1,
    'ból_w_klatce': 0,
    'ciśnienie_krwi': 140,
    'cholesterol': 240,
    'cukier_we_krwi': 0,
    'wynik_EKG': 1,
    'tętno': 150,
    'ból_wysiłkowy': 0,
    'depresja_ST': 1.0,
    'nachylenie_ST': 2,
    'naczynia': 0,
    'thal': 2
}])

data1_scaled = scaler.transform(data1)
prediction1 = model.predict(data1_scaled)
print("Istnieje ryzyko choroby serca." if prediction1[0] == 1 else "Brak ryzyka choroby serca.")
```

## 📉 Wizualizacja wyników
Wyniki treningu i oceny modelu są wizualizowane za pomocą wykresów.

Kod do wizualizacji wyników:
```python
plt.figure(figsize=(12, 8))
plt.subplot(2, 1, 1)
plt.plot(history.history['accuracy'], label='Dokładność treningu')
plt.plot(history.history['val_accuracy'], label='Dokładność walidacji')
plt.xlabel('Epoka')
plt.ylabel('Dokładność')
plt.legend()

plt.subplot(2, 1, 2)
plt.plot(history.history['loss'], label='Strata treningu')
plt.plot(history.history['val_loss'], label='Strata walidacji')
plt.xlabel('Epoka')
plt.ylabel('Strata')
plt.legend()
plt.show()

conf_matrix = confusion_matrix(y_test, y_pred)
plt.figure(figsize=(8, 6))
sns.heatmap(conf_matrix, annot=True, fmt='d', cmap='Blues', cbar=False)
plt.title('Macierz konfuzji')
plt.xlabel('Przewidywane wartości')
plt.ylabel('Rzeczywiste wartości')
plt.show()
```

## 👥 Autorzy
- [LiCHUTKO](https://github.com/LiCHUTKO)
