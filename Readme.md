# Sales Conversion Optimization Project 📈

# Table of Contents 📑

1. [Project Description](#project-description) 📝
2. [Project Structure](#project-structure) 🏗️
3. [Train Pipeline](#train-pipeline) 🚂
4. [Continuous Integration Pipeline](#continuous-integration-pipeline) 🔁
5. [Email Report](#email-report) 📧
6. [Prediction App](#prediction-app) 🎯
7. [Neptune Integration](#neptune-integration) 🌊
8. [Necessary Installations](#necessary-installations) ⚙️
9. [Running the Project](#running-the-project) 🚀


# Project Description 🚀

Welcome to the Sales Conversion Optimization Project! 📈 This project focuses on enhancing sales conversion rates through meticulous data handling and efficient model training. The goal is to optimize conversions using a structured pipeline and predictive modeling.

We've structured this project to streamline the process from data ingestion and cleaning to model training and evaluation. With an aim to empower efficient decision-making, our pipelines incorporate quality validation tests, drift analysis, and rigorous model performance evaluations.

This project aims to streamline your sales conversion process, providing insights and predictions to drive impactful business decisions! 📊✨


# Project Structure 🏗️

Let's dive into the project structure! 📁 Here's a breakdown of the directory:

- **steps Folder 📂**
  - ingest_data
  - clean_data
  - train_model
  - evaluation
  - production_batch_data
  - predict_prod_data

- **src Folder 📁**
  - clean_data
  - train_models

- **pipelines Folder 📂**
  - training_pipeline
  - continuous_integration

- **models Folder 📁**
  - saved best H20.AI model

- **reports Folder 📂**
  - Failed HTML Evidently.ai reports

- **production data Folder 📁**
  - Production batch dataset

- **Other Files 📄**
  - requirements.txt
  - run_pipeline.py
  - ci-cd.py

This organized structure ensures a clear separation of concerns and smooth pipeline execution. 🚀

# Necessary Installations 🛠️

To ensure the smooth functioning of this project, several installations are required:

1. Clone this repository to your local machine.

    ```bash
    git clone https://github.com/VishalKumar-S/Sales_Conversion_Optimization_MLOps_Project
    cd Sales_Conversion_Optimization_MLOps_Project
    ```

2. Install the necessary Python packages.

    ```bash
    pip install -r requirements.txt
    ```

3. ZenML Integration 

    ```bash
    pip install zenml["server"]
    zenml init      #to initialise the ZeenML repository
    zenml up    
    ```

4. Neptune Integration

    ```bash
    zenml experiment-tracker register neptune_experiment_tracker --flavor=neptune \
    --project="$NEPTUNE_PROJECT" --api_token="$NEPTUNE_API_TOKEN"

    zenml stack register neptune_stack \
    -a default \
    -o default \
    -e neptune_experiment_tracker \
    --set
    ```
Make sure to install these dependencies to execute the project functionalities seamlessly! 🌟
![Neptune.ai integration with ZenML](assets/zenml_dashbaord_stack.PNG)


# Train Pipeline 🚂

In this pipeline, we embark on a journey through various steps to train our models! 🛤️ Here's the process breakdown:

1. **run_pipeline.py**: Initiates the training pipeline.
2. **steps/ingest_Data**: Ingests the data, sending it to the data_validation step.
3. **data_validation step**: Conducts validation tests and transforms values.
4. **steps/clean_Data**: Carries out data preprocessing logics.
5. **data_Drift_validation step**: Conducts data drift tests.
6. **steps/train_model.py**: Utilizes h2o.ai AUTOML for model selection.
7. **src/train_models.py**: Implements the best model on the cleaned dataset.
8. **model_performance_Evaluation.py**: Assesses model performance on a split dataset.
9. **steps/email_report.py**: Here, if any of teh validation test suites, didn't meet the threshold condition, email will be sent to the user, along with the failed Evidently.AI generated HTML reports.

Each step is crucial in refining and validating our model. All aboard the train pipeline! 🌟🚆

![Training Pipeline](assets/train_pipeline_dashboard.PNG)


# Continuous Integration Pipeline ⚙️

The continuous integration pipeline focuses on the production environment and streamlined processes for deployment. 🔄

Here's how it flows:

1. **ci-cd.py**: Triggered to initiate the CI/CD pipeline.
2. **steps/production_batch_data**: Accesses production batch data from the Production_data folder
3. **pipelines/continuous_integration.py**: As we already discussed earlier, we conduct Data Quality, Data Drift as previously we did, if threshold fails, email reports are sent.
4. **steps/predict_production_Data.py**: Utilizes the pre-trained best model to make predictions on new production data. Then, we conduct Model Performance validation as previously we did, if threshold fails, email reports are sent.

This pipeline is crucial for maintaining a continuous and reliable deployment process. 🔁✨

![Continuous Integration Pipeline](assets/continuous_integraion_pipeline_Zenml_dashboard.PNG)

## Email Reports 📧

In our project, email reports are a vital part of the pipeline to notify users when certain tests fail. These reports are triggered by specific conditions during the pipeline execution. Here's how it works:

### E-mail Details

Upon data quality or data drift test or model performance validation tests failures, an email is generated detailing:

- Number of total tests performed.
- Number of passed and failed tests.
- Failed test reports attached in HTML format.


### Integration with Pipeline Steps

This email functionality is integrated into the pipeline steps via Python scripts (`steps/email_report.py`). If a particular test threshold fails, the execution pauses and an email is dispatched. Successful test completions proceed to the next step in the pipeline.

This notification system helps ensure the integrity and reliability of the data processing and model performance at each stage of the pipeline.

![Data Quality e-mail report](assets/data_quality_test_EMAIl.PNG)
![Data Drift e-mail report](assets/data_Drift_email.PNG)
![Model Performance e-mail report](assets/model_performace_email.PNG)


# Prediction App 🚀

The Prediction App is the user-facing interface that leverages the trained models to make predictions based on user input. 🎯
To run the streamlit application,
    ```bash
    streamlit run app.py
    ```

### Functionality:
- **Streamlit Application**: Utilizes Streamlit to create a user-friendly interface.
- **User Input Fields**: Allows users to input various parameters for prediction.
- **Prediction**: Generates predictions based on the provided inputs.
- **Redirect to Neptune.ai**: Offers a direct link to explore model metrics on Neptune.ai.

This application provides an intuitive interface for users to make predictions and explore model metrics effortlessly. 📊✨

### Docker Configuration 🐳

Docker is an essential tool for packaging and distributing applications. Here's how to set up and use Docker for this project:

**Running the Docker Container:** Follow these steps to build the Docker image and run a container:

    ```bash
    docker build -t my-streamlit-app .
    docker run -p 8501:8501 my-streamlit-app
    ```

3. **Best Practices:** Consider best practices such as data volume management, security, and image optimization.

## GitHub Actions 🛠️

- Configured CI/CD workflow for automated execution



# Running the Project 🚀

Follow these steps to run different components of the project:

1. **Training Pipeline**:
   - To initiate the training pipeline, execute 
        ```bash
    python run_pipeline.py
        ```

2. **Continuous Integration Pipeline**:
   - To execute the CI/CD pipeline for continuous integration, run
   ```bash
   python run_ci_cd.py
   ```

3. **Streamlit Application**:
   - Start the Streamlit app to access the prediction interface using,
    ```bash
   streamlit run app.py
   ```

Each command triggers a specific part of the project. Ensure dependencies are installed before executing these commands. Happy running! 🏃‍♂️✨





