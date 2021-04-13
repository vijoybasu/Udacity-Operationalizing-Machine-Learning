# Welcome to Vijoy's Repository!

## I'm Passionate about data (small, big, slow, fast) and the insights from data that drive business outcomes

### Udacity Azure Machine Learning Engineer Scholarship - Operationalizing Machine Learning in Azure

In this project, we use the "Bank Marketing Dataset" to train a ML model using Azure's AutoML service (which is a part of Azure Machine Learning Studio). This model is deployed and published using Azure Container Instances (ACI) later consume it using REST endpoints. We will also create, publish and consume a pipeline.


## Architecture Diagram of the Workflow
![image](https://user-images.githubusercontent.com/81923226/114523564-06d0b000-9c62-11eb-9977-e5fef2391b98.png)

### Steps:
1. Bank Marketing Dataset is registered on Azure MLS
2. Specify the dataset and configuration details such as machine learning task, here in our case its a classification task, exit criteria, etc. for selecting the best model that AutoML will produce.
3. Based on the metric selected in AutoML, select the best model and deploy it using azure container instance(ACI)
4. Enable logging and application insight service for keeping track of deployed model performance and number of request handled/failed.
5. After deployment and enabling the logs and application insights use the REST endpoint to interact with the deployed model with sample data and check its prediction results.
6. Using python SDK create a pipeline selecting the best AutoML model and publish it.


## Complete Workflow Explaination & Screenshots


Bank Marketing dataset is uploaded on Azure MLS and is consequently registered.
![image](https://user-images.githubusercontent.com/81923226/114527550-bf4c2300-9c65-11eb-880d-73dfeb1fb630.png)

Compute Cluster creation process initiated
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114527778-fde1dd80-9c65-11eb-982d-6d569e747c33.png">
</center>

Standard_DS12_v2 chosen as the VM for the cluster
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114527851-0f2aea00-9c66-11eb-8a32-04191c606d8d.png">
</center>

Cluster is named with minimum number of nodes set as = 1
![image](https://user-images.githubusercontent.com/81923226/114528111-51ecc200-9c66-11eb-84a1-7e12fbe0328d.png)


Post successful creation of compute cluster, we head over to experiment and start an AutoML run
![image](https://user-images.githubusercontent.com/81923226/114528196-6af57300-9c66-11eb-950f-0a6fdaa000c0.png)


Bank Marketing dataset is chosen for the desired AutoML run
![image](https://user-images.githubusercontent.com/81923226/114528245-75b00800-9c66-11eb-9dbf-a2c6ab202453.png)


Experiment has now been named as per choice and target column chosen as = 'y'
![image](https://user-images.githubusercontent.com/81923226/114528331-8bbdc880-9c66-11eb-8e7a-6c611d763e2e.png)


'Classification' is the chosen AutoML Task.
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114529524-a8a6cb80-9c67-11eb-9d6e-8b59540c9c4a.png"
</center>

'Accuracy' is chosen as the Primary Metric with 'Explain Best Model' checked for better explainability factors.
![image](https://user-images.githubusercontent.com/81923226/114529608-c3794000-9c67-11eb-85d0-7af9b1942cc4.png)

'Max Concurrent Iterations' is kept as = 5.
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114529700-dbe95a80-9c67-11eb-88c2-a45aa99f063c.png"
</center>

AutoML Experiment is started and is now in running stage.
![image](https://user-images.githubusercontent.com/81923226/114535658-e870b180-9c6d-11eb-92a6-8ae4edcfa091.png)


AutoML Experiment completes and 'VotingEnsemble' is the best model obtained from the run.
<center>
    ![image](https://user-images.githubusercontent.com/81923226/114535767-050ce980-9c6e-11eb-9751-3328d3f639b2.png)
</center>






















































































## Potential Improvements

1. Using Deep Learning in AutoML to accelerate the model training process and improve the accuracy, however this is subjective and may only work on larger datasets with lowly-sparsed features present.
2. Apply model interpretability of AutoML on more complex and larger datasets, to gain speed and valuable insights in feature engineering, which can in turn be used to refine complex model accuracy.
3. Apply the same concept learned here to create and publish other types of pipelines for:
     - Data Preparation
     - Validation
     - Deployment
     - Combined tasks
