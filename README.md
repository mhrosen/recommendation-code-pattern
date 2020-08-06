# Create a Recommendation System Using Watson Studio and Connecting to NodeJS 
IBM Developer code pattern, not yet published on [developer.ibm.com](https://developer.ibm.com/). IBM owns this in-process publication, all of the code is OpenSource

In this code pattern, fake travel transaction data for car rentals and hotels are used to build recommendation engines with SparkML and Watson Machine Learning. The model is used to create a list of recommendations for customers based on how soon before a trip they plan to book a trip and their hotel or car rental preferences on the IBM demo travel application Bee Travels. The hotel and car rental data is called from a PostgresSQL database as a data asset on Watson Studio. The code pattern incorporates the recommendation service into a node.js application, containerizes the application with Docker, and deploys the Docker image onto Kubernetes. For more information about how the data is generated or how this microservice is part of the full Bee Travels platform, please visit the [Bee Travels Github](https://github.com/bee-travels/). 

When you have completed this code pattern, you will understand how to:
    - Navigate IBM Cloud Pak for Data
    - Use Jupyter Notebooks in IBM Watson Studio
    - Gather data from PostgresSQL database to use in Watson Machine Learning Notebook
    - Build a k-means recommendation model with SparkML and Watson Machine Learning to provide hotel or car rental collaborative recommendations for travelers based on travel dates and priorities similar to previous customers that made transactions
    - Upload node.js docker image to Docker Hub
    - Deploy the Docker image on Kubernetes
    
The intended audience is data scientists and developers interested in building, deploying and testing machine learning models from a Jupyter notebook with Watson Machine Learning and wrapping it in a node.js application.

# Architecture
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image1.jpeg)

1. The functionality of the booking site that the User interacts with is handled by NodeJS service where the API calls are initialized.
2. The NodeJS app gets Watson Studio Machine Learning to compute the user’s preference.
3. Watson Studio gets previous transaction data on the individual and other users from PostgresSQL
4. PostgresSQL grabs many unstructured data points from the Data Object Storage service
5. Jupyter Notebook gets the data into CSV format and processes it into usable format
6. SparkML parallelizes data computation jobs with machine learning processes to find the customer’s cluster
7. The recommendation system gets representative recommendations for the customer from their cluster pairing

# Steps
 ## 1. Clone the repo locally
`cd` into the folder you wish to store this code pattern. In the terminal type:
    ```git clone https://github.com/IBM/)<my repo> ```
 ## 2. Go to [cloud.ibm.com](cloud.ibm.com)
 ## 3. Set up Watson Studio 
   a. Select Region and a pricing plan
   b. Press “Create” on the right panel
 ## 4. Establish Credentials
   a. Click “Manage”, “Access (IAM)” in the upper panel
   ![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image2.jpeg)

   b. Click in the ![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image%208-2-20%20at%2011.05%20PM.jpeg) upper left and “API keys”
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image4.jpeg)
   
   c. Click “Create an API Key”, give it a name and description
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image5.jpeg)
    
   d. Download the API key JSON and store it in the ```data-generator/src/recommender/``` folder for safe keeping
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image6.jpeg)

 ## 5. Launch your service
   a. Navigate to the IBM Dashboard by clicking the ![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image%208-2-20%20at%2011.05%20PM.jpeg) in the upper left
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image7.jpeg)

  b. Open the Services tab, search the name of your Watson Studio service, and click on it
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image8.jpeg)

  
  c. Click on Access Watson Studio. This should launch IBM Cloud Pak for Data
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image9.jpeg)

# 6. Choose a Cloud Object Storage 
  a. Click “Create a service”
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image10.jpeg)
  
  b. Search Cloud Object Storage
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image11.jpeg)
  
  c. Choose a plan, set “Select a resource group” to default, and click “Create”
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image12.jpeg)

# 7. Create a project
  a. Navigate to [the home page](https://dataplatform.cloud.ibm.com/home2?context=cpdaas) by clicking “IBM Cloud Pak for Data” in the upper-left corner. On the page select “Create a project”

  
  b. Select “Create an empty project”
  ![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image13.jpeg)
  
  c. Choose a name, description and Define storage
 (under Define storage click “Add” and navigate to existing tab then “Select”)
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image14.jpeg)

  d. Select “Create”

# 8. Load Jupyter Notebooks into Watson Studio Project
  a. On the [Cloud Pak for Data homepage](https://dataplatform.cloud.ibm.com/home2?context=cpdaas), under Overview and Recent Projects select the project you just created
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image15.jpeg)


  b. Click “Add to Project”
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image16.jpeg)


  c. Select “Notebook”
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image17.jpeg)


  d. Click the “From file” tab, Drag and drop or upload HOTEL_recommender.ipynb from ./data-generator/src/recommender/ folder. Select <ins>Spark 2.3 & Python 3.6 Driver</ins>. Click Create
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image18.jpeg)

<p><b>****Warning:</b>  selections other than Spark <ins><b>2.3</b></ins> & Python 3.6 will not work.****</p>


# 9. Go back thru step 8 to likewise add CAR_recommender.ipynb as a new notebook to your project

# 10. Run the HOTEL_recommender.ipynb
  a. Click on your project’s title on the top left of the page, select the assets tab, and open the notebook
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image19.jpeg)


  b. Click on the pencil in the upper right toolbar to edit
![alt text](https://github.com/mhrosen/recommendation-code-pattern/blob/master/Images-for-ReadMe/Image20.jpeg)

  c. To run Jupyter Notebook, press shift-enter on each tab
  
  # 11. When you are finished with the hotel notebook, try the car recommendation service as well by repeating step 10
  
  # 12. Further instructions will be available within each Notebook
  
  ## License
  This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).
