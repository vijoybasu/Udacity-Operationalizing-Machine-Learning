# Welcome to Vijoy's Repository!

## I'm Passionate about data (small, big, slow, fast) and the insights from data that drive business outcomes

### Udacity Azure Machine Learning Engineer Scholarship - Operationalizing Machine Learning in Azure

In this project, we use the "Bank Marketing Dataset" to train a ML model using Azure's AutoML service (which is a part of Azure Machine Learning Studio). This model is deployed and published using Azure Container Instances (ACI) later consume it using REST endpoints. We will also create, publish and consume a pipeline.


## Architecture Diagram of the Workflow
![image](https://user-images.githubusercontent.com/81923226/114523564-06d0b000-9c62-11eb-9977-e5fef2391b98.png)

1. Bank Marketing Dataset is registered on Azure MLS
2. Specify the dataset and configuration details such as machine learning task, here in our case its a classification task, exit criteria, etc. for selecting the best model that AutoML will produce.
3. Based on the metric selected in AutoML, select the best model and deploy it using azure container instance(ACI)
4. Enable logging and application insight service for keeping track of deployed model performance and number of request handled/failed.
5. After deployment and enabling the logs and application insights use the REST endpoint to interact with the deployed model with sample data and check its prediction results.
Using python SDK create a pipeline selecting the best AutoML model and publish it.

## Potential Improvements

1. Using Deep Learning in AutoML to accelerate the model training process and improve the accuracy, however this is subjective and may only work on larger datasets with lowly-sparsed features present.
2. Apply model interpretability of AutoML on more complex and larger datasets, to gain speed and valuable insights in feature engineering, which can in turn be used to refine complex model accuracy.
3. Apply the same concept learned here to create and publish other types of pipelines for:
     - Data Preparation
     - Validation
     - Deployment
     - Combined tasks
