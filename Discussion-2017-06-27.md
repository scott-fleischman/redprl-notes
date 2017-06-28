# RedPRL Notes from OPLSS 2017

### All types are primitive.
There are no `data` declarations for user-defined types.

In the future, they hope to add W types, which would allow for any inductive type.

### Weak vs strict bool
There are two kinds of bool:
* weak
* strict

They have different behavior at higher dimensions.

### Some syntax
```
Thm [

]
by [

]
```

#### Thm
`Thm` indicates the _judgement_ to be proved. Note this is a judgement that is proved; we are not proving that a type is inhabited.

#### by
`by` is a tactic script.

In the tactic script you can enter probes which tell you what are the goals.

Probes start with a `?` like `?hello`. 

You can even keep them in your script and they act like logging statements. For example, `?hello; <some tactic>` will print out the goals at `?hello` then run the following tactic.

#### lam tactic
`lam x.` intro rule for functions.

This is a tactic which helps push out trivial and annoying goals outside of the body of the lambda. It helps the body focus on the important parts of the proof.

You can see those trivial goals by adding a probe outside the scope of the `lam`.

#### >>
`>>` is the ASCII turnstile.

#### hyp
`hyp` uses the hypothesis in place.

#### backtick
With a backtick you can enter a literal term without a tactic. Example: `` `tt `` . You can also parenthesize a larger term: `` `(some big term)``.

### Tactics vs terms
There are terms for `if` statements as well as an `if` tactic.

Motive: with a tactic, certain trivial aspects of the proof term (trivial proof obligations, for example) can be brought outside of the body of the tactic, making the tactic code more readable as a proof. Ideally the proof obligations are trivial for RedPRL to fulfill.

### Example PathTest2
Uses higher-dimensional homotopy.

https://github.com/RedPRL/sml-redprl/blob/e136fe3e11d6cb46166c49999d57f6f50bac9d3d/test/examples.prl#L77-L89

Introduces a lemma [`h`](https://github.com/RedPRL/sml-redprl/blob/e136fe3e11d6cb46166c49999d57f6f50bac9d3d/test/examples.prl#L83-L84) which is used [here](https://github.com/RedPRL/sml-redprl/blob/e136fe3e11d6cb46166c49999d57f6f50bac9d3d/test/examples.prl#L85)

## RedPRL In 3 Parts

### Part 1: Semantic Behavior
Relations on terms of the language. In a semantic setting, define relations which delineate the behavior of types like bools and products. See [Computational Higher Type Theory II: Dependent Cubical Realizability by Angiuli, Harper](https://arxiv.org/abs/1606.09638) for gnarly details.

For example, section 4.1 on booleans, you have to pick out which things are boolean, and specify when they're equal.

### Part 2: Rules
Codify rules such as introduction and elimation for the types.

These are proof theoretic rules of inference. They don't define a type theory in the usual sense. Rather they are theorems and lemmas of the form "If premise, then conclusion".

To formulate these rules, you need some amount of constructive math as well as a bit of impredicativity.

For example implementations, see [refiner_types.fun](https://github.com/RedPRL/sml-redprl/blob/e136fe3e11d6cb46166c49999d57f6f50bac9d3d/src/redprl/refiner_types.fun#L18).

These are partial functions on the premises, which can throw an exception or similar.

### Part 3: Tactics
Tactics give you clever ways of composing proofs, making the proofs nice to write and read. They allow you to partially write the proofs and put holes to fill in incrementally.

## Advantages of RedPRL
* Reasoning extensionally with exact equality. This makes certain definitions much easier (or even possible) than in an intensional setting, such as semi-simplicial sets.

* The computational interpretation differs from the Swedish interpretation. Hopefully the style of composition allows for terms that aren't as large.

## Types
### Existing types
* weak bool
* strict bool
* circle S1
* dependent function (Pi type)
* dependent pair (Sigma type)
* path

### Future types (hopefully)
Once we have a (closed) universe, it will allow for quantifying over types.

* W types -- allows all inductive types
* coinductive types

## Extractions
You can view the extraction of the proof, which is a term in the untyped lambda calculus with additional primitives.

The extraction allows you to see the computational aspect of the proof. Potentially it could also allow implementation of the code in an existing functional language.