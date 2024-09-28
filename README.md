# Faa-di-Bruno-formula

# Faa di Bruno Formula with SymPy

This project provides an implementation of the **Faa di Bruno formula** using the symbolic computation library [SymPy](https://www.sympy.org/). The **Faa di Bruno formula** is a generalization of the chain rule for higher-order derivatives of composite functions. This implementation leverages **Bell polynomials** for efficiently computing the terms in the formula.

## Overview

### The Faa di Bruno Formula

The **Faa di Bruno formula** for the n-th derivative of a composite function can be written as:

$$
\frac{d^n}{dx^n} f(g(x)) = \sum_{k=1}^n f^{(k)}(g(x)) \cdot B_{n,k}(g'(x), g''(x), \dots, g^{(n-k+1)}(x))
$$

Where:
- \( f^{(k)} \) is the k-th derivative of \( f \),
- \( g^{(j)} \) is the j-th derivative of \( g \),
- \( B_{n,k} \) are the **Bell polynomials**, which are used to express the higher-order derivatives in terms of the lower-order derivatives of \( g(x) \).

### Bell Polynomials

The **Bell polynomials** \( B_{n,k} \) are a family of polynomials that appear in the Faa di Bruno formula. They represent the partitioning of the set of derivatives of \( g(x) \) and are defined as:

$$
B_{n,k}(y_1, y_2, \dots, y_{n-k+1}) = \sum \frac{n!}{j_1! j_2! \dots j_{n-k+1}!} \left( \frac{y_1}{1!} \right)^{j_1} \left( \frac{y_2}{2!} \right)^{j_2} \dots \left( \frac{y_{n-k+1}}{(n-k+1)!} \right)^{j_{n-k+1}}
$$

where the sum is taken over all sequences \( j_1, j_2, \dots, j_{n-k+1} \) such that:

$$
j_1 + j_2 + \dots + j_{n-k+1} = k, \quad \text{and} \quad j_1 + 2j_2 + \dots + (n-k+1)j_{n-k+1} = n.
$$

This project implements the Faa di Bruno formula using Bell polynomials to efficiently compute these terms.

## Installation

To use this project, you need to have Python installed along with the SymPy library. You can install SymPy via `pip`:

```bash
pip install sympy
