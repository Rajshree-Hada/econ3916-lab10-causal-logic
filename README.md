# econ3916-lab10-causal-logic

# Correlation & Causality: Confounders, Colliders and the Limits of Controls

## Objective

I used simulations and the LaLonde data to show that a strong correlation does not identify a causal effect, and that adding controls can remove bias or create it, depending on the causal graph.

## Methodology

- I simulated three worlds (true causation, pure confounding and pure selection) in which D and Y correlate at about 0.65 although the true effects are 2.0, 0.0 and 0.0.
- I drew a confounder, a collider and a mediator as directed graphs with `networkx`.
- I ran a regression with and without a confounder as a control to see whether it recovers the true effect.
- I ran a regression that controls for a collider to see what it does to two independent variables.
- I built an M-bias structure in which the control W is measured before treatment, and compared Y ~ D with Y ~ D + W.
- I wrote `coef_on_d()`, which returns the coefficient on the treatment for any list of controls, and used it to control for W and u1 together.
- I reproduced the LaLonde (1986) contrast between the randomised experiment and a CPS comparison group, then measured how much of the gap covariate adjustment closes.

## Key Findings

- The three worlds gave correlations of 0.654, 0.664 and 0.632, against true effects of 2.0, 0.0 and 0.0. The correlation alone could not tell them apart.
- Controlling for the confounder recovered the true effect. Controlling for the collider gave -0.592 where the truth is 0, and the result was highly significant.
- In the M-bias structure, controlling for W, which is measured before treatment, gave -0.202 where the truth is 0. When I also controlled for u1, the estimate was -0.013. Being measured before treatment did not make W a safe control.
- In the LaLonde data, the experimental estimate was $1,794, the naive CPS estimate was -$8,498, and the estimate with controls was $699. The controls closed 89% of the gap, but they did not reach the benchmark, and without a benchmark I could not have checked this.
- A DAG gives the assumptions that decide which variables to control for. It cannot tell me whether those assumptions are true.
