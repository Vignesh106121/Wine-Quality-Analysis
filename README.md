
# Wine Quality Analysis

This project aims to analyze the factors that affect the quality of wine, using a dataset of red and white wine samples. We will explore the relationships between various chemical properties of the wines and their quality ratings.

## Table of Contents
1. [Introduction](#introduction)
2. [Dataset](#dataset)
3. [Analysis Steps](#analysis-steps)
    - [Do wines with higher alcoholic content receive better ratings?](#do-wines-with-higher-alcoholic-content-receive-better-ratings)
    - [Do sweeter wines receive higher ratings?](#do-sweeter-wines-receive-higher-ratings)
    - [What level of acidity receives the highest average rating?](#what-level-of-acidity-receives-the-highest-average-rating)
4. [Conclusion](#conclusion)
5. [Visualizations](#visualizations)

## Introduction
Wine quality is influenced by a variety of chemical properties, and understanding these relationships can help winemakers improve their products. This project investigates how alcohol content, residual sugar, and acidity levels correlate with wine quality ratings.

## Dataset
The dataset used in this analysis is `wine_quality.csv`, which contains 6497 samples of red and white wines with 14 attributes:
- Fixed acidity
- Volatile acidity
- Citric acid
- Residual sugar
- Chlorides
- Free sulfur dioxide
- Total sulfur dioxide
- Density
- pH
- Sulphates
- Alcohol
- Quality (rating from 0 to 10)
- Color (red/white)
- Acidity levels (categorized as High, Moderately High, Medium, Low)

## Analysis Steps

### Do wines with higher alcoholic content receive better ratings?
1. **Objective**: Determine if wines with higher alcohol content have higher quality ratings.
2. **Method**: 
   - Calculate the median alcohol content.
   - Divide the dataset into two groups: low alcohol (< median) and high alcohol (≥ median).
   - Compute the mean quality rating for each group.
   - Create a bar chart to visualize the average quality ratings for low and high alcohol content wines.
3. **Code**:
    ```python
    import matplotlib.pyplot as plt
    import pandas as pd

    df = pd.read_csv('wine_quality.csv')

    median = df['alcohol'].median()
    low = df.query('alcohol < {}'.format(median))
    high = df.query('alcohol >= {}'.format(median))

    mean_quality_low = low['quality'].mean()
    mean_quality_high = high['quality'].mean()

    locations = [1, 2]
    heights = [mean_quality_low, mean_quality_high]
    labels = ['Low', 'High']
    plt.bar(locations, heights, tick_label=labels)
    plt.title('Average Quality Ratings by Alcohol Content')
    plt.xlabel('Alcohol Content')
    plt.ylabel('Average Quality Rating')
    plt.show()
    ```

### Do sweeter wines receive higher ratings?
1. **Objective**: Determine if sweeter wines (higher residual sugar) receive higher quality ratings.
2. **Method**: 
   - Calculate the median residual sugar content.
   - Divide the dataset into two groups: low sugar (< median) and high sugar (≥ median).
   - Compute the mean quality rating for each group.
   - Create a bar chart to visualize the average quality ratings for low and high sugar content wines.
3. **Code**:
    ```python
    median_sugar = df['residual_sugar'].median()
    low_sugar = df.query('residual_sugar < {}'.format(median_sugar))
    high_sugar = df.query('residual_sugar >= {}'.format(median_sugar))

    low_sugar_mean_quality = low_sugar['quality'].mean()
    high_sugar_mean_quality = high_sugar['quality'].mean()

    locations_sugar = [1, 2]
    points = [low_sugar_mean_quality, high_sugar_mean_quality]
    labels_sugar = ['Low', 'High']
    plt.bar(locations_sugar, points, tick_label=labels_sugar)
    plt.title('Wine Quality for Sugar Content')
    plt.xlabel('Sugar Content')
    plt.ylabel('Mean Quality Rating')
    plt.show()
    ```

### What level of acidity receives the highest average rating?
1. **Objective**: Determine which level of acidity is associated with the highest average wine quality rating.
2. **Method**: 
   - Bin the pH values into four categories: High, Moderately High, Medium, and Low.
   - Compute the mean quality rating for each acidity level.
   - Create a bar chart to visualize the average quality ratings for each acidity level.
   - Create a scatter plot to compare the average quality ratings across different acidity levels.
3. **Code**:
    ```python
    bin_edges = [2.72, 3.11, 3.21, 3.32, 4.01]
    bin_names = ['High', 'Moderately High', 'Medium', 'Low']
    df['acidity_levels'] = pd.cut(df['pH'], bin_edges, labels=bin_names)

    quality_acidity_mean = df.groupby('acidity_levels').mean()['quality']

    locations_pH = [1, 2, 3, 4]
    plt.bar(locations_pH, quality_acidity_mean, tick_label=bin_names)
    plt.title('Acidity vs Quality')
    plt.xlabel('Acidity')
    plt.ylabel('Quality')
    plt.show()

    acidity_mean = df.groupby('acidity_levels').mean()['pH']
    plt.scatter(y=quality_acidity_mean, x=acidity_mean)
    plt.xlabel('Average Acidity')
    plt.ylabel('Average Quality')
    plt.title('Quality vs Acidity')
    plt.show()
    ```

## Conclusion
The analysis revealed the following:
- Wines with higher alcohol content tend to receive better ratings.
- Sweeter wines (with higher residual sugar) do not necessarily receive higher ratings.
- Wines with lower acidity levels tend to receive slightly higher average ratings, but the differences are minimal.

## Visualizations
Sure, here are the topics of each visualization without the code:

1. **Average Quality Ratings by Alcohol Content**
   - Determine if wines with higher alcohol content receive better ratings.
   - Calculate the median alcohol content and divide the dataset into low and high alcohol groups.
   - Compute the mean quality rating for each group.
   - Create a bar chart to visualize the average quality ratings for low and high alcohol content wines.

2. **Wine Quality for Sugar Content**
   - Determine if sweeter wines (higher residual sugar) receive higher ratings.
   - Calculate the median residual sugar content and divide the dataset into low and high sugar groups.
   - Compute the mean quality rating for each group.
   - Create a bar chart to visualize the average quality ratings for low and high sugar content wines.

3. **Acidity vs Quality**
   - Determine which level of acidity is associated with the highest average wine quality rating.
   - Bin the pH values into four categories: High, Moderately High, Medium, and Low.
   - Compute the mean quality rating for each acidity level.
   - Create a bar chart to visualize the average quality ratings for each acidity level.

4. **Quality vs Acidity (Scatter Plot)**
   - Compare the average quality ratings across different acidity levels.
   - Compute the mean pH value for each acidity level.
   - Create a scatter plot to visualize the relationship between acidity levels and quality ratings.
