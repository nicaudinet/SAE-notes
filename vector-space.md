A vector space is defined by the following components:
- a [field](./field.md) $F$
- a non-empty [[set]] $V$
- a closed binary operation $+ : V \to V \to V$ called **vector addition**
- a binary function $\times : F \to V \to V$ called **scalar multiplication**

Elements of $V$ are called **vectors**. Elements of $F$ are called **scalars**.

The components must respect the following properties:
1) $V$ and $+$ form an [abelian group](./abelian-group.md) with identity $\bm{0} \in V$
2) Multiplication compatibility: for all $a,b \in F$ and $\vv \in V$ then $a(b\vv) = (ab)\vv$
3) Scalar identity: $1\vv = v$ where $1$ is the multiplicative identity in $F$
4) Distributivity of scalar multiplication with vector addition: for all $a \in F$ and $\vv, \uu \in V$ then $a(\vv + \uu) = a\vv + a\uu$
5) Distributivity of scalar multiplication with field addition: for all $a,b \in F$ and $\vv \in V$ then $(a+b)\vv = a\vv + b\vv$

A vector space is also called a linear space.