# CSDS 611 - Advanced topics and methods of Data Science I 

Final project
Due: Tuesday, December 1, by 8:00PM

Problem description: The Lotka-Volterra model is a set of mathematical equations that describes how prey $x$ and predator $y$ populations interact and change over time $t$ in an ecosystem. The model consists of an initial value problem

$$
\begin{aligned}
t & \in\left[t_{\min }, t_{\max }\right] \\
x\left(t_{\min }\right) & =\eta_{1} \\
y\left(t_{\min }\right) & =\eta_{2} \\
\frac{d x}{d t} & =+\theta_{1} x-\theta_{2} x y \\
\frac{d y}{d t} & =-\theta_{3} y+\theta_{4} x y
\end{aligned}
$$

In this project, we consider the Lotka-Volterra model with

$$
\begin{aligned}
t_{\min } & =0 \\
t_{\max } & =3 \times 10^{6} \\
\eta_{1} & =2.11 \\
\eta_{2} & =1.35
\end{aligned}
$$

and the provided data of measurements $x\left(t_{n}\right), y\left(t_{n}\right)$ at times $t_{n}$, and seek to estimate the values of the parameters $\theta_{1: 4}$ within the following parameter ranges

$$
\begin{aligned}
& \theta_{1} \in[0.10,50.0] \\
& \theta_{2} \in[0.01,2.00] \\
& \theta_{3} \in[0.10,5.00] \\
& \theta_{4} \in[0.01,2.00]
\end{aligned}
$$

Step 1: Cast the estimation of $\theta_{1: 4}$ as a least-squares optimization problem. Implement a Runge-Kutta numerical integrator to evaluate the solution of the initial value problem and the objective. Benchmark the execution time of a single objective evaluation.

Step 2: Implement a space-filling design with $\approx 50$ initial queries. Compute the objective at those queries and determine whether a surrogate for the objective or log-transformed objective might be more appropriate. Apply a Gaussian process prior and fine-tune its hyperparameters using the initial queries.

Step 3: Use your surrogate with the fine-tuned hyperparameters and implement a Bayesian optimization loop with your choice of acquisitions. Report trace plots with running incumbent optima and optimizers.

Step 4: Document your work, describe your methods, explain your choices in steps 1-3, and present your results.

