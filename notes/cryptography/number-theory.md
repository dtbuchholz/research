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

- **Commutative**: order in which two numbers are added or multiplied does not affect the result,
  $a + b = b + a$
- **Associative**: when three or more numbers are added or multiplied, the grouping of the numbers
  (i.e., how the numbers are associated) does not change the sum or product,
  $(a + b) + c = a + (b + c)$
- **Distributive**: involves two operations, multiplication _and_ addition or subtraction, such that
  a number multiplied by the sum of two others can be broken down into individual multiplications
  added together, $a \times (b + c) = a \times b + a \times c$

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

A relation denotes some kind of relationship between two objects in a set. A relation $R$ from
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

A group is a set $G$ with an arbitrary binary operation $\cdot$ (typically $+$ or $\times$) that
satisfies—i.e., $(G, \cdot)$ is a group. The axioms are:

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
