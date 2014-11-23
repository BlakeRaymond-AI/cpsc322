
# CPSC 322 2014W Assignment 4
Blake Raymond
30791107
November 28, 2014

## Question 1
### A
The typo is the third row of the matrix, namely 	$A=T$, $B=T$, $C=T$, $\mathrm{Prob}=1.2$.  The probability cannot be greater than 1.  In fact, it is constrained by the other rows of the matrix such that all probabilities sum to 1.  Its value must be $$1-0.1-0.1-0.3-0.1-0.2-0.1=0$$

### B
$$P(A) = \sum_{B\in\{T,F\}} \sum_{C\in\{T,F\}} P(A,B,C)$$
Thus,
$$\begin{align} P(A=T) &= 0.1 + 0.1 + 0 + 0.3 = 0.5 \\ P(A=F) &= 0.5 \end{align}$$
and
$$\begin{align} P(B=T) &= 0.1+0.1+0.1+0.2=0.5 \\ P(B=F) &= 0.5 \end{align}$$

If A and B were independent, then $P(A) = P(A|B)$.  We can calculate $$P(A=T|B=T)= 0.2 / 0.5 = 0.4 \ne P(A=T)$$  So A and B are not independent.

$$\begin{align} P(A=T|B=F) &= (0 + 0.3) / (0 + 0.3 + 0.1 + 0.1) \\ &= 0.3 / 0.5 \\ &= 0.6 \end{align}$$

### C
Yes, this is true.  From the product rule,
$$P(X_1, X_2, X_3) = P(X_3|X_2, X_1)\times P(X_2|X_1)\times P(X_1)$$
By changing the order of terms on the left-hand side we can see that
$$P(C|B,A) \times P(B|A) \times P(A) = P(A,B,C)$$
Similarly for the right-hand side
$$P(A|B,C) \times P(B|C) \times P(C) = P(C,B,A) = P(A,B,C)$$
Thus they are equivalent.

## Question 2
### A
![TelescopeBNet](https://docs.google.com/drawings/d/1_UZkQ9Bn6pTImmtc-vkpCimAjQTZn5k1zBiQq1XEm3E/pub?w=960&h=720)
In the causal network, the result of the measurement should depend on the true value; thus, $N$ is a parent of $M_1$ and $M_2$.  The result of the measurement for either telescope also depends on whether that telescope is in or out of focus; thus $F_1$ and $F_2$ are parents of $M_1$ and $M_2$, respectively.

### B
Given no evidence, $F_1$ is independent of $N$.  Given no information about the result of $M_1$, whether or not the telescope is in focus should not be influenced by the number of stars in the sky.  In general, in the common effect topology the causes are independent unless there is evidence on the effect.

### C
If it is known that there are between 0 and 9 stars, then $N\in{0,...,9}$ and $M_1$, $M_2$ have the same domains.  $F_1$ and $F_2$ are boolean variables.  Then the joint distribution will have $10 \times 10 \times 10 \times 2 \times 2 - 1 = 3999$ entries.  

For the belief network above, we need to specify $P(F_1)$, $P(F_2)$, $P(N)$, $P(M_1|F_1,N)$ and $P(M_2|F_2,N)$.  $P(F_1)$ and $P(F_2)$ require $2-1=1$ entry each.  $P(N)$ requires $10-1=9$ entries. The two conditional tables require $10-1=9$ entries for each combination of $N$ and $F$, of which there are $10\times 2 = 20$.  In total we will have
$$1 + 1 + 9 + 9\times 20 + 9\times 20 = 371$$ entries.  This is a savings of $3999-371=3628$ entries, or a reduction by $91\%$. 

## Question 3

### A
We will first prune leaf nodes that are not the query or are not observed; these are $F$ and $D$, and we are left with $A,B,C$ and $E$.

The factors to be created are $f_1(A)\triangleq P(A)$, $f_2(B)\triangleq P(B)$, $f_3(A,B,C)\triangleq P(C|A,B)$, and $f_4(C,E)\triangleq P(E|C)$. 

Assuming alphabetical elimination ordering, we will first eliminate $A$, then $B$ and $C$.  Then
$$ \begin{align} P(E) & = \sum_{A,B,C} f_1(A) f_2(B) f_3(A,B,C) f_4(C,E) \\
& = \sum_C  f_4(C,E) \sum_B f_2(B) \sum_A f_1(A) f_3(A,B,C) \\
 \end{align} $$

Stepping through,
$$f_5(B,C) \triangleq \sum_A f_1(A) f_3(A,B,C)$$

$$ \Rightarrow P(E) = \sum_C  f_4(C,E) \sum_B f_2(B) f_5(B,C) $$

$$f_6(C) \triangleq \sum_B f_2(B) f_5(B,C)$$

$$ \Rightarrow P(E) = \sum_C  f_4(C,E) f_6(C) $$

$$f_7(E) \triangleq \sum_C  f_4(C,E) f_6(C)$$

$$ \Rightarrow P(E) = f_7(E) $$

As a final step, to compute $P(E=e)$, normalize over $E$:
$$P(E=e) = \frac{ f_7(e) }{ \sum_{e' \in \mathrm{dom}(E)} f_7(e')} $$

### B

Given $C$, $E$ is independent of all other variables.  Then we can write directly
$$P(E|C=F) = f_8(E)$$
and 
$$ P(E=e|C=F) = \frac{ f_8(e) }{ \sum_{e' \in \mathrm{dom}(E)} f_8(e')} $$

## Question 4

### A
The sum of the entries of a stochastic matrix for a process that can be in one of 11 states is 11.  Each state must have 11 transition probabilities that sum to 1, and there are 11 states in the matrix.

### B

The self-transition probabilities are each zero.  These are the diagonal elements of the transition matrix.  Further, as probability distributions, the rows must each sum to 1.  Hence only three transition values are needed to define the matrix.
$$ T=
\left( \begin{array}{ccc}
0 & x_1 & 1-x_1 \\
x_2 & 0 & 1-x_2 \\
x_3 & 1-x_3 & 0 \end{array} \right)
$$

### C
In this paper the researchers developed a HMM for predicting precipitation using observed atmospheric circulations.  The observed atmospheric conditions included

* sea-level pressure,
* geopotential height at 850 hPa and 500 hPa,
* air temperature,
* dew point temperature, and
* $u$ (north-south) and $v$ (east-west) wind speed components.

The model includes an unobserved "weather state" that causes the observed rainfall process.  The observed atmospheric conditions are used to update the transition probabilities of the model.  The number of weather states was varied in order to produce optimal accuracy. The researchers determined that six weather states, with the duration of each state being one day, produced optimal results.

> Hughes, J. P., Guttorp, P. and Charles, S. P. (1999), A non-homogeneous hidden Markov model for precipitation occurrence. Journal of the Royal Statistical Society: Series C (Applied Statistics), 48: 15–30. doi: 10.1111/1467-9876.00136

## Question 5

### A
With 4 possible card values for each card, and two possible decisions for each case, there are $4 \times 4 \times 2 = 32$ possible policies.

### B
Variable elimination will not remove either of Card 1 or Card 2 from the *Hit Once* policy table.  Thus, performing variable elimination will not increase the efficiency of optimization.

### C
The optimal *Hit Once* policy is shown below.
$$
\begin{array}{ccc}
\text{Your card 1} & \text{Your card 2} & \text{Hit once} \\
1 & 1 & T \\
1 & 2 & F \\
1 & 3 & F \\
1 & 4 & F \\
2 & 1 & F \\
2 & 2 & F \\
2 & 3 & F \\
2 & 4 & T \\
3 & 1 & F \\
3 & 2 & F \\
3 & 3 & T \\
3 & 4 & T \\
4 & 1 & F \\
4 & 2 & T \\
4 & 3 & T \\
4 & 4 & T \end{array}
$$

This policy has an expected utility $E(U)=-0.25$.
