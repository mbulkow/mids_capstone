# <img src="./dysarthrai-website/src/images/favicon.png" width="100"> &nbsp; DysarthrAI

### A Voice for All: Deep Learning Communication Assistant for People with Dysarthric Speech

#### Simon Hodgkinson, Michael Powers, Rich Ung

### Project Deliverable

* #### [Website](https://dysarthrai.com/)

### Table of Contents

1. [About](#about)
1. [Datasets](#datasets)
1. [Model Generation](#model-generation)
1. [Final Model](#final-model)
1. [Website App Implementation](#website-app-implementation)
1. [Resources](#resources)
1. [Contact Us](#contact-us)
1. [Appendix](#appendix)

### About

Our mission is to improve the communication abilities of people with dysarthric speech. Dysarthria is a condition where muscles used for speech are weak and hard to control, resulting in slurred or slow speech that can be difficult to understand. Common causes of dysarthria include neurological disorders such as stroke, brain injury, brain tumors, and conditions that cause facial paralysis or tongue or throat muscle weakness.

Our application, DysarthrAI, is a communication assistant for people with dysarthric speech. It enables these individuals to communicate phrases to others, regardless of their vocal disabilities. The speaker-dependent model requires the user to store phrases they wish to communicate in the future, along with translations of those phrases. Once a phrase is saved, the user can speak the phrase into the app which will use our algorithm to provide a clear audio translation using text to speech.Our application, DysarthrAI, is a communication assistant for people with dysarthric speech. It enables these individuals to communicate phrases to others, regardless of their vocal disabilities. The speaker-dependent model requires the user to store phrases they wish to communicate in the future, along with translations of those phrases. Once a phrase is saved, the user can speak the phrase into the app which will use our algorithm to provide a clear audio translation using text to speech.

### Datasets

We mainly used the TORGO dataset located [here](http://www.cs.toronto.edu/~complingweb/data/TORGO/torgo.html).

The TORGO data is downloaded and unzipped to data/TORGO. This folder contains 8 folders, one for each person ("F01", "F03", etc.) - 3 females and 5 males. However, these directories are also added to the .gitignore file because they are also very large and would take up too much space within our repository.

### Model Generation

### Final Model

Our final model is located [here](./models/dtw_dysarthric_speech_all-FINAL.ipynb)

### Website App Implementation

The website was created through various services from AWS:
![Website App Architecture](./assets/web_architecture.png)

#### Backend for Model

The [final model](./models/dtw_dysarthric_speech_all-FINAL.ipynb) that we've developed was implemented into a Docker container running a Flask application. This Flask application gathers the data from S3, runs the model, and updates the results in DynamoDB. Since Flask is written in Python, implementing the final model within our app became easier using Flask and Docker. The Docker container is then deployed to Fargate, which allows us to run containers in the cloud without managing the infrastructure.

#### Frontend Website

The frontend website is built using React, which is a javascript framework that helps build interactive applications. This website is then deployed to S3, which Route53 and Cloudfront use to direct users whenever they access *dysarthrai.com*. This frontend website then uses S3 to upload, store, and manage audio files, DynamoDB to find and update audio labels, and Docker/Fargate to run the model that we've developed over the past couple of weeks.

### Resources

* [Link to Planning Google Doc](https://docs.google.com/document/d/1TVl2XQT2vtzYGe07BVmdoNZk0fiAlElBSvRJIO_-4u4/edit#)
* Presentations
  * [Presentation 1](https://docs.google.com/presentation/d/1NoQqhUkKJXRUU2JuhEzIH_LCEC_Ro_iMn56PxdU_Ie4/edit?usp=sharing)
  * [Presentation 2](https://docs.google.com/presentation/d/1oac-m1yD7Rrx0pIOM2_rAOaKrlOFsfEPtlV-CWo0OVI/edit?usp=sharing)
  * [Presentation 3](https://docs.google.com/presentation/d/1ISPXifDLj0iRdMZYYinSMcSSmrMuGREpaNuP8lE0lQ4/edit?usp=sharing)

### Contact Us

Feel free to contact any of the team members below if you have any additional questions:

* [Simon Hodgkinson](https://www.linkedin.com/in/simon-hodgkinson/)
* [Michael Powers](https://www.linkedin.com/in/michael-powers-0552204b/)
* [Rich Ung](https://www.linkedin.com/in/ungrich/)

### Appendix

#### Loading Environment

Run the following command within the base directory of this repository to **build** the notebook Docker environment for this project:
```
docker build -t w210/capstone:1.0 .
```

Run the following command within the base directory of this repository to **run** the notebook Docker environment for this project:
```
docker run --rm -p 8888:8888 -p 6006:6006 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work w210/capstone:1.0
```
