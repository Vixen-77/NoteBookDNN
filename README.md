# 🔬 Human Vital Signs Analysis with DNN (Deep Neural Network)

Ce projet vise à analyser les signes vitaux humains pour prédire le **risque médical (faible ou élevé)** à l'aide d'un **réseau de neurones artificiel** entraîné sur un jeu de données biométriques.

## 📁 Contenu du projet

Ce dépôt contient :
- Le notebook Jupyter développé sous **Google Colab** puis migré dans **VS Code**
- Les fichiers CSV pour l'entraînement, validation et test
- Les versions normalisées des datasets
- Un scaler sauvegardé (`.pkl`) pour réutilisation

## 🧠 Objectif

Créer un modèle de Deep Learning (DNN) pour prédire la variable `Risk_Category` (Low Risk ou High Risk) à partir de données biométriques telles que :
- Gender
- Heart rate
- Respiratory rate
- Temperature
- Oxygen saturation
- Blood pressure
- etc.

## 🛠️ Étapes réalisées

1. **Chargement et exploration** du dataset `human_vital_signs_dataset_2024.csv`
2. **Nettoyage** : suppression des colonnes inutiles (`Patient ID`, `Timestamp`)
3. **Encodage** : transformation de `Gender` en valeurs numériques (Male → 1, Female → 0)
4. **Mélange du dataset** pour éviter tout biais d’ordre
5. **Séparation** en 3 fichiers : `train.csv`, `val.csv`, `test.csv`
6. **Normalisation** des données avec `StandardScaler` (sklearn)
   - Enregistrement du scaler dans un fichier `.pkl`
   - Sauvegarde des fichiers normalisés : `train_normalized.csv`, `val_normalized.csv`, `test_normalized.csv`
7. **Construction du modèle DNN** avec TensorFlow/Keras :
    **nombre de couche cachées** : 5
    **nombre de noeurones par couche** :
       entré : 14 paramètre normalisé 
       couche1
       couche2
       couche3
       couche4
       couche5
       couche 6 (sortie soit 0 soit 1)
   - les couches 1-5 Dense avec `ReLU`
   - Couches `Dropout` pour éviter le surapprentissage
   - Dernière couche en `sigmoid` pour une sortie binaire

     

8. **Compilation** du modèle :
   - Optimiseur : Adam
   - Fonction de perte : Binary Crossentropy
   - Métrique : Accuracy

## 🧪 Entraînement et taille choisi
  
- Nombre d’épochs : `20`
- Batch size : `32`
- Données d'entraînement : `train_normalized.csv`
- taille de données d'entrainement : 80% ( exactement 160016 echontillons)

- Données de Validation : `test_normalized.csv`
-taille de données de test : 10% (exactement  20002)

- Données de Validation : `val_normalized.csv`
-taille de données de validation : 10%   --> les valeurs ici seront utilisé pour les test de API au moment du sign up on prend les valeur du poid , taille , age et gender dici (exactement 20002)

  ## EN somme : 160016 +20002 +20002 = 200020 