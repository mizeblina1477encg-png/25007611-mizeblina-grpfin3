# F1 – Risque de crédit en Allemagne

**Auteur :** Lina Mizeb · **Code Apogée :** 25007611 · **Groupe :** grpfin3
**Sujet :** F1, risque de crédit en Allemagne (examen individuel « Projet de science des données appliqué à la finance », S7 ENCG-2026).

**Résumé.** Ce projet construit un modèle de scoring (régression logistique) pour décider d'accorder ou non un crédit, sur 1 000 dossiers du jeu German Credit. Le seuil de décision est optimisé pour une matrice de coûts asymétrique : accorder un crédit à un mauvais payeur coûte 5 fois plus que refuser un bon client. Le modèle est comparé à des règles naïves.

## 1. Problématique et principaux résultats

**Problématique.** Un modèle de scoring avec un seuil de décision optimisé permet-il de réduire le coût moyen par dossier, par rapport à une règle naïve, quand accorder un crédit à un mauvais payeur coûte 5 fois plus que refuser un bon client ?

**Objectif mesurable (fixé avant le test).** Coût moyen = (5 × FN + 1 × FP) / n sur un test stratifié de 30 %, au moins 20 % en dessous de la meilleure règle naïve (soit ≤ 0,56).

| Méthode | Coût moyen (validation) | Coût moyen (test) |
|---|---|---|
| Tout accorder | 1,50 | 1,50 |
| Tout refuser (meilleure référence) | 0,70 | 0,70 |
| Régression logistique, seuil 0,17 | 0,53 | 0,62 |

- Le modèle réduit le coût de 11 % par rapport à la meilleure référence : **l'objectif de 20 % n'est pas atteint**.
- AUC : 0,79 en validation, 0,75 au test. Rappel des mauvais payeurs au test : 82 %.
- Incertitude : intervalle de confiance bootstrap à 95 % du coût de test [0,50 ; 0,75], qui contient 0,70. Avec seulement 90 mauvais payeurs au test, l'amélioration reste incertaine.

## 2. Données

- **Source :** German Credit Data, Kaggle (varunchawla30), https://www.kaggle.com/datasets/varunchawla30/german-credit-data, jeu issu de Statlog German Credit (UCI).
- **Licence :** aucune indiquée sur la page de téléchargement.
- **Date d'extraction :** 17/11/2026.
- **Contenu :** 1 000 observations, 21 variables, données en coupe, une ligne = un dossier de crédit.
- **Obtention :** le fichier `german_credit_data.csv` est dans `data/raw/`. Sinon, le télécharger depuis le lien ci-dessus.

## 3. Installation

Python 3.10 ou plus récent (testé avec 3.13).

```bash
pip install -r requirements.txt
```

## 4. Exécution

1. Vérifier que `data/raw/german_credit_data.csv` est présent.
2. Ouvrir `notebooks/projet_F1.ipynb` et lancer « Redémarrer et tout exécuter ».
3. Durée approximative : moins d'une minute.

Graine aléatoire fixée à 42 partout (découpage, validation croisée, bootstrap).

## 5. Structure du dépôt

```
├── README.md
├── requirements.txt
├── .gitignore
├── DECLARATION_IA.md
├── data/raw/            données brutes
├── docs/                fiche du sujet F1, références
├── notebooks/           notebook final exécuté (compte rendu)
├── figures/             graphiques utilisés
├── rapport/             rapport.pdf (export du notebook)
└── presentation/        presentation.pdf et presentation.pptx
```

## 6. Références

- Données : German Credit Data, Kaggle (varunchawla30) ; UCI Machine Learning Repository, Statlog (German Credit Data).
- Documentation scikit-learn : LogisticRegression, Pipeline, ColumnTransformer, GridSearchCV.
- Support de cours : Tp_ML.ipynb.
- Déclaration d'usage des outils d'IA : voir [DECLARATION_IA.md](DECLARATION_IA.md).
