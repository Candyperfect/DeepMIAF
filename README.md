# Protein Function Prediction via Missing Modality Imputation and Adaptive Multimodal Fusion

This is the code repository for protein function prediction model DeeepMIAF. 

**DeeepMIAF**: This method first employs advanced protein generation techniques to impute missing modality data with high fidelity, thereby mitigating the adverse impact of incomplete multimodal inputs. Subsequently, modality-specific feature extractors are utilized to capture the intrinsic and complementary characteristics of each data modality, yielding enriched protein representations. Building upon these representations, a gated attention mechanism is designed to dynamically reweight modality contributions, enabling effective and adaptive integration of heterogeneous biological evidence. Furthermore, DeepMIAF incorporates a network propagation module to exploit topological structures, integrating sequence homology and protein–protein interaction networks into the predictive model.

<div align=center><img width="800" alt="DeepMIAF" src="https://github.com/Candyperfect/DeepMIAF/tree/main/images/DeepMIAF.png"></div>

## Dependencies
* The code was developed and tested using python 3.8.
* To install python dependencies run: `pip install -r requirements.txt`. Some libraries may need to be installed via conda.
* The version of CUDA is `cudatoolkit==11.3.1`

## Data
Our experimental dataset come from [MSNGO](https://github.com/blingbell/MSNGO/tree/master/data). It covers 13 species and multiple modal data, including protein sequences, PPI networks, 3D structures, and GO annotations. Among them, the protein sequences are from Uniprot, PPI networks are from STRING (v11.0b), and protein structures have been missing-supplemented by AlphaFold2 or ESMFold methods. GO annotations are downloaded from the GOA database, filtered by species and evidence codes. For the biological textual descriptions, we collect them from the [UniProtKB](https://www.uniprot.org/). You can download [here](https://github.com/Candyperfect/DeepMIAF/tree/main/data).


## Train

If you want to train on your own dataset, please download [esm2_t33_650M_UR50D.pt](https://github.com/facebookresearch/esm?tab=readme-ov-file#esmfold) to DeeepMIAF/esm2_t33_650M_UR50D/

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

Our trained model can be downloaded from [here](https://github.com/blingbell/MSNGO/tree/master/DeepMIAF_models). 

You can use the model directly to get predictions. Run the `predict.py` script to make predictions about the input file (e.g. for CC):
```
python predict.py --ontology cc -f your_test.fasta
```

