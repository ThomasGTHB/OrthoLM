# OrthoLM

Creation of orthologous groups of proteins using large language models and unsupervised clustering

This code was developed for a computer with Linux distribution. It might need adjustments for Windows or Mac distributions.

# Instructions for use

Open the terminal and clone the GitHub repository

```
git clone https://github.com/ThomasGTHB/OrthoLM.git
cd OrthoLM
mkdir Results

git clone https://github.com/facebookresearch/esm.git # Required for running ESM
```

Create the environment

```
conda create -y --name homology_detection__env python==3.10.12
conda activate homology_detection__env
#python3 -m venv homology_detection__env.env # alternatively if you already have Python 3.10.12 installed
#source homology_detection__env.env/bin/activate

python3 -m pip install -r environment_pip.txt

python3 -m ipykernel install --user --name=homology_detection__env # set the virtual environment as a Jupyter kernel
```

Create embedding representations from protein fasta files
(Exact syntax might change depending on your system)

We provide pre-computed embeddings for the esm2_t36_3B_UR50D model in the Datasets folder.

```
# Choose the embedding model
model_list=("esm2_t48_15B_UR50D" "esm2_t36_3B_UR50D" "esm2_t33_650M_UR50D" "esm2_t30_150M_UR50D" "esm2_t12_35M_UR50D" "esm2_t6_8M_UR50D")
EMB_LAYER_list=(48 36 33 30 12 6)

model_index=1 # change to select the model

model=${model_list[$model_index]}
EMB_LAYER=${EMB_LAYER_list[$model_index]}

# Embedding of the sequences inside the fasta file
speciesName="pfal_pber"
time CUDA_VISIBLE_DEVICES=0 python3 esm/scripts/extract.py "$model" "Datasets/${speciesName}.fasta" "Datasets/${speciesName}_emb_${model}/" --repr_layers $EMB_LAYER --include mean
```

Cluster embedded proteins with the k-means algorithm and analyse the final clusters: Python code in the Jupyter notebook
```
jupyter notebook
```
After opening the notebook, select the kernel with homology_detection__env name.
