---
layout: post
title: "How To Control For Confounding Variables"
date: 2022-02-12
description: "Seperating signal from noise"
giscus_comments: true
mermaid:
  enabled: true
  zoomable: false
toc:
  sidebar: left
tags: statistics
citation: true
---

The goal of any science is to rigorously determine causal relationships between variables. In many sciences, usually social sciences, this is very difficult due to the high number of variables. Psychology studies the human mind—the most complex physical system in the universe—whose activity is determined by the interactions of 100 billion neurons. Economics and political science and sociology study the interactions of millions of irrational actors called humans.

**Example** (Tutoring). Suppose we want to investigate the impact of tutoring on high school grades. We collect data by surveying students the amount of after school tutoring they receive and their report cards. Plotting the data shows a clear linear trend; grades are proportional to tutoring hours. However, there are alternative explanations for this pattern. Wealthier households can pay for more tutoring but also reside in wealthier neighborhoods with more school.

**Example** (Cancer). Suppose we want to investigate the impact of eating 30g of fiber per day on colon cancer. We collect data by surveying adults 60 and older their average daily fiber intake and whether they have colon cancer. Fitting a logistic regression to the data shows that the probability of colon cancer decreases with the consumption of fiber. However, there are altnerative explanations for this pattern. Healthier individuals often have a diet richer in fiber. Their overall better health may be preventing colon cancer.

Variables like household wealth are called **confounders**. More formally, a variable $Z$ (household wealth, health) is confounding if it casually influences the **independent variable** $X$ (tutoring, fiber intake) and the **dependent variable** $Y$ (high school grades, cancer rates). Confounders muddle the true relationship between $X$ and $Y$. Hence the quote

> Correlation does not equal causation.

```mermaid
graph LR
    Z[Confounder] --> |causes| X[Independent variable]
    Z --> |causes| Y[Independent variable]
    X -.- |relationship of interest| Y
```

## Experiment Design

The easiest way to eliminate confounders is through careful experiment design. In a **controlled experiment**, researchers set the value of the independent variable $X$ for subjects.

### Randomization

**Randomization** assigns subjects to **control groups**, doing nothing, and **treatment groups** randomly. Assignment sets the independent variable $X$ without adjusting any confounder $Z$. For a sufficiently large sample of subjects, any overall change in $Y$ can be attributed to $X$ alone as the control and treatment groups will have identical distributions of $Z$ values.

**Example** (Tutoring). We could gather 1000 freshman high school students. 50 students would be randomly assigned weekly tutoring sessions. The remaining 50 students form the control group.

**Example** (Cancer). We could gather 1000 adults. 500 adults would be randomly assigned a diet high in fiber. The remaining 500 adults form the control group.

### Matching

If the confounder $Z$ is known, subjects can be **matched** with another subject of equal $Z$ value. Thus, any difference between the pair is attributable to the independent variable $X$ alone. This approach is inferior to randomization since it cannot address unknown confounders but doesn't require as large of a sample. A special case of matching is **restriction** which uses only subjects with a fixed $Z$ value.

**Example** (Tutoring). We could gather 200 high school students whose various households have a range of incomes. The students are grouped into pairs with equal household income. One student in each pair is assigned to treatment tutoring sessions while the other is put into the control group.

**Example** (Cancer). We could gather 200 adults who get varying levels of weekly exercise. The adults are grouped into pairs with similar weekly exercise levels. One adult in each pair is assigned to the treatment diet while the other is put into the control group.

## Data Analysis

Often, controlled experiments are unethical or impractical. In an **observation study**, the researchers record independent, dependent, and confounding variable values without affecting them.

### Stratification

**Stratification** is like a post-experiment matching. Subjects with similar confounding variable values $Z$ are grouped into strata. Any differences of the dependent variable $Y$ within strata are can attributed due to the independent variable $X$ alone. Similar to matching, stratification cannot account for unknown confounding variables. Moreover, as the number of confounding variables increases, the number of strata needed increases exponentially.

**Example** (Tutoring). After surveying data from 1000 students, we break them into 10 household income buckets. Students are placed in each bucket based on their household income.

**Example** (Cancer). After surveying data from 1000 adults, we break them into 10 time buckets. Adults are placed in each bucket based on their weekly exercise levels. If we want to account for sleep as well, we might need 100 buckets for exercise and sleep levels.

### Multi-variate Regression

Instead we can fit a multivariate linear regression predicting grades $Y$ given hours of tutoring $X$ and household income $Z$. Assuming we have diverse examples where $X, Y$ are both low and high, the estimated parameters should be accurate.

$$
Y = \alpha + \beta X + \gamma Z
$$

Here $\beta$ measures the effect of a change in $X$ assuming no change in $Z$.

Compared to stratification which exponentially increases the number of strata as confounders are added, it is easier to add confounders to a regression model.

**Example** (Tutoring). We fit a regression model to our survey data. If hours of tutoring has no effect on grades, then $\beta \approx 0$ as all the variation in $Y$ can be explained by $Z$ alone. If tutoring positively influences grades beyond the confounding effect of household income, then $\beta$ will be positive.

**Example** (Cancer). We fit a logistic regression model to our survey data. If fiber intake has no effect on colon cancer, then $\beta = 0$. If fiber intake negatively influences the probability of colon cancer beyond the confounding effect of overall health, then $\beta$ will be negative.

## Propensity Score Matching

A **propensity score** is the probability of a subject being in the treatment group given the background characteristics $\Pr(X = 1 \mid Z = z)$. We can fit a model that estimates propensity scores based any confounding variables. Each subject who received the treatment is matched to a subject who received the comparator with an equivalent propensity score.

Because propensity scores combine multiple confounders into a single summary score, these methods are preferred when the treatment of interest is common and outcome of interest are rare, a setting where multivariable outcome models are susceptible to overfitting.

**Example** (Tutoring). We fit a linear regression model that estimates tutoring hours based on household income and other variables like parent education to our survey data. We match students who have high tutoring hours with students who have low tutoring hours but equal propensity score.

**Example** (Cancer). We fit a linear regression model that estimates fiber intake based on age, weekly exercise hours, average sleep time, etc. to our survey data. We match adults who have high fiber consumption with adults who have low fiber intake.

## Overadjusting

It is important not to overadjust for confounding variables. In particular, when the "confounding variable" $Z$ is an effect of the independent variable $X$, we should not adjust for $Z$. This is because $Z$ might be a part of the mechanism through which $X$ affects the dependent variable $Y$.

```mermaid
graph LR
    X[Independent variable] --> |causes| Z["Confounder"]
    Z --> |causes| Y[Independent variable]
    X -.- |relationship of interest| Y
```

**Example** (Tutoring). If we were studying the relationship between household income and grades instead of tutoring hours and grades, extra tutoring hours might be one reason students from high income households do better. Confounders $Z$ should be correlated with $X$ but not caused by $Z$.

**Example** (Cancer). If we were studying the relationship between age and colon cancer instead of fiber intake and colon cancer, decreased fiber intake might be one reason older adults have higher rates of colon cancer.

## Resources

1. https://www.sciencedirect.com/science/article/pii/S0085253815529748
2. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8786092/
3. https://oem.bmj.com/content/62/7/500
