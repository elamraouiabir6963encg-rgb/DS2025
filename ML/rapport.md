# Rapport d’Analyse Statistique et ACP

## 1. Aperçu des données

|                      |   count |        mean |         std |     min |        25% |       50% |      75% |       max |
|:---------------------|--------:|------------:|------------:|--------:|-----------:|----------:|---------:|----------:|
| fixed acidity        |    4898 |   6.85479   |  0.843868   | 3.8     |   6.3      |   6.8     |   7.3    |  14.2     |
| volatile acidity     |    4898 |   0.278241  |  0.100795   | 0.08    |   0.21     |   0.26    |   0.32   |   1.1     |
| citric acid          |    4898 |   0.334192  |  0.12102    | 0       |   0.27     |   0.32    |   0.39   |   1.66    |
| residual sugar       |    4898 |   6.39141   |  5.07206    | 0.6     |   1.7      |   5.2     |   9.9    |  65.8     |
| chlorides            |    4898 |   0.0457724 |  0.021848   | 0.009   |   0.036    |   0.043   |   0.05   |   0.346   |
| free sulfur dioxide  |    4898 |  35.3081    | 17.0071     | 2       |  23        |  34       |  46      | 289       |
| total sulfur dioxide |    4898 | 138.361     | 42.4981     | 9       | 108        | 134       | 167      | 440       |
| density              |    4898 |   0.994027  |  0.00299091 | 0.98711 |   0.991723 |   0.99374 |   0.9961 |   1.03898 |
| pH                   |    4898 |   3.18827   |  0.151001   | 2.72    |   3.09     |   3.18    |   3.28   |   3.82    |
| sulphates            |    4898 |   0.489847  |  0.114126   | 0.22    |   0.41     |   0.47    |   0.55   |   1.08    |
| alcohol              |    4898 |  10.5143    |  1.23062    | 8       |   9.5      |  10.4     |  11.4    |  14.2     |
| quality              |    4898 |   5.87791   |  0.885639   | 3       |   5        |   6       |   6      |   9       |

### Valeurs manquantes

|                      |   0 |
|:---------------------|----:|
| fixed acidity        |   0 |
| volatile acidity     |   0 |
| citric acid          |   0 |
| residual sugar       |   0 |
| chlorides            |   0 |
| free sulfur dioxide  |   0 |
| total sulfur dioxide |   0 |
| density              |   0 |
| pH                   |   0 |
| sulphates            |   0 |
| alcohol              |   0 |
| quality              |   0 |

## 2. Graphiques

### Heatmap de corrélation
![](heatmap.png)

### Histogrammes
![](histograms.png)

### Boxplots
![](boxplots.png)

### Scree Plot
![](scree.png)

### Variance Cumulée
![](cumvar.png)

### Projection PCA
![](pca_proj.png)

### Biplot
![](biplot.png)

## Shapiro Test p-values

|                      |           0 |
|:---------------------|------------:|
| fixed acidity        | 9.33353e-09 |
| volatile acidity     | 3.27423e-18 |
| citric acid          | 1.85424e-12 |
| residual sugar       | 9.6048e-25  |
| chlorides            | 1.26608e-30 |
| free sulfur dioxide  | 3.57466e-12 |
| total sulfur dioxide | 0.0184939   |
| density              | 3.1855e-25  |
| pH                   | 8.46353e-06 |
| sulphates            | 1.95239e-10 |
| alcohol              | 2.20025e-10 |
| quality              | 4.03294e-17 |

