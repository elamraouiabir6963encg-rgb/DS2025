Voici ton **script Python complet**, correctement formaté en **Markdown** pour présentation ou documentation :

---

# 📊 Analyse Statistique et Graphique de la Base de Données **Adult**

## 🧩 1. Import des bibliothèques

```python
import zipfile
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os
```

---

## 📦 2. Extraction du fichier ZIP

```python
zip_path = "adult.zip"
extract_dir = "adult_data"

with zipfile.ZipFile(zip_path, 'r') as zip_ref:
    zip_ref.extractall(extract_dir)

# On cherche le fichier CSV ou DATA extrait
for file in os.listdir(extract_dir):
    if file.endswith(".csv") or file.endswith(".data"):
        data_path = os.path.join(extract_dir, file)
        break
```

---

## 📥 3. Chargement des données

```python
try:
    df = pd.read_csv(data_path)
except:
    df = pd.read_csv(data_path, sep=",", header=None)

# Attribution des noms de colonnes si absents
if df.shape[1] == 15:
    df.columns = [
        "age", "workclass", "fnlwgt", "education", "education_num", "marital_status",
        "occupation", "relationship", "race", "sex", "capital_gain", "capital_loss",
        "hours_per_week", "native_country", "income"
    ]
```

---

## 👁️ 4. Aperçu général

```python
print("\n===== APERÇU GÉNÉRAL =====")
print(df.head())
print("\nDimensions :", df.shape)
print("\nTypes de variables :\n", df.dtypes)
```

---

## 🧹 5. Valeurs manquantes et qualité des données

```python
print("\n===== VALEURS MANQUANTES =====")
print(df.isnull().sum())

# Remplacement des valeurs codées par " ?"
df = df.replace(" ?", np.nan)
print("\nValeurs manquantes après remplacement de '?':")
print(df.isnull().sum())
```

---

## 📈 6. Statistiques descriptives

```python
print("\n===== STATISTIQUES NUMÉRIQUES =====")
print(df.describe())

print("\n===== STATISTIQUES CATÉGORIELLES =====")
for col in df.select_dtypes(include='object'):
    print(f"\n{col} :")
    print(df[col].value_counts(normalize=True).head())
```

---

## 📊 7. Analyse univariée

```python
numeric_cols = df.select_dtypes(include=np.number).columns
categorical_cols = df.select_dtypes(exclude=np.number).columns

# Histogrammes pour variables numériques
for col in numeric_cols:
    plt.figure(figsize=(6, 4))
    sns.histplot(df[col].dropna(), kde=True, bins=30)
    plt.title(f"Distribution de {col}")
    plt.show()

# Diagrammes en barres pour variables qualitatives
for col in categorical_cols:
    plt.figure(figsize=(8, 4))
    df[col].value_counts().head(10).plot(kind='bar')
    plt.title(f"Répartition de {col}")
    plt.show()
```

---

## 🔗 8. Analyse bivariée

```python
# Corrélation entre variables numériques
plt.figure(figsize=(10, 8))
sns.heatmap(df[numeric_cols].corr(), annot=True, cmap="coolwarm")
plt.title("Matrice de corrélation")
plt.show()

# Boxplots : revenu vs variables continues
for col in ["age", "education_num", "hours_per_week"]:
    plt.figure(figsize=(6, 4))
    sns.boxplot(x="income", y=col, data=df)
    plt.title(f"{col} selon le revenu")
    plt.show()

# Diagrammes : revenu vs variables qualitatives
for col in ["sex", "marital_status", "occupation"]:
    plt.figure(figsize=(8, 4))
    sns.countplot(data=df, x=col, hue="income")
    plt.title(f"Répartition de {col} selon le revenu")
    plt.xticks(rotation=45)
    plt.show()
```

---

## 🧾 9. Synthèse

```python
print("\n===== SYNTHÈSE =====")
print("Les principales variables influençant le revenu sont généralement :")
print("- Le niveau d’éducation (education_num)")
print("- Le nombre d’heures travaillées par semaine")
print("- L’âge")
print("- La catégorie socioprofessionnelle (occupation, workclass)")
print("- Le sexe et l’état matrimonial")
```

---

### ✅ Résumé

Ce code :

* **Décompresse** et **charge** automatiquement la base de données `adult.zip`.
* Effectue un **nettoyage des valeurs manquantes**.
* Génère un **tableau complet des statistiques descriptives**.
* Produit des **graphes d’analyse univariée et bivariée** (distributions, corrélations, boxplots et countplots).
* Conclut par une **synthèse des facteurs influençant le revenu**.

---

### 📚 Référence

* UCI Machine Learning Repository — [Adult Data Set](https://archive.ics.uci.edu/ml/datasets/adult)
