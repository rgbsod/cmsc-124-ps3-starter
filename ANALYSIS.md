# Environments and the Toy Evaluator

In eval-expr, evaluating ((lambda (x) (+ x 1)) 5) reaches the default application branch. It evaluates the operator (lambda (x)(+ x 1)) into a closure using the lambda branch where (make-closure params body env) captures the environment in which the lambda was defined. This then evaluates the argument 5 and passes the closure to apply-closure, which (extend-env params args env) then binds x to 5 in the closure's captured environment, implementing lexical scoping.

If application joined the arguments, to the caller's environment, the language would use dynamic scoping instead.

CLISP needs funcall since it is a Lisp-2, which keeps variables and functions in separate namespaces. For the toy language, it is a Lisp-1 which means that variables and functions only share one namespace. In Lisp-2, a function stored in a variable cannot be called directly as an operator using that variable's name, while Lisp-1 variables can be called directly without funcall.