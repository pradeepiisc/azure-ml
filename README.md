# azure-ml

This repo is the result of learning the MLOps on azure(azure-ml) 
1. Model development (inner loop): Explore and process the data to train and evaluate the model. 
2. Continuous integration: Package and register the model.
3. Model deployment (outer loop): Deploy the model.
4. Continuous deployment: Test the model and promote to production environment.
5. Monitoring: Monitor model and endpoint performance.

Following items were performed in order resulting into the learning for the same topic. 

1. Setup including create all the necessary Azure resources like installing az, update with ml extension,  azure-workspace, azure-compute, azure-resourceGroup  
2. Used CLI(v2) by installing ml sdk as part of v2, creating workspace, resourceGroup, creating compute
3. We make the existing workspace and resource-group as default in order to not specify explicitly if we want these to be default. 
4. 'az configure --defaults workspace=<WS>'

End2End ML path
1. Converted the jupyter notebook to python script with mlflow autologging feature -> 
  Updated the job.yml file with command to train, input and output to the train.py file -> 
  updated training_data path to some location in azure -> 
  updated the compute name created using CLIv2 -> 
  till this point, job.yml file is updated with the required params like training script, compute name, environment name.
  Remember dataset is not provided via yml file but it is uploaded using CLIv2 using 'az create dataset' command. 
2. ServicePrincipal -> create using CLI -> store SP credentials in github secrets(for a particular repo not for entire github) -> 
  github action to trigger the training of the model using azure ml compute 

Using github actions to trigger the model training can be done using following steps: 
  1. Create a service principal using the Azure CLI.
  2. Store the credentials of the service principal as a secret in GitHub.
  3. Create a GitHub Action to train the model using Azure Machine Learning compute. 
  (two ways of triggering the action , one is on [push]ing the branch or another is like cron schedule) -> 
  but all this is happening in the main branch of the repo
  
 Next learning is to trigger once the non-main branch is reviewed and merged into main. 
  Automation(deploy new models) and Source control (manage code, track changes) , 
  but deploy models only when the code changes are confirmed to be merged to the main ( after review etc)
