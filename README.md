# Categorizing amazon products

Amazon has a ton of products in various categories so the task is to create a classification model which can correctly classify the products category. 

## Dataset Schema 

|Id |title |description |url |category_id |created_at |

| | | | | | |

## Project sturcture

1. `Data_cleaning.ipynb`: It has the steps to first summarize the description and keep only the top 2 relevant sentences for the title, next data cleaning is implemented on the title and the summarized decription and the resulting dataframe is stored in a csv file which can be used for feature engineering and modeling, finally keyword extraction is implemented on the cleaned title and description and only the noun keyswords are kept and the resulting dataframe is stored in another csv file which can be used for feature engineering and modeling.

2. `Modeling_naive_approach.ipynb`: The dataset is highly imbalanced so to balance the data first the keywords of the title for the categories with less than 600 products are grouped together to create a document and cosine similarity is used to merge the closely related documents. The entire data is used for modeling purposes resulting in feeding a lot of features to the model and consequently a very high running time along with more memory usage and model overfitting the training data.

3. `Modeling_keywords_naive_approach.ipynb`: The major difference between this and `Modeling_naive_approach.ipynb` is that in this file i am using keywords that are **Nouns** instead of the entire sentences.

4. `Cosine_similarity_keywords.ipynb`: The major difference between this and `Modeling_keywords_naive_approach.ipynb` is that in this file the threshold of 600 products is changed to 800 products. While performing cosine similarity i have added a threshold for remapping i.e. if the max is not more than 0.35 then it would not change the mapping to a different category. I have also tweaked with the parameters in TD-IDF part to reduce the size of the matrix being fed to the model. Parameters in the models are also tuned to reduce the amount of overfitting which is present in 2nd and 3rd ipynb.

5. `Topic_modeling_keywords.ipynb`: The major difference between this and `Cosine_similarity_keywords.ipynb` is that in this file instead of using cosine similarity to perform feature engineering to merge categories, i implemented Latent Dirichlet Allocation (LDA) with a threshold of 0.5.

P.S. - I tried implementing Linear Discriminant Analysis for dimensionality reduction in 4th and 5th ipynb but it gave very poor results.

**Caution**: While training the model in 2nd and 3rd ipynb you might run into memory issues to rectify them you can follow the steps for windows system -

    a. Press windows + x, click on system

    b. Navigate to 'Advanced system settings' in the right side, a system properties pop up will open

    c. In the 'advanced tab' click on settings, a performance options pop up will open

    d. In the 'advanced tab' click on change, a virtual memory pop up will open

    e. Deselect 'Automatically manage paging file size for all drives', select the drive on which the code is running and then click custom size
    
    f. Try to keep maximum size around 33000 MB for the code to run, click on set, ok and restart your system for the changes to take effect