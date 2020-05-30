# MLOps Integration Project

This is a project created to automate the process of training and changing and again training a ML model to get the best accuracy.
This project is an integration of Docker , Jenkins and Python.
## Python
My python code to train models and change them can be found on [github link to code
](https://github.com/prasadpriyesh1/MLO_DevOps_integration_source_code.git)
My python code is organised into classes for better understanding and structure.
Organising into classes helps in easy modification of my code.
Currently  I have 3 model training codes for CNN , ANN and KNN(sklearn). My 'modify model' code automatically detects the type of model does the required changes.

> Before running the jenkins job a base model should be created on which changes will be made



## Jenkins


I have created 4 jobs in jenkins 
1. get_code
2. train_model
3. check_accuracy
4. change_model

Here is the pipeline for the jobs![pipeline](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/pipeline.png)

              

### get_code (job1)

This job basically fetches my ML code from my [github repo](https://github.com/prasadpriyesh1/MLO_DevOps_integration_source_code.git) and transfers it to my base os.
![1](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job1%28get_code%29/job_get_code_1.png)
![2](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job1%28get_code%29/job_get_code_2.png)

### train_model(job2)
