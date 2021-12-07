# Categorizing amazon products

Amazon has a ton of products in various categories so the task is to create a classification model which can correctly classify the products category. 

## Dataset Schema 

|Id |title |description |url |category_id |created_at |

## Project sturcture

1. `Data_cleaning.ipynb`: It has the steps to first summarize the description and keep only the top 2 relevant sentences for the title, next data cleaning is implemented on the title and the summarized decription and the resulting dataframe is stored in a csv file which can be used for feature engineering and modeling, finally keyword extraction is implemented on the cleaned title and description and only the noun keyswords are kept and the resulting dataframe is stored in another csv file which can be used for feature engineering and modeling.

2. `Feature_eng_modeling_naive_approach.ipynb`: The dataset is highly imbalanced so to balance the data first the keywords of the title for the categories with less than 600 products are grouped together to create a document and cosine similarity is used to merge the closely related documents. The entire data is used for modeling purposes resulting in feeding a lot of features to the model and consequently a very high running time along with more memory usage and model overfitting the training data.

**Caution**: While training the model in this ipynb you might run into memory issues you can follow the steps for windows system -
    a. Press windows + x, click on system
    b. Navigate to 'Advanced system settings' in the right side, a system properties pop up will open
    c. In the 'advanced tab' click on settings, a performance options pop up will open
    d. In the 'advanced tab' click on change, a virtual memory pop up will open
    e. Deselect 'Automatically manage paging file size for all drives', select the drive on which the code is running and then click custom size
    f. Try to keep maximum size around 33000 MB for the code to run, click on set, ok and restart your system for the changes to take effect