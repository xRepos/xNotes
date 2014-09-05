Logistic Regression
===================

Sigmoid/Logistic function

$$ g(z) = {1 \over 1+e^{-z}} $$

Hypothesis

$$ h_\theta(x) = g(\theta^Tx) = {1 \over 1 + e^{-\theta^Tx}}$$

* $$y=1$$ if $$h_\theta(x) \ge 0.5$$ (i.e. $$\theta^T x \ge 0$$)
* $$y=0$$ if $$h_\theta(x) < 0.5$$ (i.e. $$\theta^T x < 0$$)



Logistic Regression Cost Function

$$ J(\theta) = - {1 \over m} [\sum_{i=1}^m y^{(i)} \log h_\theta(x^{(i)}) + (1-y^{(i)}) \log(1-h_\theta(x^{(i)}))] $$

Gradient Descent

$$min_\theta J(\theta)$$

Repeat: simultaneously update all $$\theta_j$$

$$\theta_j:=\theta_j - \alpha {\partial \over \partial \theta_j} J(\theta) $$

$$\theta_j:= \theta_j - \alpha \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} $$

Regularization

$$ J(\theta) = - {1 \over m} [\sum_{i=1}^m y^{(i)} \log h_\theta(x^{(i)}) + (1-y^{(i)}) \log(1-h_\theta(x^{(i)}))] + {\lambda \over 2m} \sum_{i=1}^n \theta_j^2 $$