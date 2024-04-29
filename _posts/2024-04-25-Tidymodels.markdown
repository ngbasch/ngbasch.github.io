---
layout: post
title:  "Interactive Tidymodels Report"
date:   2024-04-25
---
<img src="{{ site.baseurl }}/images/pic03.jpg">
I created an extensible [report](https://github.com/ngbasch/model-report) that allows a user to provide basic modeling information (e.g., input data, a model "recipe", etc.) and produces an easy-to-navigate report with results. 

The report is built using R Markdown based on R's `tidymodels` package. An illustrative example of the report was run on R's `iris` dataset, and can be explored <a href="240204_local.html" title="About Me">here</a>

## Motivation
I built this report for a few reasons. First off, it can b extremely useful to quickly run a model and get some quick insights on performance (e.g., distributions of features, what are the main drivers of the model, etc.). This "first pass" can provide a useful starting point in an iterative modeling process. Secondly, it can be useful to create artifacts of model performance at a specific point in time, understanding how performance shifts and changes as feature engineering and model specs change. An html report allows the user to deep dive into the given state of the model at a specific point in time and can be useful for understanding and evaluating performance improvements or catch bugs. Third (and maybe most importantly), it can be difficult to share technical modeling results with colleagues when developing new models. Documentation manually copied/pasted as wiki pages can quickly get out of date and be difficult to update. A report like this could leave a clearer paper trail within the model development lifecycle. This makes collaboration and knowledge sharing easier;


## Organization
Diving a bit deeper into the report, it's comprised of six sections, each of which I will describe in more detail below.

**Data and Features**
A description of data loading, cleaning and processing steps. Most importantly, it provides a set of visualizing the distributions of data, including

[Insert visual of EDA]

**Tidymodels Setup**
A setup of R's [Tidymodels] (https://www.tidymodels.org/) package, including the defined model "recipe" (i.e., feature engineering steps) and model specification (e.g., random forest, xgboost). This section shows how the data was split for training and test.



See [this](https://github.com/ngbasch/model-report?tab=readme-ov-file#how-to-set-up-your-own-report) for more detial on how to set up the report (and some technical detail on how it actually compiles).


