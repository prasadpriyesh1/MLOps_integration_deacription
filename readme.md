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

## DockerFiles
I have used 3 dockerfiles for my 3 models.
1. [ANN Dockerfile](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/ann_dockerfile/Dockerfile) - contains libraries for ANN and runs ANN model training code using CMD
2. [CNN Dockerfile](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/cnn_dockerfile/Dockerfile) - contains libraries for CNN and runs CNN model training code using CMD
3. [SKLEARN Dockerfile](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/sklearn_dockerfile/Dockerfile) - contains libraries for SKLEARN and runs SKLEARN model training code using CMD

		containers from these files are mounted to my base os 
		MLOps_source_code to source_code folder inside the 
		containers
## Jenkins


I have created 4 jobs in jenkins 
1. get_code
2. train_model
3. check_accuracy
4. change_model

Here is the pipeline for the jobs![pipeline](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/pipeline.png)

              

### get_code (job1)

upstream jobs - null
downstream jobs - train_model

This job basically fetches my ML code from my [github repo](https://github.com/prasadpriyesh1/MLO_DevOps_integration_source_code.git) and transfers it to my base os.
![1](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job1%28get_code%29/job_get_code_1.png)
![2](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job1%28get_code%29/job_get_code_2.png)

### train_model(job2)

upstream jobs - get_code , change_model
downstream jobs - check_accuracy

This job first checks the model type (ANN ,CNN , KNN) by running the get_model.py file.
It then starts the container according to the type of model to run the respective code to train the model. The accuracy is the  stored in a file.
![1](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job2%28train_model%29/job2_1.png)
![2](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job2%28train_model%29/job2_2.png)

### check_accuracy(job3)

upstream jobs - train_model
downstream jobs - change_model

This job runs the check_accuracy.py file and compares the accuracy of the trained model to a certain threshold which is set by me (0.82 in my case).
If accuracy is greater than the threshold the the code returns exit 1 which marks the job as failure and prevents execution of the downstream job. Else it returns exit 0 which triggers the downstream job.
![1](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job3%28check_accuracy%29/job3_1.png)
![2](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job3%28check_accuracy%29/job3_2.png)

### change_model(job4)

upstream jobs - check_accuracy
downstream jobs - train_model

This job runs the modify_model.py file which changes the model and saves the changed model.
For ANN and CNN the code changes the no. of units in Dense layers and also adds Dense layers if the no. of units in the last layer equals a certain threshold. The threshold is relative to each added layers (not same for each layer).
![1](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job4%28change_model%29/job4_1.png)
![2](https://github.com/prasadpriyesh1/MLOps_integration_deacription/blob/master/job4%28change_model%29/job4_2.png)


