# Autonomous Navigation Classifier 🤖

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Status](https://img.shields.io/badge/Status-Complete-green)

A machine learning system designed to predict the navigation behavior of a SCITOS G5 mobile robot. By analyzing raw data from 24 ultrasound sensors, this model determines the optimal movement command (e.g., *Move-Forward*, *Sharp-Right-Turn*) to navigate complex environments autonomously.

## 🚀 Project Overview

The goal of this project is to build a robust classification pipeline that can act as the "brain" of a wall-following robot. The system processes noisy sensor data, handles physical outliers (like max-range readings), and selects the best algorithm to drive the robot safely.

**Key Features:**
* **Multi-Class Classification:** Predicts 4 distinct robot actions.
* **Robust Preprocessing:** Utilizes `RobustScaler` to handle sensor noise and "open space" outliers ($5.0m$) without data loss.
* **Automated Tuning:** Implements `GridSearchCV` to optimize hyperparameters for SVM, KNN, and Random Forest.
* **Real-Time Simulation:** Includes a manual input interface to test specific sensor scenarios.

## 📂 Dataset

The project uses the **Wall-Following Robot Navigation Data** (UCI Machine Learning Repository).
* **Input:** 24 continuous ultrasound sensor readings (sampled at 9Hz).
* **Output:** 4 Class Labels:
    * `Move-Forward`
    * `Sharp-Right-Turn`
    * `Slight-Right-Turn`
    * `Slight-Left-Turn`
* **Size:** 5,456 instances.

## 🛠️ Tech Stack

* **Language:** Python
* **Data Manipulation:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (SVM, KNN, Random Forest, Logistic Regression)
* **Visualization:** Matplotlib, Seaborn

## ⚙️ The Pipeline

1.  **Data Loading:** Parsed raw `.data` files using column definitions from `.names`.
2.  **Preprocessing:**
    * **Label Encoding:** Converted text labels to integers (0-3).
    * **Robust Scaling:** Applied `RobustScaler` to mitigate the impact of sensor "max range" readings ($5.0m$) and specular reflections.
    * **Train-Test Split:** Stratified split (80/20) to maintain class balance.
3.  **Model Selection:**
    * Trained 4 classifiers: Logistic Regression, KNN, SVC, and Random Forest.
    * Used `GridSearchCV` (5-fold cross-validation) to find the best hyperparameters (e.g., `C`, `n_neighbors`, `kernel`).
4.  **Evaluation:**
    * Selected the best model based on **Weighted F1-Score**.
    * Generated Confusion Matrices to analyze specific misclassification errors (e.g., confusing *Slight-Right* with *Sharp-Right*).

## 📊 Results

| Model | Accuracy | F1-Score (Weighted) |
| :--- | :--- | :--- |
| **Random Forest** | **99.xx%** | **0.99** |
| SVM (RBF Kernel) | 9x.xx% | 0.9x |
| KNN | 9x.xx% | 0.9x |
| Logistic Regression | 6x.xx% | 0.6x |

*Note: The Random Forest model demonstrated the highest resilience to sensor noise and is the recommended model for deployment.*

## 💻 How to Run

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/autonomous-nav-classifier.git](https://github.com/yourusername/autonomous-nav-classifier.git)
    cd autonomous-nav-classifier
    ```

2.  **Install dependencies:**
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```

3.  **Run the script:**
    ```bash
    python main.py
    ```

4.  **Test the Robot:**
    When prompted, paste a row of 24 sensor values to see the prediction:
    ```text
    # Example Input (Wall on left, open front):
    0.8 0.8 0.8 0.8 5.0 5.0 5.0 ... (24 values)
    ```

## 📈 Visualizations

* **Confusion Matrix:** Shows exactly where the robot gets confused.
* **Model Comparison:** Bar chart comparing the performance of all tested algorithms.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](issues/).

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
