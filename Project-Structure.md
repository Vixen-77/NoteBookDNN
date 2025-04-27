# STRCUTURE DU PROJET :

Ce projet implémente un pipeline complet de traitement de données, d'entraînement de modèles et d'évaluation pour un problème de classification. Il présente la structure des répertoires, les notebooks associés et les résultats produits (modèles, courbes d'apprentissage, matrices de confusion, courbes ROC).

Table des matières

Structure du projet

Jeux de données (Data)

Modèles (Models)

Performance et visualisations

Notebooks

Licence

Structure du projet

├── Data/   # Données brutes et normalisées
|-  Architecture                     
├── Models/                         # Modèles sauvegardés aux formats Keras et ONNX
│   ├── .keras/                     # Modèles au format .keras
│   │   ├── model1.keras
│   │   ├── model2.keras
│   │   └── model3.keras
│   └── .onnx/                      # Modèles convertis au format ONNX
│       ├── model1.onnx
│       ├── model2.onnx
│       └── model3.onnx
├── performance/                    # Courbes d'apprentissage (accuracy et loss)
├── Courbe ROC&MC-model-1/          # Courbe ROC et matrice de confusion pour le modèle 1
├── Courbe ROC&MC-model-2/          # Courbe ROC et matrice de confusion pour le modèle 2
├── Courbe ROC&MC-model-3/          # Courbe ROC et matrice de confusion pour le modèle 3
├── NoteBookDataCleaning.ipynb      # Notebook de nettoyage et préparation des données
├── Training3model.ipynb            # Notebook d'entraînement des 3 modèles et évaluation
├── Project-Structure.md            # Schéma de la structure du projet (en cours)
├── README.md                       # (Ce fichier)
└── LICENSE                         # Licence du projet

Jeux de données (Data)

Le dossier Data/ contient :

brute/ : données initiales non transformées.

train/, val/, test/ : partitions du dataset original (20020 échantillons au total) :

Train : 80% (16 016 échantillons)

Validation : 10% (2 002 échantillons)

Test : 10% (2 002 échantillons)

train_normalized/, val_normalized/, test_normalized/ : mêmes partitions après normalisation des features.

La répartition et la normalisation sont réalisées dans NoteBookDataCleaning.ipynb.

Modèles (Models)

Les modèles entraînés sont sauvegardés dans deux formats :

Keras (.keras) : poids et architecture originels.

ONNX (.onnx) : modèles exportés pour interopérabilité.

Chaque sous-dossier .keras/ et .onnx/ contient trois fichiers : model1, model2 et model3.

Performance et visualisations

Le dossier performance/ contient les courbes d'apprentissage :

accuracy_vs_epoch_modelX.png : précision d'entraînement & validation par epoch.

loss_vs_epoch_modelX.png : fonction de perte par epoch.

Les dossiers Courbe ROC&MC-model-*/ contiennent pour chaque modèle X :

roc_modelX.png : courbe ROC.

confusion_matrix_modelX.png : matrice de confusion.

Notebooks

NoteBookDataCleaning.ipynb

Nettoyage des données brutes.

Mélange aléatoire et split en jeux train/val/test.

Normalisation des features.

Training3model.ipynb

Définition et compilation de trois architectures de réseaux de neurones.

Entraînement sur le jeu d'entraînement.

Évaluation sur les jeux validation et test.

Sauvegarde des modèles et génération des courbes.