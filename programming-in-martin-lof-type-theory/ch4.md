# Chapter 4: The Semantics of the Judgment Forms

canonical expressions (expressions on canonical form)
- represents values
- for each set (of expressions), there are conditions for how to form a canonical expression of the set
- closed and saturated
- form: `c(e_1 , e_2 , ... , e_n)` for `n ≥ 0`
  - `c` is a canonical constant
  - `e_i` are expressions

primitive constants
- form: `α_1 ⊗ ... ⊗ α_n →→ 0, n ≥ 0`
- canonical constant
  - begins a canonical expression
- non-canonical constant
  - associated a computation rule

| type theory     | denotational semantics |
|                 | of lambda calculus     |
|-----------------|------------------------|
| value           | value                  |
| evaluated       | weak head normal form  |
| fully evaluated | normal form            |

## 4.1 Categorical (assumption free) judgments

### 4.1.1 What does it mean to be a set?

`A set`
- judgment: A is a set
- definition
  1. how to form/construct the canonical elements in the set
    - syntax
  2. under what conditions two canonical elements are equal
    - equality relation introduced between the canonical elements 
      - extensionality: must be an *equivalence relation*
      - intensionality: two canonical elements are equal if they have the same form and their parts are equal

### 4.1.2 What does it mean for two sets to be equal?

`A = B`
- `A set`
- `B set`
- equality relation on sets preserves (bidirectionally)
  1. canonical elements
  2. equality relation between canonical elements
- is an equivalence relation

### 4.1.3 What does it mean to be an element in a set?

`a ∈ A`
- `A set`
- `a expression` (?)
- `a`, when evaluated, yields a canonical element of `A` as value

### 4.1.4 What does it mean for two elements to be equal in a set?

`a = b ∈ A`
- `a ∈ A`
- `b ∈ A`
- `a` and `b` yields equal canonical elements in the set `A` as values

### 4.1.5 What does it mean to be a proposition?

`A proposition`
- `A set`

### 4.1.6 What does it mean for a proposition to be true?

`A true`
- there exists an element `a` in `A` (proof: `a ∈ A`)

## 4.2 Hypothetical judgments with one assumption

`x ∈ A`
- `A set`
- `x` is a variable of arity 0
- means an assumption `A true` with `x` being a construction/proof

context
- an assumption list
- form: `x_1 ∈ A_1 , x_2 ∈ A_2(x_1), ... , x_n ∈ A_n(x_1, x_2, ... , x_(n−1))`
  - where each `A_i(x_1, ... , x_(i−1))` is a set under the preceding assumptions

### 4.2.1 What does it mean to be a set under an assumption?

`A(x) set [x ∈ C]`
- `C set`
- `A(x)` is extensional
  - if `b = c ∈ C` then `A(b) = A(c) ∈ C`

### 4.2.2 What does it mean for two sets to be equal under an assumption?

`A(x) = B(x) [x ∈ C]`
- `A(x) set [x ∈ C]`
- `B(x) set [x ∈ C]`

### 4.2.3 What does it mean to be an element in a set under an assumption?

`a(x) ∈ A(x) [x ∈ C]`
- `A(x) set [x ∈ C]`
- `a(x)` is extensional
  - if `b = c ∈ C` then `a(b) = a(c) ∈ C`

### 4.2.4 What does it mean for two elements to be equal in a set under assumption?

`a(x) = b(x) ∈ A(x) [x ∈ C]`
- `A(x) set [x ∈ C]`
- `a(x) ∈ A(x) [x ∈ C]`
- `b(x) ∈ A(x) [x ∈ C]`

### 4.2.5 What does it mean to be a proposition under an assumption?

`A(x) proposition [x ∈ C]`
- `A(x) set [x ∈ C]`

### 4.2.6 What does it mean for a proposition to be true under an assumption?

`A(x) true [x ∈ C]`
- `a(x) ∈ A(x) [x ∈ C]`
