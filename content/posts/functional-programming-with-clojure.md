---
title: "Functional Programming with Clojure"
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
(if false "a" "b") ; => will output "b"
(if false "a") ; => will output nil
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


> continue
