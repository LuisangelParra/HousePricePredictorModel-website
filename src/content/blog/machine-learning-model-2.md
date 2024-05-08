---
draft: false
title: "Machine learning model II"
snippet: "At the forefront of artificial intelligence, neural networks are constantly redefining what's achievable. Today, we introduce a neural network architecture specifically designed to tackle the complex challenge of predicting house sale prices.  Traditionally, house price prediction relies on statistical models that struggle to capture the intricate relationships between numerous factors influencing market value."
image:
  {
    src: "https://images.unsplash.com/photo-1511376777868-611b54f68947?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
    alt: "data analysis",
  }
publishDate: "2024-03-31 16:30"
category: "Article"
author: "Luisangel Parra"
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
        }

        li {
          margin-bottom: 1em;
        }

        img {
          margin: 4em auto;
        }
</style>

At the forefront of artificial intelligence, neural networks are constantly redefining what's achievable. Today, we introduce a neural network architecture specifically designed to tackle the complex challenge of predicting house sale prices. Traditionally, house price prediction relies on statistical models that struggle to capture the intricate relationships between numerous factors influencing market value.

<div>
  <p>We define a list named inputs containing the following features:</p>
  <ul  class="list-disc list-inside">
    <li><b>TotalBsmtSF:</b> Total square footage of the basement area.</li>
    <li><b>GrLivArea:</b>  Above-ground living area square footage.</li>
    <li><b>OverallQual:</b> Overall quality grade (categorical variable).</li>
    <li><b>GarageCars:</b> Number of cars the garage can hold (categorical or numerical depending on how it's encoded).</li>
  </ul>
</div>

These features are chosen because they likely have a significant influence on a house's price. For example, larger living area and higher overall quality likely correspond to higher prices.

Also, we define a list named output containing a single element: SalePrice. This represents the target variable the MLP model is trying to predict - the selling price of the house.

![Alt Text](../../assets/table-input-output.png)

Multi-Layer Perceptron (MLP) regressor is chosen for this task. MLPs are a type of artificial neural network well-suited for regression problems like predicting real estate prices.

![Alt Text](../../assets/architecture.png)

### Hyperparameters:

<p>We define the following hyperparameters for the MLP model:</p>
<ul  class="list-disc list-inside">
  <li><b>Hidden layers:</b> Four hidden layers, each containing 10 nodes.</li>
  <li><b>Activation function:</b>  ReLU (Rectified Linear Unit) activation function.</li>
  <li><b>Regularization:</b> Alpha value of 0.05 (L1 regularization parameter).</li>
  <li><b>Training:</b> Maximum of 600 iterations.</li>
</ul>

## Let's take a look at the code!!!

```python
  scores_ = []
  for k in range(100):
    #Separar los datos en entrenamiento y validación (testing)
    Train, Test = train_test_split(data, test_size=0.3, random_state = k+1)
    mlp_ = MLPRegressor(hidden_layer_sizes=(10,10,10,10), activation='relu', alpha = 0.05, max_iter=600)
    mlp_.fit(Train[inputs], Train[output])
    scores_.append(mlp_.score(Test[inputs],Test[output]))
```

<p>This code performs a loop that trains and evaluates an MLP model 100 times.</p>

<ol class="list-decimal list-inside">
  <li><b>Initialization:</b>
    <ul  class="list-disc list-inside ml-4">
     <li>An empty list called <b>scores_</b> is created to store the evaluation scores of each model. </li>
    </ul>
  </li>
  <li><b>Data Splitting (K-Fold Simulation):</b>
    <ul  class="list-disc list-inside ml-4">
     <li>The loop iterates 100 times (represented by k).</li>
     <li>Inside the loop, the <b>train_test_split</b> function splits the entire data (<b>data</b>) into two sets: 
        <ul  class="list-disc list-inside ml-4">
          <li><b>Training set (Train):</b> This contains 70% of the data (default for <b>test_size=0.3</b>). This set is used to train the MLP model.</li>
          <li><b>Testing set (Test):</b> This contains the remaining 30% of the data. This set is used to evaluate how well the trained model performs on unseen data.</li>
        </ul>     
     </li>
     <li><b>random_state = k+1</b>  is used to shuffle the data differently in each iteration. This helps reduce the impact of the order in which data is presented to the model.</li>
    </ul>
  </li>
  <li><b>Model Creation and Training:</b>
    <ul  class="list-disc list-inside ml-4">
     <li>An MLP regressor model (<b>mlp_</b>) is created. The model (<b>mlp_</b>) is then trained using the training data (<b>Train[inputs], Train[output]</b>). </li>
    </ul>
  </li>
  <li><b>Model Evaluation:</b>
    <ul  class="list-disc list-inside ml-4">
     <li>After training, the model's performance is evaluated on the testing data (<b>Test[inputs], Test[output]</b>). The <b>mlp_.score</b> method used for evaluation might be employing a different metric, possibly the coefficient of determination (R-squared). R-squared ranges from 0 to 1, where a higher value (closer to 1) indicates a better fit between the predicted and actual selling prices.</li>
    </ul>
  </li>
  <li><b>Looping:</b>
    <ul  class="list-disc list-inside ml-4">
     <li>The loop iterates 99 more times, repeating steps 2-4 with different data splits due to the <b>random_state</b> variation.</li>
    </ul>
  </li>
  
</ol>

### Evaluation Metric:

<p>The 100 iterations are used to train 100 different MLP models with slightly different random weight initializations. This helps in:</p>
<ul  class="list-disc list-inside">
  <li><b>Reducing Overfitting: </b> By training multiple models with different starting points, the model is less likely to overfit to the specific training data and might generalize better to unseen data.</li>
  <li><b>Improving Generalizability:</b> Training with different weight initializations can explore different regions of the solution space, potentially leading to a more robust model.</li>
</ul>

### What the code must be doing:

<p>The code must be performing the following:</p>

<ol class="list-decimal list-inside ml-4">
  <li>Train 100 MLP models, each with the defined hyperparameters, but with different random weight initializations due to <b>random_state = k+1.</b></li>
  <li>For each model, evaluate its performance on the testing data using <b>mlp_.score</b> (which might be using R-squared or another metric).</li>
  <li>Store the evaluation scores (e.g., R-squared) in the <b>scores_ list.</b></li>
</ol>

### Later Analysis:

<p>After the loop completes, we might have 100 evaluation scores in <b>scores_.</b> You could then analyze these scores to:</p>
<ul  class="list-disc list-inside ml-4"">
  <li><b>Understand the model's variability:</b> See how much the performance varies across different model initializations.</li>
  <li><b>Select a "good" model:</b> Choose a model with a high evaluation score (e.g., R-squared) to represent your final model.</li>
</ul>

<div class="flex justify-center mt-10">
<a href="https://colab.research.google.com/drive/11M6GkYTUHQzPCFlJZEBNw1sCiE7yZdZ6?usp=sharing" class="inline-flex items-center px-5 py-2.5 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
            Google Colab
  <svg class="w-3.5 h-3.5 ms-2 rtl:rotate-180" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
</svg>
</a>
</div>
