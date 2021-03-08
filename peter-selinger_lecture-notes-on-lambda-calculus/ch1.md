# Chapter 1: Introduction

## 1.1 Extensional vs. intensional view of functions

- Extensional
  - "functions as graphs"
  - input-output behavior
  - in most of mathematics
    - "any differentiable function is continuous" meant to be true for all functions, not just those functions for which a rule can be given

- Intensional
  - "functions as rules"
  - intensional questions in computer science
    - how much time does it take?
    - how much memory and disk space is used in the process?
    - how much communication bandwidth is used?

## 1.2 The lambda calculus

### Exercise 1. Evaluate the lambda-expression

(λf.λx.f (f (f (x)))) (λg.λy.g(g(y))) (λz.z + 1) (0).

```
(\f x -> f (f (f x))) (\g y -> g (g y))
= \x -> (\g y -> g (g y)) ((\g y -> g (g y)) ((\g y -> g (g y)) x))
= \x -> (\g y -> g (g y)) ((\g y -> g (g y)) (\y -> x (x y)))
= \x -> (\g y -> g (g y)) ((\g y -> g (g y)) (\z -> x (x z)))
= \x -> (\g y -> g (g y)) (\y -> (\z -> x (x z)) ((\z -> x (x z)) y))
= \x -> (\g y -> g (g y)) (\y -> (\z -> x (x z)) (x (x y)))
= \x -> (\g y -> g (g y)) (\y -> x (x (x (x y))))
= \x -> (\g y -> g (g y)) (\z -> x (x (x (x z))))
= \x -> \y -> (\z -> x (x (x (x z)))) ((\z -> x (x (x (x z)))) y)
= \x -> \y -> (\z -> x (x (x (x z)))) (x (x (x (x y))))
= \x -> \y -> x (x (x (x (x (x (x (x y)))))))
= \x y -> x (x (x (x (x (x (x (x y)))))))
```

apply `x` 2^3 times

```
(\f x -> f (f (f x))) (\g y -> g (g y)) (\z -> z + 1)
= (\x y -> x (x (x (x (x (x (x (x y)))))))) (\z -> z + 1)
= \y -> (\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) ((\z -> z + 1) y)))))))
= \y -> (((((((y + 1) + 1) + 1) + 1) + 1) + 1) + 1) + 1

(\f x -> f (f (f x))) (\g y -> g (g y)) (\z -> z + 1) 0
= (\y -> (((((((y + 1) + 1) + 1) + 1) + 1) + 1) + 1) + 1) 0
= (((((((0 + 1) + 1) + 1) + 1) + 1) + 1) + 1) + 1
```

## 1.3 Untyped vs. typed lambda-calculi

- Untyped lambda calculus
- Simply-typed lambda calculus
  - completely specify the type of every expression
  - like in set theory
- Polymorphically typed lambda calculus
  - allow universal quantification like `forall X. X -> X`

### Exercise 2. Let ω = λx.x(x). What is ω(ω)?

```
w w
= (\x -> x x) (\x -> x x)
= (\x -> x x) (\x -> x x)
= ...
```

cannot be reduced to simpler form by beta-reduction

## 1.4 Lambda calculus and computability

1. Turing: Turing machine
2. Godel: general recursive functions
3. Church: lambda calculus

All above define the same class of computable functions
- proven by Church, Kleene, Rosser, Turing

Church-Turing thesis
- "intuitive computability" is equivalent to these models of computation

## 1.5 Connections to computer science

Lambda calculus
- the simplest possible programming language
- Turing complete
- useful for defining and proving properties of programs

Functional programming languages
- extensions to lambda calculus
  - data types
  - input/output
  - side effects
  - updatable memory
  - object oriented features

## 1.6 Connections to logic

"what a proof is"

Classical logicians
- Hilbert
- existence of mathematical objects 
  - proof by contradiction from the assumption that it doesn't exist

Constructivists
- Brouwer, Heyting
- existence of mathematical objects 
  - proof by explicit constructions

"proofs-as-program" paradigm

Constructive proof vs. Classical proof
- give more information
  - allow one to compute solutions to problems
  - as opposed to merely knowing the existence of a solution

## 1.7 Connections to mathematics

mathematical models of lambda calculus
- to provide spaces in which lambda terms can be given meaning
  - algebra
  - poset
  - topology
  - category theory

