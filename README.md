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
On as-is data processing from paper repo:  

| Model         | DDI    | Jaccard | PRAUC  |       F1-score | Avg # of Meds |
|---------------|--------|---------|--------|----------------|---------------|
| LR            | 0.0776 | 0.4892  | 0.648  | 0.7576         | 17.1273       |
| RETAIN        | 0.0813 | 0.4521  | 0.6157 | 0.7549         | 15.5979       |
| RETAINrev     | 0.0851 | 0.4469  | 0.6109 | 0.7541         | 15.2285       |
| GAMENet       | 0.0588 | 0.7582  | 0.8574 | 0.9348         | 19.3785       |
| GAMENetPID    | 0.0149 | 0.236   | 0.3738 | 0.7815         | 4.9307        |
| SafeDrug_paper| 0.062  | 0.5091  | 0.6655 | 0.7626         | 20.6382       |
| SafeDrug      | 0.0688 | 0.525   | 0.6795 | 0.7689         | 21.8901       |


On data filtered by top-40 side-effects instead of bottom-40, see `process_data.ipynb`:

| Model         | DDI    | Jaccard | PRAUC  |       F1-score | Avg # of Meds |
|---------------|--------|---------|--------|----------------|---------------|
| LR            | 0.778  | 0.4894  | 0.6483 | 0.7579         | 17.146        |
| RETAIN        | 0.7838 | 0.4521  | 0.6157 | 0.7549         | 15.5979       |
| RETAINrev     | 0.7694 | 0.4473  | 0.6113 | 0.7535         | 15.117        |
| GAMENet       | 0.1859 | 0.2387  | 0.3778 | 0.7837         | 4.8137        |
| GAMENetPID    | 0.7392 | 0.3813  | 0.5456 | 0.6569         | 10.6871       |
| SafeDrug_paper| 0.102  | 0.1721  | 0.2896 | 0.6149         | 5.517         |
| SafeDrug      | 0.3542 | 0.2392  | 0.3789 | 0.7088         | 5.7149        |


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
Run notebook titled `process_data.ipynb` for data replication attempt  
Run notebook titled `process_data_paper.ipynb` for data as per the paper repo

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
