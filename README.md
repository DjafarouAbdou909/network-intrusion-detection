# Network Intrusion Detection Challenge

Compétition ML sur la détection d'intrusion réseau — classification de flux réseau en 10 catégories (trafic normal ou famille d'attaque).

## Résultats

| Métrique | Score |
|----------|-------|
| Macro F1 | 0.5984 |
| F1 Worms | 0.6071 |
| F1 Pondéré | 0.8188 |
| Accuracy | 0.7927 |

**Classement : 1er** sur sekcoder.com/leaderboard

## Dataset

- 180 371 flux réseau, 42 features, 10 classes
- Source : Cyber Range Lab, Université de New South Wales
- Déséquilibre sévère : Label 0 (Normal) = 51%, Label 9 (Worms) = 0.07%

## Approche

- Suppression de 61 522 doublons
- Target Encoding sur proto (132 valeurs), service (13), state (9)
- Feature engineering : ratios bytes/paquets, totaux
- SMOTE ciblé sur les classes minoritaires (labels 6, 7, 8, 9)
- LightGBM avec class_weight="balanced"
- Entraînement sur 100% des données pour la soumission finale

## Structure

├── data/

│   └── raw/

│       ├── train.csv

│       ├── test_public.csv

│       └── validation.csv

├── notebooks/

│   ├── 01_data_understanding.ipynb

│   ├── 02_data_preparation.ipynb

│   ├── 03_eda.ipynb

│   └── 04_modeling.ipynb

├── outputs/

│   └── submission.csv

└── requirements.txt

## Installation

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```