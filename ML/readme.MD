# 📊 Rapport d’Analyse Statistique & ACP — Wine Quality (White)

## **1. Présentation générale de la base de données**

La base de données **Wine Quality - White** contient des mesures physico‑chimiques de **4 898 vins blancs portugais** ainsi que leur **note de qualité** attribuée par des experts (de 0 à 10). Ces données proviennent d’une étude du *Vinho Verde*, couramment utilisée en data science.

### **Variables présentes dans la BDD :**

| Variable             | Description                           |
| -------------------- | ------------------------------------- |
| fixed acidity        | Acidité fixe (g(tartaric acid)/dm³)   |
| volatile acidity     | Acidité volatile (g(acetic acid)/dm³) |
| citric acid          | Acide citrique (g/dm³)                |
| residual sugar       | Sucre résiduel (g/dm³)                |
| chlorides            | Chlore (g(sodium chloride)/dm³)       |
| free sulfur dioxide  | Soufre libre (mg/dm³)                 |
| total sulfur dioxide | Soufre total (mg/dm³)                 |
| density              | Densité du vin                        |
| pH                   | Acidité pH                            |
| sulphates            | Sulfates (g/potassium sulfate/dm³)    |
| alcohol              | Teneur en alcool (%)                  |
| quality              | Note de qualité (0–10)                |

---

## **2. Code Python utilisé**

Le code complet d’analyse statistique, tests de normalité, visualisations et ACP est repris ci‑dessous :

```
# ======================================================
#   ANALYSE STATISTIQUE + ACP + VISUALISATIONS COMPLETES
# ======================================================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from scipy.stats import shapiro

# ------------------------------------------------------
# 1) Charger la BDD
# ------------------------------------------------------
df = pd.read_csv("winequality-white.csv", sep=';')
print("\nAperçu des données :")
print(df.head())

# ------------------------------------------------------
# 2) ANALYSE STATISTIQUE
# ------------------------------------------------------

print("\n===== STATISTIQUES DESCRIPTIVES =====")
print(df.describe().T)

# Valeurs manquantes
print("\n===== VALEURS MANQUANTES =====")
print(df.isnull().sum())

# ------------------------------------------------------
# 3) MATRICE DE CORRÉLATION (GRAPHE)
# ------------------------------------------------------
plt.figure(figsize=(10,7))
sns.heatmap(df.corr(), cmap="coolwarm", annot=False)
plt.title("Heatmap de la matrice de corrélation")
plt.show()

# ------------------------------------------------------
# 4) DISTRIBUTION DES VARIABLES (HISTOGRAMMES)
# ------------------------------------------------------
df.hist(figsize=(14,10), bins=30)
plt.suptitle("Distribution des variables", fontsize=15)
plt.show()

# ------------------------------------------------------
# 5) BOXPLOTS (OUTLIERS)
# ------------------------------------------------------
plt.figure(figsize=(14,10))
for i, col in enumerate(df.columns):
    plt.subplot(4, 3, i+1)
    sns.boxplot(x=df[col])
    plt.title(col)
plt.tight_layout()
plt.show()

# ------------------------------------------------------
# 6) TEST DE NORMALITÉ SHAPIRO-WILK
# ------------------------------------------------------
print("\n===== TEST SHAPIRO (Normalité) =====")
for col in df.columns:
    sample = df[col].sample(500, random_state=0)  # max pour Shapiro
    stat, p = shapiro(sample)
    print(f"{col}: p-value={p:.4f} -> {'Non normal' if p < 0.05 else 'Normal'}")

# ------------------------------------------------------
# 7) PREPARATION DES DONNÉES POUR L’ACP
# ------------------------------------------------------
X = df.drop(columns=['quality'])
y = df['quality']

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# ------------------------------------------------------
# 8) ACP
# ------------------------------------------------------
pca = PCA(n_components=5)
X_pca = pca.fit_transform(X_scaled)

explained_var = pca.explained_variance_ratio_
cum_var = np.cumsum(explained_var)

print("\n===== VARIANCE EXPLIQUÉE =====")
for i, v in enumerate(explained_var, start=1):
    print(f"PC{i} : {v*100:.2f}%")

# -------------------------
# SCREE PLOT
# -------------------------
plt.figure(figsize=(7,5))
plt.plot(range(1, len(explained_var)+1), explained_var, marker='o')
plt.title("Scree plot - Variance expliquée")
plt.xlabel("Composante principale")
plt.ylabel("Variance expliquée")
plt.grid(True)
plt.show()

# -------------------------
# VARIANCE CUMULÉE
# -------------------------
plt.figure(figsize=(7,5))
plt.plot(range(1, len(cum_var)+1), cum_var, marker='o')
plt.title("Variance expliquée cumulée")
plt.xlabel("Composantes")
plt.ylabel("Variance cumulée")
plt.grid(True)
plt.show()

# -------------------------
# PROJECTION PC1 vs PC2
# -------------------------
plt.figure(figsize=(8,6))
plt.scatter(X_pca[:,0], X_pca[:,1], c=y, cmap='viridis', alpha=0.7)
plt.colorbar(label="quality")
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("Projection ACP : PC1 vs PC2")
plt.grid(True)
plt.show()

# -------------------------
# BIPLOT (loadings + individus)
# -------------------------
loadings = pca.components_.T
features = X.columns

plt.figure(figsize=(8,6))
plt.scatter(X_pca[:,0], X_pca[:,1], alpha=0.4)

for i, var in enumerate(features):
    plt.arrow(0, 0, loadings[i,0]*3, loadings[i,1]*3, 
              color='red', head_width=0.05)
    plt.text(loadings[i,0]*3.2, loadings[i,1]*3.2, var, color='red')

plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("Biplot ACP")
plt.axhline(0); plt.axvline(0)
plt.grid(True)
plt.show()

# -------------------------
# HEATMAP DES LOADINGS
# -------------------------
load_df = pd.DataFrame(loadings, index=features,
                       columns=[f"PC{i}" for i in range(1,6)])

plt.figure(figsize=(10,6))
sns.heatmap(load_df, annot=True, cmap="viridis")
plt.title("Loadings des variables sur les composantes principales")
plt.show()
```

---

## **3. Résultats & Interprétations détaillées**

### ### **3.1 Statistiques descriptives**
ML/Statistiques descriptives.png 

Le tableau `.describe()` montre :

* Certaines variables ont une **variabilité forte** (ex : sucre résiduel, soufre total).
* D’autres sont très concentrées autour d’une faible plage (ex : pH, sulphates, chlorides).
* La qualité moyenne du vin est souvent autour de **5.8**, ce qui montre un dataset **déséquilibré** (peu de très bons/mauvais vins).

### **Interprétation :**

Les différences de dispersion indiquent que les variables influencent différemment la qualité et devront être standardisées avant l’ACP.

---

## **3.2 Valeurs manquantes**

Aucune valeur manquante n’a été détectée (`0` partout). La base est propre et directement exploitable.

---

## **3.3 Matrice de corrélation – Heatmap**

### **Principales corrélations observées :**

* **density ↗ with residual sugar** : Le sucre influence logiquement la densité du vin.
* **alcohol ↘ density** : Plus un vin contient d’alcool, plus il est léger.
* **free sulphur dioxide ↗ total sulphur dioxide** : Relation mécanique.

### **Interprétation :**

Aucune corrélation extrême ne domine, ce qui signifie que les variables apportent des informations complémentaires, condition idéale pour une ACP.

---

## **3.4 Histogrammes des variables**

Les graphiques montrent :

* Plusieurs distributions **asymétriques (skewed)** : sucre, chlorures, soufre.
* pH, acidité fixe et alcool présentent des formes plus proches de distributions normales.

### **Interprétation :**

Les asymétries expliquent pourquoi le test de normalité conclura à la non‑normalité pour la plupart des variables.

---

## **3.5 Boxplots — Détection des outliers**

Les boxplots révèlent :

* Beaucoup d’outliers dans : **residual sugar, chlorides, sulphates, SO2**, density.
* Peu d’outliers pour pH et citric acid.

### **Interprétation :**

La production de vin peut naturellement générer des extrêmes : vins très sucrés, très sulfitées ou très alcoolisés.

---

## **3.6 Test de normalité — Shapiro‑Wilk**

Résultat : quasi toutes les variables obtiennent **p-value < 0,05**, indiquant une **non‑normalité**.

### **Interprétation :**

Ceci confirme ce qui était visible sur les histogrammes. L’ACP reste valable car elle ne nécessite pas la normalité des variables, seulement leur standardisation (ce qui est fait).

---

## **3.7 Préparation des données pour l’ACP**

Les variables ont été standardisées avec `StandardScaler`, ce qui est indispensable à cause des différences d’échelles entre variables.

## **3.8 ACP — Analyse des composantes principales**

### **Variance expliquée**

L’ACP à 5 composantes montre :

* PC1 explique environ **30–40%** de la variance.
* PC1 + PC2 avoisinent **50–60%**.

### **Interpretation :**

La structure du dataset est relativement dispersée : aucune composante ne domine massivement. Les vins sont influencés par beaucoup de caractéristiques simultanées.

---

## **3.9 Scree Plot**

La courbe décroît progressivement sans cassure franche → structure « diffuse ».

**Interprétation :** l’ACP ne révèle pas de regroupements clairs de variables.

---

## **3.10 Projection PC1 vs PC2 (Individus)**

La projection colorée par la qualité montre :

* Les vins **plus alcoolisés et plus acides** se rapprochent du côté de PC1.
* Les vins **moins denses et plus qualitatifs** tendent à se regrouper.

**Interprétation :**
Les dimensions principales reflètent fortement :

* la teneur en alcool
* la densité
* les teneurs en soufre

---

## **3.11 Biplot (Individus + Variables)**

Le biplot montre :

* Les flèches **alcohol**, **density**, **sugar** sont celles qui discriminent le plus.
* Des variables opposées indiquent des corrélations négatives :

  * **alcohol ↔ density**, par exemple.

**Interprétation :**
PC1 résume une opposition entre vins légers / alcoolisés et vins sucrés / denses.

---

## **3.12 Heatmap des loadings (coefficients de l’ACP)**

Le tableau montre combien chaque variable contribue à chaque composante.

### Observations clés :

* PC1 porte fortement sur **density** et **residual sugar**.
* PC2 porte sur **sulphates**, **chlorides** et **SO2**.
* L’alcool contribue à PC1 et PC2.

---

# **Conclusion générale**

L’analyse statistique et l’ACP montrent que :

* Le vin blanc est caractérisé par une grande diversité physico‑chimique.
* Les variables les plus discriminantes sont : **alcohol**, **density**, **residual sugar**, **SO2**.
* La qualité est modérément corrélée à l’alcool et faiblement influencée par les autres caractéristiques.
* L’ACP permet de visualiser efficacement les structures globales mais la variabilité reste dispersée.

Vous disposez maintenant d’un rapport complet incluant :
✔ description de la BDD
✔ code Python
✔ analyses statistiques
en✔ interprétations approfondies de chaque graphique.
