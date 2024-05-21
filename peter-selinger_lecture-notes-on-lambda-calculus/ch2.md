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
  - `x` in `λx` is binding
- scope `N`
  - occurrences of variable `x` in subterm `N` are bound
  - variables without binder are free

The set `FV(M)` of free variables of a term `M`
- `FV(x)` = `{x}`,
- `FV(M N)` = `FV(M)` ∪ `FV(N)`,
- `FV(λx.M)` = `FV(M)` \ `{x}`.

rename a variable `x` as `y` in a term `M` whether free, bound, or binding
- `x{y/x}` ≡ `y`,
- `z{y/x}` ≡ `z`, if `x ≠ z`,
- `(M N){y/x}` ≡ `(M{y/x})(N{y/x})`,
- `(λx.M){y/x}` ≡ `λy.(M{y/x})`,
- `(λz.M){y/x}` ≡ `λz.(M{y/x})`, if `x ≠ z`.

α-equivalence
- smallest congruence relation `= α` on lambda term
  - congruence requires rule (cong) and rule (ξ)
- `λx.M` = α `λy.(M {y/x})`
  - for all terms `M`, and for all variables `y` that do not occur in `M`
  - `∀M, ∀y, y ∉ M`
- rules on `= α`
  - (refl) reflexivity
    - ---
    - `M = M`
  - (trans) transitivity
    - `M = N`
    - `N = P`
    - ---
    - `M = P`
  - (symm) symmetry
    - `M = N`
    - ---
    - `N = M`
  - (cong)
    - `M = M'`
    - `N = N'`
    - ---
    - `M N = M' N'`
  - (ξ)
    - `M = M'`
    - ---
    - `λx.M = λx.M'`
  - (α)
    - `y ∉ M`
    - ---
    - `λx.M = λy.(M{y/x})`

Barendregt's variable convention
- without loss of generality
- always assume all bound variables have been renamed to be distinct

## 2.3 Substitution

naively replacing variables by a lambda term might
1. (bound -> free) break existing bindings to bound variables
  - `x(λxy.x)[N/x]`
    - wrong: `N(λxy.N)`
    - correct: `N(λxy.x)`
2. (free -> bound) introduce unintended bindings to free variables
  - `M[N/y]` where `M ≡ λx.yx`, `N ≡ λz.xz`
    - wrong: `M[N/y] = (λx.yx)[N/y] = λx.Nx = λx.(λz.xz)x`
    - correct: `M[N/y] = (λx'.yx')[N/y] = λx'.(λz.xz)x'`

fresh variable
- a variable that is currently unused
- an infinite set `V` of variables means a fresh variable is always available

capture-avoiding substitution
- `x[N/x]` ≡ `N`
- `y[N/x]` ≡ `y`
- `(MP)[N/x]` ≡ `(M[N/x])(P[N/x])`
- `(λx.M)[N/x]` ≡ `λx.M` (`x`s in scope `M` are bound already)
- `(λy.M)[N/x]` ≡ `λy.M[N/x]` if `x ≠ y` and `y ∉ FV(N)`
- `(λy.M)[N/x]` ≡ `λy'.(M{y'/y}[N/x])` if `x ≠ y`, `y ∈ FV(N)`, `y'` is fresh
  - how to deterministically decide which `y'` to use?
    1. (computational) define ordering and join on variable set `V` and choose least `y'` that doesn't occur in `M` or `N`
    2. (theoretical) weaken `≡` to `= α` so lambda terms are identified up to α-equivalence, and prove that substitution is well-defined modulo α-equivalence

## 2.4 Introduction to β-reduction

convention
- from now on, we regard lambda terms as equivalence class modulo α-equivalence meaning we identify lambda terms up to α-equivalence

- β-reduction
  - evaluating lambda terms by "plugging arguments into functions"
    1. find a subterm that is a redex
    2. replace the redex by its reduct
      - reducing a redex (`λz.zz`) can create new redexes (multiple `λw.w`)
        - `(λz.zz)(λw.w)` ->β `(λw.w)(λw.w)`
      - reducing a redex (`λx.y`) can delete some other redexes (`λw.w`)
        - `(λx.y)(λw.w)` ->β `y`
    3. repeat step 1,2
      - the number of steps that it takes to reach β-normal form can vary
      - depending on the order in which the redexes are reduced
        - `(λx.y)((λw.ww)(λw.ww))`
          - if reduce function `λx.y` first then reach normal form `y` immediately
          - if reduce argument `(λw.ww)(λw.ww)` first then it's non-terminal
- β-redex (reducible expression)
  - `(λx.M)N`
- β-reduct (reduced) 
  - `M[N/x]`
- β-normal form
  - a lambda term without any β-redexes
- M `->> β` M' (M evaluates to M')
  - where M' is β-normal form

## 2.5 Formal definitions of β-reduction and β-equivalence

single-step β-reduction `-> β`, the smallest relation on terms (`Λ`) satisfying
- (β)
  - ---
  - `(λx.M)N` -> β `M[N/x]`
- (cong_1)
  - `M` -> β `M'`
  - ---
  - `MN` -> β `M'N`
- (cong_2)
  - `N` -> β `N'`
  - ---
  - `MN` -> β `MN'`
- (ξ)
  - `M` -> β `M'`
  - ---
  - `λx.M` -> β `λx.M'`

multi-step β-reduction `->> β`
- the reflexive-transitive closure of `-> β`
- i.e. the smallest reflexive-transitive relation containing `-> β`

β-equivalence `= β`
- the reflexive-transitive-symmetric closure of `-> β`
- i.e. the smallest equivalence relation containing `-> β`
