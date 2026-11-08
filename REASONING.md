# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
It heads with the function `+`, so every argument is evaluated in order before it runs. The inner `(* 2 3)` gives 6, and `+` receives 1 and 6 and returns 7. Thus, the result is an integer, not a sequence, so the length is `none` and the head is a function.

## P02
`'(+ 1 2)` is read as `(quote (+ 1 2))`, so it heads with `quote`. `quote` is a special operator that evaluates nothing and returns its argument untouched, which is why it is not a function. The result is the list `(quote, (+,1,2))`, which has at least one element, so the kind is `cons` and the length is `2`.

Correction: Described the form instead of its result, but `quote` strips its own layer and returns the list untouched, so it should return as `(+,1,2)` instead of including `quote`. This also changes the length to be `3`.

## P03
`nil` is an atom, so it has no head to classify. It is evaluated as itself, and is read as `null`. It has `0` length as it is a sequence, albeit an empty one.

## P04
`t` is an atom, so there is no head to be classified. It is evaluated as `t`, the language's true value, but is read as `symbol`. It read as a symbol and has length of `0`.

Correction: As `t` is read as a symbol, it should have a length of `none` rather than `0`.

## P05
`symbolp` is the head, so its argument is evaluated first: `nil` evaluates to itself. `nil` is a symbol, so `symbolp` returns `t`.  Like P04, it read as a symbol and has length of `0`.

Correction: Similar to P04, `t` is read as a symbol, it should have a length of `none` rather than `0`.

## P06
`car` is the head, which is a function, so its argument is evaluated first. The argument is the empty list, and `car` of an empty list is `nil`. From P03, it is read as `null`, has `0` length.

## P07
`cons` is the head, which is a function. The quote gives it the list `(2 3)` as it is, and `cons` puts `1` on the front, making `(1,2,3)`. That is a list, so the kind is `cons`, and it has three items, so the length is `3`.

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
