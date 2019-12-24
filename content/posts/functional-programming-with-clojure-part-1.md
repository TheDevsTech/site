---
title: "Functional Programming with Clojure: Part 1"
date: 2019-12-09T14:10:00+06:00
draft: true
authors:
- Mazhar Ahmed
tags:
- functional
- clojure
---

Now-a-days everyone has fantasy with functional programming. Obviously OOP (Object Oriented Programming) is ruling the world
for couple of decades leaving functional programming behind long ago. But now-a-days people are getting insterested in
functional programming. It's fun and also you can find new way of thinking how to solve a problem in programming. Clojure
is an awesome functional programming language. It's said that it is Lisp for JVM as it runs on top of JVM (Java Vertual Machine).
There is another amazing fact of Clojure, you have to write everything in Prefix basis.

```clojure
; that means if you want to write (a + b) - (a + c)
; what you have to write is:
- (+ a b) (+ a c)
```

Clojure is written in "forms", which are just lists of things inside parentheses, separated by whitespace. The clojure reader assumes that the first thing is a function or macro to call, and the rest are arguments.

The first thing you want to do in Clojure is define a namespace. To do that use keyword `ns`. Let's define a namespace named devstech:

```clojure
(ns devstech)
```

The next thing you want to learn is how to print a line. In clojure, we just simply use `str` to output string. `str` will print all of its parameters. Let's print `Hello DevsTech`:

```clojure
(str "Hello" " " "DevsTech")
```

The third thing you want to learn is how to comment. In clojure we use `;` to comment. Yes, you heard it right.

```clojure
; this is a comment
```

We can use mathmatical, logical expressions just like other languages. The only diffrence is we need to write in prefix order.

```clojure
; mathmatical statements
(+ 9 90) ; that means 9 + 90 the result is 99
(- 100 1) ; that means 100 - 1 the result is 99
(* 11 9) ; that means 11 * 9 the result is 99
(/ 99 99) ; that means 99 / 99 the result is 1

; logical statements (we use = not == like other languages)
(= 1 1) ; that means 1 == 1 the result is true
(= 2 1) ; that means 2 == 1 the result is false

; not operator
(not true) ; that means !true the result is false

; Nesting forms works as you expect
(+ 1 (- 3 2)) ; that means 1 + (3 - 2) which is 2
```

Defining variable is easy. We use `def` to define variables and `let` to create temporary bindings. But `let` only works on its own scope where `def` works everywhere like:

```clojure
(def n 10)
(let [a 1 b 2]
    (str a " " b)
)
```

Branching statements are also similar to other languages but in prefix order:

```clojure
; Actually if is just like macro in clojure
(if false "a" "b") ; => will return "b"
(if false "a") ; => will return nil
(if (< 1 2) "true" "false") ; it will output true as 1 < 2 is true

; if you want elseif just make branch of nested if
(if (= a 1)
    "a is 1"
    (if (= a 2)
        "a is 2"
        "a is something else"
    )
)
```

Loop is also a little bit tricky like (keep in mind that `do` does not loop, it only groups statements):

```clojure
(loop [x 10]
  (when (> x 1)
    (println x)
    (recur (- x 2))))
; => 10 8 6 4 2

(for [x [0 1 2 3 4 5]
      :let [y (* x 3)]
      :when (even? y)]
  y)
; => (0 6 12)

(for [x (range 1 6) 
      :let [y (* x x) 
            z (* x x x)]] 
  [x y z])
; => ([1 1 1] [2 4 8] [3 9 27] [4 16 64] [5 25 125])
```

And now the most important part of functional programming. How to define functions. We use `fn`, `def` and `defn` to define functions. Let's define some functions.

```clojure
; Use fn to create new functions. A function always returns
; its last statement.
(fn [] "Devs Tech") ; => fn

; (You need extra parens to call it)
((fn [] "Devs Tech")) ; => "Devs Tech"

; You already know declaring a var using def
(def x 1)
x ; => 1

; Assign a function to a var, you know, just like js
(def devstech (fn [] "Devs Tech"))
(devstech) ; => "Devs Tech"

; You can shorten this process by using defn
(defn devstech [] "Devs Tech")

; The [] is the list of arguments for the function.
(defn devs [name]
  (str "Devs " name))
(hello "Tech") ; => "Devs Tech"

; You can also use this shorthand to create functions:
(def devs2 #(str "Devs " %1))
(devs2 "Tech") ; => "Devs Tech"

; You can have multi-variadic functions, too
(defn devs3
  ([] "Devs Tech")
  ([name] (str "Devs " name)))
(devs3 "Mazhar") ; => "Devs Mazhar"
(devs3) ; => "Devs Tech"

; Functions can pack extra arguments up in a seq for you
(defn count-args [& args]
  (str "You passed " (count args) " args: " args))
(count-args 1 2 3) ; => "You passed 3 args: (1 2 3)"

; You can mix regular and packed arguments
(defn devs-count [name & args]
  (str "Hi " name ", you passed " (count args) " extra args"))
(devs-count "Mazhar" 1 2 3)
; => "Hi Mazhar, you passed 3 extra args"
```

I will not make this part any longer. Let's close this article and continue in Part 2. In Part 2 we will see more clojure way of writing programs.

To be continued.
