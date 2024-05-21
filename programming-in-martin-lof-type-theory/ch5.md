# Chapter 5: General rules

1. formation rules
  - under which conditions we may infer `A` is a set and when two sets `A` and `B` are equal
2. introduction rules
  - how the canonical elements are formed
  - when two canonical elements are equal
3. elimination rules
  - how to prove a proposition about an arbitrary element in the set
  - a kind of structural induction rules
    - to prove an arbitrary element `p` in the set `A` has property `C(p)`, it is enough to prove an arbitrary *canonical* element in the set has that property
  - *selector* is introduced in this kind of rules
    - a primitive non-canonical constant associated with the set
    - enables pattern-matching and primitive recursion over the elements in the set
4. equality rules
  - describes the equalities which are introduced by the computation rules for the *selector* associated with the set

## 5.1 Assumptions

```
A set
---
x ∈ A [x ∈ A]
```
- if `A` is a set, then we can introduce a variable `x` of that set

## 5.2 Propositions as sets

```
a ∈ A
---
A true
```
- if we have an element in a set, then we will interpret that set as a true proposition

## 5.3 Equality rules

Reflexivity
```
a ∈ A
---
a = a ∈ A

A set
---
A = A
```

Symmetry
```
a = b ∈ A
---
b = a ∈ A

A = B
---
B = A
```
- equality between canonical elements is symmetric
- preservation of canonical elements and equality of canonical elements is symmetric

Transitivity
```
a = b ∈ A
b = c ∈ A
---
a = c ∈ A

A = B
B = C
---
A = C
```

## 5.4 Set rules

```
a ∈ A
A = B
---
a ∈ B
```
- equality between sets preserves canonical elements

```
a = b ∈ A
A = B
---
a = b ∈ B
```
- equality between sets preserves equality of canonical elements

## 5.5 Substitution rules

### 5.5.1 Substitution in sets

hypothetical judgment `C(x) set [x ∈ A]` means
- `C(a)` is a set provided `a ∈ A`
- `C(a) = C(b)` whenever `a = b ∈ A`

```
C(x) set [x ∈ A]
a ∈ A
---
C(a) set

C(x) set [x ∈ A]
a = b ∈ A
---
C(a) = C(b)
```

### 5.5.2 Substitution in elements

hypothetical judgment `c(x) ∈ C(x) [x ∈ A]` means
- `c(a) ∈ C(a)` if `a ∈ A`
- `c(a) = c(b) ∈ C(a)` if `a = b ∈ A`

```
c(x) ∈ C(x) [x ∈ A]
a ∈ A
---
c(a) ∈ C(a)

c(x) ∈ C(x) [x ∈ A]
a = b ∈ A
---
c(a) = c(b) ∈ C(a)
```

### 5.5.3 Substitution in equal sets

hypothetical judgment `B(x) = C(x) [x ∈ A]` means
- `B(a)` and `C(a)` are equal sets for any element `a` in `A`

```
B(x) = C(x) [x ∈ A]
a ∈ A
---
B(a) = C(a)
```

### 5.5.4 Substitution in equal elements

hypothetical judgment `b(x) = c(x) ∈ B(x) [x ∈ A]` means
- `b(a)` and `c(a)` are equal elements in `B(a)` provided that `a ∈ A`

```
b(x) = c(x) ∈ B(x) [x ∈ A]
a ∈ A
---
b(a) = c(a) ∈ B(a)
```

### 5.5.5 `n` simultaneous substitutions 

extension of 5.5 with `n` simultaneous substitutions

for example, 5.5.3 Substitution in equal sets becomes

Substitution in equal sets of n variables
```
B(x_1, ... , x_n) = C(x_1, ... , x_n) [x_1 ∈ A_1, ... , x_n ∈ A_n]
a_1 ∈ A_1
a_2 ∈ A_2(a_1)
...
a_n ∈ A_n(a_1, ... , a_(n-1))
---
B(a_1, ... , a_n) = C(a_1, ... , a_n)
```

### 5.5.6 substitution in the middle of a context

for example
```
C(x, y) set [x ∈ A, y ∈ B(x)]
a ∈ A
---
C(a, y) set [y ∈ B(a)]
```
