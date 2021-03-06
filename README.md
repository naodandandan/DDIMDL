# DDIMDL
DDIMDL builds multimodal deep learning framework with multiple features of drugs to predict drug-drug-interaction(DDI) events.
## Usage
*Example Usage*
```
    python DDIMDL.py -f smile target enzyme -c DDIMDL -p read
```
-f *featureList*: A selection of features to be used in DDIMDL. The optional features are smile(substructure),target,enzyme and pathway of the drugs. It defaults to smile,target and enzyme.  
-c *classifier*: A selection of prediction method to be used. The optional methods are DDIMDL, RF, KNN and LR. It defaults to DDIMDL.  
-p *NLPProcess*: The choices are read and process. It means read the processed result from database directly or process the raw data again with *NLPProcess.py*. It defaults to read. In order to use *NLPProcess.py*, you need to install StanfordNLP package:

```
    pip install stanfordnlp
```
And you need to download english package for StanforNLP:
```
    import stanfordnlp
    stanfordnlp.download('en')
```
## Dataset
Event.db contains the data we compiled from [DrugBank](https://www.drugbank.ca/). It has 4 tables:  
**1.drug** contains 572 kinds of drugs and their features.  
**2.event** contains the 37264 DDIs we between the 572 kinds of drugs.  
**3.extraction** is the process result of *NLPProcess*. Each interaction was transformed to a tuple: *{mechanism, action, drugA, drugB}*  
**4.event_numer** lists the kinds of DDI events and their occurance frequency.  
## Evaluation
Simply run *DDIMDL.py* will start the train-test procedure.
![avatar](https://raw.githubusercontent.com/YifanDengWHU/img/master/%E6%B5%81%E7%A8%8B%E5%9B%BE0316-3.bmp)
The function *prepare* will calulate the similarity between each drugs based on their features.  
The function *cross_validation* will take the feature matrix as input to perform 5-CV and calculate metrics. Two csv files will be generated. For example, *smile_all_DDIMDL.csv* and *smile_each_DDIMDL.csv*. The first file evaluates the method's overall performance while the other evaluates the method's performance on each event. The meaning of the metrics can be seen in array *result_all* and *result_eve* of *DDIMDL.py*.
## Requirement
- numpy (==1.18.1)
- Keras (==2.2.4)
- pandas (==1.0.1)
- scikit-learn (==0.21.2)
- stanfornlp (==0.2.0)
Use
```
    pip install requirement.txt
```
to install all dependencies.  
**Notice: Too high version of sklearn will probably not work. We use 0.21.2 for sklearn.**
