# Number Theory

## Numbers

### Types

Numbers can be classified into different types:

- **Integers**: whole numbers (e.g., 1, 2, 3)
- **Rational numbers**: numbers that can be expressed as a fraction (e.g., 1/2, 3/4); includes
  integers.
- **Irrational numbers**: numbers that cannot be expressed as a fraction (e.g., $\sqrt{2}$, $\pi$).
- **Real numbers**: numbers that can be represented on a continuous number line (e.g., 1.5, 2.75);
  this includes both rational and irrational numbers.
- **Complex numbers**: numbers that can be expressed as a combination of a real number and an
  imaginary number (e.g., $3 + 4i$).

Special types of numbers:

- **Prime numbers**: integers greater than 1 that have no positive divisors other than 1 and
  themselves (e.g., 2, 3, 5, 7). They are the building blocks of all numbers.
- **Composite numbers**: integers greater than 1 that are not prime (e.g., 4, 6, 8, 9).

### Properties

- **Closure**: the result of an operation on two numbers in a set remains in that set, if
  $a, b \in S$ then $a + b \in S$ and $a \times b \in S$
- **Commutative**: order in which two numbers are added or multiplied does not affect the result,
  $a + b = b + a$ and $a \times b = b \times a$
- **Associative**: when three or more numbers are added or multiplied, the grouping of the numbers
  does not change the result, $(a + b) + c = a + (b + c)$ and
  $(a \times b) \times c = a \times (b \times c)$
- **Distributive**: multiplication over addition, $a \times (b + c) = a \times b + a \times c$
- **Identity**: there exist elements that don't change a number when combined with it
  - Additive identity: $a + 0 = a$
  - Multiplicative identity: $a \times 1 = a$
- **Inverse**: for each number, there exists another number that combines with it to give the
  identity
  - Additive inverse: $a + (-a) = 0$
  - Multiplicative inverse: $a \times a^{-1} = 1$ (when $a \neq 0$)

These properties are fundamental to understanding groups, rings, and fields, as different algebraic
structures require different combinations of these properties.

### Operations

You can perform operations on numbers, e.g., addition, subtraction, multiplication, division,
exponentiation, and modular arithmetic:

- **Addition**: $a + b$
- **Subtraction**: $a - b$
- **Multiplication**: $a \times b$
- **Division**: $a / b$
- **Exponentiation**: $a^b$
- **Modular arithmetic**: $a \mod b$

### Modular arithmetic

Modular arithmetic is a system of arithmetic for integers, where numbers "wrap around" upon reaching
a certain value, called the modulus. It's an important concept in prime fields, used in
cryptography. The arithmetic is denoted as $a \equiv b \pmod{m}$, where $a$ is the number, $b$ is
the result of the operation, and $m$ is the modulus:

- **Addition**: $a + b \equiv c \pmod{m}$
- **Subtraction**: $a - b \equiv c \pmod{m}$
- **Multiplication**: $a \times b \equiv c \pmod{m}$
- **Exponentiation**: $a^b \equiv c \pmod{m}$

E.g., in modulo 5 arithmetic, $4 + 3 \equiv 2 \pmod{5}$. This is because $4 + 3 = 7$, and
$7 \mod 5 = 2$. Thus, $7 \equiv 2 \pmod{5}$.

A quick example of finding `m` in modular arithmetic:

- Starting with $10 \equiv 2 \pmod{m}$
- Find the absolute difference between $10$ and $2$, which is $10 - 2 = 8$
- Determine all factors (or divisors) of $8$, which are $1, 2, 4, 8$
- Any of these factors can be the modulus, $m$, so $m = \{1, 2, 4, 8\}$

Or algorithmically:

```python
def find_moduli(a: int, b: int) -> list[int]:
    # Step 1: Find absolute difference
    diff = abs(a - b)

    # Step 2: Find all divisors of the difference
    # We only need to check up to the square root of the difference to find all divisors
    divisors = []
    for i in range(1, int(diff ** 0.5) + 1):
        if diff % i == 0:
            # Add both divisors (i and diff/i)
            divisors.append(i)
            if i != diff // i:  # Avoid adding square roots twice
                divisors.append(diff // i)

    return sorted(divisors)

# Find all m where 10 ≡ 2 (mod m)
moduli = find_moduli(10, 2)
print(moduli)  # Output: [1, 2, 4, 8]
```

## Sets

A set is a collection of elements $S = \{a, b, c, \ldots\}$. The order of members is not important,
it can be finite or infinite, and each member is _unique_. Notation defines some $x \in S$ as "$x$
belongs to (or is in) $S$".

There are different types of sets:

- **Empty sets**: has no members, denoted as $\emptyset$.
- **Singleton**: has one and only one member, e.g., $\{x\}$ has only $x$ as a member.
- **Subsets**: a set of elements that are all members of another set. E.g., if $A = \{a, b\}$ and
  $B = \{a, b, c\}$, then $A \subseteq B$ ($A$ is a subset of $B$) or $B \supseteq A$ ($B$ is a
  superset of (or contains) $A$).

Special sets are well known and have specific names:

- $\mathbb{N}$—natural numbers: $\mathbb{N} = \{1, 2, 3, \ldots\}$ (zero is usually excluded)
- $\mathbb{Z}$—integers: $\mathbb{Z} = \{\ldots, -2, -1, 0, 1, 2, \ldots\}$
- $\mathbb{Q}$—rational numbers: $\mathbb{Q} = \{\frac{a}{b} \mid a, b \in \mathbb{Z}, b \neq 0\}$
  (i.e., fractions)
- $\mathbb{R}$—real numbers: $\mathbb{R} = \{\ldots, -2, -1, 0, 1, 2, \ldots\}$ (i.e., all numbers
  that can be represented on a continuous number line)
- $\mathbb{C}$—complex numbers: $\mathbb{C} = \{a + bi \mid a, b \in \mathbb{R}\}$
- Although irrational numbers do not have their own special set, they are the difference between the
  real numbers and rational numbers: $\mathbb{R} - \mathbb{Q}$

### Partitions

A partition of a set $S$ is a collection of disjoint subsets of $S$ that cover all elements of $S$
and have no overlap. E.g., if $S = \{1, 2, 3, 4, 5\}$, then $\{ \{1, 2\}, \{3, 4, 5\} \}$ is a
partition of $S$ because it covers all elements of $S$ and **has no overlap**. This is also known as
a "disjoint partition". Any two sets of the partition contain no element in common, and the union of
all sets in the partition is equal to the original set.

### Cardinality

The cardinality of a set is the number of elements in the set, denoted $|A|$. E.g.,
$A = \{1, 2, 3\}$ has a cardinality of 3.

### Operations

You can perform operations on sets. Let's assume a universal set $U$ that contains all elements,
including $A$ and $B$.

- **Absolute complement**: all members of $U$ that are not in $A$, thus,
  $A' = U - A = \{x \mid x \in U \text{ and } x \notin A\}$
- **Union**: members are in $A$ or $B$ or both, $A \cup B = \{x \mid x \in A \text{ or } x \in B\}$
- **Intersection**: members are in both $A$ and $B$,
  $A \cap B = \{x \mid x \in A \text{ and } x \in B\}$
- **Set difference** (relative complement): members are in $A$ but not in $B$,
  $A - B = \{x \mid x \in A \text{ and } x \notin B\}$
- **Symmetric difference**: members are in $A$ or $B$ but not both,
  $A \oplus B = (A - B) \cup (B - A)$
- **Cartesian product**: ordered pairs of elements from $A$ and $B$,
  $A \times B = \{(a, b) \mid a \in A \text{ and } b \in B\}$

Here are some examples for $A = \{1, 2, 3\}$ and $B = \{2, 3, 4\}$ in $U = \{1, 2, 3, 4\}$:

- $A' = \{4\}$
- $A \cup B = \{1, 2, 3, 4\}$
- $A \cap B = \{2, 3\}$
- $A - B = \{1\}$
- $A \oplus B = \{1, 4\}$
- $A \times B = \{(1, 2), (1, 3), (1, 4), (2, 2), (2, 3), (2, 4), (3, 2), (3, 3), (3, 4)\}$

## Relations

A relation denotes some kind of relationship between two _elements_ in a set. A relation $R$ from
domain $A$ to codomain $B$ is a set of ordered pairs $(a, b)$ where $a$ is from the domain and $b$
is from the codomain. That is, it's a subset of the Cartesian product $A \times B$. Often, the
domain and codomain are the same set, $A = B$.

This is why functions are a subset of relations; they are a special type of relation where each
element of the domain maps to exactly one element of the codomain. It's also why the notation will
use $X$ as the domain, $Y$ as the codomain, $(x,y)$ as the ordered pairs within the relation, and
$R$ as the relation.

For example, if $X = \{1, 2, 3\}$, $Y = \{2, 3, 4\}$, and $R$ is a relation for "less than", then
$R = \{(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)\}$ where $(x,y) \in R$. $(x,y) \in R$ reads "x
is R-related to y", often denoted as $xRy$. Note that in this case, order matters, so $(1, 2) \in
R$
but $(2, 1) \notin R$.

### Functions

A function (or mapping) is a relation where each element of $A$ is related to _exactly one_ element
of $B$. That is, inputs in $A$ (domain) maps to outputs in $B$ (codomain). Functions are a subset of
relations, and there are a few special types of functions:

- **Injective (one-to-one; left-unique)**: each element of $A$ maps to at most one element of
  $B$—i.e., no two inputs give the same output. Set sizes can differ (e.g., |A| > |B|).
- **Surjective (onto; right-total)**: for every element of $B$, there is at least one element of $A$
  that maps to it—i.e., every output is mapped to by at least one input, so all possible outputs are
  it—i.e., every output is mapped to by at least one input, so all possible outputs are used.
- **Bijective (one-to-one correspondence)**: each element of $A$ maps to a unique element of $B$,
  and each element of $B$ is mapped to a unique element of $A$. That is, it's both injective and
  surjective, so the domain and codomain have the same number of elements.

When comparing two sets $A$ and $B$, you refer to $A$ as the "domain" and $B$ as the
"codomain"—these are terms defined in the context of relations. Here's a quick and dirty example of
each of these:

```python
X = {1, 2, 3}
Y = {4, 5, 6}

# Regular relation (not a function - one input maps to multiple outputs)
relation = {(1,4), (1,5), (2,5), (3,6)}

# Function (each input maps to exactly one output)
function = {(1,4), (2,5), (3,6)}

# Injective function (each output mapped to by at most one input)
injective = {(1,4), (2,5), (3,6)}

# Surjective function (each output mapped to by at least one input)
surjective = {(1,4), (2,5), (3,6)}

# Bijective function (perfect pairing)
bijective = {(1,4), (2,5), (3,6)}
```

And a more algorithmic example:

```python
# Using the following sets
X = {1, 2, 3} # input, or domain
Y = {4, 5, 6, 7} # output, or codomain

# 1. Injective (one-to-one): each input maps to a different output
def injective_example(x):
    """Each input maps to a unique output, but doesn't use all of B"""
    return x * 2 + 2  # 1->4, 2->6, 3->8
    # Note: This maps to 4,6,8 (misses 5,7 but that's okay for injective)

Y = {4, 5, 6} # ensure equal sized sets
# 2. Surjective (onto): every element in B must be mapped to
def surjective_example(x):
    """Maps to every element in B, but with duplicates allowed"""
    if x == 1: return 4
    if x == 2: return 5
    return 6

# 3. Neither injective nor surjective
def neither_example(x):
    """Neither unique mappings nor covers all outputs"""
    return 4  # Everything maps to 4
    # Not injective (all inputs -> 4)
    # Not surjective (never reaches 5,6,7)

# 4. Bijective example (needs equal sized sets)
def bijective_example(x):
    """Perfect one-to-one correspondence"""
    return x + 3  # 1->4, 2->5, 3->6
    # Injective (all unique)
    # Surjective (hits everything in B)
```

#### Properties

Relations can have the following properties, and properties can be combined:

- **Reflexive**: every element relates to itself

  - Definition: For all $a \in X$, $(a,a) \in R$
  - Example: $\geq$, $=$, "is same age as", "is similar to"

- **Irreflexive**: no element relates to itself

  - Definition: For all $a \in X$, $(a,a) \notin R$
  - Example: $>$, $<$, "is child of", "is taller than", "is parent of"

- **Symmetric**: if $a$ relates to $b$, then $b$ relates to $a$

  - Definition: If $(a,b) \in R$ then $(b,a) \in R$
  - Example: $=$, "is friend of", "is married to", "is sibling of"

- **Asymmetric**: if $a$ relates to $b$, then $b$ never relates to $a$

  - Definition: If $(a,b) \in R$ then $(b,a) \notin R$
  - Example: $>$, $<$, "is ancestor of", "is strictly older than", "is strictly taller than"

- **Antisymmetric**: if $a$ relates to $b$ and $b$ relates to $a$, then $a = b$

  - Definition: If $(a,b) \in R$ and $(b,a) \in R$ then $a = b$
  - Example: $\geq$, $\leq$, "divides", "is older than or same age as", "is at least as tall as"

- **Transitive**: if $a$ relates to $b$ and $b$ relates to $c$, then $a$ relates to $c$

  - Definition: If $(a,b) \in R$ and $(b,c) \in R$ then $(a,c) \in R$
  - Example: $>$, $<$, $\geq$, $\leq$, $=$, "is taller than", "is greater than"

- **Connected**: for different elements, at least one relates to the other

  - Definition: For all $a,b \in X$ where $a\neq b$, either $(a,b) \in R$ or $(b,a) \in R$
  - Example: $\leq$, $\geq$, "is comparable to"

- **Strongly Connected**: for any elements, at least one relates to the other

  - Definition: For all $a,b \in X$, either $(a,b) \in R$ or $(b,a) \in R$
  - Example: $\leq$ or $\geq$, "is comparable to or equal to"

Or, thinking about it in terms of operators:

- $=$ (equals) is:
  - Reflexive ($a = a$)
  - Symmetric (if $a = b$, then $b = a$)
  - Transitive (if $a = b$ and $b = c$, then $a = c$)
- $\leq$ (less than or equal) is:
  - Reflexive ($a \leq a$)
  - Antisymmetric (if $a \leq b$ and $b \leq a$, then $a = b$)
  - Transitive (if $a \leq b$ and $b \leq c$, then $a \leq c$)
  - Connected (for any $a,b$, either $a \leq b$ or $b \leq a$)
- $<$ (less than) is:
  - Irreflexive ($a < a$)
  - Asymmetric (if $a < b$, then $b < a$)
  - Transitive (if $a < b$ and $b < c$, then $a < c$)
  - Connected (for any $a \neq b$, either $a < b$ or $b < a$)

The key is that these properties describe how elements relate to:

- Themselves (reflexive or irreflexive)
- Each other (symmetric or antisymmetric)
- Through intermediaries (transitive)

Let's look at some examples:

```python
# Define the set
X = {1, 2, 3}

X = {1, 2, 3}  # domain and codomain are the same set

# Reflexive: every element relates to itself
reflexive_equals = {(1,1), (2,2), (3,3), (1,2), (2,1)}  # "equals or is friends with"
reflexive_gte = {(1,1), (2,2), (3,3), (2,1), (3,1), (3,2)}  # "greater than or equal to"
# Must include (1,1), (2,2), and (3,3)

# Irreflexive: no element relates to itself
irreflexive_gt = {(2,1), (3,1), (3,2)}  # "greater than"
# Must NOT include (1,1), (2,2), or (3,3)

# Symmetric: if aRb then bRa
symmetric_friends = {(1,2), (2,1), (1,3), (3,1)}  # "is friends with"
# If (1,2) exists, (2,1) must also exist

# Asymmetric: if aRb then bRa is NEVER true (even when a=b)
asymmetric_gt = {(2,1), (3,1), (3,2)}  # "is greater than"
# Stricter than antisymmetric - no reflexive pairs allowed
# Think: "is strictly older than", "is proper subset of"

# Antisymmetric: if aRb then NOT bRa (unless a=b)
antisymmetric_gte = {(1,1), (2,2), (3,3), (2,1), (3,1), (3,2)}  # "greater than or equal to"
# If (2,1) exists, (1,2) cannot exist (unless 1=2)

# Transitive: if aRb and bRc then aRc
transitive_gt = {(2,1), (3,1), (3,2)}  # "greater than"
# If (3,2) and (2,1) exist, (3,1) must also exist

# Connected: for any two different elements, at least one relates to the other
connected_lte = {(1,1), (1,2), (1,3), (2,2), (2,3), (3,3)}  # "less than or equal to"
# For any a,b where a≠b, either aRb or bRa must exist
# Think: "is comparable to", "is less than or equal to"

# Strongly connected: for ANY two elements, at least one relates to the other
strongly_connected = {(1,1), (1,2), (1,3), (2,1), (2,2), (2,3), (3,1), (3,2), (3,3)}
# For ANY a,b (even same elements), either aRb or bRa must exist
# Think: "is less than or equal to or greater than or equal to"
```

## Groups, Rings, and Fields

Groups, rings, and fields are sets of elements with binary operations. The hierarchy is:

- Groups (one operation, inverses)
- Rings (two operations, additive inverses)
- Fields (two operations, both types of inverses)

Namely, groups are the most basic set, and fields are the most restrictive.

### Groups

A group is a pair containing a set $G$ with an arbitrary binary operation $\cdot$ (typically $+$ or
$\times$) that satisfies—i.e., $(G, \cdot)$ is a group. In other words, it's a set _with_ an
operation that satisfies the following axioms:

- **Closure**: for all $a, b \in G$, $a \cdot b \in G$; i.e., the result of the operation is in the
  set
- **Associativity**: for all $a, b, c \in G$, $(a \cdot b) \cdot c = a \cdot (b \cdot c)$; i.e., the
  operation is associative (the order of operations doesn't matter)
  - Note: the associative property deals with grouping, while the transitive property deals with
    relating values through equality
- **Identity**: there exists an element $e \in G$ such that for all $a \in G$,
  $e \cdot a = a \cdot e = a$; i.e., there is an identity element that, when combined with any
  element of the group, yields that element
  - E.g., for addition, the identity element is $0$ (since $a + 0 = a$ and $0 + a = a$), or for
    multiplication, the identity element is $1$ (since $a \times 1 = a$ and $1 \times a = a$)
- **Invertibility**: for all $a \in G$, there exists an element $b \in G$ such that
  $a \cdot b = b \cdot a = e$; i.e., there is an inverse element that, when combined with any
  element of the group, yields the identity element
  - E.g., for addition, the inverse element is $-a$ (since $a + (-a) = -a + a = 0$), or for
    multiplication, the inverse element is $1/a$ (since $a \times 1/a = 1/a \times a = 1$)

Here's a simple example:

```python
# Example: Integers under addition (Z,+)
def integer_group_example():
    # 1. Closure: sum of integers is integer
    assert 5 + 3 == 8  # stays in integers

    # 2. Associativity: (a+b)+c = a+(b+c)
    a, b, c = 1, 2, 3
    assert (a + b) + c == a + (b + c)

    # 3. Identity: 0 is the identity for addition
    assert 0 + 5 == 5
    assert 5 + 0 == 5

    # 4. Inverse: each number has additive inverse (-n)
    n = 5
    assert n + (-n) == 0
    assert (-n) + n == 0
```

#### Abelian (commutative) groups

Abelian (commutative) groups are groups where the operation is commutative (i.e.,
$a \cdot b = b \cdot a$). Conversely, non-abelian groups are groups where the operation is not
commutative (i.e., $a \cdot b \neq b \cdot a$). For example, adding integers is commutative, but
matrix multiplication (typically) is not.

#### Cyclic groups

A cyclic group is a group that can be generated by a single element $g$ such that every other
element of the group may be obtained by repeatedly applying the group operation to g or its inverse.
That is, for some element $g \in G$, every element of the group can be written as $g^k$ for some
integer $k$.

For example, the integers under addition modulo $n$ form a cyclic group, where the generator is $1$.
Or algorithmically:

```python
# Cyclic group example: integers mod 5 under addition
def cyclic_group_example():
    # Generator element (2)
    # Repeatedly adding 2 generates all elements:
    # 2 -> 4 -> 1 -> 3 -> 0 -> back to 2
    mod = 5
    generator = 2
    element = generator
    seen = {element}

    for _ in range(4):  # mod-1 times
        element = (element + generator) % mod
        seen.add(element)

    # We've generated all elements {0,1,2,3,4}
    assert seen == {0,1,2,3,4}
```

Note that cyclic groups can be finite or infinite. For example, the integers under addition form an
infinite cyclic group, where the generator is $1$ (e.g., $1, 2, 3, 4, \ldots$) or its inverse $-1$
(e.g., $\ldots,4, 3, 2, 1$).

#### Order of a group & element

The order of a (finite) _group_ is the number of elements in the group. The order of an _element_
(or "period") $a$ is the order of the cyclic subgroup generated by the element. That is, the
smallest positive integer $m$ such that $a^m = e$. If the group is not finite, the order of an
element is infinite.

For example, in the integers under addition modulo $5$, the order of the group is $5$ (since there
are 5 elements: $\{0,1,2,3,4\}$), and the order of the element $2$ is $5$ (since $2^5 = 0$).

Here's how to find the order of elements in modulo 5:

```python
def find_element_order(element: int, modulus: int) -> int:
    """Find the order of an element in a modular group."""
    current = element
    order = 1

    while current != 0:  # For additive groups, identity is 0
        current = (current + element) % modulus
        order += 1

    return order

# Example in Z5 (integers modulo 5)
mod = 5
for element in range(1, mod):
    order = find_element_order(element, mod)
    print(f"Order of {element} in Z{mod}: {order}")
    # Order of 1 in Z5: 5
    # Order of 2 in Z5: 5
    # Order of 3 in Z5: 5
    # Order of 4 in Z5: 5
```

Note that:

- The order of an element must divide the order of the group
- In a finite group, the order of any element is finite
- The identity element always has order 1
- If an element generates the entire group, its order equals the group's order

#### Homomorphisms

A group homomorphism is a mapping $h : G \to H$ between two groups, from $(G, *)$ to $(H, \cdot)$,
that preserves the group operation. That is, for all $u, v \in G$, $h(u * v) = h(u) \cdot h(v)$, so
the group operation on the left side of the equation is that of $G$ and on the right side that of
$H$. There are five properties of group homomorphisms:

- **Monomorphism**: $h$ is injective (one-to-one)
- **Epimorphism**: $h$ is surjective (onto)
- **Isomorphism**: $h$ is bijective (one-to-one and onto)
- **Endomorphism**: $h$ is a homomorphism from a group to itself; $h : G \to G$ (domain and codomain
  are the same), but it is not necessarily bijective
- **Automorphism**: $h$ is both an endomorphism and an isomorphism from a group to itself;
  $h : G \to G$ (domain and codomain are the same), so it _is_ bijective

> [!NOTE]
>
> A homomorphism is like a relation but for groups. Relations relates elements within/between sets
> (and no requirement to preserve any structure), while homomorphisms relates groups while
> preserving their structure.

Here's an example of a homomorphism:

```python
# Example: Homomorphism from (Z,+) to (Z_2,×)
def parity_homomorphism(n: int) -> int:
    """Maps integers to {0,1} based on parity"""
    return n % 2

a, b = 3, 5
# Left side: f(a + b)
assert parity_homomorphism(a + b) == 1  # f(8) = 0
# Right side: f(a) × f(b)
assert (parity_homomorphism(a) * parity_homomorphism(b)) % 2 == 1  # (1 × 1) % 2 = 1
# Verify they're equal
assert parity_homomorphism(a + b) == (parity_homomorphism(a) * parity_homomorphism(b)) % 2

# Example: Endomorphism vs Automorphism
# Endomorphism example (not an automorphism)
def double_map(n: int) -> int:
    """Maps Z → Z by doubling
    This is an endomorphism but not an automorphism
    because it's not bijective (misses odd numbers)"""
    return 2 * n

# Automorphism example
def negate_map(n: int) -> int:
    """Maps Z → Z by negating
    This is an automorphism because it's bijective"""
    return -n
```

Homomorphisms have the following properties. Let $e_H$ be the identity element of $H$, and $e_G$ be
the identity element of $G$, for any $u \in G$:

- Thus, $h(u) \cdot e_H = h(u) = h(u * e_G) = h(u) \cdot h(e_G)$
  - $h(u) \cdot e_H = h(u)$ (since $e_H$ is the identity element in $H$)
  - $h(u) = h(u * e_G)$ (since $e_G$ is the identity element in $G$)
  - $h(u) = h(u) \cdot h(e_G)$ (since $h$ is a homomorphism)
- Therefore, $e_H = h(e_G)$ (via cancellation or multiplying for the inverse of $h(u)$)
- Similarly, $e_H = h(e_G) = h(u * u^{-1}) = h(u) * h(u^{-1})$
  - $e_H = h(e_G)$ (from above)
  - $e_H = h(u * u^{-1})$ (since $u * u^{-1} = e_G$)
  - $e_H = h(u) * h(u^{-1})$ (since $h$ is a homomorphism)
- Therefore, $h(u^{-1}) = h(u)^{-1}$

So, our two properties are:

1. $e_H = h(e_G)$
2. $h(u^{-1}) = h(u)^{-1}$

We can take our example from above and verify these properties:

```python
def parity_homomorphism(n: int) -> int:
    """Maps integers to {0,1} based on parity"""
    return n % 2

# Identity property: h(e_G) = e_H
# In (Z,+), e_G = 0
# In (Z_2,×), e_H = 1
assert parity_homomorphism(0) == 1  # h(e_G) = e_H

# Inverse property: h(-n) = h(n)^(-1)
n = 3
assert parity_homomorphism(-n) == parity_homomorphism(n)  # In Z_2, 1 is its own inverse
```

#### Kernel and image

The kernel of a homomorphism $h : G \to H$ is the set of elements in $G$ that map to the identity
element in $H$, denoted as $\ker(h) := \{ u \in G : h(u) = e_H \}$. The image of a homomorphism
$h : G \to H$ is the set of elements in $H$ that are the result of applying the homomorphism to some
element in $G$, denoted as $\text{im}(h) \colonequals h(G) \equiv \{ h(u) : u \in G \}$.

- Note: $\colonequals$ (colon equals) is used for definitions and assignments, and $\equiv$
  (equivalent) is used for logical equivalence or identical equality.

For example, in the homomorphism from the integers under addition to the integers modulo 2 under
multiplication:

```python
def parity_homomorphism(n: int) -> int:
    """Maps integers to {0,1} based on parity"""
    return n % 2

# Kernel: elements that map to identity (0 in Z_2)
# These are all even integers {..., -2, 0, 2, 4, ...}
assert parity_homomorphism(0) == 0
assert parity_homomorphism(2) == 0
assert parity_homomorphism(4) == 0

# Image: all possible outputs
# In this case, {0, 1}
seen_outputs = {parity_homomorphism(n) for n in range(5)}
assert seen_outputs == {0, 1}  # Complete image of Z_2

# Verify kernel maps to identity
def is_in_kernel(n: int) -> bool:
    """Check if n is in kernel (maps to identity)"""
    return parity_homomorphism(n) == 0

assert is_in_kernel(0)   # True (even)
assert is_in_kernel(2)   # True (even)
assert not is_in_kernel(1)  # False (odd)
assert not is_in_kernel(3)  # False (odd)
```

### Rings

A ring is a set of elements with _two_ binary operations. They are similar to groups but have two
operations (typically addition and multiplication), defined as $(R, +, \times)$. Namely, groups have
_one_ operation with inverses, and rings have _two_ operations but only requires that inverses apply
to the _additive_ operation.

The axioms extend the group axioms:

1. $(R,+)$ must be an abelian group:
   - Closure under addition
   - Associative addition
   - Additive identity (0)
   - Additive inverse ($-a$)
   - Commutative addition
2. $(R, \times)$ must satisfy:
   - Closure under multiplication
   - Associative multiplication
   - Multiplicative identity (1)
3. Distributive laws:
   - Left: $a \times (b + c) = (a \times b) + (a \times c)$
   - Right: $(b + c) \times a = (b \times a) + (c \times a)$

```python
# Example: Integers form a ring under + and ×
def integer_ring_example():
    # Group properties (under +)
    a, b, c = 2, 3, 4

    # 1. Additive group properties
    assert 5 + 3 == 8                    # closure
    assert (a + b) + c == a + (b + c)    # associative
    assert 0 + a == a                    # identity
    assert a + (-a) == 0                 # inverse
    assert a + b == b + a                # commutative

    # 2. Multiplicative properties
    assert 5 * 3 == 15                   # closure
    assert (a * b) * c == a * (b * c)    # associative
    assert 1 * a == a                    # identity

    # 3. Distributive laws
    assert a * (b + c) == (a * b) + (a * c)  # left distributive
    assert (b + c) * a == (b * a) + (c * a)  # right distributive
```

Common examples of rings:

- Integers ($\mathbb{Z}$) under $+$ and $\times$ (abelian)
- Real numbers ($\mathbb{R}$) under $+$ and $\times$ (abelian)
- Polynomials under $+$ and $\times$ (abelian)
- Matrices under $+$ and $\times$ (non-abelian)

### Fields

A field is a ring where the multiplicative operation is commutative, defined as $(F, +, \times)$.
That is, it is a special case of a ring. A field $(F,+,\times)$ must satisfy the following:

- _All_ ring properties (abelian group under $+$, closure/associative under $\times$, distributive)
- Multiplication is commutative (abelian)
- Every (non-zero) element has a multiplicative inverse

Here's an example of a field:

```python
# Example: Real numbers form a field
def real_number_field_example():
    a, b, c = 2.0, 3.0, 4.0

    # 1. Ring properties
    # Addition group
    assert 5.0 + 3.0 == 8.0              # closure
    assert (a + b) + c == a + (b + c)    # associative
    assert 0.0 + a == a                  # additive identity
    assert a + (-a) == 0                 # additive inverse
    assert a + b == b + a                # commutative

    # Multiplication properties
    assert 5.0 * 3.0 == 15.0             # closure
    assert (a * b) * c == a * (b * c)    # associative
    assert 1.0 * a == a                  # multiplicative identity

    # Distributive
    assert a * (b + c) == (a * b) + (a * c)

    # 2. Field-specific properties
    # Multiplication is commutative
    assert a * b == b * a

    # Non-zero elements have multiplicative inverses
    assert a * (1.0/a) == 1.0 # multiplicative inverse

    # Note: Can't divide by zero!
    # 1.0/0.0 would raise an error

# Counter-example: Integers are NOT a field
def integer_non_field_example():
    # Most ring properties work...
    assert 5 + 3 == 8
    assert 5 * 3 == 15

    # But: No multiplicative inverses for most elements!
    # For `2`, we have `2 * (1/2) = 1` (identity)...but `1/2` is not an integer
    # This is why we need fractions/rational numbers
```

Common examples of fields:

- Real numbers ($\mathbb{R}$)
- Complex numbers ($\mathbb{C}$)
- Rational numbers ($\mathbb{Q}$)

## Finite fields

A finite field (or Galois Field, $GF$) is a field with a finite number of elements. The order of a
finite field is always a prime power ($p^n$ where $p$ is prime and $n \geq 1$).

### Prime fields

The simplest finite fields are prime fields, denoted as $GF(p)$ or $\mathbb{F}_p$, where $p$ is
prime. These are the integers modulo $p$ with addition and multiplication; a field with a prime
number of elements. Properties of $GF(p)$ include:

1. Contains exactly $p$ elements: $\{0, 1, ..., p-1\}$
2. Every non-zero element has a multiplicative inverse
3. Addition and multiplication are closed (i.e., closure) and associative
4. Both operations are commutative
5. Multiplication distributes over addition (i.e., distributing/factoring)

Here's an example of $GF(5)$:

```python
def mod_add(a: int, b: int, p: int) -> int:
    """Addition in GF(p)"""
    return (a + b) % p

def mod_mul(a: int, b: int, p: int) -> int:
    """Multiplication in GF(p)"""
    return (a * b) % p

def mod_inv(a: int, p: int) -> int:
    """Find multiplicative inverse in GF(p) using extended Euclidean algorithm"""
    if a == 0:
        raise ValueError("Zero has no multiplicative inverse")

    def extended_gcd(a: int, b: int) -> tuple[int, int, int]:
        """Returns (gcd, x, y) where ax + by = gcd"""
        if a == 0:
            return b, 0, 1
        gcd, x1, y1 = extended_gcd(b % a, a)
        x = y1 - (b // a) * x1
        y = x1
        return gcd, x, y

    _, x, _ = extended_gcd(a, p)
    return x % p

# Example operations in GF(5)
p = 5
assert mod_add(3, 4, p) == 2     # 3 + 4 ≡ 2 (mod 5)
assert mod_mul(3, 4, p) == 2     # 3 * 4 ≡ 2 (mod 5)
assert mod_mul(3, mod_inv(3, p), p) == 1  # 3 * 3^(-1) ≡ 1 (mod 5)
```

Prime fields are used in cryptography because they are simple and have well-understood properties:

1. **Finite**: Operations wrap around, giving us a bounded space to work in
2. **Structure**: Every non-zero element has a multiplicative inverse (crucial for division)
3. **Security**: The discrete logarithm problem is hard in well-chosen prime fields
4. **Efficiency**: Modular arithmetic can be implemented efficiently

Thus, prime fields form the foundation for:

- Elliptic curve cryptography (like secp256k1 used in Bitcoin)
- Diffie-Hellman key exchange
- Many other cryptographic protocols

### Finite fields of order $p^n$

Finite fields of order $p^n$ are denoted as $GF(p^n)$ or $\mathbb{F}_{p^n}$. These fields are
constructed from the prime field $GF(p)$ by "adding a root" (call it $\alpha$) of an irreducible
polynomial of degree $n$ over $GF(p)$. _Adding a root_ means introducing a new element ($\alpha$)
that satisfies some polynomial equation over $GF(p)$. This new element lets us construct more field
elements as polynomials in $\alpha$, and the irreducible polynomial tells us how to reduce higher
powers of $\alpha$ back into the field.

More specifically, an irreducible polynomial is a polynomial that cannot be factored into the
product of two non-constant (i.e., degree $\geq 1$) polynomials with coefficients in the same field.
A simple example:

- $x^2 - 1$ _is_ reducible because it can be factored into $(x-1)(x+1)$, and both factors $1$ and
  $-1$ are within the same field. That is, we can factor it into the product of two constant (i.e.,
  degree zero) polynomials.
- However, $x^2 + 1$ is irreducible over the _real_ numbers because it cannot be factored into
  $(x-a)(x-b)$ for real numbers $a$ and $b$; it factors into $(x-i)(x+i)$ over the complex numbers.
- Similarly, $x^2 - 2$ is irreducible over the _rational_ numbers because it cannot be factored into
  $(x-a)(x-b)$ for rational numbers $a$ and $b$; it factors into $(x-\sqrt{2})(x+\sqrt{2})$ over the
  _real_ numbers (which includes irrational numbers).

#### Properties

1. Contains $p^n$ elements
2. Every non-zero element has a multiplicative inverse
3. Addition and multiplication are closed and associative
4. Both operations are commutative
5. Multiplication distributes over addition

#### Construction

1. Start with a prime field $GF(p)$
2. Find an irreducible polynomial of degree $n$ over $GF(p)$
3. Elements are polynomials of degree $< n$ with coefficients in $GF(p)$

Think about how we construct complex numbers from real numbers:

1. We start with real numbers (like $GF(p)$)
2. We add a "root" $i$ where $i^2 = -1$ (an irreducible polynomial $x^2 + 1 = 0$)
3. This gives us new numbers of the form $a + bi$

Example of $GF(2^3)$:

```python
# GF(2^3) constructed using irreducible polynomial x³ + x + 1
# Elements are binary polynomials: a₂x² + a₁x + a₀
# where aᵢ ∈ {0,1}
def poly_add(a: list[int], b: list[int]) -> list[int]:
    """Add polynomials in GF(2^n)"""
    # XOR coefficients (addition mod 2)
    return [x ^ y for x, y in zip(a, b)]

def poly_mul(a: list[int], b: list[int], mod_poly: list[int]) -> list[int]:
    """Multiply polynomials in GF(2^n) with reduction
    mod_poly represents x³ + x + 1 as [1,0,1,1]"""
    # Initialize result with zeros (degree 2n-2)
    result = [0] * (len(a) + len(b) - 1)

    # Multiply polynomials
    for i in range(len(a)):
        for j in range(len(b)):
            result[i + j] ^= a[i] & b[j]  # XOR for addition in GF(2)

    # Reduce modulo the irreducible polynomial
    while len(result) > len(mod_poly) - 1:
        if result[0] == 1:  # If leading coefficient is 1
            # XOR with shifted modular polynomial
            shift = len(result) - len(mod_poly)
            for i in range(len(mod_poly)):
                result[i + shift] ^= mod_poly[i]
        result = result[1:]  # Remove leading coefficient

    # Pad result to match field element size
    while len(result) < len(mod_poly) - 1:
        result.append(0)

    return result

# Example: GF(2³) with irreducible polynomial x³ + x + 1
mod_poly = [1,0,1,1]  # x³ + x + 1

# Elements of GF(2³)
elements = [
    [0,0,0],  # 0
    [0,0,1],  # 1
    [0,1,0],  # x
    [0,1,1],  # x + 1
    [1,0,0],  # x²
    [1,0,1],  # x² + 1
    [1,1,0],  # x² + x
    [1,1,1]   # x² + x + 1
]

# Example operations
a = [0,1,0]  # x
b = [1,0,0]  # x²

# Addition: x + x² = x² + x
sum_result = poly_add(a, b)  # [1,1,0]
assert sum_result == [1,1,0]

# Multiplication: x × x² = x³ = x + 1 (using reduction)
mul_result = poly_mul(a, b, mod_poly)  # [0,1,1]
assert mul_result == [0,1,1]
```

Note: When we multiply elements, we reduce using the irreducible polynomial $x^3 + x + 1$. For
example:

- $x \times x^2 = x^3 = x + 1$ (because $x^3 + x + 1 = 0$ in the field)
- $(x + 1) \times x = x^2 + x$

#### Verifying irreducibility

To verify that $x^3 + x + 1$ is irreducible over $GF(2)$, we can:

1. Check that it has no roots in $GF(2)$
2. Check that it's not divisible by any polynomial of degree 1

```python
def evaluate_poly(poly: list[int], x: int, p: int) -> int:
    """Evaluate polynomial at x in GF(p)"""
    result = 0
    for coef in reversed(poly):  # Start from constant term
        result = (result * x + coef) % p
    return result

def is_irreducible_degree3(poly: list[int]) -> bool:
    """Check if polynomial of degree 3 is irreducible over GF(2)
    poly is represented as [a₃,a₂,a₁,a₀] for a₃x³ + a₂x² + a₁x + a₀"""

    # 1. Check for roots in GF(2)
    # If f(0) = 0 or f(1) = 0, polynomial has a root
    if evaluate_poly(poly, 0, 2) == 0 or evaluate_poly(poly, 1, 2) == 0:
        return False

    return True  # No roots found, must be irreducible

# Verify x³ + x + 1 is irreducible
mod_poly = [1,0,1,1]  # x³ + x + 1
assert is_irreducible_degree3(mod_poly)

# Example of reducible polynomial
reducible = [1,0,1,0]  # x³ + x
assert not is_irreducible_degree3(reducible)  # Because x is a factor

# Let's see why x³ + x + 1 has no roots:
print(f"f(0) = {evaluate_poly(mod_poly, 0, 2)}")  # = 1
print(f"f(1) = {evaluate_poly(mod_poly, 1, 2)}")  # = 1
# Since neither 0 nor 1 are roots, and these are all elements of GF(2),
# x³ + x + 1 has no linear factors over GF(2)
```

Note: For a cubic polynomial over $GF(2)$, being irreducible is equivalent to having no roots in
$GF(2)$. This is because:

1. If it were reducible, it would have at least one linear factor $(x + \alpha)$
2. That linear factor would give us a root $\alpha \in GF(2)$
3. Therefore, no roots implies irreducible

For higher degrees or larger fields, we would need more sophisticated irreducibility tests.

#### Applications in cryptography

1. AES uses $GF(2^8)$ for its S-box operations
2. Error-correcting codes often use extension fields
3. Some elliptic curves are defined over extension fields
