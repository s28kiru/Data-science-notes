
### what is A/B testing?

Testing new products or features - experiment new user.
How do the user respond differently?
two sets of users - control set existing set
experiment group - new group

can use to test new features/ UI

amazon - personalized recommendation - significant increase revenue
linkedIn - ranking change - show new article/ new contact to add

test changes that user might not notice - time to load the data can be checked

cant do? 
cannot test new experiences - change aversion
novelty effect
there is no baseline for comparison
How much time needed for the user to adapt to new experience

cannot tell you if you are missing
only for comparison - you cant find something new

need a clear control group and experiment group
Need clear metric

- if AB testing not used??

- analyze the data using some hypothesis and then randomize the experiment
- Develop a hypothesis - test whether its right/not

AB testing gives broad quantitative data

Complete redo site/ user interaction - tough to test using AB testing

you need consistent response from control and experimental group

online data - not much information 
design experiment that is robust

---

Audacity example

creates online finance course

### user flow - called customer funnel:

top is most common and becomes less as we go down

home page visit
explore the site
create account
complete purchase/ finish course  - does not complete a class in consistent manner

### Experiment:

changing start now button from orange to pink will increase many students explore audacity courses

#### Refining hypothesis:

initial hypothesis: changing start button from orange to pink will increase number of students explore audacity courses

Which metric?

- Total number of courses - takes a lot of time to get this metric
- Number of clicks  - problem is - what if more number of users view version 1 and less view version 2
- so instead of number of clicks use fraction of clicks called as `click through rate`

click-through-rate = number of clicks / number of page views

click-through-probability = unique visitors who clicks/ unique visitors to page

two users x and y - clicks page 0 and 5 times

click through rate is 2.5 and click through probability is 0.5

- we will use click through probability from now on

Updated hypothesis: Changing the start now button from orange to pink will increase the click through probability of the button

use rate for measuring the usability and probability when measuring the total impact

usability of a particular button - use rate - how often the user finds the button
total impact - how many times user moved to next page - dont care about how many times they clicked

in our example, we are interested in how many people moved to 2nd stage

compute the probability: work with engineers to change the website

rate: sum the page views, sum the clicks and divide
probability: match each view with child view so find max 1 click for each child view


### Repeated measurement of click through probability

visitors = 1000
unique clicks = 100

click through prob = 10%

will the results repeat if you repeat the experiment?

---

Binomial distributions:
we will use binomial here cuz click is success and no click is failure
two exclusive outcomes

graph: x axis = number of heads and y axis probability
as n increases - x axis fraction of head and binomial becomes normal

binomial approximated to normal:
mean = p
std = sqrt(p(1-p)/N)

N = 20
X = 16 (16 times it becomes head)

p-hat (estimate of bias): 16/20 = 4/5 = best estimate

binomial:
only two types of outcomes
IID

- confidence interval
- true population value will be within this interval of estimate

p-hat = X/N - number of user/number of click

p-hat = 0.1

need to find margin of error: use standard error of binomial distribution

can use standard error of normal if N.p > 5 and N(1-p) > 5

for normal distribution:

m = Z * SE

m = Z * sqrt(p-hat * (1-p-hat) / N)

If N is larger, standard error is smaller and CI is smaller

for normal distribution with mean of 0, std of 1 it is called as z-distribution
The true value will be between -1.96 and 1.96. 1.96 is the z-score

m = 0.019

p-hat +/- m = 0.081 and 0.119

so if similar experiment is done, the result will be between 0.081 and 0.119

replicated experiment:

N = 2000 X = 300

p-hat = 3/20 = 0.15
m = 2.58 * sqrt(0.15 * 0.85 / 2000) = 0.021

value varies b/w: 0.121 and 0.171

---

hypothesis testing

- how likely the result are obtained by chance?

Null hypothesis: baseline for comparison
alternate - which we want to check

find probability that the results are due to chance?

control group: orange box - p_cont
experimental group: pink box - p_exp

null hypothesis: H_0 => p_cont - p_exp = 0
alternate: H_a => p_cont - p_exp != 0

aim: to reject the null hypothesis

reject null if p < 0.05 (cut off)

another example: change checkout flow of shopping site
test old flow vs new flow

null: control and experimental group have same prob of completing the checkout (p_exp - p_cont = 0)
alternate: both do not have same probability


---

Comparing two samples

X_cont, X_exp, N_cont, N_exp

p_pool => (X_cont + X_exp) / (N_cont + N_exp)

SE_pool = sqrt(p_pool * (1 - p_pool) * (( 1/ N_cont) + (1 / N_exp)))

d_cap = p_exp - p_cont

H_0 -> d = 0   d_cap ~ N(0, SE_pool)
H_a -> d != 0

if d_cap > 1.96 * SE_pool or d < -1.96 * SE_pool -> reject Null

---
- decide from business perspecitive what change in the click through probability is significant
- what change size matters to us?

What substantive 

- every change does not matter to the experiment?
- You need to find the change size to make sure that its worth the change for investment

- medicine 5/10/15% change is good
But in google - 1/2% is very good

- repeatability is important - the results are repeatable so it is statistically significant

- type of change you are interested in the business standpoint is practically significant is also statistically significant
- We need to pick a practical significant boundary for our Audacity example

- Lets say 2% change is practically significant from business perspective for our example

---

## Design the experiment

- We need to find how many pages we need to get statistical significance - it is also called as statistical power
- If we see some interesting result we want to conclude we have enough power to conclude with high probability that the interesting result is in fact statistically significant

- Power is inverse of size
- smaller the change you want to detect larger the experiment
- increase in confident means you need more pages in your sample

- we need to decide how many pages we should use?


alpha - P(reject null when null is true)
beta - P(fail to reject null when null is false)

small ssample size: low alpha and high beta

1 - beta = sensitivity -> we want high sensitivity - people generally choose 80% of practical significance boundary

larger sample: alpha is the same, but beta is lower

---

sensitivtiy calculation

- built in lib
- look table
- online calculator

- for our example: N = 1000, X = 100, d_min = 2% = 0.02
alpha = 0.05 beta = 0.2

https://www.evanmiller.org/ab-testing/sample-size.html

- baseline conversion is 10%
- minimum detectable effect is 2%

we need 3623

How number of page view varies:

- Higher click through probability in control (but still less than 0.5) - have direct effect on SE

sqrt(0.5 * 0.5) sqrt(0.1 * 0.9) - higher prob means reduce standard error - to reduce standard error - increase page views

standard calc: change baseline conversion rate to 20% - sample size increased


- Increased practical significance - larger changes are easier to detect - so decrease sample size
increase min detectable effect to 5% - sample size decreases

- Increased confidence level - increase number of pages

- Higher sensitivity - increase number of pages

---

Analyze results

N_cont = 10072 X_cont = 974
N_exp = 9886   X_exp = 1242

step 1: find p_pool =  (974 + 1242) / (10072 + 9886) = 0.111

step 2: SE_pool = SQRT( 0.111 * (1- 0.111) ( (1/10072) + (1/9886))) = 0.00445

d_hat = (X_exp / N_exp) - (X_cont / N_cont) = 0.0289

m = z * SE = 1.96 * 0.00445 = 0.0087

CI => d_hat +/- m = 0.0202 and 0.0376

We conclude that that click through prob change by atleast 2%
It holds for both significant and practical significance

---

- see 26th video
- data could be uncertain so communicate to decision maker and take the risk










