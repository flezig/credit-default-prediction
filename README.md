# Credit Card Default Prediction (Credit Scoring)

Проект бинарной классификации: предсказать, допустит ли клиент дефолт по платежу по кредитной карте в следующем месяце

## Model Comparison

Датасет умеренно несбалансирован (~22% defaults), поэтому accuracy не является основной метрикой.
Я сравнил baseline и несколько моделей градиентного бустинга

### Test results

| Model | ROC-AUC (test) | PR-AUC (test) | F1 (test, tuned threshold) | Best threshold (val) |
|------|----------------:|--------------:|----------------------------:|---------------------:|
| Logistic Regression (baseline) | ~0.709 | ~0.492 | ~0.500 | ~0.55 |
| HistGradientBoosting (sklearn) | ~0.777 | ~0.551 | ~0.542 | ~0.25 |
| **CatBoost (final model)** | **0.7783** | **0.5564** | **0.5498** | **~0.256** |
| LightGBM | 0.7773 | 0.5433 | 0.5323 | 0.3925 |

### Key takeaways
- Baseline Logistic Regression показывает адекватное качество и служит точкой отсчёта
- Gradient Boosting модели существенно улучшают качество на табличной задаче кредитного скоринга
- Среди протестированных GBDT лучшей оказалась **CatBoost**, особенно по **PR-AUC** и **F1**, что важно при дисбалансе классов
- Подбор **threshold** на validation заметно влияет на F1, поэтому порог выбирался отдельно, а test использовался только для финальной оценки

### Как запустить:
1. Поместить датасет в `data/credit_default.csv` (или изменить`PATH` в notebook)
2. Установить зависимости:
   ```bash
   pip install -r requirements.txt
3. Запустить:

	notebooks/01_eda.ipynb

	notebooks/02_modeling.ipynb