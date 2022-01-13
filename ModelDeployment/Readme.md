1. load necessary modules, then download data, in our case we use sklearn so it's simple
2. Split data into test, train and validation dataset
3. Save the data locally
4. Upload it to S3
5. Once the train dataset is ready on S3, we can set the training job, (what algorithm we want to use, what hyperparameter is specific to that algorithm, and where our data is stored.) 
6. Once we decribe training job, we ask Sagemaker to create and run the traning job.
7. The output of the xgboost algo is saved to S3 and those resulting files are called “Model Artifacts” 
8. Then we need to create endpoint configuration (endpoint name must be unique)
9. Once we create endpoint configuration, there is a bluepoint creating
10. Then we can test our model, which means serializing the data and sending to the endpoint
11. Use Lambda and API Getaway.



