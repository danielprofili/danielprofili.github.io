# Tropical resultants

Suppose we have polynomials $$f_1, \dots, f_n \in \mathbb{C}[x_1,
\dots, x_m],$$ each of the form

$$f_i = b_{i, 1} x_1^{a_{i,1}} + \dots + b_{i, m} x_m^{a_{i, m}},$$

where $$b_{i,k} \in \mathbb{C}$$ and $$a_{i, k} \in \mathbb{Z}.$$ What
can we say about the choices of coefficients $$b_{i,k}$$ which satisfy
$$f_1 = \dots = f_n = 0$$?

As it turns out, there is a unique polynomial called the *resultant*
which is defined as a polynomial $$R$$ of
the coefficients such that $$R(b_{1,1}, \dots, b_{n, m}) = 0$$ if and
only if the $$b_{i, j}$$'s satisfy $$f_1 = \dots = f_n = 0$$. 

The resultant is readily computed by calculating the elimination ideal
(e.g. by Groebner basis) the ideal $$I = (f_1, \dots, f_n)$$ generated
by the polynomials. The generator of the elimination ideal is
precisely the resultant. 

Below is an example resultant computed using
[SageMath](https://www.sagemath.org). Here, we define

$$p_1 = a_{11}x_1 + a_{12}x_2 + a_{13}$$

$$p_2 = a_{21}x_1 + a_{22}x_2 + a_{23}$$

$$p_1 = a_{31}x_1 + a_{32}x_2 + a_{33}$$

which live in $$\mathbb{Z}[x_1, x_2]$$, and compute the generator of
the corresponding elimination ideal.

<script src="https://gist.github.com/danielprofili/0e7df987e0f86b290edc6db38da4d9a0.js"></script>

# Sampling of strong orientations
