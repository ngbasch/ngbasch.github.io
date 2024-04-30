---
layout: post
title:  "Interactive Tidymodels Report"
date:   2024-04-25
---
<img src="{{ site.baseurl }}/images/pic03.jpg">
I created an extensible [report](https://github.com/ngbasch/model-report) that allows users to provide basic modeling information (e.g., input data, a model "recipe", etc.) and produce an easy-to-navigate report containing data visualizations and model performance.

The report is built using R Markdown based on the [Tidymodels](https://www.tidymodels.org/) package. The Tidymodels framework leverages a few different different packages to create [workflows](https://workflows.tidymodels.org/) that make it easier to split a model into its core pre-processing, modeling, post-processing steps. Additionally, [workflowsets](https://workflowsets.tidymodels.org/) make it easy to create and fit multiple workflows based on different workflows. Together, I combine the extensibility of tidymodels with R Markdown to generate customizable html documents that outline model data, steps, and performance. An illustrative example of the report was run on R's `iris` dataset, and can be explored <a href="{{ site.baseurl }}/240204_local.html">here</a>.

## Why I built this
I was motivated to build this report for a few reasons:
1. **Lower setup time**: as a useful starting point to the iterative modeling process, it can be helpful to quickly run a model and get some basic insights on performance (e.g., distributions of features, main drivers of the model, etc.). However, in developing my own "first pass" of model performance, I found myself spending too much time copying and pasting the same code. Frustrated by this challenge, I built a report that only required minimal information to simply train models, run, and produce meaningful insights.
2. **Easier tracking of model development**: There's no worse feeling as a data scientist than a model is running as expected one day but then produces an unexpected result the next day with no meaningful explanation. This dreaded dynamic can require hours of de-bugging to answer the basic question: "what happened?". My report (hopefully) makes that question far easier to answer as it creates **clear artifacts** of model performance. By comparing reports over time and seeing if/how the underlying data, feature engineering, or model specs change, the model report makes it far easier to understand why and how the model has changed. The report encourages easier and more frequent "deep dives" into a model, making evaluation, improvement, and de-bugging a lot easier.
3. **Easier collaboration**:  In my experience, "final results" are most often copied into wiki pages, which can quickly get out of date and are painfully manual to update. In addition, when developing most models, there are some highly subjective choices that may have a large effect on model performance but are sometimes not communicated well (e.g., "why did you choose that hyperparameter?") A report like this leaves a clear paper trail of the model development lifecycle not only for the user, but also for their collaborators. 

## How It's Organized
Diving a bit deeper into the report, there are four key sections which I will describe in more detail below.

### Data and Features
A description of data loading, cleaning and processing steps. Most importantly, it provides a set of visualizing the distributions of data, including

<img src="{{ site.baseurl }}/images/tidy_eda.jpg">

### Tidymodels Setup
A setup of R's `Tidymodels` package, including the defined model "recipe" (i.e., feature engineering steps) and model specification (e.g., random forest, xgboost). This section shows how the data was split for training and test.

<img src="{{ site.baseurl }}/images/tidy_setup.jpg">

### Tuning and Metrics
Model results, including potential parameter tuning opportunities. The tabs in this section contain useful summaries of model performance for both k-fold cross-validation as well as performance across the entire training/test data.

<img src="{{ site.baseurl }}/images/tidy_metrics.jpg">

### Expain
Key explainability metrics including global metrics (variable importance, dependence profiles) and local metrics (breakdown and stability plots).

<img src="{{ site.baseurl }}/images/tidy_explain.jpg">

## How does it actually work?

 The repo structure contains three key mechanisms that help us make this report more modular and extensible.

- General RMarkdown code: `model-report.Rmd` and all `/children/` files help us generate the bones of the html report. **These files will stay constant across reports.**
- Project-specific R code: After the user creates a directory and adds `/src` folder, they can customize how data is read, cleaned, feature engineered, and modeled. **These files will be unique to a given project/report.**
- Project-specific parameter YAML file: These are model specific specs defining **compilation-level** information including where to access project-specific R code, stratification variables, specific models to run for that report, etc. **These files will be unique to a given project/report.**

See [github](https://github.com/ngbasch/model-report?tab=readme-ov-file#how-to-set-up-your-own-report) for more detail on how to set up your own report!

