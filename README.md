Prot2Func: Predicting Enzyme Function from Protein Sequences

Prot2Func is a machine learning project that explores the feasibility of predicting enzymatic activity (enzyme vs. non-enzyme) from protein sequences using only their amino acid composition.

Background:

Predicting whether a protein acts as an enzyme is a fundamental problem in computational biology, with applications in drug discovery, metabolic engineering, and synthetic biology. This project attempts a first-principles approach using amino acid composition as a basic feature set.


Dataset:
	•	Source: Subset of 500 proteins from the UniProt Swiss-Prot database
	•	Representation: Each protein is a string of amino acids (e.g., "MVKVGVNGFGRIGRL...")
	•	Labeling: Proteins were queried via the UniProt REST API for Catalytic Activity (EC Number) to assign binary labels:
	•	1 → Enzyme
	•	0 → Non-enzyme
	•	Class Distribution:
	•	Enzymes: 140
	•	Non-enzymes: 360


Feature Engineering:

Protein sequences were featurized using amino acid composition—a simple 20-dimensional vector representing the relative frequency of each standard amino acid.

from collections import Counter

AMINO_ACIDS = "ACDEFGHIKLMNPQRSTVWY"

def aa_composition(seq):
    count = Counter(seq)
    total = len(seq)
    return [count.get(aa, 0) / total for aa in AMINO_ACIDS]


Models Trained:

1. Logistic Regression (Sklearn)
	•	Input: 20-dimensional amino acid frequency vector
	•	Performance:
	•	Accuracy: 84%
	•	Precision (Enzyme): 0.00
	•	Recall (Enzyme): 0.00
	•	Observation: Strong class imbalance led to a degenerate classifier (predicting all as non-enzymes).

2. Feedforward Neural Network (PyTorch)
	•	Architecture:
	•	Input layer: 20 features
	•	Two hidden layers (ReLU)
	•	Output: 2 logits (enzyme vs non-enzyme)
	•	Loss Function: CrossEntropyLoss
	•	Epochs: 20
	•	Performance:
	•	Accuracy: 21%
	•	Precision: 16%
	•	Recall: 100% (predicts all as enzyme)
	•	F1 Score: 28%


Challenges & Key Learnings
	•	Protein function is not linearly separable by amino acid composition alone.
	•	The dataset suffers from label imbalance and potential noise in UniProt annotations.
	•	Even small neural networks overfit or collapse into trivial predictions under these conditions.
	•	There is significant potential in exploring sequence-aware models like:
	•	Convolutional Neural Networks (CNNs)
	•	Transformers (e.g., ProtBERT, ESM)
	•	Embedding-based representations
