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

$T(n) = 3T(n / 3) + n^5$ if n > 1  
     = $3(3T(n / 9) + (n/3)^5) + n^5$  
     = $9T(n / 9) + (1/3^5)n^5 + n^5$  
     = $27T(n / 27) + (1/9^5)n^5 + (1/3^5)n^5 + n^5$  
     Let c = some constant factor that doesn't really matter in the end  
     = $27T(n / 27) + cn^5$  
     = $27T(n / 27) + n^5$  
     = $3^iT(n / 3^i) + in^5$  
     Let $i = log_3(n)$  
     = $n * T(n / n) + n^5log(n)$  
     = $n * 1 + n^5log(n)$  
     = $n + n^5log(n)$  
     = $n^5log(n)$

