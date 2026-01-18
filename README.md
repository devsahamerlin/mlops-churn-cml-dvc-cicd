# CI/CD pour le Machine Learning GitHub Actions + CML

Repository GitHub: https://github.com/devsahamerlin/mlops-churn-cml-dvc-cicd 

Automatisation MLOps côté GitHub :

- exécuter l’entraînement du modèle à chaque git push sur la main et chaque PR sur la main et la dev,
- générer les métriques (metrics.txt) et la matrice de confusion,
- publier automatiquement un rapport lisible en commentaire sur GitHub grâce à CML.

## Vue d’ensemble

1. Vous avez un projet ML classique (dataset.csv, script.py).
2. Vous poussez ce projet sur GitHub.
3. GitHub Actions lance automatiquement l’entraînement (CI).
4. Les perfs du modèle (scores, F1-score, matrices de confusion) sont publiées en commentaire.
C’est utile pour un projet de data science en équipe :
- visibilité instantanée de la qualité du modèle,
- traçabilité des changements,
- boucle d’amélioration continue.

## Rôle de chaque fichier
- *dataset.csv*: données d’entraînement/test utilisées par le script.
- *script.py*:
  - lit dataset.csv, 
  - prépare les features (imputations, encodage, équilibrage), 
  - entraîne un modèle (ex. RandomForestClassifier), 
  - calcule des métriques (F1, précision, rappel, etc.), 
  - génère une figure conf_matrix.png, 
  - écrit un résumé clair dans metrics.txt. 
- *requirements.txt*: dépendances Python à installer dans la CI. 
- *.github/workflows/cml-churn.yaml*: pipeline GitHub Actions + CML.

## Local Environment Setup

```shell
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Local test
```shell
python3 script.py
```

## Results Local

### Metrics
*Aperçu des métriques de performance (Accuracy, F1-score, ROC-AUC) générées lors de l'exécution locale du script.*

![metrics.png](images%2Fmetrics.png)

### Confusion Matrix
*Matrice de confusion montrant la capacité du modèle à bien classer les clients (churn vs non-churn).*

![conf_matrix.png](images%2Fconfusion_matrix.png)

### With Class Weights
*Résultats obtenus en utilisant des poids de classe pour compenser le déséquilibre des données.*

![with-class-weights.png](images%2Fwith_class_weights.png)

### With SMOTE
*Résultats après application de SMOTE (Synthetic Minority Over-sampling Technique) pour générer des exemples synthétiques de la classe minoritaire.*

![with-smote.png](images%2Fwith_smote.png)

### Without Imbalance
*Comparaison avec un jeu de données où le déséquilibre de classe n'est pas traité (baseline).*

![without-imbalance.png](images%2Fwithout_imbalance.png)

### .gitignore
*Fichier configuré pour exclure les fichiers temporaires, l'environnement virtuel et les données sensibles du dépôt Git.*

![gitignore.png](images%2Fgitignore.png)

## GitHub Actions + CML Run
*Interface GitHub Actions montrant le succès de l'exécution du workflow CML.*

![github-actions.png](images%2Fgithub-actions.png)

## CML Reports https://github.com/devsahamerlin/mlops-churn-cml-dvc-cicd/commit/4b1904dde888d0b9ead3462d32ec6cd626f6a54a#commitcomment-174990771
*Rapport automatique publié par CML en commentaire du commit, incluant les métriques et la matrice de confusion.*

![cml-report.png](images%2Fcml-report.png)

## GitHub's collaborations (PR)

### Open Pull Request
*Création d'une Pull Request pour intégrer les changements de la branche de développement vers la branche principale.*

![pull-request-open.png](images%2Fpull-request-open.png)

### Pull Request List
*Vue d'ensemble des Pull Requests ouvertes dans le projet.*

![pull-request.png](images%2Fpull-request.png)

### GitHub Actions (Merged PL)
*Exécution automatique du pipeline CI/CD suite à la fusion (merge) d'une Pull Request.*

![github-actions-merged-pr.png](images%2Fgithub-actions-merged-pr.png)

### CML E-mail Notifications
*Notification par e-mail reçue indiquant le statut de l'exécution du workflow.*

![email-notifications.png](images%2Femail-notifications.png)

## CML API rate limit exceeded (5th Run)

### API rate limit exceeded
*Erreur rencontrée lorsque le nombre de requêtes à l'API GitHub dépasse la limite autorisée (souvent dû à trop d'exécutions rapprochées).*

![cml-API-rate-limit-exceeded.png](images%2Fcml-API-rate-limit-exceeded.png)

### Reduce Pipeline Run
- Reduce GitHub Actions Pipeline Run: Run only on PR to Main and PR to DEV 

```
on:
  push:
    branches: [ main]
  pull_request:
    branches: [ main, dev ]
```

### Git log
*Visualisation de l'historique Git montrant les branches, les commits et les fusions.*

![git-graph.png](images%2Fgit-graph.png)

## Résumé
Nous avons :
- automatisé l’entraînement du modèle à chaque push sur la main et chaque PR sur la main et la dev,
- généré automatiquement les métriques (metrics.txt),
- généré automatiquement la matrice de confusion (conf_matrix.png),
- publié un rapport lisible directement dans GitHub (CML).
C’est déjà une CI ML : mesure continue, feedback centralisé, traçabilité.

## Limites actuelles
- Données dans le repo (dataset.csv) : pas scalable, pas sécurisé.
- Modèle entraîné non archivé automatiquement sur stockage externe.
- Pas de versioning propre pour les artefacts lourds (.pkl, gros CSV, etc.).
- Runner sur un CPU et non GPU, bien pour les petits model et dataset

## Conclusion
Nous venons de construire une boucle *entraînement + reporting* entièrement automatisée via
GitHub Actions et CML : *Mesurer en continu*. Dans l’atelier suivant, on ajoute *stocker et
versionner en continu*.