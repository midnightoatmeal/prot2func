# Prot2Func: Enzyme Classification from Protein Sequences

This project develops a machine learning model to predict whether a given protein is an enzyme based solely on its amino acid sequence. The workflow involves fetching and labeling data from the UniProt database, engineering features based on amino acid composition, and training a neural network with PyTorch to perform the classification.

A key challenge in this project was handling a significant class imbalance, which was overcome using a weighted loss function to train a high-performing and balanced classifier.

***

## Features

-   **Automated Data Labeling**: Programmatically queries the UniProt REST API to label proteins as "Enzyme" or "Non-Enzyme".
-   **Feature Engineering**: Converts raw protein sequences into numerical features based on amino acid frequency.
-   **Machine Learning Models**: Implements and compares a Logistic Regression baseline with a PyTorch-based neural network.
-   **Handling Imbalance**: Successfully addresses class imbalance to build a useful and predictive model.
-   **Jupyter Notebook**: A clean, step-by-step notebook (`main_prot2func_model.ipynb`) documents the entire process from data loading to model evaluation.

***

##� Workflow Overview

1.  **Data Loading**: Protein sequence data is loaded from `protein_sequences.csv`.
2.  **API Labeling**: A subset of the data is labeled by querying UniProt to identify proteins with catalytic activity (EC numbers).
3.  **Feature Engineering**: The 20 standard amino acid frequencies are calculated for each sequence to serve as model features.
4.  **Model Training**: The data is split into training and testing sets. A PyTorch neural network is trained using a weighted cross-entropy loss to handle class imbalance.
5.  **Evaluation**: The trained model is evaluated on the unseen test set to measure its accuracy, precision, and recall.

***

## Installation & Setup

To run this project locally, please follow these steps.

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/midnightoatmeal/prot2func
    cd prot2func
    ```

2.  **Create and Activate a Virtual Environment**
    ```bash
    # Create the environment
    python3 -m venv venv

    # Activate it (macOS/Linux)
    source venv/bin/activate

    # Activate it (Windows)
    .\venv\Scripts\activate
    ```

3.  **Install Dependencies**
    Install all the required Python libraries from the `requirements.txt` file.
    ```bash
    pip install -r requirements.txt
    ```

***

## Usage

All the code and analysis are contained within the Jupyter Notebook:
`main_prot2func_model.ipynb`

Simply open the notebook in a Jupyter environment (like Jupyter Lab or VS Code) and run the cells sequentially from top to bottom.

***

## Results & Performance

The initial challenge was a significant class imbalance, where a naive model completely failed to identify the minority class (enzymes), resulting in a precision and recall of **0.00**.

After implementing a weighted loss function and other improvements, the final PyTorch neural network achieved excellent, well-balanced performance on the test set:

-   **Accuracy:** 87.25%
-   **Precision (for Enzymes):** 87.25%
-   **Recall (for Enzymes):** 87.25%
