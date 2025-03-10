# Hy

Hy (or Hylang for long) is a dialect of Lisp that is embedded in Python. It allows developers to write Lisp-like code that compiles into Python's Abstract Syntax Tree (AST), making it possible to use all of Python's libraries while benefiting from Lisp's powerful macro system.

## Hy vs. Lisps vs. Python

Compared to Python, Hy offers a variety of new features, generalizations, and syntactic simplifications, as would be expected of a Lisp. The familiar parentheses-based syntax brings the elegance and expressiveness that Lisp is known for.

Compared to other Lisps, Hy provides seamless direct access to Python's rich ecosystem of built-ins and third-party libraries. This unique position allows developers to freely mix imperative, functional, and object-oriented programming styles while maintaining the power of Lisp macros.

## Useful for

Hy excels in several key areas:

- **Metaprogramming** – Harness the full power of Lisp-style macros for elegant code transformation
- **Functional Programming** – Write clean, composable code using Lisp's functional programming paradigms
- **Learning Lisp** – Explore the beauty of Lisp concepts while staying within Python's familiar ecosystem
- **Scientific Computing** – Leverage Python's scientific stack (NumPy, Pandas, etc.) with Lisp's expressiveness
- **Domain-Specific Languages** – Create custom languages that compile directly to Python's AST


## Macros Example

```python
def train_model(model, X_train, y_train):
    model.fit(X_train, y_train)
    return model

def evaluate_model(model, X_test, y_test):
    return model.score(X_test, y_test)
```

```hy
(defmacro train-evaluate [model X_train y_train X_test y_test]
  `(do
     (.fit ~model ~X_train ~y_train)
     (.score ~model ~X_test ~y_test)))

(def model (sklearn.linear_model.LogisticRegression))
(train-evaluate model X_train y_train X_test y_test)
```

## Symbolic Computation

```hy
(def grammar
  {"NP" ["Noun" "Adj Noun"]
   "VP" ["Verb" "Verb NP"]
   "S"  ["NP VP"]})

(print grammar)
```

## Functional Programming

```hy
(import [pandas :as pd])

(defn normalize [col]
  (/ (- col (.min col)) (- (.max col) (.min col))))

(defn clean-data [df]
  (-> df
      (.dropna)
      (.apply normalize)))

(setv df (pd.read_csv "data.csv"))
(setv df (clean-data df))
```

## DSL Creation

```hy
(setv config
  {"layers" [{"type" "Dense" "units" 128 "activation" "relu"}
             {"type" "Dense" "units" 64 "activation" "relu"}
             {"type" "Dense" "units" 10 "activation" "softmax"}]
   "optimizer" "adam"
   "loss" "categorical_crossentropy"})
```

## Probabilistic Programming

```hy
(import [pymc3 :as pm])

(setv model
  (pm.Model))

(with model
  (setv mu (pm.Normal "mu" mu 0 sigma 10))
  (setv sigma (pm.HalfNormal "sigma" sigma 1))
  (setv likelihood (pm.Normal "obs" mu mu sigma sigma observed data)))
```

## Meta-Programming

```hy
(defmacro choose-policy [policy-name]
  `(case ~policy-name
     "epsilon-greedy" (lambda [q-values] ...)
     "softmax" (lambda [q-values] ...)
     "random" (lambda [q-values] ...)))
```

## Links
- [Official Hy Website](https://hylang.org/)
- [Learn Hy in Y Minutes](https://learnxinyminutes.com/hy/)
- [Hy Tutorial Documentation](https://hylang.org/hy/doc/v1.0.0/tutorial)

