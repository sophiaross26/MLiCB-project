# MLiCB-project
This repository contains code and documentation for the Project in Machine Learning in Computational Biology:
Enhancing Single-Cell RNA-seq Analysis: Transitioning scPML from R to Python with Advanced Explainability

## Download scPML.zip
The `scPML.zip` file can be downloaded from [Google Drive](https://drive.google.com/file/d/1zFWLsCgHTD02Hg2Y4v65iNKL5VmCRmpu/view?usp=drive_link).

Project Structure

-- proj_name
  -- raw_data
    -- ref
        data_1.csv
        label_1.csv
    -- query
        data_1.csv
  -- data
    -- ref
    -- query       
  -- demo
    -- seq_well_10x_v3
      -- data.h5
      -- hyper_parameters
      -- ret.pkl
      -- results
      -- model
      -- explainability_outputs

Directory Descriptions
raw_data: Contains the raw training and test data.
data: Contains the pre-processed data.
demo/seq_well_10x_v3: Contains results and outputs from various stages of the analysis.

Steps for Running the Analysis

First decompress all the directories and sub-directories.

Construct Similarity Matrices:
python utils/get_sm.py demo/seq_well_10x_v3

Preprocessing:
python utils/pre_process.py demo/seq_well_10x_v3

Data Pre-processing:
python utils/pre_process.py demo/seq_well_10x_v3
python utils/data_csv2h5.py --path=demo/seq_well_10x_v3 --subpath=raw_data
python utils/data_csv2h5.py --path=demo/seq_well_10x_v3 --subpath=data


Run scPML:
cd demo/seq_well_10x_v3 
python main.py

Run Explainability Analysis:
python explainability.py --[cluster_by, max_clusters, num_features, importance_threshold, top_n]

Run Specific Explainability Methods:
python explainability.py --task [classification_report, confusion_matrix, hierarchical_clustering, feature_importance, correlation]

Explainability Analysis Options
--task hierarchical_clustering --cluster_by [samples, genes] --max_clusters [int]
--task feature_importance --importance_threshold [float] --num_features [int]
--task correlation --top_n [int]

Default Parameters
--cluster_by genes
--cluster_by samples --max_clusters 6
--importance_threshold 0.01
--num_features 10
--top_n 20

Outputs
results Directory
Confusion Matrix Plot:
pred_confusion_plot.png: A heatmap representing the confusion matrix for the predicted vs. true labels of the query data.

UMAP Visualizations:

reference-query raw true label.png
reference-query h true label.png
reference-query h pred label.png
raw batches.png
h batches.png

CSV Files:
query_preds.csv
query_labels.csv
all_preds.csv
raw_labels.csv
embeddings_2d.csv
raw_data_2d.csv

model Directory
Classifier Model:
classifier.pt: Contains the trained classifier component of the MVCC model.

Graph Convolutional Network (GCN) Models:
gcn_model_0.pt
gcn_model_1.pt
gcn_model_2.pt

seq_well_10x_v3 directory:
Hyperparameters:
hyper_parameters: Configuration parameters used for training the MVCC model.

Explainability Outputs Directory
Contains various plots and analysis results from the explainability analysis script.
