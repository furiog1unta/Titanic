# Titanic Survival Prediction

Учебный проект по соревнованию [Kaggle Titanic](https://www.kaggle.com/c/titanic): по данным пассажира предсказать, выжил он или нет (`Survived`: 0 / 1).

## Структура

```
Titanic/
├── data/
│   ├── raw/                  # исходные данные Kaggle
│   │   ├── train.csv
│   │   ├── test.csv
│   │   └── gender_submission.csv
│   └── processed/            # данные после 02_data_processing
│       ├── train.csv
│       └── test.csv
├── nootebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_data_processing.ipynb
│   ├── 03_model_selection.ipynb
│   └── 04_final_submission.ipynb
├── submissions/              # готовые сабмиты для Kaggle
│   ├── submissionlgbm.csv
│   └── NNsubmission.csv
├── NN.ipynb
├── requirements.txt
└── README.md
```

## Ноутбуки

- **`01_EDA`** — пропуски в данных, выживаемость в зависимости от пола, класса и возраста.
- **`02_data_processing`** — заполнение пропусков, кодирование `Sex`, one-hot для `Embarked`, новые признаки `FamilySize` и `IsAlone`, масштабирование `Age` и `Fare`. Результат сохраняется в `data/processed/`.
- **`03_model_selection`** — сравнение 7 моделей (LogReg, KNN, DecisionTree, RandomForest, XGBoost RF, CatBoost, LightGBM) на 5-fold CV, сначала с параметрами по умолчанию, потом с `RandomizedSearchCV`.
- **`04_final_submission`** — подбор параметров LightGBM, CatBoost и RandomForest через Optuna, обучение лучшей модели (LightGBM) и запись `submissions/submissionlgbm.csv`.
- **`NN.ipynb`** — простой MLP на PyTorch (1 скрытый слой + Dropout), сохранение весов с лучшим val loss в `best_model.pt` и запись `submissions/NNsubmission.csv`.

Итоговые признаки: `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `FamilySize`, `IsAlone`, `Embarked_Q`, `Embarked_S`.

## Запуск

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Ноутбуки запускаются по порядку: `01` → `02` → `03` → `04`. `NN.ipynb` использует данные из `data/processed/`, поэтому запускается после `02`.

## Результаты

CV — accuracy на 5-fold кросс-валидации, LB — скор на Kaggle.

| Модель       | CV     | LB      |
|--------------|--------|---------|
| LightGBM     | 0.8507 | 0.77033 |
| CatBoost     | 0.8496 | —       |
| RandomForest | 0.8451 | —       |
| MLP (PyTorch)| —      | 0.76794 |
