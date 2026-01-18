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

## Results

### Metrics
![metrics.png](images%2Fmetrics.png)

### Confusion Matrix
![conf_matrix.png](images%2Fconfusion_matrix.png)

### With Class Weights
![with-class-weights.png](images%2Fwith_class_weights.png)

### With SMOTE
![with-smote.png](images%2Fwith_smote.png)

### Without Imbalance
![without-imbalance.png](images%2Fwithout_imbalance.png)

### .gitignore
![gitignore.png](images%2Fgitignore.png)

## GitHub Actions Run
![github-actions.png](images%2Fgithub-actions.png)

## CML Reports https://github.com/devsahamerlin/mlops-churn-cml-dvc-cicd/commit/4b1904dde888d0b9ead3462d32ec6cd626f6a54a#commitcomment-174990771
![cml-report.png](images%2Fcml-report.png)

## GitHub collaborations (PR)

### Open Pull Request
![pull-request-open.png](images%2Fpull-request-open.png)

### Pull Request List
![pull-request.png](images%2Fpull-request.png)

### GitHub Actions (Merged PL)
![github-actions-merged-pr.png](images%2Fgithub-actions-merged-pr.png)

### CML E-mail Notifications
![email-notifications.png](images%2Femail-notifications.png)

## CML API rate limit exceeded (5th Run)

### API rate limit exceeded
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
![git-graph.png](images%2Fgit-graph.png)