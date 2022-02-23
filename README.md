# Differentially Private Synthetic Data Generation
"Privacy preserving approaches for generating synthetic data sets without having to compromise on data utility"<br/> 
~ Summary by [Stefan Rummer](https://www.linkedin.com/in/stefanrmmr/)

## Foundations and Purpose

<strong>What is synthetic data generation [SDG]? </strong> <br/>In our context, synthetic data is algorithmically created data that looks and behaves like real data. Generative models learn the statistical distribution in the original data and draw artificial samples from it to generate synthetic data. The synthetic data generation process completely breaks the 1-1 relation between the original and synthetic records. Contrary to other techniques, like pseudonymization, there is no key to go back from the synthetic records to the original ones.This process is irreversible.

<strong>Why is there the need for synthetic data?  </strong><br/>Real-world data is sometimes expensive to collect, or simply hard to come by. In these cases, synthetic data is easier to produce than collecting original data. It also allows the training of models on a wide variety of situations that real-world data might not capture. 

<strong>Why is there the need to enhance synthetic data generation to fulfill privacy standards? </strong><br/>There exist various scenarios where companies use synthetic data is to make information available for processing when regulations or other privacy concerns restrict access to the original data. For instance, the processing of customer data in a post-GDPR world involves strict compliance and governance rules for companies. In these cases, synthetic data is used as an anonymization method that brings companies more agility and freedom to process data in a safe and compliant way.<br/><br/>


## Types of Attributes in the Data

- <strong>PII Direct Identifiers:</strong> Confidential Information like Name, email, etc. that uniquely identifies an individual<br/>

- <strong>Quasi-Identifiers Attributes:</strong> Indirectly linked to individuals, Quasi-identifiers don't uniquely identify an individual, but, when combined and cross-referenced with individual records, they can substantially increase the likelihood that an attacker will be able to re-identify an individual. (e.g. Characteristics like, address, zip code, age, working title, company - Information that is available publically anyways and not personal)<br/>

- <strong>Sensitive Attributes:</strong> Data that is protected against unauthorized exposure. Attributes like health conditions, salary, criminal offenses,<br/> and geographic location are typically considered sensitive data. Note that there can be overlap between identifiers and sensitive data.<br/><br/>


## Types of Synthetic Data  

When determining the best method for creating synthetic data, it is important to first consider what type of synthetic data you aim to have. <br/>There are three broad categories to choose from, each with different benefits and drawbacks:

- <strong>Fully synthetic Data:</strong> This data does not contain any original data. This means that<br/> re-identification of any single unit is almost impossible and all variables are still fully available.<br/>

- <strong>Partially synthetic Data:</strong>
Only data that is sensitive is replaced with synthetic data. This requires a heavy dependency on the imputation model. This leads to decreased model dependence, but does mean that some disclosure is possible owing to the true values that remain within the dataset.<br/>

- <strong>Hybrid synthetic Data:</strong> Hybrid synthetic data is derived from both real and synthetic data. While guaranteeing the relationship and integrity between other variables in the dataset, the underlying distribution of original data is investigated and the nearest neighbor of each data point is formed. A near-record in the synthetic data is chosen for each record of real data, and the two are then joined to generate hybrid data.<br/><br/>


## Risks in Synthetically Generated Data

Please refer to this [article by statice](https://www.statice.ai/post/how-manage-reidentification-risks-personal-data-synthetic-data) which served as the source for the following paragraph.

A common misconception is to think that synthetic data is inherently private. Even though Synthetic data does not contain any PII in theory (CCP&GDPR conforming data structure), there still exists the chance that it resambles unique characteristics of the original dataset that could make it possible to gather information on real events or individuals in the original dataset from the synthetic data. 

Neural network based synthetic data generation approaches might memorize features in the training data. Ultimately, memorized patterns can be reproduced in the synthetic data, leading to privacy leaks. Luckily, we can add additional layers of privacy to the synthesization mechanisms, such as training the model using algorithms that satisfy the definition of differential privacy.<br/><br/>


## Differentially-Private Synthetic Data 

Differential Privacy [DP] minimizes re-identification- and privacy risks to a theoretical mathematical minimum and outputs privacy-preserving synthetic data robust against privacy attacks. From a high level perspective, DP uses noise to mask the presence of any particular individual in the input data. To generate differentially-private synthetic records, the models learn the original data distribution with a DP algorithm. This way, the synthetic data benefits from the theoretical guarantees that DP provides.

Differential privacy offers significantly higher privacy protection levels than commonly used disclosure limitation practices like data anonymization. Nevertheless, the synthetically generated data set fulfilling K-Anonymity/L-Diversity can still be considered to add an additional layer of privacy. These layers of privacy protection greatly enhance the privacy of the synthetic data. However, no technique can guarantee perfect privacy while keeping some utility. <br/><br/>


## The Ideal Target Solution 

- The overall goal is to generate synthetic data that perfectly mimics characteristics of an original source dataset.<br/>

- The amount of records with unique attribute value combinations needs to be minimized - achieve zero K=1 anonymous data points. Consequently, the granularity of the synthetically generated dataset is constrained, also consider L-Diversity and T-Closeness<br/>

- There is the need to implement smart noise into the synthetic dataset generation so that the principles of differential privacy are fullfilled.<br/><br/>


## Implementation of Privacy-preserving SDG Approaches

The information displayed in this section has been sourced and aggregated from [Andreas Kopp's article](https://cloudblogs.microsoft.com/opensource/2021/02/18/create-privacy-preserving-synthetic-data-for-machine-learning-with-smartnoise/) in Microsoft's open source Blog entry on the topic of "Create privacy-preserving synthetic data for machine learning with SmartNoise"

Please refer to this [research paper by Microsoft AI](https://arxiv.org/pdf/2011.05537.pdf) to learn more about DP-SDG synthesizers and their performance in machine learning scenarios.<br/><br/>

- <strong>Multiplicative Weights Exponential Mechanism (MWEM):</strong> Achieves Differential Privacy by combining Multiplicative Weights and Exponential Mechanism techniques, A relatively simple but effective approach, Requires fewer computational resources, shorter runtime 

- <strong>Differentially Private Generative Adversarial Network (DPGAN):</strong> Adds noise to the discriminator of the GAN to enforce Differential Privacy, Has been used with image data and electronic health records (HER) 

- <strong>Private Aggregation of Teacher Ensembles Generative Adversarial Network (PATEGAN):</strong> 	
A modification of the PATE framework that is applied to GANs to preserve Differential Privacy of synthetic data 
Improvement of DPGAN, especially for classification tasks 

- <strong>DP-CTGAN: </strong>Takes the state-of-the-art CTGAN for synthesizing tabular data and applies DPSGD (the same method for ensuring Differential Privacy that DPGAN uses), Suited for tabular data, avoids issues with mode collapse, Can lead to extensive training times 

- <strong>PATE-CTGAN: </strong>Takes the state-of-the-art CTGAN for synthesizing tabular data and applies PATE (the same method for ensuring Differential Privacy that PATEGAN uses), Suited for tabular data, avoids issues with mode collapse 

- <strong>Qualified Architecture to Improve Learning (QUAIL):</strong> Ensemble method to improve the utility of synthetic differentially private datasets for machine learning tasks, Combines a differentially private synthesizer and an embedded differentially private supervised learning model to produce a flexible synthetic data set with high machine learning utility<br/><br/> 


## Validation & Characteristics that need to be assessed 
- <strong>Characteristics Review </strong> - Does the Generator actually posess the same characteristics as the original data?
- <strong>Ethics Review </strong> - make sure that there are no discriminatory or potentially harmful characteristics to data subjects


- <strong>Differential Privacy Risk Analytics</strong> - Evaluate the synthetic data using the SAME metrics as for original datasets 
- <strong>Anonymization Risk Analytics</strong> - Evaluate the synthetic data using the SAME metrics as for original datasets<br/><br/>
