# fifa21-data-cleaning

## FIFA21 Players Database

A FIFA21 Players Database built from the players' in-game data extracted from https://sofifa.com/players
## Data Extraction

The data is included in this repo.

To get the latest data, run the following script for extracting the data:

cd source_datasets
python fifa21_data_crawler.py

## Data Preprocessing

cd data_preprocessing_script

python process_fifa21_data.py # preprocess players' data
python language_process.py # preprocess country-language data

This will generate the csv files under cleaned_tables

## Summary

In this project, my goal is to showcase the Data Mining and Preprocessing techniques I have spent the last several months researching and practicing and put them to use. I use the FIFA 21 dataset which is found on Kaggle. I use both Python (Jupyter Notebook) and R in my analysis.

Data Preprocessing is an integral step that took up about 60% of the time in this project. It started with dropping problematic variables, and lead to some functional data cleaning of object types to numeric. This was done on 'Wage', 'Value', 'Height' and 'Weight' variables (ie. object type '€625K' cleaned to be numerical 625000). Once Wage and Value were cleaned, I found that there were 0's in place for some observations. I cross validate this with sofifa.com (where the data comes from), and it turns out the website just doesn't yet have data on those players. Essentially, every '0' in place for 'Value' overlaps with that of 'Wage', so we drop observations relative to Wage = 0, and that takes care of the Data Cleaning.

Feature Engineering is composed of two parts:

    Creating variables that connote the general position of a player relative to their Best Position (BP).
    Creating a variable for BMI (body mass index) with the given 'Height' and 'Weight' observations for each player.

Data Normalization is done in two steps:

    Min-Max Normalization of the accompanying variables alongside our target variable, 'Value'.
    'Value' is un-normally distributed (skewed to the right), so to combat this a Log-Normalization was applied to 'Value'.

I begin modeling with a Principal Component Analysis of the data. I then perform K-Means clustering on two PCA dimensions which leads me to some very interesting discoveries upon which I elaborate further in the results section.

In terms of predictive modeling, my target variable in this project is 'Value', which is the monetary worth of a player given their attributes. Predicting 'Value' can lead us further into more detailed player analysis that can potentially help us capitalize on stars, current or future. I choose Linear Regression, Random Forest Regression and Neural Network to predict 'Value' in this project.

## Configuration

Everything is configured via the user interface.

To add a player, retrieve their Futbin (insert link) URL and click Add Player. The bot will automatically open the Futbin link and retrieve the data, which will populate in the table.

The maximum bid ceiling is hard set to 85%, and will be customizeable in a later update. The sell price is 95% of market price.

## Demo

Some demos on example interactions can be found in the following files:

    load_data_demo.txt
    simple_demo.txt
    simple_demo2.txt
    run_queries_demo.txt
