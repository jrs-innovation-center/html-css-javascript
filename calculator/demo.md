# Calculator Demo

https://hyperdev.com/#!/project/ginger-thunder

https://ginger-thunder.hyperdev.space/

```
const ADD = '+', MINUS = '-', TIMES = '*', DIVIDE = '/'

const add = (a,b) => b ? a + b : b => a + b
const subtract = (a,b) => b ? a - b : b => a - b

const multiply = (a,b) => b ? a * b : b => a * b
const divide = (a,b) => b ? a / b : b => a / b

const isNumber = v => typeof v === 'number' ? true : false
const isFunction = v => typeof v === 'function' ? true : false

const operator = {
  ADD: add,
  MINUS: subtract,
  TIMES: multiply,
  DIVIDE: divide
}

const calc = function (acc, x) {
  if (isNumber(acc)) {
    return operator[x](acc)
  }

  if (isFunction(acc)) {
    return acc(x)
  }

  return x
}


// [ 10, '+'', 20, '-', 30] = 0
const calculate = function (...e) {
  return e.reduce(calc, 0)
}

calculate(10, '+', 2, '-', 4, '*', 2)
```

[Back](/calculator)
