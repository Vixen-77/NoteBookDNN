# EXPLICATION DU NOTE BOOK DE TRAINING

# NOTE : le resulatat des courbe de chaque model seront mit dans le projet dans le docier "performance"

**Ce notebook présente le processus de traitement des données, l'entraînement de modèles de classification, et la conversion d'un modèle TensorFlow en format ONNX pour faciliter son utilisation avec d'autres frameworks. Il est divisé en plusieurs étapes principales, que voici :**



# 1. Installation des Dépendances
Le notebook commence par l'installation des bibliothèques nécessaires, y compris tf2onnx via !pip install tf2onnx, qui permet de convertir des modèles TensorFlow en format ONNX pour une meilleure interopérabilité.

# 2. Chargement et Exploration des Données
Les données sont chargées depuis Google Drive en utilisant pandas. Trois fichiers CSV contenant des données normalisées sont utilisés :

train_normalized.csv : Ensemble d'entraînement.

val_normalized.csv : Ensemble de validation.

test_normalized.csv : Ensemble de test (utilisé pour des tests après l'entraînement).

Chaque jeu de données est inspecté pour vérifier sa structure et sa description à l'aide des méthodes info(), describe() et head(), ce qui permet de s'assurer que les données sont correctement chargées et qu'elles présentent les caractéristiques attendues.

# 3. Préparation des Données
Une fois les données chargées, elles sont séparées en features (X) et cibles (y). Les ensembles X_train, y_train, X_val, y_val sont préparés à partir des données d'entraînement et de validation, prêts à être utilisés pour l'entraînement du modèle.

# 4. Entraînement des Modèles
Le notebook utilise le même code d'entraînement pour plusieurs modèles. Chaque modèle est défini à l'aide de l'API Keras de TensorFlow, avec des couches Dense et Dropout pour éviter le surapprentissage. Le modèle est compilé avec l'optimiseur Adam et la fonction de perte binary_crossentropy, adaptée pour une classification binaire.

Le modèle est ensuite entraîné sur les données d'entraînement avec validation sur l'ensemble de validation. Un callback ModelCheckpoint est utilisé pour enregistrer le meilleur modèle pendant l'entraînement, basé sur la meilleure performance de validation (val_accuracy).

# 5. Affichage des Courbes d'Apprentissage
Après l'entraînement, des courbes d'apprentissage sont tracées pour chaque modèle, montrant l'évolution de :

Accuracy en fonction des époques pour l'entraînement et la validation.

Loss en fonction des époques pour l'entraînement et la validation.

Ces courbes permettent de visualiser la performance du modèle au fil des époques et d'analyser s'il y a un surapprentissage ou sous-apprentissage.

# 6. Conversion en ONNX
Une fois le modèle entraîné et validé, il est converti au format ONNX à l'aide de la bibliothèque tf2onnx. Cette conversion est effectuée afin de rendre le modèle compatible avec d'autres frameworks comme ONNX Runtime, PyTorch, ou Caffe2, facilitant ainsi son déploiement dans divers environnements.

Le modèle converti est ensuite sauvegardé et prêt à être utilisé dans des applications extérieures.
