# Data and Code for SafeDrug replication study
Deep learning replication study on patient medication prediction.  
[Paper repo](https://github.com/ycq091044/SafeDrug)


BibTex Citation of source paper
---
```
@inproceedings{yang2021safedrug,
    title = {SafeDrug: Dual Molecular Graph Encoders for Safe Drug Recommendations},
    author = {Yang, Chaoqi and Xiao, Cao and Ma, Fenglong and Glass, Lucas and Sun, Jimeng},
    booktitle = {Proceedings of the Thirtieth International Joint Conference on
               Artificial Intelligence, {IJCAI} 2021},
    year = {2021}
}
```
Table of results
---
asdf


Data download
---
Obtain permission to download the patient history MIMIC3 csv files:
- prescriptions.csv
- diagnoses_ICD.csv
- procedures_ICD.csv

Obtain drug code mapping files from the paper repo
- ndc2atc_level4.csv [https://github.com/sjy1203/GAMENet](https://github.com/sjy1203/GAMENet), RXCUI to ATC (MIMIC)
- drug-atc.csv [https://github.com/sjy1203/GAMENet](https://github.com/sjy1203/GAMENet), CID to ATC (side-effects)
- ndc2rxnorm_mapping.csv [https://github.com/sjy1203/GAMENet](https://github.com/sjy1203/GAMENet), rxnorm to RXCUI (MIMIC)
- drugbank_drugs_info.csv [Paper repo](https://github.com/ycq091044/SafeDrug), ATC to SMILES molecule strings
- drug-DDI.csv: [Paper repo](https://github.com/ycq091044/SafeDrug), side-effect pair tables in CID

Preprocessing code
---
Run notebook titled ...

Training and Evaluation code
---
Run the eponymous notebooks for each model.  
Set the argparser variables as desired.
- `args.Test = True` for bootstrap evaluation against test dataset
- `args.Inf_time = True` for inference timing
- both `False` for training
- `args.reverse = 1` to reverse patient visits in RETAIN
- `args.beta = 1` to use the SafeDrug PID controller to dynamically adjust DDI_loss contribution
- `args.mydata = 1` to use alternate MYDATA_PATH source file paths
- `args.smalldata = 1` to use alternate data cut

Mind the model state save and resume paths to proceed to evaluation and inference.

Dependencies
---
- rdkit-pypi
- memory_profiler
- torch
- pandas
- numpy
- sklearn
- dill
- random
- math
- statistics
- time
- datetime
- sys
- os
- logging
- argparse
- warnings
- collections
