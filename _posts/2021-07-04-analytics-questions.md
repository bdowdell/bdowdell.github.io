---
layout: post
title: "Analytics: Asking the right questions"
katex: False
---

## Types of Data Analytics Questions

![https://pixabay.com/illustrations/questions-font-who-what-how-why-2245264/](https://cdn.pixabay.com/photo/2017/04/20/10/11/questions-2245264_960_720.jpg)

[The 4 Types of Data Analytics](https://www.kdnuggets.com/2017/07/4-types-data-analytics.html) is a great article that gives an overview of four different categories of analytics questions. Before embarking on any sort of data analysis journey, it is crucial to first identify what you want to learn from the data and what are the business goals. The different categories of analytics questions can help structure any subsequent analysis by framing questions in a way that can be answered using a combination of statistical analysis and machine learning tools. A data scientist's primary role is to generate insights and business value from data, but this can only be accomplished by taking a recognized business problem and framing it as an analytics question. So what are they?

While different sources may add additional types of questions or use slightly different terminology, the four basic types of analytics questions can be summarized as:

1. Descriptive
2. Diagnostic
3. Predictive
4. Prescriptive

Now that we've identified the types of questions, let's take a look at what each question attempts to answer.

## Descriptive

![https://pixabay.com/illustrations/statistics-graph-chart-data-3411473/](https://cdn.pixabay.com/photo/2018/05/18/16/25/statistics-3411473_960_720.jpg)

**What:** Descriptive analytics questions are the most basic, but that doesn't mean that they are the least useful. Descriptive analytics questions are just that: they seek to describe what has happened. These are answered by summary statistics which are always the first glimpse into a data set. For data that measure quantitative variables, this includes summary statistics such as mean, median, mode, minimum, maximum, quartiles, standard deviation and variance. Likewise, for data that are qualitative measures, this includes class frequencies and proportions.

A descriptive analytics question might ask "What was the average units sold per month last year?", "What is the 90th percentile in height of children aged 9-11 years?", or "What is the median air speed velocity of an unladen swallow?". The answers to these types of questions don't require interpetation because they are factual statements based upon data. Excepting the possibility of less-than-honest or well-intentioned-yet-flawed data collection methods, this is the ground truth of what happened.

**Why:** Regardless of your ultimate end-goal, this should always be the starting point. If you don't understand the basic summary statistics and distributions of your data, any results you may find could be meaningless if the data doesn't satisfy the statistical assumptions made by whichever model you use. Additionally, descriptive analytics help identify problems in the data during the exploratory data analysis and data cleaning stages.

**How:** Descriptive analytics questions add value by describing the truth as measured by data. Data dashboards are very popular currently, and they are driven predominantly by descriptive analytics. Understanding the summary statistics of your data can help guide further analysis.

## Diagnostic

![https://pixabay.com/photos/laboratory-chemistry-subjects-1009190/](https://cdn.pixabay.com/photo/2015/10/27/15/27/laboratory-1009190_960_720.jpg)

**What:** Diagnostic analytics questions seek to answer whether relationships and patterns exist in the data and potentially describe why they exist. These types of questions are answered using statistical tests such as the Independent t-test, Pearson Correlation Coefficient, Chi-square test, and ANOVA, just to name a few. Put another way, diagnostic analytics test the hypotheses we make about associations beteween variables.

A diagnostic analytics question might ask "Is there an association between salary and highest attained education level?" (ANOVA), "Is there an association between latitude and median annual precipitation?" (Correlation), or "Is there an association between being a witch and being made of wood?" (Chi-square). These questions are formed as a hypothesis which is then tested by the data. The hypothesis consistst of a null hypothesis, $h_0$, which states there is no association, and the alternate hypothesis, $h_a$, which states that there is an association. The null hypothesis is tested using an appropriate statistical test and the resulting p-value of the test statistic leads us to either reject the null hypothesis, or fail to do so. This process is called *statistical inference*.

Going a step further, *causal inference* attempts to assign causality based upon statistically significant association between variables. In practice, accounting for all confounding factors is truly difficult and true causality is challenging to establish.

**Why:** We answer diagnostic analytics questions because we want to identify which relationships in the data are statistically significant and which are not. This can help us identify which features are most important in predicting the target, or response, variable. Diagnostic analytics questions also allow us to identify and understand confounding factors in the data so that we can be more certain that the effect we estimate of one feature is isolated from the effect of the other features.

**How:** Diagnostic analytics questions add value because they quantify the effects of statistically significant associations. In a clinical trial, for example, we may wish to know whether or not a new treatment has a statistically significant benefit over a placebo for people with hypertension. Answering this question can lead to a new drug discovery that can positively impact peoples' lives while also producing new revenue for a drug manufacturer. Another classic example we can use to illustrate the value is deciding how many dollars of a fixed budget to allocate amongst different advertising media. We can model a linear relationship of sales onto the advertising media (email, social media, web page ad). Diagnostic analytics will allow us to identify which of the media have a statistically significant impact on sales and the linear model will quantify this effect. This actually starts to move towards *prescriptive analytics*, so you can see how the different types of analytics questions are more of a continuum than discrete categories.

## Predictive

![https://pixabay.com/photos/fortune-symbol-mystery-paranormal-2414239/](https://cdn.pixabay.com/photo/2017/06/18/01/04/fortune-2414239_960_720.jpg)

**What:** Predictive analytics questions focus on predicting what will happen in the future. Simple, right? In order to answer a predictive analytics question, a predictive model must be fitted onto the observed data. For time series data, this means forecasting a number of periods into the future. For data with a qualitative target, this means predicting what class a new observation belongs to, while for data with a quantitative target it means predicting a value using regression. Predictive models are trained using data already collected, tested using some portion of data held-out during the training phase, and then make predictions whenever new data comes available.

A predictive analytics question might ask "What is the expected sale price of a house with 3 bedrooms, 2 bathrooms, 2,500 square feet, and located nearby a shopping center?" and is answered using regression. Another example of a predictive analytics question might be "What are the forecasted operating expenses for the next four quarters?" and is answered using time series analysis. Yet another predictive analytics question might ask "Can we predict if a part will fail based upon various sensor measurements?" which is an example of a classification problem. Continuing with our Monty Python examples, another example of a classification predictive analytics question would be "Can we predict Sir Lancelot and Sir Galahad's favorite color?".

**Why:** We answer predictive analytics questions in order to predict what might happen based on what we have already observed. Whether it is making predictions about customers, production, expenditures, etc., a business wants to be able to make the most accurate predictions possible in order to optimize the business planning cycles.

**How:** An ability to build accurate predictive models to answer predictive analytics questions can obviously bring huge competitive advantage to a company, and thus value. Whether the goal is forecasting, regression, or classification, predictive models can add business value by enhancing a subject matter expert's knowledge and trained intuition. Additionally, predictive models can augment or even drastically accelerate the rate at which humans can manually solve a problem.

## Prescriptive

![https://pixabay.com/illustrations/prescription-medical-doctor-pad-4545598/](https://cdn.pixabay.com/photo/2019/10/13/08/20/prescription-4545598_960_720.jpg)

**What:** Prescriptive analytics questions strive to answer how a business can influece what happens. One way to think of this is imagining a control panel with a lot of different knobs. This control panel controls how efficiently a certain widget is manufactured. Some of the control knobs have a large effect on the efficiency, some of the control knobs have a small effect on the efficiency, and the rest don't have any effect at all. What is the best setting for each knob that results in the most efficient widget production?

A prescriptive analytics question might ask "How much sand proppant should we use in our next frac job to maximize stimulated rock volume and expected ultimate recovery?", or "How much money should we place in our R&D budget to accelerate innovation?". King Aruther might ask "What is the fastest route to finding a shrubbery for the Knights Who Say Ni?".

**Why:** We ask prescriptive analytics questions because the answers we derive from them can inform and influence business strategy. These types of questions naturally arise once the other analytics questions have been answered, establishing a new success baseline that we now want to fine-tune and optimize for even better performance.

**How:** In all business settings, there are events that a company would like to minimize, such as customer churn, while there are other events they would like to maximize, such as profit. Prescriptive analytics questions add value by empowering companies to make decisions which influence these types of outcomes.

## Summary

We've now gone through a brief overview of the four major types of analytics questions. These categories are: 

1. Descriptive: *what happened?*
2. Diagnostic: *why did it happen and is the association statistically signficant?*
3. Predictive: *what will happen based upon what we already know?*
4. Prescriptive: *how can we influence what might happen in our favor?*

Recall that a data scientist's primary role is to take a business problem or challenge and frame it as an analytics question so that data can lead to insights and business value. It is entirely plausible that a business challng will have multiple analytics questions from multiple analytics question categories.

*Framing the business problem as an analytics question(s) will guide and focus the analysis as data gets transformed into actionable insights and business value.*
