# Experimental Implementation of DP-WGAN<br/>Differentially Private Synthetic Data Generation 
For **Continuous Data with binary Targets** using the Differentially Private Wasserstein GAN

1) DP-WGAN **Synthetic Data** for "Health care: Heart attack possibility" [Kaggle Dataset](https://www.kaggle.com/datasets/nareshbhat/health-care-data-set-on-heart-attack-possibility?select=heart.csv) --> [view Notebook](https://github.com/stefanrmmr/differentially_private_synthetic_data/blob/main/dpwgan_borealis_heart_disease.ipynb)<br/>
2) DP-WGAN **Synthetic Data** for "BankNote Authentication UCI" [Kaggle Dataset](https://www.kaggle.com/datasets/shantanuss/banknote-authentication-uci) --> [view Notebook](https://github.com/stefanrmmr/differentially_private_synthetic_data/blob/main/dpwgan_borealis_banknote.ipynb)<br/><br/>

___

### Metrics achieved for DP-WGAN on the Heart Disease Dataset
<br/>

<img width="684" alt="synthdata_sc1" src="https://user-images.githubusercontent.com/82606558/180919628-b0720159-df65-40b9-90be-ea5d79279e84.png">
*after multiple attempts using normalized input data, epsilon = approx 3.4 and delta = 1e-5

___

###  Process Steps & Key Concepts
- The data needs to be in csv format and has to be partitioned as train and test before feeding it to the models. 
- Missing values are not supported and needs to replaced appropriately by the user before usage.
- In case the data has continuous and categorical attributes, it needs to be pre-processed <br/>(discretization for continuous values/ encoding for categorical attr.)<br/><br/>
- The generative GAN-based ML models are trained using the training dataset. 
- The generative model is used to create a synthetic version of the train dataset
- To compensate for irregularities multiple GAN-Generator models are trained
- To compensate for irregularities multiple synthetic datasets are generated,<br/> the optimal best-performing dataset that yields the max AUC is selected<br/><br/>
- **Logistic Regression Classifiers** are trained using the real data, as well as, the synthetically generated dataset
- Both classifiers are evaluated regarding performance on the left-out real test dataset (preserved for evaluation)
- Relevant Metrics (mainly AUC) and visualizations of correlation-matrices of synthetic datasets were generated

___

### Acknowledgements & Sources
Major parts of this summary notebook were extracted from this [BOREALIS Private Data Generation](https://github.com/BorealisAI/private-data-generation) Github repository by BorealisAI. Note that, this Jupyter notebook covers only one (DP-WGAN) of various possible datasets and generative models for differentially private synthetic data generation. The aforementioned analysis aproaches have yielded the following results as extracted from the original notebook. For more information rearding **differential privacy specific privacy arguments Delta & Epsylon** please refer to this [info-page by Microsoft]( https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/dwork.pdf)
