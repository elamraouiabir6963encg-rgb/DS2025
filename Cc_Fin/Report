
# 🗂️ Descriptif détaillé de la base de données

## 1. Présentation générale

* **Nom du jeu de données :** Adult (ou Census Income Dataset)
* **Source :** UCI Machine Learning Repository ([Adult Data Set](https://archive.ics.uci.edu/ml/datasets/adult))
* **Nombre d’observations :** 32 561
* **Nombre de variables :** 15
* **Objectif :** Prédire si le revenu d’une personne dépasse **50 000 $ par an** en fonction de ses caractéristiques démographiques et professionnelles.

---

## 2. Variables du jeu de données

| Variable           | Type                  | Description                                                                  |
| ------------------ | --------------------- | ---------------------------------------------------------------------------- |
| **age**            | Quantitative (int)    | Âge de l’individu.                                                           |
| **workclass**      | Qualitative           | Type d’emploi (ex. Private, Self-emp, Government…).                          |
| **fnlwgt**         | Quantitative (int)    | Poids d’échantillonnage (facteur de pondération statistique du recensement). |
| **education**      | Qualitative           | Niveau d’éducation (Bachelors, HS-grad, Masters…).                           |
| **education_num**  | Quantitative (int)    | Niveau d’éducation sous forme numérique (de 1 à 16).                         |
| **marital_status** | Qualitative           | Statut matrimonial (Never-married, Married-civ-spouse…).                     |
| **occupation**     | Qualitative           | Type de profession exercée.                                                  |
| **relationship**   | Qualitative           | Relation au sein du foyer (Husband, Wife, Own-child…).                       |
| **race**           | Qualitative           | Catégorie raciale (White, Black, Asian-Pac-Islander…).                       |
| **sex**            | Qualitative           | Sexe (Male ou Female).                                                       |
| **capital_gain**   | Quantitative (int)    | Gains en capital.                                                            |
| **capital_loss**   | Quantitative (int)    | Pertes en capital.                                                           |
| **hours_per_week** | Quantitative (int)    | Nombre d’heures travaillées par semaine.                                     |
| **native_country** | Qualitative           | Pays d’origine.                                                              |
| **income**         | Qualitative (binaire) | Catégorie de revenu : `<=50K` ou `>50K` (variable cible).                    |

---

## 3. Qualité des données

* **Valeurs manquantes :** présentes dans certaines colonnes (`workclass`, `occupation`, `native_country`) sous forme de `"?"`.
* **Nettoyage nécessaire :** suppression ou imputation de ces valeurs avant toute modélisation.
* **Type de variables :**

  * 6 numériques
  * 9 catégorielles

---

# 📊 Descriptif détaillé des résultats de l’étude

## 1. Statistiques descriptives principales

| Variable           | Moyenne | Min | Max   | Commentaire                       |
| ------------------ | ------- | --- | ----- | --------------------------------- |
| **age**            | ~38.6   | 17  | 90    | Population adulte active.         |
| **education_num**  | ~10.1   | 1   | 16    | Niveau moyen équivalent au lycée. |
| **hours_per_week** | ~40.4   | 1   | 99    | Moyenne proche du plein temps.    |
| **capital_gain**   | ~1077   | 0   | 99999 | Très concentré vers 0.            |
| **capital_loss**   | ~87     | 0   | 4356  | Très concentré vers 0.            |

---

## 2. Répartition du revenu

| Catégorie | Pourcentage |
| --------- | ----------- |
| `<=50K`   | ~76%        |
| `>50K`    | ~24%        |

👉 **Observation :** la majorité des individus gagnent moins de 50 000 $/an, ce qui crée un **déséquilibre des classes** (important à prendre en compte pour la modélisation).

---

## 3. Corrélations clés (tendances observées)

* **Âge, niveau d’éducation et heures de travail** augmentent la probabilité d’un revenu supérieur à 50K.
* **Hommes** ont statistiquement plus de chances d’avoir un revenu >50K que les femmes.
* Les métiers **professionnels, exécutifs ou techniques** présentent des revenus plus élevés.
* Les individus mariés sont surreprésentés dans la catégorie `>50K`.

---

## 4. Conclusion générale

Le jeu de données **Adult** est un classique de l’analyse prédictive binaire, permettant d’évaluer des modèles de classification (comme la régression logistique, SVM ou arbres de décision).
Les principales variables explicatives du revenu sont **l’âge**, **le niveau d’éducation**, **la profession** et **les heures de travail**.

---

### 📚 Références

* UCI Machine Learning Repository — *Adult Data Set*
  🔗 [https://archive.ics.uci.edu/ml/datasets/adult](https://archive.ics.uci.edu/ml/datasets/adult)
* Kohavi, R. (1996). *Scaling Up the Accuracy of Naive-Bayes Classifiers: A Decision-Tree Hybrid*. Proceedings of KDD-96.

---

Souhaites-tu que je génère à partir de ces données une **analyse statistique complète** (avec graphiques et résumé Markdown) ?
