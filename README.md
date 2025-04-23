# 🔬 Human Vital Signs Analysis with DNN (Deep Neural Network)

Ce projet vise à analyser les signes vitaux humains pour prédire le **risque médical (faible ou élevé)** à l'aide d'un **réseau de neurones artificiel** entraîné sur un jeu de données biométriques basé sur une classification bianire

## 📁 Contenu du projet

Ce dépôt contient :
- Le notebook Jupyter développé sous **Google Colab** puis migré dans **VS Code**
les fichier normaliser et dataset sont dans google drive


## 🧠 Objectif

Créer un modèle de Deep Learning (DNN) pour prédire la variable `Risk_Category` (Low Risk ou High Risk) à partir de 14 données biométriques 
Colonne | Description
0. Heart_Rate | Fréquence cardiaque : nombre de battements de cœur par minute. Normal : entre 60 et 100 bpm chez l'adulte.
1. Respiratory_Rate | Fréquence respiratoire : nombre de respirations par minute. Normal : 12–20 pour un adulte.
2. Body Temperature | Température corporelle en °C. Normal : environ 36.5–37.5°C. Trop basse = hypothermie, trop haute = fièvre.
3. Oxygen_Saturation | Saturation en oxygène du sang (SpO₂) en %. Normal > 95%. En dessous = possible problème respiratoire.
4. Systolic_Blood_Pressure | Tension artérielle systolique (le chiffre du haut). Pression lorsque le cœur se contracte. Normal ~120 mmHg.
5. Diastolic_Blood_Pressure | Tension diastolique (le chiffre du bas). Pression quand le cœur est au repos. Normal ~80 mmHg.
6. Age | Âge de la personne. Peut influencer tous les autres paramètres (ex : un senior aura des risques différents).
7. Gender | Sexe de la personne (Male, Female, etc.). Peut jouer sur certains indicateurs médicaux.
8. Weight | Poids en kg. Important pour le calcul de l’IMC (Indice de Masse Corporelle).
9. Height | Taille en mètres. Utilisée avec le poids pour calculer l’IMC.
10. Derived_HRV | Variabilité de la fréquence cardiaque (HRV) : indicateur de stress, de fatigue ou de bon état de santé cardiovasculaire. Plus c’est élevé, mieux c’est (en général).
11. Derived_Pulse_Pressure | Pression pulsée = Systolique - Diastolique. Un indicateur de rigidité artérielle ou de problème cardiaque potentiel.
12. Derived_BMI | Indice de masse corporelle : poids / (taille²). Permet de savoir si la personne est en sous-poids, normal, en surpoids ou obèse.
13. Derived_MAP | Pression artérielle moyenne (MAP) : reflète la perfusion sanguine des organes. Calcul : (2*diastolique + systolique) /3
14. Risk_Category | Catégorie de risque : High ou Low. Étiquette finale pour la classification binaire (1 = High Risk, 0 = Low Risk).

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

- Données de test : `test_normalized.csv`
-taille de données de test : 10% (exactement  20002)

- Données de Validation : `val_normalized.csv`
-taille de données de validation : 10%   --> les valeurs ici seront utilisé pour les test de API au moment du sign up on prend les valeur du poid , taille , age et gender dici (exactement 20002)

  ## EN somme : 160016 +20002 +20002 = 200020 

  ## NOTE IMPORTANTE:
  noublié pas d'activer le GPU sur google collab 


  # RESULTAT: evalusation des performance dans les phase d'entrainement
  **en entrainement**
  **en test**

# CODE TRES PRESIEUX

import tensorflow as tf
import tf2onnx
from google.colab import drive

# Monter Google Drive
drive.mount('/content/drive')

# Charger le modèle Keras Sequential
seq_model = tf.keras.models.load_model('/content/drive/MyDrive/my_model.keras')

# Créer un modèle fonctionnel pour éviter l'erreur .output_names
inputs = tf.keras.Input(shape=(14,), name="input")  # adapte selon ton dataset
outputs = seq_model(inputs)
model = tf.keras.Model(inputs=inputs, outputs=outputs)

# Conversion vers ONNX
spec = (tf.TensorSpec([None, 14], tf.float32, name="input"),)

onnx_model, _ = tf2onnx.convert.from_keras(
    model,
    input_signature=spec,
    opset=13
)

# Sauvegarde
with open("/content/drive/MyDrive/mon_model.onnx", "wb") as f:
    f.write(onnx_model.SerializeToString())

print("✅ Modèle converti avec succès en ONNX !")

