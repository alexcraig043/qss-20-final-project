# QSS 20 Final Project

## Exploring Education Outcomes in Massachusetts

### Team Members

Alex Craig & Aaron Xie

### Project Summary

Our project hopes to explore the relationship between a multitude of factors with testing outcomes in the Massachussets school system. Some factors we wish to compare include expenditure per student, racial makeup, school district income level, school size, and more. We wish to identify the primary trends / indicators that point towards high performing schools and low performing schools, as well as clustering schools into various profiles. To accomplish this, we will analyze the publicly available [school data](https://www.doe.mass.edu/SchDistrictData.html), provided by the Massachusett's Department of Elementary and Secondary Education and [funding data](https://edunomicslab.org/nerds/) compiled by the _National Eduction Resource Database on Schools (NERDS)_.

### Project Directory

- [Memo](https://www.overleaf.com/read/hvfwqpmshnnk)
- [Data Cleaning & Merging](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/00_data_cleaning_merging.ipynb)
- [Initial Data Analysis](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/01_data_exploration.ipynb)
- [Output Figures](https://github.com/alexcraig043/qss-20-final-project/tree/main/src/output/figures)

### Project Notebook Scripts

- [00_data_cleaning_merging.ipynb](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/00_data_cleaning_merging.ipynb)

  - #### Functionality:

    This notebook cleans and merges all the necessary datasets that are needed for the analysis of Massachusetts public schools. All the datasets are merged based on the school and district names, and lowercase versions of the names are created for consistency. This cleaning process prepares the data for the main analysis and makes it easier to merge the datasets based on the school and district names.

  - #### Inputs:

    - NERDS Data: The NERDS contains revenue and expenditure data for Massachusetts school districts and individual schools for the year 2019.
    - MCAS Elementary and High School Data: MCAS (Massachusetts Comprehensive Assessment System) data is the standardized test used in Massachusetts for all grade levels through high school. Separate datasets are used for elementary and high school.
    - Enrollment and Demographic Data: This dataset contains information about student enrollment and demographic data.
    - Graduation Rates Data: This dataset contains information about graduation rates for Massachusetts schools.
    - Socio-Economic Status Data: This dataset contains information about the socio-economic status of students in Massachusetts schools.
    - Staff Demographics Data: This dataset contains information about the demographic of staff in Massachusetts schools.
    - Student to Teacher Ratio Data: This dataset contains information about the student to teacher ratio in Massachusetts schools.
    - Teacher Salaries Data: This dataset contains information about the salaries of teachers in Massachusetts schools.

  - #### Outputs:
    - `master_df`: The master dataframe that contains all the merged datasets. Each row is an individual school in Massachusetts.

- [01_data_exploration.ipynb](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/01_data_exploration.ipynb)

  - #### Functionality:

    This notebook first aims to identify which features have a correlation with school performance. A function named `make_scatter_plot` is defined which makes scatter plots of different features against the `avg_score` column. The function takes in the feature column name, the title for the plot, the x-axis label, and the dataframe. It then generates a scatter plot with a linear fit line, saves the plot as a PNG file in the output directory, and shows the plot. Scatter plots are made of the following features against the `avg_score` column:

    - Percent of Student Body Male
    - Percent of Student Body Asian
    - Percent of Student Body African American
    - Student to Teacher Ratio
    - Average Teacher Salary
    - Economically Disadvantaged % of School
    - First Language Not English % of School
    - State Funding Per Pupil
    - Federal Funding Per Pupil
    - Total Funding Per Pupil
    - Total State Funding
    - Total Federal Funding
    - Total Funding
    - Total Enrollment
    - Graduation Rate

    After the scatter plot section, several heat maps are generated to display the cross correlation between different features.

  - #### Inputs:

    - `master_df`: The master dataframe that contains all the merged datasets. Each row is an individual school in Massachusetts.

  - #### Outputs:

    - Scatter Plots: Scatter plots of different features against the `avg_score` column.
    - Heat Maps: Heat maps of the cross correlation between different features.

- [02_cluster_analysis.ipynb](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/02_cluster_analysis.ipynb)

  - #### Functionality:

    This notebook uses the KMeans clustering function from the sklearn.cluster library to identify "profiles" within the school dataset. We apply 2 - 6 clusters for a generalized dataset that includes financial, demographic, and enrollment data for each school. Next, we filter the dataset for high schools, and apply the KMeans clustering algorithm. Finally, we apply clustering to high income, high performing schools; high income, low performing schools; low income, low performing schools; and low income, high perfroming schools. To accomplish this, we write a generalized KMeans function called `kmeans_func`, which takes in two parameters: number of clusters and a dataframe. The function standardizes the data, applies the clustering algorithm, and labels each school in the dataframe to a cluster.

  - #### Inputs:

    - `master_df`: The master dataframe that contains all the merged datasets. Each row is an individual school in Massachusetts.

  - #### Outputs:
    Several Kmeans clustering models are generated and saved in the output directory. The models are named as follows:
    - All Schools - 2 Clusters
    - All Schools - 4 Clusters
    - All Schools - 6 Clusters
    - High Schools - 2 Clusters
    - High Schools - 4 Clusters
    - High Performing, High Income - 2 Clusters
    - High Performing, High Income - 4 Clusters
    - Low Performing, Low Income - 2 Clusters

- [03_model_prediction.ipynb](https://github.com/alexcraig043/qss-20-final-project/blob/main/src/code/03_model_prediction.ipynb)

  - #### Functionality:

    This notebook uses a Lasso and Ridge to try to accurate predict MCAS scores based on some of the features in the dataset. The features include financial, demographic, and enrollment data for each school. Once the two models are trained, their performance and metrics are compared. We find that they have similar performance and residual values, but their feature coefficients differ.

  - #### Inputs:

    - `master_df`: The master dataframe that contains all the merged datasets. Each row is an individual school in Massachusetts.

  - #### Outputs:
    - `lasso_model`: The Lasso model that was trained on the data.
    - `ridge_model`: The Ridge model that was trained on the data.
