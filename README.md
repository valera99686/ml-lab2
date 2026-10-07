# Лабораторна робота №2 — Baseline Classification Pipeline

Машинне навчання, КПІ ім. Ігоря Сікорського, ННІ прикладного системного аналізу, кафедра системного проектування.
Повзун Валерій, група КН-43.

**Ноутбук:** [`Lab2_BaselineClassification.ipynb`](Lab2_BaselineClassification.ipynb) — усі виводи та графіки вже збережені у файлі, тож його можна просто переглянути.

## Завдання

Відтворити базовий життєвий цикл класифікації на даних змагання Kaggle [Home Credit Default Risk](https://www.kaggle.com/c/home-credit-default-risk/data) (таблиці `application_train.csv` та `application_test.csv`): підготувати дані, розділити їх на навчальну й валідаційну вибірки, навчити `DecisionTreeClassifier` із параметрами за замовчуванням, оцінити за ROC-AUC, побудувати матрицю помилок, провести аналіз помилок і сформувати submission-файл.

## Результати

Accuracy, Recall, Precision та матриця помилок рахувалися на валідаційній вибірці (20 % навчальних даних); оцінки Kaggle — на прихованих відповідях для `application_test.csv`.

| Метрика | Значення |
|---|---|
| ROC-AUC (навчальна вибірка) | 1.0000 |
| ROC-AUC (валідаційна вибірка) | **0.5382** |
| Kaggle Late Submission, Public score | 0.52714 |
| Kaggle Late Submission, Private score | 0.53287 |
| Accuracy | 0.8539 (проста відповідь «завжди 0» дала б 0.9193) |
| Recall (знайдено дефолтів) | 0.1617 |
| Precision | 0.1428 |

Матриця помилок: TN = 51716, FP = 4822, FN = 4162, TP = 803.

Дерево без обмеження глибини сильно перенавчилось (AUC 1.0000 на навчальних даних проти 0.5382 на валідаційних), а дисбаланс класів (8.07 % дефолтів) ще й робить accuracy оманливою метрикою. Докладний аналіз причин і висновки — в ноутбуці.

## Структура ноутбука

1. Завантаження даних
2. Відокремлення цільової змінної від ознак
3. Розділення на навчальну та валідаційну вибірки
4. Базова обробка даних
5. Навчання дерева рішень
6. Оцінка якості: ROC-AUC
7. Матриця помилок
8. Аналіз помилок
9. Прогноз для тестових даних та submission-файл
10. Результат на Kaggle (Late Submission)

## Дані

Дані до репозиторію не додано: правила змагання забороняють передавати їх поза командою. Щоб запустити ноутбук, завантажте `application_train.csv`, `application_test.csv` та `sample_submission.csv` зі [сторінки змагання](https://www.kaggle.com/c/home-credit-default-risk/data) (потрібен акаунт Kaggle й прийняті правила) і покладіть їх поруч із ноутбуком або в папку `data/`.

## Запуск

```bash
pip install numpy pandas scikit-learn matplotlib jupyter
jupyter notebook Lab2_BaselineClassification.ipynb
```

Ноутбук шукає файли в `data/`, поруч із собою, у `/content` (Google Colab) та в `/kaggle/input/home-credit-default-risk` (Kaggle). Виконано на Python 3.12.7, NumPy 2.5.3, pandas 3.0.6, scikit-learn 1.9.1, Matplotlib 3.11.2.
