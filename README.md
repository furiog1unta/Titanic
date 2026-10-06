# Titanic Survival Prediction

Учебный проект по соревнованию [Kaggle Titanic](https://www.kaggle.com/c/titanic): по признакам пассажира предсказать, выжил он или нет (`Survived`: 0 / 1).

Пайплайн: разведочный анализ → предобработка → сравнение моделей и подбор гиперпараметров → сабмит.

## Структура

```
Titanic/
├── EDA.ipynb                 # разведочный анализ сырых данных
├── data_processing.ipynb     # предобработка (train/test → processed)
├── model_selection.ipynb     # сравнение моделей и RandomizedSearchCV
├── final_submission.ipynb    # обучение финальной модели и сабмит
├── submission.csv            # предсказания для Kaggle
├── requirements.txt
├── data/
│   ├── raw/                  # исходные файлы соревнования
│   │   ├── train.csv
│   │   ├── test.csv
│   │   └── gender_submission.csv
│   └── processed/            # признаки после обработки
│       ├── train.csv
│       └── test.csv
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

## Результаты `final_submission.ipynb`

Финальный прогноз для Kaggle лежит в `submission.csv`: 418 пассажиров из `test.csv`.

| | Значение |
|---|---|
| Предсказано погибших (`0`) | 274 |
| Предсказано выживших (`1`) | 144 |
| Доля выживших в сабмите | 34.4% |

Формат файла — как требует соревнование: `PassengerId`, `Survived`.
