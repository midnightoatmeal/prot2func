Prot2Func: Predicting Enzyme Function from Protein Sequences

Prot2Func is a machine learning project that attempts to classify whether a given protein sequence is an enzyme or not, using only its amino acid composition.

⸻

Dataset

I start with a subset of 500 protein sequences sampled from the UniProt Swiss-Prot database. Each protein is a string of amino acids (e.g., "MVKVGVNGFGRIGRL...").

To label whether a protein is an enzyme, I query the UniProt REST API using its ID and check for a Catalytic Activity (EC number) in the metadata.
This gives a binary label:
	•	1 → Enzyme
	•	0 → Non-enzyme

Class distribution:
	•	Enzymes: 140
	•	Non-enzymes: 360

⸻

Feature Engineering

I compute the amino acid composition of each protein:
For each of the 20 standard amino acids, I calculated its relative frequency in the sequence.

from collections import Counter

AMINO_ACIDS = "ACDEFGHIKLMNPQRSTVWY"

def aa_composition(seq):
    count = Counter(seq)
    total = len(seq)
    return [count.get(aa, 0) / total for aa in AMINO_ACIDS]


⸻

Models Trained

1. Logistic Regression (Sklearn)
	•	Input: 20-dimensional amino acid frequency vector
	•	Output: binary enzyme classification
	•	Performance:
	•	Accuracy: 84%
	•	Precision (Enzyme): 0.00
	•	Recall (Enzyme): 0.00
	•	Note: The model completely failed to predict any enzymes, likely due to class imbalance

2. Feedforward Neural Network (PyTorch)
	•	Architecture:
	•	Input layer: 20 features
	•	2 hidden layers (ReLU activation)
	•	Output: 2 logits (enzyme vs non-enzyme)
	•	Loss Function: CrossEntropyLoss
	•	Epochs: 20
	•	Performance:
	•	Accuracy: 21%
	•	Precision: 16%
	•	Recall: 100% (predicted everything as enzyme)
	•	F1 Score: 28%

⸻

Key Learnings
	•	Protein function cannot be accurately predicted from composition alone in this dataset.
	•	The model overfits to the dominant class or makes degenerate predictions (e.g., classifies everything as enzyme).
	•	Labeling enzyme functionality via UniProt API works but is noisy, limited, and results in imbalanced data.
	•	There is significant potential in modeling raw protein sequences with more expressive architectures (e.g., CNNs, transformers, embeddings like ESM or ProtBERT).
