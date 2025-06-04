# Projeto-Machine-Learning-Quantico
This project uses a Variational Quantum Classifier (VQC) with PennyLane to predict low birth weight. It pre-processes health data, balances classes, and trains a 3-qubit, 6-layer quantum circuit. The VQC classifies newborns based on features, with performance monitored via cost, accuracy, precision, recall, and F1-score.

Project Overview
The main goal of this project is to classify newborns into two categories: "low birth weight" (below 2500 grams) and "normal birth weight" (2500 grams or above). This is achieved by training a Variational Quantum Classifier on a dataset containing various maternal and neonatal health indicators.

Dataset
The dataset used in this project is sourced from amostra_sinasc.csv (not included in the repository, but expected to be in /content/drive/MyDrive/). It includes features such as:

IDADEMAE: Mother's age
QTDFILVIVO: Number of living children
QTDFILMORT: Number of deceased children
SEMAGESTAC: Gestational weeks
APGAR5: Apgar score at 5 minutes
APGAR1: Apgar score at 1 minute
CONSULTAS: Number of prenatal consultations
SEXO: Newborn's sex
PARTO: Type of delivery
STTRABPART: Labor status
GRAVIDEZ: Type of pregnancy (single, twin, etc.)
PESO: Birth weight (target variable for initial classification)
ESCMAE: Mother's schooling
KOTELCHUCK: Kotelchuck prenatal care index
MESPRENAT: Month prenatal care began
IDANOMAL: Presence of anomalies
TPAPRESENT: Type of presentation
Data Preprocessing and Cleaning
The projetooficialquantica (8).py script performs extensive data cleaning and preprocessing steps, including:

Loading Data: Loads selected columns from the CSV file to optimize memory usage.
Outlier Removal: Identifies and removes outliers, specifically cases where birth weight is less than 500g for full-term pregnancies.
Handling Missing Values:
IDADEMAE, QTDFILVIVO, QTDFILMORT: Missing values are filled with the mode.
PARTO, CONSULTAS, STTRABPART, ESCMAE, TPAPRESENT, GRAVIDEZ, MESPRENAT, IDANOMAL: Specific handling for ignored values (e.g., 9, 99) and NaNs, often replacing them with the mode or a sensible default.
APGAR1, APGAR5, SEMAGESTAC: Missing values are filled with the mode.
PESO: Rows with missing birth weight are dropped, as PESO is the target variable.
Feature Engineering: A new target column ALVO_BAIXO_PESO is created, where 1 indicates low birth weight (< 2500g) and -1 indicates normal birth weight (>= 2500g).
Data Balancing: A balanced subset of the data (500 samples per class) is created for training the quantum classifier.
Data Splitting: The balanced dataset is split into training and validation sets (70% train, 30% validation) with stratification to maintain class distribution.
Feature Scaling: StandardScaler is applied to the selected features to normalize the input data for the quantum circuit.
Variational Quantum Classifier (VQC)
The core of this project is the VQC, implemented using PennyLane.

Quantum Circuit Architecture
Qubits: The circuit uses 3 qubits (qtd_qubits = 3).
Layers: It consists of 6 layers (qtd_layers = 6).
Embedding: qml.AmplitudeEmbedding is used to encode the classical features into the quantum state.
Variational Layers: Each layer consists of qml.Rot gates on individual qubits followed by CNOT gates for entanglement, including a cyclic CNOT to ensure all qubits are entangled. The StronglyEntanglingLayers template was considered but a custom layer function was used.
Measurement: The expectation value of qml.PauliZ on the last qubit is measured to obtain the classification output.
Training
Optimizer: Nesterov Momentum Optimizer (NesterovMomentumOptimizer) with a learning rate of 0.05 is used for training.
Cost Function: Square loss (square_loss) is employed to quantify the difference between predicted and true labels.
Accuracy Metrics: The accuracy function calculates the classification accuracy. Precision, Recall, and F1-Score are also calculated for the validation set.
Batch Training: The model is trained using mini-batches of size 32 over 200 iterations.
Prediction: The raw predictions from the quantum circuit are converted to signed labels (-1 or 1) using np.sign.
How to Run (Local or Google Colab)
Environment Setup:
Install PennyLane: pip install pennylane
Ensure numpy, pandas, scikit-learn, and matplotlib are installed.
Google Drive Access: If running in Google Colab, enable Google Drive access by running the provided google.colab.drive.mount command.
Dataset: Make sure the amostra_sinasc.csv file is accessible at /content/drive/MyDrive/amostra_sinasc.csv.
Execute the Script: Run the projetooficialquantica (8).py script. The training progress, including cost, training accuracy, validation accuracy, precision, recall, and F1-score, will be printed iteratively.
Results
The training output provides insights into the model's performance during iterations, showing the cost function value, training accuracy, validation accuracy, precision, recall, and F1-score on the validation set. This helps in monitoring convergence and assessing the classifier's ability to generalize.
