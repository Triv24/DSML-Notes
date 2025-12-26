# Probability :
    It is about determining the likelihood of an event.
    
    Example -- Tossing a coin and possibility of getting a head is 50%.

### Mutual Exclusive Events :
    2 Events are mutual exclusive if they cannot occur at the same time.

    Example : tossing a coin -- we can not get `head` and `tail` at the **same** time.

### Non-Mutual Exclusive Events :
    2 Events are non-mutual exclusive if they can occur at the same time.

    Example : Deck of cards -- we can get a `k` and a `heart` at the same time.

## Addition Rule :

- Addition Rule for mutual exclusive event :

![addition rule 1](assets/image14.png)

- Addition Rule for non-mutual exclusive event :

![addition rule 2](assets/image15.png)

## Multiplication Rule :

### Independent Events :
    2 Events are independent if their occurrence do not affect each other.

    Example -- Tossing a coin, Rolling a dice

### Dependent Events :
    2 Events are dependent if their occurence directly affect each other.

    Example : Take out a king card from the deck and after that, we get a queen card at the deck.

- Multiplication rule for independent event :

![Multiplication rule 1](assets/image16.png)

- Multiplication rule for dependent event :
    - idea towards Bayes theorem (conditional probability)

![multiplication rule 2](assets/image17.png)

# Probability Distribution Functions :
    Probability distribution function describe how the probabilities are distributed over the values of a random variable.

![pdf](assets/image18.png)

### 3 main types of probability distribution function :
    1. PMF -- Probability Mass Function
    2. PDF -- Probability Density Function
    3. CDF -- Cumulative Distribution Function

### 1. PMF :
    Used for Discrete random variable.

    Example - Rolling a dice (fair dice)

![pmf](assets/image19.png)

### 2. PDF :
    Used for continuous random variables

    It is the gradient (derivative) / slope of the cumulative curve.

![pdf](assets/image20.png)

#### Properties of PDF :
    1. It is non-negative `f(x) >= 0` for all values
    2. Total area under the curve is equal to 1

## Types of Probabilty Distributions :
    1. Bernoulli Distribution -> (pmf)
    2. Binomial distribution -> (pmf)
    3. Normal/ guassian distribution -> (pdf)
    4. Poisson Distribution -> (pmf)
    5. Log Normal distribution -> (pdf)
    6. Uniform distribution -> (pmf)
    7. Power law distribution
    8. Pareto distribution

- As a data scientist, you will be given a dataset abt house price, number of rooms, location of the house, floor, sea side. 
- Some of these features are discrete, whereas some will be continuous.
- So, based on different distributions, we can make a lot of assumptions which will fuel `EDA` and `Feature Engg`.

