#  **Mietpreis-Prognose für Wohnungen in Deutschland**
### *Ein Machine-Learning-Projekt zur Vorhersage der Kaltmiete (`baseRent`)*

![Status](https://img.shields.io/badge/Projekt-aktuell-success?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)
![ML](https://img.shields.io/badge/Machine%20Learning-Regression-orange?style=flat-square)

---

##  **Ziel des Projekts**
Dieses Projekt untersucht, wie sich die **Kaltmiete** für Wohnungen in Deutschland mithilfe von Machine Learning zuverlässig prognostizieren lässt.  
Es basiert auf dem Kaggle-Datensatz:

 **„Apartment Rental Offers in Germany“**

Dabei wurden modernste ML-Techniken genutzt:

- Datenbereinigung  
- Feature Engineering  
- Explorative Datenanalyse  
- Encoding-Strategien  
- Modelltraining (Random Forest, XGBoost, ANN)  
- Modellvergleich anhand von R², MAE  

---

##  **Inhaltsverzeichnis**
1. Überblick  
2. Datenquelle & Verständnis  
3. Datenbereinigung (Data Cleaning)  
4. Feature Engineering  
5. Explorative Datenanalyse (EDA)  
6. Encoding-Strategien  
7. Modelltraining  
8. Evaluation der Modelle  
9. Erkenntnisse  
10. Nächste Schritte  
11. Projektstruktur  
12. Installation & Ausführung  

---

# 1) **Überblick**
Das Projekt umfasst eine vollständige End-to-End-Pipeline:

- Daten einlesen  
- Struktur und Qualität prüfen  
- Bereinigung & Transformation  
- Feature Engineering  
- Modelltraining  
- Evaluation & Vergleich  

Alle Schritte sind im Notebook **`immo_pricing.ipynb`** dokumentiert.

---

# 2) **Datenquelle & Datenverständnis**

Die wichtigsten Merkmale des Datensatzes:

| Kategorie | Beispiele |
|----------|-----------|
| **Lage** | Bundesland, Kreis, PLZ |
| **Struktur** | Wohnfläche, Zimmeranzahl, Baujahr |
| **Ausstattung** | Balkon, Aufzug, Einbauküche |
| **Zustand** | saniert / unsaniert |
| **Preisattribute** | Kaltmiete, Warmmiete, Nebenkosten |

###  Entfernte bzw. nicht verwendete Spalten
- Spalten zur Warmmiete (`heatingCosts`, `electricityBasePrice`)  
- Spalten mit extrem vielen Missing Values  
- Spalten, die Target-Leakage verursachen (`baseRentRange`)  

---

# 3) **Datenbereinigung (Data Cleaning)**

###  **Typkonvertierungen**
- `geo_plz`, `geo_krs`, `geo_bln` → kategorisch  
- Jahreswerte → numerisch  
- Boolean-Spalten → 0/1  

###  **Fehlende Werte**
- Median/Mode-Imputation  
- Ableitung fehlender Werte aus bestehenden Spalten (z. B. Baujahr vs. Renovierungsjahr)  
- Logische Annahmen auf Basis von Domänenwissen  

###  **Ausreißerbehandlung**
- IQR-Clipping für numerische Variablen  

---

# 4) **Feature Engineering**

| Feature | Bedeutung |
|---------|-----------|
| `Bau_alt` | Alter der Immobilie |
| `lastRefurbish_in_years` | Jahre seit der letzten Renovierung |
| `room_ratio` | Verhältnis Zimmer / Wohnfläche |

Diese Features verbessern die Modellleistung und Erklärbarkeit.

---

# 5) **Explorative Datenanalyse (EDA)**

Durchgeführte Analysen:

- Korrelationen (Heatmaps)  
- Preisverteilung nach PLZ, Kreis, Bundesland  
- Scatterplots (z. B. Wohnfläche ↔ Kaltmiete)  
- Analyse des Einflusses von Ausstattung & Zustand  

###  Erkenntnisse aus der EDA
- Wohnfläche ist der stärkste Preistreiber  
- Modernisierte Wohnungen sind teurer  
- `room_ratio` & `noRooms` korrelieren stark mit der Miete   

---

# 6) **Encoding-Strategien**

| Encoding | Einsatz |
|---------|---------|
| **One-Hot Encoding (OHE)** | für Merkmale mit wenigen, überschaubaren Ausprägungen |
| **Target Encoding** | für Merkmale mit sehr viele unterschiedliche Ausprägungen |

---

# 7) **Modelltraining**

Trainierte Modelle:

- Baseline (Durchschnitt)  
- Lineare Regression  
- Random Forest   
- XGBoost  
- Artificial Neural Network (ANN)  

Evaluation anhand:

- **R²**  
- **MAE**   

---

# 8) **Evaluation der Modelle**

| Modell | Einschätzung |
|--------|--------------|
| **Lineare Regression** | einfach, aber geringe Genauigkeit |
| **Random Forest** | robust, solide Performance |
| **XGBoost** | **bestes Modell** |
| **ANN** | stabil, aber nicht besser als XGBoost |

---

# 9) **Erkenntnisse**

###  **Wichtigste Einflussfaktoren**
1. Lage (PLZ, Kreis, Bundesland)  
2. Wohnfläche  
3. Renovierungsstatus  
4. Zimmeranzahl  
5. Ausstattung (Balkon, Einbauküche, Aufzug)

###  **Business-Relevanz**
- Mietpreisbewertung  
- Marktanalyse  
- Identifikation ungewöhnlicher Angebote  
- Entscheidungsunterstützung für Investoren  

---

# 10) **Nächste Schritte**

- Hyperparameter-Tuning (GridSearch / Optuna)  
- SHAP-Analyse zur Modellinterpretation  
- Regionale Teilmodelle  
- Deployment als Web-App (Streamlit / FastAPI)  

---

# 11) **Projektstruktur**

```
immo-pricing/
│
├── immo_pricing.ipynb         # Hauptnotebook
├── data/
│     └── sample_data.csv
├── README.md
├── requirements.txt
└── .gitignore
```

---

# 12) **Installation & Ausführung**

###  **Benötigte Pakete installieren**
```bash
pip install -r requirements.txt
```

###  **Notebook starten**
```bash
jupyter notebook immo_pricing.ipynb
```

---

#  **Kontakt**
**Autor:** Iyad Aljundi 
**GitHub:** Iyad-Aljundi 

---
