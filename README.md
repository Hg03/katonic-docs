# From R-Scripts to Kubeflow Pipeline Using Katonic Studio

## 1. Get Started

Jupyter Notebook is a very popular tool that data scientists use every day to write their ML code, experiments, and visualize the results. However, when it comes to converting a Notebook to a Pipeline, data scientists struggle a lot. It is a very challenging, time-consuming task, and most of the time it needs the cooperation of several different subject-matter experts: Data Scientist, Machine Learning Engineer, Data Engineer.

A typical machine/deep learning pipeline begins as a series of preprocessing steps followed by experimentation/optimization and finally deployment. Each of these steps represents a challenge in the model development lifecycle. Katonic Studio provides a Pipeline Visual Editor for building AI pipelines from notebooks, Python scripts and R scripts, simplifying the conversion of multiple notebooks or scripts files into batch jobs or workflows.

This tutorial will guide you to use the Katonic Studio to assemble pipelines from R notebooks or scripts without the need for any coding.

### 1.1 Sign In

Once the admin creates your ID in the respective cluster, you will get your username and temporary password over the e-mail.

Open the login page,set your permanent password and login to try the Katonic platform.


Enter your email and password, and click on the **“Sign In”** button to sign in to the platform.

### 1.2 Orient yourself to the Katonic MLOps Platform

Once you are logged in, you will land to the Dashboard section of the Katonic Platform. You can use the left sidebar to navigate to other sections of the Katonic Platform.


1. To view the platform in full screen click on the **“full-screen mode“** on the top right of the page.

2. If you would like to search the Katonic documentation for help, click on the **“?”** icon on the top right of the page.

3. To send a question to a member of the Katonic support staff, use the Support button on the bottom right of the page.

### 1.3 Create a Workspace

1. Click on **Workspace** from the left sidebar and create your workspace by clicking on **‘Create Workspace’** in the top right side of the page.

2. Fill in the following information.

   **o** Give your Workspace an informative name (like iris-flower-classification).

     **Note** : Workspace name should contain only lowercase(a-z), numbers(0-9) and hyphen(-).

   **o** Select Environment as **JupyterLab**.

   **o** Select Image as **Katonic Studio**.

   **o** Select the type of Resources(eg. small,medium,large,xlarge,xxlarge) you want to allocate to the Workspace.

   **o** Click on the create button.
   
   
### 1.4 Start the Notebook

1. Once you create a workspace you could see it will be in **'Processing'** state.

2. The moment workspace reaches **'Running'** state, you will able to see the connect button. This will connect you to the notebook server.

3. When you click the connect button, your browser is automatically redirected to the Notebook UI.

4. Once your notebook is up and running, you will see a fresh Jupyter interface.

### 1.5 Configure Kubeflow Runtime

Runtime configuration can be listed, added, updated, duplicated and removed from the runtime panel.

#### 1.5.1 Accessing the Panel(Optional)

1. Click on **Runtime panel** from the Jupyterlab sidebar.

2. Click on the **‘+’** button on the top right.

3. Select **"New Kubeflow Pipelines runtime configuration"**.

4. Fill in all the details on the page.

5. Provide a runtime configuration display name, an optional description, and tag the configuration to make it more easily discoverable.

Fill in the Cloud Object Storage.Refer to the section **Cloud Object storage**.

Click on **SAVE & CLOSE** with the given configurations.

Save the runtime configuration. The new entry is displayed in the list.

#### 1.5.2 Cloud Object Storage

Go to the **File Manager** from the left panel.Click on the **Access token** ,generate access token and secret keys by clicking **Create Access Token**.

1. **Cloud Object Storage bucket name**

Name of the bucket you want to store pipeline artifacts in. Buckets can be shared-storage or your private bucket name.

2. **Cloud Object Storage username**

Username used to connect to the cloud Object Storage, credentials are required for the selected authentication type USER_CREDENTIALS and KUBERNETES_SECRET.
Give your generated access token as username.

3. **Cloud Object Storage password**

Password used to connect to the cloud Object Storage, credentials are required for the selected authentication type USER_CREDENTIALS and KUBERNETES_SECRET.
Give your generated secret key as password.

### 1.6 Configure Runtime Image

In this section, we can use the existing images or create a new custom image that will pull an already created image from your docker hub for easy access.

1. Click on the **“Runtime Images”** Icon in the left bar.

2. Click on the **“+”** button on the top right.

3. Fill in all the details on the page.

   **o Name**: User-friendly name that will appear under Runtime images list

   **o Description**(Optional) of the image. Small description defining your image

   **o Image Name**: Name of the image that you need from the docker hub.

**o Image Pull Policy**: Select an option from the dropdown.

4. Click on **“SAVE & CLOSE”** to save the image.

5. A list of additional images can be seen in the left panel

### 1.7 Get your Files and Data

You can either upload your code and data files to your notebook space, or you can clone from Github if you maintain a repository for your codes.

If you want to perform any development activity using R language then you either use the [Katonic's R-Studio Environment](https://docs.katonic.ai/Getting-started/Getting-Started-with-R-Studio) or Katonic's custom image [katonic-R-Julia](https://docs.katonic.ai/Getting-started/Getting-Started-with-R-Notebook) support as workspace. Follow the instructions provided in the respective documentation to access these development environments.

Once your scripts are ready on these environment, push the codes back to Github, so that they can be easily cloned to Katonic Studio workspace.

In this section, we will be showing you how can you clone data and files from our open-source R-Examples repository available on GitHub.

Click [here](https://github.com/katonic-dev/R-Examples.git) for Katonic use cases repository specifically for examples built on R-language.

1. Click on the **“Git”** icon on the left bar

2. Click on the **“Clone a Repository”** button available in the left panel. This will open up a window.

3. Enter the Clone [URI Link](https://github.com/katonic-dev/R-Examples.git) that is available in GitHub Repository.

4. Click on the **“clone”** button.

5. This process will clone the whole repository into the workspace.

6. Click on **“File Manager”** in the left bar.

7. Go to location “/R-Examples/iris_scripts”.

### Creating a Pipeline

A pipeline comprises one or more nodes that are (in many cases) connected with each other to define execution dependencies. Each node is implemented by a component and typically performs only a single task, such as loading data, processing data, training a model, evaluating models or prediction.

When you open the iris_flower_classification.pipeline file it will show you the created pipeline as below.

#### 1.8.1 How to create a pipeline

1. Open the Launcher (File > New Launcher or “+” in the top left) if it is not already open.

2. Open the pipeline editor to create a new untitled generic pipeline. Rename the pipeline to iris_flower_classification.

3. In the Visual Pipeline Editor open the properties panel on the right side. Select the Pipeline properties tab and fill in the pipeline details.

    **o Pipeline Name**: Name of the pipeline will appear here.

    **o Pipeline Runtime**: A generic pipeline comprises only of nodes that are implemented using generic components. This release includes three generic components that allow for execution of Jupyter notebooks, Python scripts, and R scripts.

    **o Pipeline Description**: An optional description summarizing the pipeline purpose.

    **o Object Storage Path Prefix**: For generic components, this path prefix is used when storing artifacts on Object Storage.

    **o Runtime Image**: As Runtime Image choose “R script”. The runtime image identifies the container image that is used to execute the notebook or R script when the pipeline is run on Kubeflow Pipelines or Apache Airflow. This setting must always be specified, but is ignored when you run the pipeline locally.

   **o Environment Variables**: If desired, you can customize additional inputs by defining environment variables.

   **o Data volumes**: Volumes to be mounted in all nodes. The specified volume Claims must exist in the Kubernetes namespace where the nodes are executed or the pipeline will not run.

4. Expand the component palette panel on the left-hand side. Note that there are multiple component entries, one for each supported file type.

5. Drag the R-script component entry onto the canvas (or double click on a palette entry) and hover over the node. The error messages are indicating that the node is not yet configured properly.

6. Select the newly added node on the canvas, right-click, and select Open Properties from the context menu.

7. Configure the node properties.

   **o Label**: Assign the node a descriptive label. If you leave the label empty, the file name will be used.

   **o Filename**: Browse to the file location. Navigate to the “/R-Examples/iris_scripts” directory and select “read_data.r”.

   **o Runtime Image**: As Runtime Image choose **“quay.io/katonic/common:r-base”**. This image will not be available in the dropdown. Follow the instructions from section 1.6 Configure Runtime Image above to add this image. Once the image is added you can refresh the page and this image name would appear in the dropdown.

``` The runtime image identifies the container image that is used to execute the notebook or R script when the pipeline is run on Kubeflow Pipelines. This setting must always be specified but is ignored when you run the pipeline locally.```

   **o CPU/GPU/RAM**: If the container requires a specific minimum amount of resources during execution, you can specify them.

   **o File Dependencies**: The read_data file does not have any input file dependencies. Leave the input field empty.

   **o Environment Variables**: If desired, you can customize additional inputs by defining environment variables.
   
   
8. For a component, you can comment from the comment button.

   **o** Select the component

   **o** Click on the comment button on the top
   
#### 1.8.2 How to connect components

Earlier in this tutorial, you added a (R script) file component to the canvas using the palette. You can also add Jupyter notebooks, Python scripts to the canvas by dragging and dropping from the JupyterLab File Browser.

1. From the JupyterLab File Browser drag and drop the “split data.r” notebook from location “/R-Examples/iris_scripts“ onto the canvas.

2. Customize the file's execution properties as follows:

**o Runtime image**: quay.io/katonic/common:r-base

**o Output files**: train.csv and validation.csv

3. Connect the output port of the read_data node to the input port of the split_data node to establish a dependency between the two scripts.

4. Save the pipeline.

#### 1.8.3 Iris Flower Classification Pipeline Flow

Earlier in the tutorial, we have how to create pipeline components and connect the components. In this section, we will see how the end-to-end iris flower classification pipeline is implemented.

1. Open "iris_flower_classification.pipeline” pre-build pipeline for iris flower classification use case.

2. When you double click on any of the components it will open the R script file.

3. In every component, you should read the output from the previous step and save the results of the current step.

4. **Read Data**: Read the iris dataset already available in R. Save the result in the iris.csv file

```python
# attach the iris dataset to the environment
data(iris)

# rename the dataset
dataset <- iris

colnames(dataset) <- c("Sepal.Length","Sepal.Width","Petal.Length","Petal.Width","Species")

write.csv(dataset,'iris.csv',row.names = FALSE)
```
5. **Split Data**: It reads the outfile file of read data script and after processing saves the results in train.csv and validation.csv files.

```python
install.packages("caret", dependencies=c("Depends", "Suggests"),repos = "http://cran.us.r-project.org")

install.packages("gower",repos = "http://cran.us.r-project.org")
install.packages("parallelly",repos = "http://cran.us.r-project.org")
install.packages("ModelMetrics",repos = "http://cran.us.r-project.org")
library(caret)

dataset<-read.csv("iris.csv")

# create a list of 80% of the rows in the original dataset we can use for training
validation_index <- createDataPartition(dataset$Species, p=0.80, list=FALSE)
# select 20% of the data for validation
validation <- dataset[-validation_index,]
# use the remaining 80% of data to training and testing the models
dataset <- dataset[validation_index,]

# dimensions of dataset
dim(dataset)

sapply(dataset, class)

head(dataset)
head(validation)

percentage <- prop.table(table(dataset$Species)) * 100
cbind(freq=table(dataset$Species), percentage=percentage)

# summarize attribute distributions
summary(dataset)

write.csv(dataset,'train.csv',row.names=FALSE)
write.csv(validation,'validation.csv',row.names=FALSE)

```

6. Similarly, other scripts also follows the same structure of reading the output file of previous scripts and saving the output of for downstream files.

7. Now pipeline is built and ready. Save the pipeline to run.

### 1.9 Run Pipeline

In the previous section, we have seen how the generic pipeline and iris flower classification pipeline is built. In this section, you will learn how to run a pipeline in the Kubeflow runtime environment.

1. Run pipeline from the button available on the top bar.

2. Enter pipeline name (eg: iris flower classification), select Runtime Platform as Kubeflow Runtime, and click on the **“OK”** button.

3. Pipeline is now submitted to Kubeflow environment. Click on **“OK”**.

4. The pipeline will run in the Kubeflow environment. You can see the pipeline in Pipeline section of the left panel of the platform.

5. Click on the **pipeline** to view the complete pipeline. The pipeline status is in Running stage. Once all the components ran successfully it will show a green tick on every component.

   **Note**: To view the pipeline clearly use “full screen mode" (button available on the top right).
   
6. Click on the component to see the logs and visualizations of the current step.

### 1.10 Schedule Pipeline

In the previous section, we have seen how to run the Kubeflow pipeline. In this section, you will learn how to schedule this pipeline or re-run the same pipeline again.

1. Go to Pipeline section and select **Runs** in the left sidebar.

2. Click on **“Create Run”** to run the pipeline or schedule the pipeline.

3. Click on **Choose** in the pipeline text box.

4. Select a pipeline that you want to run or schedule (Eg: iris flower classification). Click on the **“Use this pipeline”** button.

5. Give a new Run Name (Eg: iris_flower_classification_scheduling). Also choose the respective experiment name under which you want to perform your run.

6. The pipeline can be run in two ways i.e., run once or schedule

   **o Run Once**: Select Run Type as One-off radio button and click on start to run the pipeline.
   
   **o Scheduling**: Select Run Type as Recurring.
   
   **o Trigger Type**: Select if the pipeline should run as a Periodic or cron Job.
   **o Maximum Concurrent Runs**: limit the number of runs launched in parallel
   **o Start Date and End Date**: Give the start and end date of the scheduler (Optional)
   **o Catchup**: Specify how many runs every minute/hour/day/week/month.
   
7. Scheduled runs can be seen here in the experiments.

8. Click on manage to enable or disable the scheduler.

9. Click on run to check the schedule configurations.


