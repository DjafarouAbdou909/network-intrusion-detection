# 🛡️ Network Intrusion Detection Challenge

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![LightGBM](https://img.shields.io/badge/LightGBM-latest-green?logo=lightgbm)
![Sekcoder](https://img.shields.io/badge/Sekcoder-1st%20Place-gold)
![Macro F1](https://img.shields.io/badge/Macro%20F1-0.6486-brightgreen)

Compétition ML sur la détection d'intrusion réseau classification de flux réseau en 10 catégories (trafic normal ou famille d'attaque), organisée sur **[Sekcoder](https://sekcoder.com)**.

## 🏆 Résultats

| Metric | Score |
|---|---|
| **Macro F1** | **0.6486** |
| F1 Worms | 0.6545 |
| Weighted F1 | 0.8357 |
| Accuracy | 0.8275 |

**🥇 Classement : 1er** sur [sekcoder.com](https://sekcoder.com)

## Dataset

- **180 371** flux réseau · **42 features** · **10 classes**
- Source : Cyber Range Lab, Université de New South Wales (UNSW-NB15)
- Déséquilibre sévère : Label 0 (Normal) = 51% · Label 9 (Worms) = 0.07%

| Label | Classe | Exemples |
|---|---|---|
| 0 | Normal | 65 100 |
| 1 | Generic | 41 209 |
| 2 | Exploits | 31 167 |
| 3 | Fuzzers | 16 972 |
| 4 | DoS | 11 447 |
| 5 | Reconnaissance | 9 791 |
| 6 | Backdoor | 1 874 |
| 7 | Analysis | 1 631 |
| 8 | Shellcode | 1 058 |
| 9 | Worms | 122 |

## Approche

### Découverte clé
La suppression des doublons (`drop_duplicates`) réduisait massivement les classes minoritaires — la garder améliore le Macro F1 de +0.05.

### Pipeline

1. **Pas de suppression des doublons** — clé pour les classes minoritaires
2. **LabelEncoder** sur `proto`, `service`, `state` (fit sur train + val + test)
3. **Feature engineering riche** 30+ features :
   - Ratios bytes/paquets, TTL, fenêtres TCP
   - Features HTTP, FTP, connexions
   - Transformations logarithmiques
4. **Oversampling ciblé** — classes 6, 7, 8, 9 augmentées
5. **LightGBM** avec early stopping sur validation set
6. **Optimisation des seuils** par classe sur validation set
7. **Retrain sur train + val** pour la soumission finale

##  Stack technique

![scikit-learn](https://img.shields.io/badge/scikit--learn-latest-orange?logo=scikit-learn)
![LightGBM](https://img.shields.io/badge/LightGBM-latest-green)
![Pandas](https://img.shields.io/badge/Pandas-latest-blue?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-latest-blue?logo=numpy)
![Jupyter](https://img.shields.io/badge/Jupyter-latest-orange?logo=jupyter)


## 📁 Project Structure

```
network-intrusion-challenge/
├── data/
│   └── raw/
│       ├── train.csv
│       ├── validation.csv
│       └── test_public.csv
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_preparation.ipynb
│   ├── 03_eda.ipynb
│   ├── 04_modeling.ipynb
│   └── 05_final_model.ipynb
├── outputs/
│   └── submission.csv
└── requirements.txt
```

## Getting Started

```bash
git clone https://github.com/DjafarouAbdou909/network-intrusion-challenge.git
cd network-intrusion-challenge
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

## 👤 Author

**Djafarou Abdou** Computer Engineering Student, IUA Abidjan
[![GitHub](https://img.shields.io/badge/GitHub-DjafarouAbdou909-black?logo=github)](https://github.com/DjafarouAbdou909)