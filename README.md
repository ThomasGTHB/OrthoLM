# OrthoLM

Creation of orthologous groups of proteins using large language models and unsupervised clustering

This code was developed for a computer with Linux distribution. It might need adjustments for Windows or Mac computers.

# Instructions for use

Open terminal and clone the GitHub repository

```
cd "~/project_repository/"
mkdir Results
git clone https://github.com/facebookresearch/esm.git
```

Create the environment

```
conda create -y --name homology_detection__env python==3.10.12
conda activate homology_detection__env
#python3 -m venv homology_detection__env.env # alternatively if you have already Python 3.10.12 installed
#source homology_detection__env.env/bin/activate

python3 -m pip install -r environment_pip.txt
```

Create embedding representations from protein fasta files
(Exact syntax might change depending on your system)

```
# Choose the embedding model
model_list=("esm2_t48_15B_UR50D" "esm2_t36_3B_UR50D" "esm2_t33_650M_UR50D" "esm2_t30_150M_UR50D" "esm2_t12_35M_UR50D" "esm2_t6_8M_UR50D")
EMB_LAYER_list=(48 36 33 30 12 6)

model_index=2 # change to select the model
model=${model_list[$model_index]}
EMB_LAYER=${EMB_LAYER_list[$model_index]}

# Embedding of the sequence file data.fasta
speciesName="data"
time CUDA_VISIBLE_DEVICES=0 python3 /esm/scripts/extract.py "$model" "$speciesName.fasta" "/$speciesName_emb_$model/" --repr_layers $t_size --include mean
```

# The rest of the code for clustering embedded proteins and analysing the results is in the notebook.

jupyter notebook # clustering with the Python notebook
# Within the notebook, if you cannot load all modules verify that you are loading with Python 3.10.12 (import sys; print(sys.version))
