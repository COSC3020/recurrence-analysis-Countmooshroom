[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=11730512&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

# Answer

This algorithm ends when n <= 1, and it returns nothing:

$T(n) = 1$ if n <= 1

Otherwise, this algorithm calls itself three different times, each with 1/3 the size of $n$.  There is also a loop in each run that executes $n^2$ times, with a loop inside that executes n times, with a loop inside that executes $n^2$ times.  Together, it runs $n^5$ iterations.  All that can be written and solved as this:

$T(n) = 3T(\frac{n}{3}) + n^5$ if n > 1

= $3(3T(\frac{n}{9}) + (\frac{n}{3})^5) + n^5$
     
= $9T(\frac{n}{9}) + (\frac{3}{3^5})n^5 + n^5$
     
= $27T(\frac{n}{27}) + (\frac{9}{9^5})n^5 + (\frac{3}{3^5})n^5 + n^5$
 
= $27T(\frac{n}{27}) + (\frac{9}{9^5} + \frac{3}{3^5} + \frac{1}{1^5})n^5$

= $27T(\frac{n}{27}) + (\frac{1}{9^4} + \frac{1}{3^4} + \frac{1}{1^4})n^5$

= $3^iT(\frac{n}{3^i}) + (\sum\limits_{j=1}^{i} \frac{1}{j^4})n^5$

Let $i = log_3n$

= $n * T(\frac{n}{n}) + (\sum\limits_{j=1}^{log_3n} \frac{1}{j^4})n^5$

= $n * 1 + n^5$

= $n + n^5$

= $n^5$

The time complexity is $\Theta(n^5)$

