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





