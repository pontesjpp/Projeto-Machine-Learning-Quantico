# Projeto-Machine-Learning-Quantico
This project uses a Variational Quantum Classifier (VQC) with PennyLane to predict low birth weight. It pre-processes health data, balances classes, and trains a 3-qubit, 6-layer quantum circuit. The VQC classifies newborns based on features, with performance monitored via cost, accuracy, precision, recall, and F1-score.

Quantum Low Birth Weight Classifier
This project implements a Variational Quantum Classifier (VQC) using PennyLane to predict low birth weight. It pre-processes health data, balances classes, and trains a 3-qubit, 6-layer quantum circuit. The VQC classifies newborns based on features, with performance monitored via cost, accuracy, precision, recall, and F1-score.

Features
Data Preprocessing: Comprehensive cleaning and handling of missing values for various maternal and neonatal health indicators.

Feature Engineering: Creation of a binary target variable for low birth weight classification.

Data Balancing: Stratified sampling to ensure balanced classes for robust model training.

Quantum Circuit: Implementation of a 3-qubit, 6-layer Variational Quantum Classifier.

Training Loop: Iterative training with Nesterov Momentum Optimizer and square loss function.

Performance Metrics: Real-time monitoring of training and validation accuracy, precision, recall, and F1-score.

Technologies Used
Python 3.x

PennyLane: For quantum machine learning.

NumPy: For numerical operations (specifically PennyLane's NumPy for autograd).

Pandas: For data manipulation and analysis.

Scikit-learn: For classical machine learning utilities (data splitting, scaling).

Matplotlib: For data visualization.

Setup and Installation
Clone the repository:

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

Install dependencies:

pip install pennylane numpy pandas scikit-learn matplotlib

Note: If you are running this in Google Colab, !pip install pennylane might be needed.

Usage
Dataset: Ensure you have the amostra_sinasc.csv file in your Google Drive (if using Colab) or in the same directory as the script if running locally. The script expects it at /content/drive/MyDrive/amostra_sinasc.csv.

Run the script:

python projetooficialquantica (8).py

The script will output the training progress, including cost and various accuracy metrics, for each iteration.

Data
The project uses a subset of a birth records dataset (expected from amostra_sinasc.csv). Key features include mother's age, gestational weeks, Apgar scores, prenatal consultations, and more. The target variable is derived from birth weight, classifying newborns as "low birth weight" or "normal birth weight".

Results
The training process logs show the convergence of the cost function and the evolution of accuracy, precision, recall, and F1-score on both training and validation sets, providing insights into the model's performance and generalization capabilities.

Contributing
Contributions are welcome! Please feel free to open issues or submit pull requests.

License
This project is licensed under the MIT License - see the LICENSE file for details.
