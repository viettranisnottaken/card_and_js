Test questions: https://docs.google.com/document/d/1t0cYbtyMaYR33b7VaSHYhkjM7dKQThFGLw9YnlzZaXQ/edit?usp=sharing

1. Q1
    - Answer: B, C
    - Explanation: Variable names in JS must begin with a letter or '_'.
2. Q2
    - Answer: C
    - Explanation: An outer scope does not have access to its inner scope's variables. Because variable `a` was declared in the scope of the provided function, in the scope of `Window`/`Global`, there is no `a`. By default, `a = undefined`.
3. Q3
    - Answer: B
    - Explanation: A function returns undefined by default. The provided function returns before running `'Hello: ' + name` so the function returns undefined.
4. Q4
    - Answer: C
    - Explanation: floating point: some decimal numbers bear values different from those we know. In this case `0.1 + 0.2 == 0.30000000000000004`
5. Q5
    - Answer: D
    - Explanation: 
        - When a property in an object is referenced, JS looks into that object for the property. If the object does not have that property, JS looks down into the prototype chain of that object. In this case, because obj has a `toString` property, that property will be called instead of `Object.prototype.toString`.  
        - `obj.toString()` returns a string of the current moment because of implicit type coercion: the operator `+` when placed next to a string is treated at a `concat()`
        - `+obj.toString()` returns NaN because the string that `obj.toString()` returns cannot be converted into a number.
6. Q6
    - Answer: A
    - Explanation: 
        - When JS encounters an object where a primitive value is expected, it calls `valueOf()`. In this case, because obj has `valueOf()`, it will be called instead of `Object.prototype.valueOf()`.
        - When the operator `+` is used with arrays, JS converts the arrays (and the other operand) into strings. In this case, `console.log([1, 2, 3] + obj);` will log a string.
        - In this case, `obj.valueOf()` returns the number `456`, which will be converted in to string, then concatinated with the string `'1, 2, 3'` (converted from the provided array) -> the console logs `'1, 2, 3456'`
7. Q7
    - Answer: D
    - Explanation: `setTimeout()` moves its callback to the bottom of the event loop queue, even if the timer is `0`, therefore `1` and `4`, in said sequence, will be logged first. `3` will then be logged, then `2` because of the timer.
8. Q8
    - Answer: A
    - Explanation: The outer function is an IIFE, which returns another IIFE, which logs `x`. Because the outer function is called with `1`, `x` equals `1` -> `1` is logged into the console. 
9. Q9
    - Answer: D
    - Explanation: 
        - Async function returns a resolved promise of which value is that the function returns. In this case, `r5()` returns `Promise.resolved(5)`.
        - The second function is suspended by the keyword `await` until it receives `Promise.resolved(5)` from `r5()`
        - When the second function is called, in order to run the line `x += await r5()`, it has to get the value of `x`, which is `0`. Then, it waits until the value `5` is emitted from `r5()`. After `r5()` finishes, the line is run, then we get `x = 5`. Basically, JS runs the left side of the equation, then it waits until the promise is resolved, then runs the right side of the equation.
        This is the function desugarized:
        ```
        let x = 0;
        async function r5() {
            x += 1;
            console.log(x);
            return 5;
        }

        (async () => {
            x = 0 
            x = x + await r5();
            console.log(x);
        })();
        ```
10. Q10
    - Answer: C, D
    - Explanation: in answer D, function sum when called with and `x` value returns a function which requires a `y` value and returns the sum of `x` and `y`. C is just the arrow function version of D.