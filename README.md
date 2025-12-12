# Sigma-Fold
Предсказание вторичной структуры белка по аминокислотной последовательности (задача последовательной разметки, аналог NER в NLP).

Создатели: Иктисанов А. В., Галигузов Д. А., Хохлов А. А.

## Описание проекта

Sigma-Fold — учебно-исследовательский проект по биоинформатике, в котором задача предсказания вторичной структуры белков (H/E/C) решается как поэлементная классификация аминокислот в последовательности. Проект содержит:
- Бейзлайны на классических методах (scikit-learn) для быстрой оценки сложности задачи.
- Полный конвейер подготовки данных (кодирование, padding, маски, стратифицированный split).
- Модели глубокого обучения (реализуется трансформер, опционально ESM-эмбеддинги).
- Единые метрики и визуализации (Q3, per-class F1, confusion matrix).

## Постановка задачи

Для каждой аминокислоты последовательности необходимо предсказать одну из трёх меток вторичной структуры:
- H — Helix (α-спираль)
- E — Sheet (β-слой)
- C — Coil (петля/контур)

Выход модели — строка меток той же длины, что и входная последовательность.

## Датасет

- [Kaggle: Protein Secondary Structure Dataset](https://www.kaggle.com/datasets/kirkdco/protein-secondary-structure-2022)

Формат:
- Вход: строка из 20 стандартных аминокислот (A, C, D, E, F, G, H, I, K, L, M, N, P, Q, R, S, T, V, W, Y)
- Выход: строка меток H/E/C той же длины

## Архитектура и подход

- Baselines:
  - LinearSVC, Logistic Regression, RandomForest (scikit-learn)
- Глубокое обучение:
  - Трансформер (последовательная классификация, токен-уровень)
  - Опционально: предобученные эмбеддинги (ESM) как входные представления

## Метрики

- Q3 (3-state accuracy) — доля правильно предсказанных меток по валидным позициям (mask==1)
- Precision/Recall/F1 по каждому классу (H/E/C)
- Confusion matrix — структура ошибок между классами

## Структура проекта

```
project-root/
├─ data/
│  ├─ raw/                    # исходные данные
│  └─ processed/              # подготовленные массивы и словари
│     ├─ X_train.npy, y_train.npy, X_val.npy, y_val.npy, X_test.npy, y_test.npy
│     ├─ mask_train.npy, mask_val.npy, mask_test.npy
│     ├─ class_weights.npy
│     └─ vocabularies.pkl     # aa_to_int, int_to_aa, ss_to_int, int_to_ss, max_length
│
├─ notebooks/
│  ├─ 01_data_exploration.ipynb     # EDA: распределения длин, баланс классов
│  ├─ 02_preprocessing.ipynb        # кодирование, padding, split, сохранение
│  ├─ 03_baseline_models.ipynb      # sklearn бейзлайны и метрики
│  └─ 04_transformer.ipynb          # трансформер / ESM + классификатор
│
├─ results/
│  ├─ figures/                       # графики (PNG/SVG)
│  ├─ metrics/                       # метрики (CSV/JSON)
│  └─ reports/                       # краткие отчёты/выводы
│
├─ requirements.txt
├─ .gitignore
└─ README.md
```
