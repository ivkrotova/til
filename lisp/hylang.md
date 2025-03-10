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
;; Define a macro `train-evaluate` that trains a model and evaluates it
(defmacro train-evaluate [model X_train y_train X_test y_test]
  `(do  ;; `do` allows multiple expressions to be evaluated sequentially
     (.fit ~model ~X_train ~y_train)  ;; Train the model with training data
     (.score ~model ~X_test ~y_test)))  ;; Evaluate the model with test data

;; Create an instance of LogisticRegression from sklearn
(def model (sklearn.linear_model.LogisticRegression))

;; Use the macro to train and evaluate the model
(train-evaluate model X_train y_train X_test y_test)
```

## Symbolic Computation

```hy
;; Define a simple grammar representation as a dictionary
(def grammar
  {"NP" ["Noun" "Adj Noun"]  ;; A noun phrase (NP) can be a noun or an adjective followed by a noun
   "VP" ["Verb" "Verb NP"]  ;; A verb phrase (VP) can be a verb or a verb followed by an NP
   "S"  ["NP VP"]})  ;; A sentence (S) consists of an NP followed by a VP

;; Print the grammar dictionary
(print grammar)
```

## Functional Programming

```hy
;; Import pandas for data manipulation
(import [pandas :as pd])

;; Define a function to normalize a column in a dataframe
(defn normalize [col]
  (/ (- col (.min col)) (- (.max col) (.min col))))  ;; Normalization formula: (x - min) / (max - min)

;; Define a function to clean a dataset
(defn clean-data [df]
  (-> df
      (.dropna)  ;; Remove missing values
      (.apply normalize)))  ;; Apply normalization to all columns

;; Read a CSV file into a dataframe
(setv df (pd.read_csv "data.csv"))

;; Apply the cleaning function to the dataframe
(setv df (clean-data df))
```

## DSL Creation

```hy
;; Define a neural network configuration as a dictionary
(setv config
  {"layers" [{"type" "Dense" "units" 128 "activation" "relu"}  ;; First hidden layer
              {"type" "Dense" "units" 64 "activation" "relu"}   ;; Second hidden layer
              {"type" "Dense" "units" 10 "activation" "softmax"}]  ;; Output layer with 10 classes
   "optimizer" "adam"  ;; Use Adam optimizer
   "loss" "categorical_crossentropy"})  ;; Loss function for multi-class classification
```

## Probabilistic Programming

```hy
;; Import pymc3 for Bayesian modeling
(import [pymc3 :as pm])

;; Create a probabilistic model
(setv model
  (pm.Model))  ;; Instantiate a PyMC3 model

;; Define random variables within the model context
(with model
  (setv mu (pm.Normal "mu" mu 0 sigma 10))  ;; Define a normal prior for mu
  (setv sigma (pm.HalfNormal "sigma" sigma 1))  ;; Define a half-normal prior for sigma
  (setv likelihood (pm.Normal "obs" mu mu sigma sigma observed data)))  ;; Define likelihood function with observed data
```

## Meta-Programming

```hy
;; Define a macro that chooses a reinforcement learning policy
(defmacro choose-policy [policy-name]
  `(case ~policy-name  ;; Match the policy name to corresponding functions
     "epsilon-greedy" (lambda [q-values] ...)  ;; Epsilon-greedy policy
     "softmax" (lambda [q-values] ...)  ;; Softmax policy
     "random" (lambda [q-values] ...)))  ;; Random action selection policy
```

## Links
- [Official Hy Website](https://hylang.org/)
- [Learn Hy in Y Minutes](https://learnxinyminutes.com/hy/)
- [Hy Tutorial Documentation](https://hylang.org/hy/doc/v1.0.0/tutorial)

