# Statistics :

## What is statistics ?
- Statistics is a field that deals with :
    - collection
    - organisation
    - analysis
    - interpretation
    - presentation

- of data.

- At the end of the day, we need to make decision.
    - we make decision based on some kind of data.
    - we need to do the statistical analysis of data and based on the analysis we make decisions.

### Types of Statistics :

![Types of Statistics](assets/Whiteboard.png)

- 2 different types of statistics :
    1. **Descriptive** :
        - organising and summarising data 
        - measures of central tendencies 
            - mean 
            - median 
            - mode
        - measures of dispersion - 
            - variance
            - standard deviation

    2. **Inferential** :
        - collect data - make conclusions/inferences using some experiments
            - Ztest 
            - tTest

        - consider a college A -- with data for students height -- {180cm, 170cm, 165cm}
        - total students = 1000
        - sample data of = 200 students
        - so, we can conclude the height of remaining 800 students  by infering using inferential statistics.

### Population data `N` v/s Sample data `n`:
- consider a town with 100K population
- to analyse the data for all people is a hassle.
- so we just take 10k people's data
- this data is called as `sample data`

# Measures of Central Tendency :
    1. Mean
    2. Median
    3. Mode

1. **Mean :** 
    - 

2. **Median :**
    a. Sort the numbers
    b. find the central element
        i. if odd elements then central element
        ii. if even elements then central element is avg of the two mid numbers
    
    - median helps us mitigate the impact of `outliers`.

    - example :
        - consider ages : {1, 3, 2, 4, 5} -- mean = `3`
        - if outlier is present -- {1, 3, 2, 4, 100} -- mean = `22`
        outlier impacts the mean significantly, which is not at all desired.
        - median solves this problem -- median for {1, 3, 2, 4, 100} is `3`.

3. **Mode :**
    - we select element with maximum frequency
    - even though there are outliers, it will not affect the central tendencies that much.

![Measures of central tendency](assets/image.png)

# Measures of Dispersion :
    1. Variance
    2. Standard deviation

![Measures of dispersion](assets/image2.png)

1. **Variance :**
    - example :
        - ages1 = {2, 2, 4, 4} : mean = 3
        - ages2 = {1, 1, 5, 5} : mean = 3
        - here we can see that both has the same mean, but the closeness of actual values varies in both the sets.
        the `ages2` set is more **dispersed** than the `ages1` set

**Interview Question :**
- why is the formula for computing variance for sample data is slightly different than that of population data ?

> we need to make inferences about the population from the sample data. So, if we keep the same formula, we underestimate the true population variance. hence, we need to tak (n - 1) `Bensel's correction`

![Sample Variance](assets/image3.png)

2. **Standard Deviation :**
    - It suggests that how far is the data element away from the mean.
    - it is simply the square root of variance.

![Standard deviation](assets/image4.png)

# Variables :

**Defn :** Variable is a property that can take up any value.

### Different types of variables :

    1. **Quantitative**
        i. Discrete -- whole number 
            - examples : number of students in a class
        ii. Continuous -- any fraction
            - example : height, weight
    2. **Qualitative / Categorical**
        - example : gender = [Male, Female]
        - Colors = [Red, Green , Blue]

![Variables](assets/image5.png)

## Random Variables :
- it is a function whose values are derived from different proccesses or experiments

### Different types of random variables :
    1. Discrete -- tossing a coin
    2. Continuous -- how much is it going to rain tomorrow

# Histograms : Descriptive Statistics 

- we have a bin - size. So we count the frequency of the data lying between the range of a bin.
- it represents the number of elements present in a distribution
- we can derive a `probability density function` from a histogram.
- There is a concept called `Kernel Density Estimation` that smoothens the curve of the histogram, this smoothened curve will give the probability distribution function.

![Histograms](assets/image6.png)

