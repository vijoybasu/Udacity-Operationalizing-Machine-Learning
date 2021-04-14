# Welcome to Vijoy's Repository!

## I'm Passionate about data (small, big, slow, fast) and the insights from data that drive business outcomes

### Udacity Azure Machine Learning Engineer Scholarship - Operationalizing Machine Learning in Azure

## Project Overview
In this project, we use the "Bank Marketing Dataset" to train a ML model using Azure's AutoML service (which is a part of Azure Machine Learning Studio). This model is deployed and published using Azure Container Instances (ACI) later consume it using REST endpoints. We will also create, publish and consume a pipeline.


## Architecture Diagram of the Workflow
![image](https://user-images.githubusercontent.com/81923226/114523564-06d0b000-9c62-11eb-9977-e5fef2391b98.png)

## How can we improve the project further?

1. Using Deep Learning in AutoML to accelerate the model training process and improve the accuracy, however this is subjective and may only work on larger datasets with lowly-sparsed features present. (https://www.ijcai.org/proceedings/2019/0602.pdf)
2. Apply model interpretability of AutoML on more complex and larger datasets, to gain speed and valuable insights in feature engineering, which can in turn be used to refine complex model accuracy.
3. Apply the same concept learned here to create and publish other types of pipelines for:
     - Data Preparation
     - Validation
     - Deployment
     - Combined tasks

## Key Steps:
1. The Bank Marketing Dataset is registered on Azure MLS.
2. Specify the dataset target variable and configuration details such as the machine learning task, model explainability and concurrent runs. Here in our case, we proceed with a classification task, an exit criteria for selecting the best model that AutoML will produce.
3. Based on the primary metric selected in AutoML, we go ahead and select the best model and deploy it using azure container instance(ACI)
4. We also make sure to enable logging and consequently application insights for keeping track of the deployed model performance and number of HTTP API Response and Request.
5. After deployment and enabling the logs and application insights, we use the REST endpoint to consume the deployed model with sample data and check its prediction results with a JSON Payload.
6. Using the python SDK create a pipeline selecting the best AutoML model and publish it.
7. The published pipeline is viewed in the AML Studio for confirmation.

#### Authentication
This step used the `az cli` interface to log in to the `AML Studio`, then create a Service Principal (SP) to access the project workspace. As Udacity provisioned AML lab environment does not have sufficient privilege to create the SP, this step was not performed.

#### Auto ML Model
This step used AML AutoML to train a collection of classification models on this Bank Marketing dataset and present the trained models in descending order of AUC weighted accuracy.

#### Deploy the best model
In this step, the top performing model, i.e. the one with the best AUC weighted accuracy was selected for deployment, and an endpoint to interact with the model was generated.

#### Enable Logging
This step used `az cli` interface to enable Application Insights and retrieve logs of the operational health of the deployed model endpoint.

#### Consume Model Endpoints
In this step, a provided script was run in the `az cli` interface to make a request to the deployed model endpoint and display the response received. The payload data used for testing the endpoint was also saved to a json file named `data.json` for use in conducting a benchmarking test on the endpoint.

#### Create and publish a pipeline

This involved creating and publishig an endpoint for the AutoML training pipeline, allowing the training process to be automated.

#### Documentation

In this final step, a screencast was created to show the entire process of the working ML application, along with a README.md file to describe the project and document the main steps.

## SCREENCAST YOUTUBE VIDEO LINK 
https://www.youtube.com/watch?v=_D0UccIcd6c

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/_D0UccIcd6c/0.jpg)](https://www.youtube.com/watch?v=_D0UccIcd6c)

## Complete Workflow Step-by-Step Explaination & Screenshots

### Bank Marketing dataset is uploaded on Azure MLS and is consequently registered.
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

## Create a new AutoML Run

### Initializing AutoML Run

Bank Marketing dataset is chosen for the desired AutoML run
![image](https://user-images.githubusercontent.com/81923226/114528245-75b00800-9c66-11eb-9dbf-a2c6ab202453.png)


Experiment has now been named as per choice and target column chosen as = 'y'
![image](https://user-images.githubusercontent.com/81923226/114528331-8bbdc880-9c66-11eb-8e7a-6c611d763e2e.png)


'Classification' is the chosen AutoML Task (without checking the enable Deep Learning box).
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114529524-a8a6cb80-9c67-11eb-9d6e-8b59540c9c4a.png"
</center>

'Accuracy' is chosen as the Primary Metric with 'Explain Best Model' checked for better explainability factors.
![image](https://user-images.githubusercontent.com/81923226/114529608-c3794000-9c67-11eb-85d0-7af9b1942cc4.png)

'Exit criterion' is set to =1hr and 'Max Concurrent Iterations' is kept as = 5.
<center>
    <img src="https://user-images.githubusercontent.com/81923226/114529700-dbe95a80-9c67-11eb-88c2-a45aa99f063c.png"
</center>

AutoML Experiment is started and is now in running stage.
![image](https://user-images.githubusercontent.com/81923226/114535658-e870b180-9c6d-11eb-92a6-8ae4edcfa091.png)


AutoML Experiment completes and 'VotingEnsemble' is the best model obtained from the run.
![image](https://user-images.githubusercontent.com/81923226/114535767-050ce980-9c6e-11eb-9751-3328d3f639b2.png)


We also have the option to view the explaination as we had checked the explain best model parameter during AutoML run initiation time.
![image](https://user-images.githubusercontent.com/81923226/114537422-ce37d300-9c6f-11eb-8620-27cb88af568e.png)

Model achieves 92% accuracy via VotingEnsemble (AUTOML) with other metrics displayed.
![image](https://user-images.githubusercontent.com/81923226/114537515-eb6ca180-9c6f-11eb-8a44-87abefbbf89f.png)

RESULT GRAPHS OF AUTOML RUN DISPLAYED BELOW:

![image](https://user-images.githubusercontent.com/81923226/114537728-2c64b600-9c70-11eb-87f1-d151c3735e14.png)
![image](https://user-images.githubusercontent.com/81923226/114537750-31296a00-9c70-11eb-9756-d11db7701a9f.png)
![image](https://user-images.githubusercontent.com/81923226/114537766-34bcf100-9c70-11eb-88f3-55b8dfc8345c.png)
![image](https://user-images.githubusercontent.com/81923226/114537791-3c7c9580-9c70-11eb-900d-8da03f10d504.png)
![image](https://user-images.githubusercontent.com/81923226/114537812-443c3a00-9c70-11eb-95d1-cc304c0fb9e2.png)

## Deploy a model and consume a model endpoint via an HTTP API
### Deploying Model Obtained via AutoML

Now, we proceed for Model Deployment. We click on "Deploy" button to initiate deployment of the best run. We name the deployment too.

![image](https://user-images.githubusercontent.com/81923226/114537883-5d44eb00-9c70-11eb-96dd-d23ff95a12d2.png)

Deployment is now in 'Transitioning' State.

![image](https://user-images.githubusercontent.com/81923226/114537919-6a61da00-9c70-11eb-9269-9c27302fd9bb.png)

### Model successfully deployed on Azure MLS
Successfully Deployed! Deployment State changed to 'Healthy'

![image](https://user-images.githubusercontent.com/81923226/114537976-777ec900-9c70-11eb-93ab-54c595410307.png)


We now choose the best model and enable 'Authentication' while deploying the model using Azure Container Instances (ACI)

![image](https://user-images.githubusercontent.com/81923226/114538008-81a0c780-9c70-11eb-97fe-b9e0f9042c8b.png)


### Application Insights set to 'True' and `logs.py` is executed to enable logging

The executed code in logs.py enables 'Application Insights'. This parameter was disabled before executing `logs.py`.

![image](https://user-images.githubusercontent.com/81923226/114538105-9b420f00-9c70-11eb-8357-8f451925760b.png)
![image](https://user-images.githubusercontent.com/81923226/114584063-e45d8780-9c9f-11eb-8d20-4ffa916d1c10.png)

We now download the `swagger.json` file to the parent directory folder from the deployment endpoint in the `AML Studio` to publish our pipeline.
![image](https://user-images.githubusercontent.com/81923226/114538167-b14fcf80-9c70-11eb-8355-cfe01c432b59.png)


We open two other GitBash `az cli` to execute the `swagger.sh` and `serve.py` files individually.
- bash swagger.sh
- python serve.py

![image](https://user-images.githubusercontent.com/81923226/114538360-efe58a00-9c70-11eb-8865-4c5da6e5f885.png)
![image](https://user-images.githubusercontent.com/81923226/114538386-f83dc500-9c70-11eb-8e02-9d0047d0d083.png)
![image](https://user-images.githubusercontent.com/81923226/114538417-025fc380-9c71-11eb-84e4-8eef928bcd78.png)

We change the port number to 9000 in `swagger.sh` as it was giving an error to us

![image](https://user-images.githubusercontent.com/81923226/114538474-0ee41c00-9c71-11eb-957c-987bea4a81a1.png)

Swagger.sh file ran again to publish the pipeline.

![image](https://user-images.githubusercontent.com/81923226/114538514-199eb100-9c71-11eb-9ec3-1585723518fb.png)


We run the Serve.py file on new port no - 9000 to check the swagger output.

![image](https://user-images.githubusercontent.com/81923226/114538565-26230980-9c71-11eb-8d97-c2ed86a864e6.png)


### Swagger runs on localhost

![image](https://user-images.githubusercontent.com/81923226/114538836-6d10ff00-9c71-11eb-986f-c9895bbd78a6.png)

### Swagger runs on localhost showing the HTTP API Methods and responses for the model
We now check for our deployed model on the swagger hosted page.

![image](https://user-images.githubusercontent.com/81923226/114538878-7c904800-9c71-11eb-8b60-c33d037a0d9e.png)

We run the web service model and try to obtain the predicted output.

![image](https://user-images.githubusercontent.com/81923226/114538903-85811980-9c71-11eb-8e8b-73677d82aff1.png)

![image](https://user-images.githubusercontent.com/81923226/114538944-929e0880-9c71-11eb-9a1f-a0b7539fdef8.png)


Once we have confirmed that the model is successfully predicting and the pipeline is successful, we try to consume the model using an endpoint.
We now will edit the `endpoint.py` file and put our obtained REST Endpoint from the deployment into the `scoring uri` parameter here.

![image](https://user-images.githubusercontent.com/81923226/114539102-c0834d00-9c71-11eb-9d70-8ccd49948ba4.png)

### Endpoint.py script runs against the API producing JSON output from the model
We execute the `endpoint.py` file and try to check the consumed model's final output.
Output is obtained in the similar format as desired, hence validating our approach.

![image](https://user-images.githubusercontent.com/81923226/114539207-e27ccf80-9c71-11eb-95f9-06746542fb45.png)


All the project files in the parent directory are displayed here for further review and confirmation. We use the `ls -lrtF` command to check this.

![image](https://user-images.githubusercontent.com/81923226/114539274-f4f70900-9c71-11eb-99dc-418f8c4046e0.png)

## Configure a pipeline with the Python SDK
We now go back to the Azure MLS, and upload the jupyter notebook and try to execute the notebook step-by-step to confirm our approach using code.

![image](https://user-images.githubusercontent.com/81923226/114539354-0cce8d00-9c72-11eb-844c-473c43ecca28.png)

![image](https://user-images.githubusercontent.com/81923226/114539366-10621400-9c72-11eb-8587-007d0ce2fcaf.png)

![image](https://user-images.githubusercontent.com/81923226/114539376-13f59b00-9c72-11eb-84d5-82c4e20eb22b.png)

![image](https://user-images.githubusercontent.com/81923226/114539389-17892200-9c72-11eb-8664-d257841698fd.png)

![image](https://user-images.githubusercontent.com/81923226/114539410-1b1ca900-9c72-11eb-8340-c165077d0feb.png)

![image](https://user-images.githubusercontent.com/81923226/114539424-1eb03000-9c72-11eb-8f40-f5d7684e0fa8.png)

![image](https://user-images.githubusercontent.com/81923226/114539436-21ab2080-9c72-11eb-94ee-6c8f514ebd2e.png)

![image](https://user-images.githubusercontent.com/81923226/114539466-27a10180-9c72-11eb-8d52-403287172522.png)

![image](https://user-images.githubusercontent.com/81923226/114539490-2b348880-9c72-11eb-8108-5ba6bde3c2cf.png)

![image](https://user-images.githubusercontent.com/81923226/114539508-2ff93c80-9c72-11eb-9879-4485d8cdfe0a.png)

### RunDetails Widget successfully completes execution

![image](https://user-images.githubusercontent.com/81923226/114539543-3982a480-9c72-11eb-956a-85ca8e89cfbb.png)

![image](https://user-images.githubusercontent.com/81923226/114539561-3daec200-9c72-11eb-8da4-1be5f01d1d8b.png)

![image](https://user-images.githubusercontent.com/81923226/114539574-42737600-9c72-11eb-86a5-6432e23274cf.png)

FINAL OUTPUT OF COMPLETED RUN!

![image](https://user-images.githubusercontent.com/81923226/114539601-469f9380-9c72-11eb-8046-9d6a790c10d7.png)

![image](https://user-images.githubusercontent.com/81923226/114539642-50c19200-9c72-11eb-9bb7-7a433abdb9df.png)

![image](https://user-images.githubusercontent.com/81923226/114539657-54551900-9c72-11eb-9f16-d89f5369477f.png)

### Final Metrics of our completed AutoML Run.

![image](https://user-images.githubusercontent.com/81923226/114539693-5b7c2700-9c72-11eb-8c36-01f2192aaaa0.png)
![image](https://user-images.githubusercontent.com/81923226/114539702-5f0fae00-9c72-11eb-9dc7-213ef5c7e0c9.png)


### The Best model is being retrieved.

![image](https://user-images.githubusercontent.com/81923226/114539729-6636bc00-9c72-11eb-9d88-5621b8012ab9.png)

![image](https://user-images.githubusercontent.com/81923226/114539737-6931ac80-9c72-11eb-9d0b-8a352263a68e.png)

![image](https://user-images.githubusercontent.com/81923226/114539753-6df66080-9c72-11eb-91bb-4418888b2a03.png)

![image](https://user-images.githubusercontent.com/81923226/114539780-72bb1480-9c72-11eb-8525-dbf22307e775.png)


## Publishing a ML Pipeline
We now try and publish the REST Endpoint.

![image](https://user-images.githubusercontent.com/81923226/114539812-79e22280-9c72-11eb-836d-ec8931fc952a.png)

![image](https://user-images.githubusercontent.com/81923226/114539824-7d75a980-9c72-11eb-89ff-d9748102f28b.png)

![image](https://user-images.githubusercontent.com/81923226/114539835-81093080-9c72-11eb-9c0c-3f3eb01d2fc8.png)

![image](https://user-images.githubusercontent.com/81923226/114539850-849cb780-9c72-11eb-9f30-506fcf283f42.png)

![image](https://user-images.githubusercontent.com/81923226/114539870-89fa0200-9c72-11eb-8351-85c682241dc8.png)

![image](https://user-images.githubusercontent.com/81923226/114539883-8f574c80-9c72-11eb-842d-3afcf95297ee.png)

## Use a REST endpoint to interact with a Pipeline.
Pipeline endpoint is successfully displayed as 'pipeline-rest-endpoint'

![image](https://user-images.githubusercontent.com/81923226/114540018-b281fc00-9c72-11eb-8b85-d9c3d23e9cf4.png)

![image](https://user-images.githubusercontent.com/81923226/114540033-b746b000-9c72-11eb-9e6e-e6a479ab05c7.png)

![image](https://user-images.githubusercontent.com/81923226/114540074-bd3c9100-9c72-11eb-9280-4a7259a5d50d.png)

PIPELINE RUN OVERVIEW

![image](https://user-images.githubusercontent.com/81923226/114540094-c3327200-9c72-11eb-8859-9bab6538670e.png)

### Bank Marketing Dataset with AutoML Module

![image](https://user-images.githubusercontent.com/81923226/114540123-cb8aad00-9c72-11eb-9c84-0f302fe5bcf7.png)

![image](https://user-images.githubusercontent.com/81923226/114540142-d1808e00-9c72-11eb-9c19-49da402a84f3.png)

### The "Published Pipeline Overview" showing a REST Endpoint and a status of ACTIVE

![image](https://user-images.githubusercontent.com/81923226/114540181-d9d8c900-9c72-11eb-829c-a5c18d1f65ae.png)

![image](https://user-images.githubusercontent.com/81923226/114540192-dd6c5000-9c72-11eb-81f6-72f3ac634a0f.png)

![image](https://user-images.githubusercontent.com/81923226/114540210-e2310400-9c72-11eb-83d5-bdaac527b33a.png)
