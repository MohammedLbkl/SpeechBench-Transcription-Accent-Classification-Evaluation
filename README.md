# Classification des accents & Évaluation de transcription audio

Ce projet a pour objectif d’évaluer plusieurs modèles de transcription automatique de la parole, puis de classifier des accents.

## Objectifs

- **Tâche 1** : Évaluation des modèles de transcription audio à l’aide du **Word Error Rate (WER)** et mesure des temps de transcription
- **Tâche 2** : Classification automatique des accents à partir des fichiers audio et des transcriptions
- **Données(Transcription)** : Corpus Common Voice (Mozilla), LibriSpeech et L2-ARCTIC — Enregistrements audio, transcription.
- **Données(classification d'accents)** : Corpus Common Voice (Mozilla) — Enregistrements audio, accents, transcription, durées, etc.

# Installation

Cloner le dépôt :  
```bash
git clone https://github.com/MohammedLbkl/SpeechBench-Transcription-Accent-Classification-Evaluation
cd accent-classification-asr
```
### Installer les dépendances

```bash
pip install -r requirements.txt
```

# Description des données

Les données proviennent du corpus Common Voice de Mozilla, LibriSpeech et L2-ARCTIC disponible ici :  
[https://commonvoice.mozilla.org/fr/datasets](https://commonvoice.mozilla.org/fr/datasets).  
[https://www.openslr.org/12](https://www.openslr.org/12).  
[https://psi.engr.tamu.edu/l2-arctic-corpus/](https://psi.engr.tamu.edu/l2-arctic-corpus/).    


Les fichiers audio ont été convertis en `.wav` pour une meilleure qualité sonore, car ce format est non compressé et mieux adapté aux traitements acoustiques et à l’extraction de caractéristiques.

# Évaluation des modèles de transcription

Les modèles testés sont :  
- Whisper : tiny, base, small, medium, turbo, large  
- Wav2Vec2 (base)
- Vosk  

La métrique principale utilisée est le **Word Error Rate (WER)**

La durée moyenne de transcription a également été calculée pour chaque modèle afin d’évaluer la rapidité.

## Résultats moyens obtenus

|    Data      | Modèle           | WER moyen (%) | Durée moyenne (secondes) |
| -------------|------------------|--------------:|-------------------------:|
|              | Vosk             |         50.66 |                     1.40 |
| Common Voice | Whisper (tiny)   |         49.04 |                     1.32 |
|              | Wav2Vec2 (base)  |         49.61 |                     0.54 |
| -------------|------------------|--------------:|-------------------------:|
|              | Vosk             |         40.89 |                     1.57 |
| LibriSpeech  | Whisper (tiny)   |         8.86  |                     1.34 |
|              | Wav2Vec2 (base)  |         2.50  |                     0.82 |
| -------------|------------------|--------------:|-------------------------:|
|              | Vosk             |         44.61 |                     1.12 |
|  L2-ARCTIC   | Whisper (tiny)   |         31.18 |                     0.85 |
|              | Wav2Vec2 (base)  |         27.22 |                     0.32 |


# Classification des accents

## Modèles testés

- Régression Logistique  
- Forêt Aléatoire   
- Wav2Vec2 (fine-tune)

## Résultats et comparaison

Le modèle Wav2Vec2 s’est révélé être le plus performant globalement pour la classification des accents, avec un bon compromis entre précision, rappel et F1-score.

|           Modèle           |     Type     | Précision  | Recall | F1-score |
|----------------------------|--------------|-----------:|-------:|---------:|
|                            | Accuracy     |      -     |    -   |     0.87 |
|    Régression Logistique   | Macro avg    |       0.62 |   0.72 |     0.65 |
|                            | Weighted avg |       0.90 |   0.87 |     0.88 |
|----------------------------|--------------|-----------:|-------:|---------:|
|                            | Accuracy     |      -     |    -   |     0.89 |
|      Forêt Aléatoire       | Macro avg    |       0.58 |   0.50 |     0.52 |
|                            | Weighted avg |       0.88 |   0.89 |     0.87 |
|----------------------------|--------------|-----------:|-------:|---------:|
|                            | Accuracy     |      -     |    -   |     0.93 |
| W2V2 (CNN + Transformeurs) | Macro avg    |       0.73 |   0.71 |     0.70 |
|                            | Weighted avg |       0.94 |   0.93 |     0.94 |

