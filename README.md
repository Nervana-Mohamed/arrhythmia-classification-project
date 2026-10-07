# Arrhythmia classification

Classifying ECG recordings into arrhythmia types with six scikit-learn models, and checking whether PCA improves the results.

The data is the Cardiac Arrhythmia Database from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/5/arrhythmia): 452 patients, 279 attributes and a class label with 16 possible values (1 = normal, 2-15 = arrhythmia types, 16 = other). The raw file `arrhythmia.data` is included.

## What's in the notebook

1. Load the data and build column names from the dataset documentation
2. Missing values: `?` is turned into NaN, `J_angle` (83% missing) is dropped, the other columns are filled with the median
3. Remove constant columns, stratified train/test split, standard scaling (fitted on the training set only)
4. Train KNN, Logistic Regression, Decision Tree, Linear SVM, Kernel SVM and Random Forest
5. Check overfitting by comparing train and test accuracy
6. PCA keeping 95% of the variance (261 features down to 92 components)
7. Train the same models on the PCA features and compare

## Results (test set, 113 patients)

| Model | Accuracy before PCA | Accuracy after PCA |
|---|---|---|
| KNN | 0.566 | 0.566 |
| Logistic Regression | 0.637 | 0.637 |
| Decision Tree | 0.690 | 0.389 |
| Linear SVM | 0.646 | 0.664 |
| Kernel SVM | 0.584 | 0.602 |
| Random Forest | 0.743 | 0.584 |

PCA helped a little for the SVMs and clearly hurt the tree-based models, so it was not an improvement overall. The best model was Random Forest without PCA. These numbers come from a single split of a small dataset, so small differences should not be taken too seriously.

## Running it

```bash
git clone <repo-url>
cd <repo-folder>
pip install -r requirements.txt
jupyter notebook Arrhythmia_Classification.ipynb
```

Run the cells from top to bottom. `arrhythmia.data` has to be in the same folder as the notebook.

## Files

```
.
├── Arrhythmia_Classification.ipynb
├── arrhythmia.data
├── requirements.txt
└── README.md
```
