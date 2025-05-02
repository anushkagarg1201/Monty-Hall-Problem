# The Monty Hall Problem 

This project is a part of course **Data Science and Analysis** (EP4130), instructed by **Dr. Shantanu Desai**.


## Introduction

In the Monty Hall problem, a contestant is presented with **three doors**. Behind one door is a **valuable prize (a car)**, and behind the other two are **goats**. The sequence of play is:

1. The contestant selects one door (but does not open it).
2. The host, who knows what is behind each door, opens one of the two remaining doors, always revealing a goat.
3. The contestant is then offered the choice to *stay* with their initial selection or *switch* to the other unopened door.

We seek the contestant's **probability of winning the car** under each strategy (**staying** vs. **switching**) from a theoretical perspective.

This project also explores the problem through **simulation**, **statistical testing**, **visualization**, and **extensions**(including **generalization** and **modeling human bias**).

## Notation and Setup

Let the doors be labeled $\{1,2,3\}$, and let $C$ denote the door hiding the car. Let $S$ be the door initially selected by the contestant, and let $H$ be the door opened by the host.

- $C \in \{1,2,3\}$, with $\Pr(C=i)=\frac{1}{3}$ for $i=1,2,3$.
- $S \in \{1,2,3\}$ is chosen uniformly at random by the contestant, so $\Pr(S=i)=\frac{1}{3}$.
- Given $(C,S)$, the host picks $H\neq S$ such that $H\neq C$ (i.e., he never opens the car door), breaking ties uniformly if both remaining doors have goats.

## Theoretical Interpretation

We wish to compute:

$$
P_{\text{stay}} = \Pr(\text{win car} \mid \text{contestant stays}), 
\quad
P_{\text{switch}} = \Pr(\text{win car} \mid \text{contestant switches}).
$$

### Staying

If the contestant stays, they win exactly when their initial pick was correct:

$$
P_{\text{stay}} = \Pr(S = C) = \frac{1}{3}.
$$

### Switching

If the contestant switches, they win whenever their initial pick was wrong. Indeed:

$$
P_{\text{switch}} = \Pr(\text{initial pick wrong}) = 1 - \Pr(S = C) = 1 - \frac{1}{3} = \frac{2}{3}.
$$

We can enumerate all equally likely pairs \((C, S)\):

| Case | Car \(C\) | Initial pick \(S\) | Host opens \(H\)          |
|------|-----------|---------------------|----------------------------|
| 1    | 1         | 1                   | either 2 or 3 (goat)       |
| 2    | 1         | 2                   | host must open 3           |
| 3    | 1         | 3                   | host must open 2           |
| 4    | 2         | 1                   | host must open 3           |
| 5    | 2         | 2                   | either 1 or 3              |
| 6    | 2         | 3                   | host must open 1           |
| 7    | 3         | 1                   | host must open 2           |
| 8    | 3         | 2                   | host must open 1           |
| 9    | 3         | 3                   | either 1 or 2              |

There are 9 equally likely cases. In cases where \(S = C\) (cases 1, 5, 9), staying wins; in the other 6 cases, switching wins. Hence:

$$
P_{\text{stay}} = \frac{3}{9} = \frac{1}{3},
\quad
P_{\text{switch}} = \frac{6}{9} = \frac{2}{3}.
$$
