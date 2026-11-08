# Reasoning for the Predictions Table
## P01

The head for this case is function +. Evaluation starts with (\* 2 3) which leads to 6 and then it adds 1 so it becomes 7. The results is an integer that is an atom and the length is none.

## P02

The case is read as (quote(+ 1 2)) so it has a special operator. Quote returns the argument without evaluation so it leads to (+,1,2). It is a cons with length of 3 based on the results.

## P03

The case ('nil) has an atomic form with no operator head so it evaluates directly as nil, making its course kind automatically as null and its length as none.

## P04

The case ('t) is an atomic symbol with no operator head. Evaluating it returns t as a symbol, and automatically has no length.

## P05

The case (symbolp nil) starts with a function symbolp. Evaluating this returns nil with an assigned symbol and no length.

## P06

The case (car '()) starts with a function car. It extracts the first element of the empty list which leads to nil. Results takes null for its kind and has no length.

## P07

The case (cons 1 '(2 3)) starts with function cons. It prepends 1 to 2 and 3 to form a list (1,2,3). The kind becomes cons because it is a cell list with 3 top-level elements.

## P08
`if`, as the head, is a special operator. It tests `(null '())`, which is true for empty lists, leading `if` to the first branch, where `quote` will return `empty`. This is a symbol other than `nil`, so the kind is `symbol`, and it is not a sequence, so the length is `none`.

## P09
`and` is the head, which is a special operator. It evaluates `1`, which is true, then `nil`, which is false, so it stops there and never evaluates 3. It returns `nil`. As in P03, nil is read as `null`, with length `0`.

## P10
`progn` is the head, a `special operator` which evaluates its arguments in order and returns last value. As the first argument, `defvar` declares `*ps3-rate*` special, so the `let` rebinds `*ps3-rate*` to `10`, and `ps3-scale` looks the variable up once it runs, rather than when it was written. It will then see 10 and returns `30`, an integer, which is not a sequence, so the length is `none`.

## P11
`defun` is the head, which is a `macro` making it expand to other code before anything is evaluated. It defines the global function `ps3-twice`, and `defun` form returns the function's name, a `symbol` which is its kind. This means the length is `none`.

## P12
`labels` is the head, which is a special operator; it creates local function `down` that can call itself, then evaluates the `down 3`. Each call returns `'()` when `n` is 0, and otherwise puts `n` on the front of the list that `(down (- n 1))` returns. This chain builds `(3,2,1)`, a list, so kind is `cons` with length `3`.

## P13
`mapcar` is the head, which is a function. `#'length` evaluates to the function obj for `length`, and the quoted list will be  `((1 2) () (3))`. `mapcar` applies the `length` to each element and collects them into a new list. The result `(2,0,1)` is a list, so the kind is `cons`, with length `3`.

## P14
`mapcar` is the head, a function. The `lambda` expression evaluates to a function that squares its argument, which `(1 2 3)` is (`quote` gives the list as is) . `mapcar` applies the function to each element and collects them into list `(1,4,9)`. The kind is `cons`, with length `3`.

## P15
`lambda` is the head, which is a macro, so it rewrites into another form that expands into `(function (lambda (n) (* n 2)))`. Evaluating that returns a function object without calling it, since nothing provides an argument. The value is a function, so the kind is `function`. length is `none`, since it is not a sequence.

## P16
`let` is the head, a special operator. The `lambda` in `f`  remembers the `factor` that was captured as `2` (Unlike P10, this variable is not special, so even when it is rebound it would change nothing), so the later `factor` of `10` doesn't affect it, and the result is `6`. The returned value is an integer, so the kind is `integer` and the length is `none`.
