# Chapter 2: The untyped lambda calculus

Lambda calculus
- a formal language
  - expressions
    - lambda terms
  - rules for manipulating expressions

## 2.1 Syntax

Definition
- assumption: given an infinite set `V` of variables
  - denoted by `x`, `y`, `z`, etc.
- the set `Λ` of lambda terms 
  - in BNF (Backus-Naur Form)
    - `M, N :: = x | (M N) | (λx.M)`
      - variables `x`
      - applications `(M N)`
      - lambda abstractions `(λx.M)`
  - in traditionally mathematical definition
    - `x ∈ V` => `x ∈ Λ`
    - `M ∈ Λ`, `N ∈ Λ` => `(M N) ∈ Λ`
    - `x ∈ V`, `M ∈ Λ` => `(λx.M) ∈ Λ`

Convention
- omit outmost parenthesis
  - `M N` = `(M N)`
- applications associate to the left
  - `M N P` = `(M N) P`
  - `f x y z` = `((f x) y) z`
- body of a lambda abstraction extends as far to the right as possible
  - `λx.M N` = `λx.(M N)`, not `(λx.M) N`
- multiple lambda abstractions can be contracted
  - `λxyz.M` = `λx.λy.λz.M`

### Exercise 3

(a) Write the following terms with as few parenthesis as possible,
without changing the meaning or structure of the terms:
(i) (λx.(λy.(λz.((xz)(yz))))), `λxyz.xz(yz)`
(ii) (((ab)(cd))((ef )(gh))), `ab(cd)(ef(gh))`
(iii) (λx.((λy.(yx))(λv.v)z)u)(λw.w). `(λx.((λy.yx)(λv.v)z)u)(λw.w)`

(b) Restore all the dropped parentheses in the following terms, without chang-
ing the meaning or structure of the terms:
(i) xxxx, `(((x x) x) x)`
(ii) λx.xλy.y, `(λx.(x(λy.y)))`
(iii) λx.(xλy.yxx)x. `(λx.((x(λy.((yx)x)))x))`

## 2.2 Free and bound variables, α-equivalence

α-equivalent
- `M = α N`
- two terms differ only in the name of bound variable
  - `λx.x` = α `λy.y`

identical
- `M ≡ N`
- two terms are precisely equal, symbol for symbol

`λx. N`
- binder `λx`
  - occurrence of variable `x` in subterm `N` is bound
- scope `N`



