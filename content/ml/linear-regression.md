Linear Regression
=================

Hypothesis

$$ h_\theta(x) = \theta^T x $$

Parameter

$$ \theta $$

Cost function

$$ J(\theta) = {1 \over 2m} \sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})^2 $$

Goal

$$\underset{\theta}{\min} J(\theta)$$

Gradient Descent: simultaneously update all $$\theta_j$$

$$\theta_j:=\theta_j - \alpha {\partial \over \partial \theta_j} J(\theta) $$

Regularization

$$ J(\theta) = {1 \over 2m} {\Big [} \sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})^2 + \lambda \sum_{i=1}^n \theta_j^2 {\Big ]}$$