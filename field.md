A field is defined as a set $F$ and two closed binary operations $+$ and $\times$ which satisfy the following properties:

$F$ and $+$ form an [abelian group](./abelian-group.md):
1) Associativity: for all $a, b, c \in F$  then $(a + b) + c = a + (b + c)$
2) Commutativity: for all $a, b \in F$ then $a + b = b + a$
3) Identity: there exists an identity element $0 \in F$ such that for all $a \in F$ then $a + 0 = a$
4) Inverse: for all $a \in F$ there exists a $-a \in F$ such that $a + (-a) = 0$

$G = F - \{0\}$ and $\times$ form a [abelian group](./abelian-group.md):
5) Associativity: for all $a, b, c \in G$ then $(a \times b) \times c = a \times (b \times c)$
6) Commutativity: for all $a, b \in G$ then $a \times b = b \times a$
7) Identity: there exists an identity element $1 \in G$ such that for all $a \in G$ then $a \times 1 = a$
8) Inverse: for all $a \in G$ there exists a $1/a \in F$ such that $a \times (1/a) = 1$

$\times$ is [[distributivity|distributive]] with respect to $+$:
7) Left distributivity: for all $a,b,c \in R$ then $a \times (b + c) = (a \times b) + (a \times c)$
8) Right distributivity: for all $a,b,c \in R$ then $(b + c) \times a = (b \times a) + (c \times a)$

A field is a commutative [ring](./ring.md) where $0 \neq 1$ and non-zero elements are invertible under multiplication.

A field is a set for which addition, subtraction, multiplication and division are defined and behave as they would for rational numbers.