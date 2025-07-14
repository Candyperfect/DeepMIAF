# Protein Function Prediction via Missing Modality Imputation and Adaptive Multimodal Fusion

This is the code repository for protein function prediction model DeeepMIAF. 

**DeeepMIAF** This method first employs advanced protein generation techniques to impute missing modality data with high fidelity, thereby mitigating the adverse impact of incomplete multimodal inputs. Subsequently, modality-specific feature extractors are utilized to capture the intrinsic and complementary characteristics of each data modality, yielding enriched protein representations. Building upon these representations, a gated attention mechanism is designed to dynamically reweight modality contributions, enabling effective and adaptive integration of heterogeneous biological evidence. Furthermore, DeepMIAF incorporates a network propagation module to exploit topological structures, integrating sequence homology and protein–protein interaction networks into the predictive model.

<p align="center">
    <br>
    <img src="./fig/DeepHGAT.png?raw=true" width="800" height="381"/>
    <br>
</p>

<div align=center><img width="800" alt="DeeepMIAF" src="https://github.com/blingbell/MSNGO/blob/master/images/DeeepMIAF.jpg"></div>

## Dependencies
* The code was developed and tested using python 3.8.
* To install python dependencies run: `pip install -r requirements.txt`. Some libraries may need to be installed via conda.
* The version of CUDA is `cudatoolkit==11.3.1`

## Data
<div align=center><img width="147" alt="uniprot" src="https://github.com/blingbell/MSNGO/blob/master/images/uniprot.jpg"><img width="175" alt="string" src="https://github.com/blingbell/MSNGO/blob/master/images/string.png"><img width="143" alt="goa" src="https://github.com/blingbell/MSNGO/blob/master/images/goa.png"><img width="206" alt="go" src="https://github.com/blingbell/MSNGO/blob/master/images/go.png"><img width="280" alt="alphafold" src="https://github.com/blingbell/MSNGO/blob/master/images/1724076793413.jpg"></div>

\
The data used are:
* Sequence: download from the [UniProt website](https://www.uniprot.org/).
* Biological text: download from the [UniProt website](https://www.uniprot.org/).
* PPI Network: download from the [STRING website](https://string-db.org/).
* Annotation: download from the [GOA website](https://www.ebi.ac.uk/GOA/).
* Gene Ontology: download from the [GO website](http://geneontology.org/).
* AlphaFold structure: download from the [AlphaFold website](https://alphafold.com/).

We also provide a small dataset which has less than 50 proteins to quickly test the model. It can be found [here](data/readme.md).

For a detailed description of data files, please see [here](data/readme.md).


## Train

If you want to train on your own dataset, please download [esm2_t33_650M_UR50D.pt](https://github.com/facebookresearch/esm?tab=readme-ov-file#esmfold) to MSNGO/esm2_t33_650M_UR50D/

Preprocessing.sh is for processing your raw data. 

Then run the following command, it can process raw data.
```
./scripts/preprocessing.sh
```

The mf, bp, and cc branches will be trained, predicted, and evaluated by the following files respectively.
```
./scripts/run_mf.sh
./scripts/run_bp.sh
./scripts/run_cc.sh
```

## Predict

Our trained model can be downloaded from [here](https://drive.google.com/file/d/1fRZYmTlPFmb6rmMSS87HoqACVm5YsNNR/view?usp=drive_link). 

You can use the model directly to get predictions. Run the `predict.py` script to make predictions about the input file (e.g. for CC):
```
python predict.py --ontology cc -f your_test.fasta
```

