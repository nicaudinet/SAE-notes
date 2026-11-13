A ring is defined as a set $R$ and two closed binary operations $+$ and $\times$ which satisfy the following properties:

$R$ and $+$ form an [abelian group](./abelian-group.md):
1) Associativity: for all $a, b, c \in R$  then $(a + b) + c = a + (b + c)$
2) Commutativity: for all $a, b \in R$ then $a + b = b + a$
3) Identity: there exists an identity element $0 \in R$ such that for all $a \in R$ then $a + 0 = a$
4) Inverse: for all $a \in R$ there exists a $-a \in R$ such that $a + (-a) = 0$

$R$ and $\times$ form a [monoid](./monoid.md):
5) Associativity: for all $a, b, c \in R$ then $(a \times b) \times c = a \times (b \times c)$
6) Identity: there exists an identity element $1 \in R$ such that for all $a \in R$ then $a \times 1 = a$

$\times$ is [[distributivity|distributive]] with respect to $+$:
7) Left distributivity: for all $a,b,c \in R$ then $a \times (b + c) = (a \times b) + (a \times c)$
8) Right distributivity: for all $a,b,c \in R$ then $(b + c) \times a = (b \times a) + (c \times a)$