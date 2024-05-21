---
draft: false
title: "Machine learning model I"
snippet: "Model selection in machine learning is crucial for developing effective predictive systems. It involves exploring various algorithms, from linear regressions to more complex models like decision trees or neural networks, with the aim of striking a balance between model complexity and its ability to generalize patterns in the data. Exhaustive testing, cross-validation, and optimization techniques are used to select the model that produces the most accurate and reliable predictions for the sale price."
image: {
    src: "https://images.unsplash.com/photo-1511376777868-611b54f68947?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    alt: "data analysis"
}
publishDate: "2024-03-31 16:30"
category: "Article"
author: "Yitzhak Peña"
tags: [analysis, Linear regression, model]
---

<style>
        h2 { 
          font-size: 1.5em;  
          font-weight: bold;
          margin-bottom: 1em;
        }


        h3 {
          font-size: 1.2em;
          font-weight: bold;
          margin-bottom: 1em;
        }

        p {
          margin-bottom: 1em;
          text-align: justify;
        }

        li {
            margin-bottom: 1em;
        }

        img {
            margin: 4em auto;
        }
</style>

- Model selection in machine learning is crucial for developing effective predictive systems. It involves exploring various algorithms, from linear regressions to more complex models like decision trees or neural networks, with the aim of striking a balance between model complexity and its ability to generalize patterns in the data. Exhaustive testing, cross-validation, and optimization techniques are used to select the model that produces the most accurate and reliable predictions for the sale price.

- ## Objectives for estimation

The primary goal of utilizing a linear regression model in this context is to accurately predict the sale prices of real estate properties based on the dataset provided. This predictive capability can be highly beneficial for real estate agents, investors, and potential buyers by offering a reasonable estimate of a property's value grounded in its various characteristics. Moreover, by analyzing the relationships between a property's features and its sale price, valuable insights can be gained into which features have the most significant impact on sale prices. This understanding can help in enhancing a property's value strategically by focusing on the most influential features.

Before constructing the linear regression model, the dataset was meticulously analyzed and several filters were applied to ensure the data's quality and relevance. These filters included:
- **SaleCondition:** Normal Sale, exclude outliers such as family sales
- **Utilities:** All public utilities
- **PoolArea:** No pool
- **CentralAir:** Yes
- **SaleType:** WD = Conventional

By applying these filters, the goal was to refine the dataset to include only relevant and high-quality data. This preparation step is crucial for ensuring that the linear regression model accurately captures the significant relationships between the predictor variables (property features) and the response variable (sale price). Consequently, the model is better equipped to provide precise and generalizable predictions about real estate property values.

## About our initial model selection

A linear regression model has been selected as a starting point due to its simplicity and ease of interpretation. Since the goal is to predict  **Sale Prices**, a linear regression model provides a straightforward way to model the relationship between a property's features and its  **Sale Price**. Additionally, linear regression is easily interpretable, which means we can clearly understand how each feature contributes to the prediction of the **Sale Price**. When it's suspected that the relationship between the predictor variables and the response variable is approximately linear, the linear regression model is a natural choice. Although real relationships may not be strictly linear, the linear regression model can provide a good approximation in many cases.

## Our linear regression model
![Alt Text](../../assets/linear-regresion-model.png)
We select these variables to estimate the sale price because they represent key features of a property that are widely recognized to influence its value in the real estate market. 

1. **BsmtFinSF1:** type 1 finished square feet

2. **TotalBsmtSF:** total square feet of basement area

3. **GrLivArea:** above grade (ground) living area square feet

4. **OverallQual:** Rates the overall material and finish of the house

5. **GarageCars:** size of garage in car capacity


![Alt Text](../../assets/columns.png)

By including these variables in our regression model, we aim to capture the influence of these fundamental property characteristics on the sale price. This selection is based on common knowledge and empirical evidence in the real estate industry, suggesting that these factors are significant predictors of housing prices.

## Correlation heatmap 

The correlation heatmap, as evidenced earlier, is useful for identifying which variables are most correlated with the response variable. Additionally, by understanding the relationship between predictor variables and the response variable, it becomes possible to validate whether the linear regression model is suitable for the given dataset; if predictor variables have low correlation with the response variable, it may indicate that a linear regression model may not be the best option and that another modeling approach might be more appropriate.

In the case of BsmtFinSF1, there is a moderate positive correlation with the response variable SalePrice. However, this correlation suggests that when one variable increases, the other tends to increase, although not very strongly. This indicates that upon conducting a more detailed analysis, we might find that this variable may not have such a significant influence on the response variable.

![Alt Text](../../assets/correlation.png)

## Validation methods and employed metrics

**Validation Method**
- **·** The dataset is split into two subsets, one for training the model and the other for validation/testing. 
- **·** 70% of the data is used for training (`train_size=0.7`), and the remaining 30% is used for testing.
- **·** Random state is set to 15 (`random_state=15`) to ensure reproducibility.

**Metrics Employed**
- The `score()` method from the `LinearRegression` model is used to calculate the coefficient of determination (R^2 score) on the test data. This score indicates the proportion of the variance in the dependent variable (SalePrice) that is predictable from the independent variables (inputs).

**Predict values vs Real values**
![Alt Text](../../assets/plot.png)

## Preliminary conclusions derived from current analysis

Based on the obtained R^2 score of 0.8418, our preliminary analysis suggests that the linear regression model provides a robust framework for predicting property sale prices using the selected input features. This high coefficient of determination indicates that approximately 84.18% of the variability in sale prices can be explained by the included predictors, namely BsmtFinSF1, TotalBsmtSF, GrLivArea, OverallQual, and GarageCars. Such a strong performance underscores the significance of these features in determining property values. However, while the model demonstrates promising predictive capability, further examination is warranted to explore potential refinements and enhancements. This could involve assessing additional variables, exploring alternative modeling techniques, or conducting diagnostic assessments to ensure the model's assumptions hold. Overall, our preliminary findings suggest that the linear regression model is a valuable tool for understanding and predicting property sale prices, providing a foundation for further analysis and refinement.


<div class="flex justify-center mt-10">
<a href="https://colab.research.google.com/drive/1iByFQQvMtFCemksTe0-bHszYAgnriGTj?usp=sharing" class="inline-flex items-center px-5 py-2.5 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
            Google Colab
  <svg class="w-3.5 h-3.5 ms-2 rtl:rotate-180" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
</svg>
</a>
</div>
