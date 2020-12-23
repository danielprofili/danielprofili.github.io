# Research

My research interests are in algebraic geometry, number theory, and combinatorics.

## Tropical resultants

### Resultant polytopes

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
precisely the resultant; however, in general, this operation is very
slow as computing Groebner bases is computationally intensive.

Below is a simple example resultant computed using
[SageMath](https://www.sagemath.org). Here, we define

$$p_1 = a_{11}x_1 + a_{12}x_2 + a_{13}$$

$$p_2 = a_{21}x_1 + a_{22}x_2 + a_{23}$$

$$p_1 = a_{31}x_1 + a_{32}x_2 + a_{33}$$

which live in the ring $$\mathbb{Q}[x_1, x_2]$$, and compute the generator of
the corresponding elimination ideal of $$I$$ with respect to $$x_1$$ and $$x_2$$.

<script src="https://gist.github.com/danielprofili/0e7df987e0f86b290edc6db38da4d9a0.js"></script>

The last line, `resultant.newton_polytope()`, computes the *Newton
polytope* of the resultant, which is defined as the convex hull of the
exponent vectors of the resultant polynomial. (By exponent vectors, we
mean the ordered tuples of integers whose $$i$$th entry is the exponent of
$$x_i$$ in any particular monomial.)

The Newton polytope is useful not only because it is a way to
visualize a polynomial, but it also provides a link to the powerful
tools of algebraic and tropical geometry. As it turns out, there is a
bijection between the number of vertices of the Newton polytope of the
resultant and the number of arrangements of so-called *tropical
hypersurfaces* corresponding to the original polynomials. 

### Tropical geometry

Tropical geometry is the study of the tropical semiring, which is
usually defined as $$\mathcal{T} = (\mathbb{R} \cup \{+\infty\},
\oplus, \otimes)$$ where the ring operations are defined by

$$x \oplus y = \min(x, y)$$

$$x \otimes y = x + y.$$

Equivalently, we can substitute $$-\infty$$ and define $$x \oplus y =
\max(x, y).$$ Under this interpretation, the tropical semiring can be
thought of as a projection of the real numbers under the logarithm map, 
using the fact that for $$x$$ and $$y$$ sufficiently far apart we have

$$\log(x + y) \approx \log \max(x, y) \text{ and}$$

$$\log(xy) = \log x + \log y.$$ 

An important fact to note is that these definitions satisfy all but
one of the ring axioms; i.e. the set $$\mathbb{R} \cup \infty$$ is an
abelian group under $$\oplus$$, the $$\otimes$$ operation
distributes and is associative, and $$\infty$$ acts as the additive
identity or "zero." The only missing axiom is the presence of additive
inverses; for instance, there is no element $$y$$ such that $$\min(5, y) = \infty$$.

The tropical semiring induces a mechanism by which we can
"linearlize" polynomials. For example, the tropical projection of

$$p(x) = x^5 + x^2 + 2x + 10$$

is

$$\mathcal{T}(p(x)) = (x \otimes \dots \otimes x) \oplus (x \otimes x)
\oplus (2 \otimes x) \oplus 10 =
\min(2x, 5x, 2+x, 10).$$

<script src="https://gist.github.com/danielprofili/edb4bf030d2ae6adeeed9ba4b76f028a.js"></script>

As we can see, plotting the tropical curve results in a
concave, piecewise linear function (note that if we use the maximum instead of
the minimum, we get a convex function instead). The points where the
piecewise components join together are called *roots*; equivalently,
these are the points at which the minimum of the tropical polynomial
is achieved more than once. The number of times the minimum value is
achieved is called the *order* of the root, and this is equal to the
difference in neighboring slopes at each root point.

The last line prints the Newton polytope of the original
polynomial. If you look closely, you'll see that the slopes of the
edges of the polytope are inverses of the slopes of the tropical
curve---put precisely, the tropical curve can be identified with the
*normal fan* of the polytope. Here is where the connection between
tropical geometry and resultants shines through: it is much easier to
deal with minima and sums than it is to deal with multiplication,
addition, and exponentiation, so if we can think about tropical
curves, we might be able to speed up resultant computations and avoid
Groebner basis calculations altogether.  

This connection forms the basis of this project. My co-advisor
Dr. Josephine Yu [proved](https://arxiv.org/pdf/1109.2368v1.pdf) that
the tropical resultant of a set of polynomials can be computed in
polynomial time, which is a huge improvement over the exponential
running time of Buchberger's algorithm for computing Groebner bases.
Thus, if we can come up with ways to cleverly manipulate tropical
resultants, it may be possible to deduce properties of the resultant
polynomial with much less computational effort.

# Sampling of strong orientations

Let $$G = (V, E)$$ be a strongly connected directed graph with $$|V| =
n$$ and $$|E| = m$$. An
*orientation* $$\mathcal{O}$$ of $$G$$ is a particular assignment of
edge directions. Define for each vertex $$v_i \in V$$

$$\alpha_i = \text{indeg}(v_i) - \text{outdeg}(v_i).$$

If we define $$\alpha = (\alpha_1, \dots, \alpha_{n})$$ then we say
that $$\mathcal{O}$$ is an $$\alpha$$-orientation of $$G$$. Clearly,
every orientation $$\mathcal{O}$$ of $$G$$ has some $$\alpha \in \mathbb{Z}^n$$ such
that $$\mathcal{O}$$ is an $$\alpha$$-orientation of $$G$$; thus the
mapping of orientations to $$\alpha$$'s induces an equivalence
relation on the set of all orientations of $$G$$.

It is a basic fact that any orientation can be transformed into any
other orientation via a sequence of *directed cycle
reversals*. Further, directed cycle reversals do not change the
$$\alpha$$ of a particular orientation, so the equivalence classes
under directed cycle reversals are the same as the equivalence classes
under the mapping from $$\mathcal{O} \mapsto \alpha(\mathcal{O})$$.

A *strong orientation* of a graph $$G$$ is an orientation such that
there exists a directed path from any vertex to any other vertex. From
this discussion, we can ask the following question: how can we
uniformly sample strong orientations of graphs?