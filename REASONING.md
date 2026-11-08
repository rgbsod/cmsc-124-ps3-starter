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

The case starts with special operator if. The condition (null '()) becomes true, which leads to the true branch evaluated as 'empty. Empty has a symbol kind and none for its length.

## P09

The and in this case is a special operator. The evaluation short-circuits then returns nil. It has a null kind and a length of 0.

## P10

The progn in this case is a special operator. The variable defvar declares _ps3-rate_ as a special variable and makes dynamic let binding 10 visible to ps3-scale, so it evaluates 3 \* 10 to 30. The result is an integer and has a scalar length of 1.

## P11

The case starts with defun which is a macro. Defining a named function returns ps3-twice which is a symbol. It has no length.

## P12

The labels in this case is a special operator. It has local recursive bindings, so it creates a list (3,2,1) as down decrements. The list has cons as its kind and has a length of 3 due to its top-level elements.

## P13

The case starts with the function mapcar. It applies length to each sublist, which ends in (2,0,1). The result is a cons list and has a length of 3 due to its top-level elements.

## P14

The case starts with the function mapcar. It maps the anonymous squaring lambda across (1,2,3), resulting in (1,4,9). This is a cons list with length 3.

## P15

The case starts with the macro lambda. The lambda is uncalled so it returns a function object #. It has a function kind and has no length.

## P16

The case starts with special operator let. f in this case is a lambda closure and captures lexical binding factor = 2 when defined. Calling (funcall f 3) evaluates 3 \* 2 to 6 regardless of binding so result becomes an integer and has no length.
