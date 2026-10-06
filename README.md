# Titanic Survival Prediction

Учебный проект по соревнованию [Kaggle Titanic](https://www.kaggle.com/c/titanic): по признакам пассажира предсказать, выжил он или нет (`Survived`: 0 / 1).

## Структура

```
Titanic/
├── data/
│ ├── processed/
│ │ ├── test.csv
│ │ └── train.csv
│ └── raw/
│ ├── gender_submission.csv
│ ├── test.csv
│ └── train.csv
├── notebooks/
│ ├── 01_EDA.ipynb
│ ├── 02_data_processing.ipynb
│ ├── 03_model_selection.ipynb
│ └── 04_final_submission.ipynb
├── .gitignore
├── README.md
├── requirements.txt
└── submission.csv
```

**`EDA.ipynb`** — словарь признаков, пропуски, связь выживаемости с полом, классом и возрастом.

**`data_processing.ipynb`** — подготовка признаков. В processed-данных: `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `FamilySize`, `IsAlone`, `Embarked_Q`, `Embarked_S` (Age/Fare масштабированы, Sex закодирован, Embarked — dummy).

**`model_selection.ipynb`** — сравнение моделей и подбор гиперпараметров.

**`final_submission.ipynb`** — обучение финальной модели и запись `submission.csv` (результаты ниже).

## Установка

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Ноутбуки запускаются по порядку: `EDA` → `data_processing` → `model_selection` → `final_submission`.

## Результаты

Финальный прогноз для Kaggle лежит в `submission.csv`: 418 пассажиров из `test.csv`.

| Name         | CV       | LB      |
|--------------|----------|---------|
| LightGBM     | 0.850712 | 0.77033 |
| CatBoost     | 0.849595 | NaN     |
| RandomForest | 0.845107 | NaN     |
