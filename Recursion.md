---


---

<h1 id="recursion">Recursion</h1>
<h2 id="the-idea-of-recursion">The Idea of Recursion</h2>
<p>Recursion is a computer science concept that is present in almost every programming language. Compared to loops, which are absent in racket, or matching, which is absent in python and java, recursion is present in all three. This is because, unlike most other features of programming languages, recursion is in and if itself, fairly simple. Any programming language with the ability to call functions within the program will be able to implement recursion. Recursion itself involves a function calling itself. The implementation and syntax of recursion is fairly straightforward. However, the concept of recursion as well as the multitude of its uses and flexibility can make the concept an extremely complex part of computer science.</p>
<p>A recursive function contains two elements, a base case and a recursive case. A recursive case is a case which will case the function to call itself. This is the primary element that causes recursive functions to behave the way that that do. Without a recursive case, a function will act as it normally would. A base case is a case which will cause the function to not call itself and instead return a normal value. This is extremely important. Without a base case, a recursive function will call itself over and over again without any way to terminate.</p>
<pre><code>def recursiveFunction(num)
    if (num == 0):
	    return 1
	else:
		return recursiveFunction(num - 1)
</code></pre>
<p>This is a fairly simple recursive function. The base case would trigger if the the input is equal to 0, at which point the function would return 1. Otherwise, the recursive case would trigger. The function would call itself again with the argument (num - 1). If main were to call this function with an argument of 2, the first call of the recursiveFunction would result in the the function calling itself with an argument of 1 (the result of this first call of the recursiveFunction would be equal to the result of this next call of resursiveFunction), which would then call itself again with an argument of 0, which would trigger the base case and return 1. In this example, and in most cases of recursion, you see a linear recursion implementation.</p>
<h3 id="the-purpose-of-recursion">The Purpose of Recursion</h3>
<p>Imagine you want to count the number of leaves on a tree. The trunk of the tree splits up into 2 branches, which can contain any number of leaves and further splits itself up into either 1 or 2 smaller branches. Each branch of the tree will either diverge into smaller branches, or will not split up into any at all. What would be the best approach for us to count every leaf on the tree? The best way for us to approach a problem as large as this would be to break it into smaller problems. If we were to start on the trunk of the tree, we would see it split up into 2 smaller branches. We would know that the value of the the total number of leaves on the tree would equal the total number of leaves on the trunk, plus the number of leaves in each of the branches attached to the trunk combined. And the number of leaves on each branch of the tree extending from the trunk would equal the number of leaves on that branch plus the number of leaves on the branches extending from that branch. In this way, we have created a function, countLeaves, which would take in a branch and return the number of leaves on that branch. But in order for it to do so, it would have to recursively call itself, countLeaves, on each branch extending from itself and add the values from that to the number of leaves on that branch.</p>
<pre><code>def countLeaves(node):
    if (node == null):
	    return 0
	else:
		return (node.data + countLeaves(node.left) + countLeaves(node.right))
</code></pre>
<p>We have implemented countLeaves above in code. The tree we are counting the leaves are is being represented as a binary tree. Each node of the binary tree represents a branch, containing a node.data value, which represents the amount of leaves on that branch, as well as a node.left and node.right value, which represent the branches extending from that branch. The base case is triggered if the node value is null, which returns 0. This is the case where a branch does not exist. A branch with no smaller branches extending from itself will thus have a node.right and node.left value that are both equal to null (a branch with one extending branch will have one node.right or node.left value that is equal to null). In this case, calling countLeaves with this branch as an argument will return only the number of leaves on the branch plus 0 because the recursive calls to node.left and node.right will both return 0. The recursive case is triggered if the current node is not null. This is a branch that exists and may contain leaves and smaller branches. In this case, countLeaves is recursively called again on the smaller branches. Notice in this case, that a single call to countLeaves will recursively call itself two times if the recursive case is triggered. This is called binary recursion.</p>
<p>In computer science, you will likely encounter similar examples to the one we just covered. In in most of these cases, recursion will one of the best ways you can approach these problems, if not the only viable solution. Think about how we would calculate the sum of a binary tree without recursion. We could try using loops, but we would need to organize the nodes of the tree in a linear manner in order for us to iterate over them. Loops are unable to deal with diverging cases like the one we encountered, at least not in an efficient manner where you could justify using them over recursive functions. Recursion acts to break down a problem into smaller pieces, which you either know the value of, or can solve by applying the same algorithm to even smaller pieces and combining the results you find. These are some examples of where you might find recursion.</p>
<pre><code>def fibonacci(num):
	if (num &lt;= 1):
		return n
	else:
		return (fibonacci(n - 1) + fibonacci(n - 2))
</code></pre>
<p>The value of a Fibonacci number given its index in the sequence will be one if its place in the sequence is either one or zero. This is the base case. Otherwise, the value of the number will be equal to the Fibonacci number with an index one less of the given index plus the value of the number with an index two less than the given index. This is the recursive case.</p>
<pre><code>def binarySearch(arr, low, high, x):
if high &gt;= low:
    mid = (high + low)
    if arr[mid] == x:
        return mid
    elif arr[mid] &gt; x:
        return binarySearch(arr, low, mid - 1, x)
    else:
        return binarySearch(arr, mid + 1, high, x)
else:
    return -1
</code></pre>
<p>A binary search a more efficient search algorithm than traditionally iterating through a list to find a value. The algorithm works by partitioning the array it was given in half, finding out which of the two halves can contain the value it is looking for, and then recursively calling that particular half. The base case occurs when the low value is greater than the high value, a case where the given value does not exist in the array, and when the middle value of the array is found to equal the given value, at which point the value has been found. The recursive case occurs when the middle value does not equal the given value, which means that the value exists in either of the two halves we partitioned, meaning that we would have to recursively call binarySearch on those two halves.</p>
<h2 id="things-to-look-out-for">Things To Look Out For</h2>
<p>You’ve probably seen from the examples that we’ve covered, just how important the base case is. Calling a function recursively means that you expect a response, a return value. No matter how many calls of the recursive function you make, every single one of them should return a value, and the base case is responsible for that. Take a look at the given example that we looked at before.</p>
<pre><code>def recursiveFunction(num)
    if (num == 0):
	    return 1
	else:
		return recursiveFunction(num - 1)
</code></pre>
<p>If the main were to call this function with a negative argument value, such as -5, the base case will never be reached. The first call of the function will fail the if conditional and recursively call the function again with an argument of -6. Because of this, the function will call itself over and over again without terminating since the recursive function will never be called with an argument of 0. This is not a compile time or run time error and may be hard to find if you’re not careful.</p>
<p>Similarly, circularity is another problem that will prevent you from reaching your base case. Circularity occurs when the arguments for a recursive function either are the same as the arguments in the previous call of the function in the stack, or the same as with a previous function call somewhere further back. If you call a recursive function with an argument of 4, which leads the function to call itself with an argument of 4, you end up with an infinite loop, but if an argument of 4 leads to a function call with an argument of 5, which leads to a function call with an argument of 8, which leads to a function call with an argument of 4, you will also find an infinite loop. The sequence of 4 to 5 to 8 to 4 will repeat itself forever. Sometimes, it’s hard to correctly identify circularity in a function.</p>
<pre><code>def syracuse(num):
    if (num == 1):
	    print("Terminated")
	elif (num % 2 == 0):
		syracuse(num / 2)
	else:
		syracuse(3 * num + 1)
</code></pre>
<p>The Syracuse problem is an unsolved math problem that states that any number will eventually reach 1 if it is put in this sequence: If the number is even, the next value in the sequence is the number divided by 2. If the number is odd, the next value in the sequence is the number multiplied by 3 and added to 1. If this statement is true, the given code for the syracuse problem will never result in circularity, because the base case of num == 1 will eventually be solved in the sequence and the function will eventually terminate with the print statement. Because the syracuse problem has yet to be solved, however, it is unknown whether there exists an argument that will cause circularity; that is to say, recursively call itself with no termination. And noticeably, any negative argument in this function will also cause circularity.</p>
<h2 id="time-complexity-and-efficiency">Time Complexity and Efficiency</h2>
<p>Calling a function itself can be fairly simple. Taking in an argument, calculating a value based on the input, and returning the value is fairly intuitive. But using recursion to call a function over and over again can lead to some significant issues in regards to your program’s efficiency over time. And while recursion can be a very good solution to some computer science examples, sometimes it’s important to see if there’s a better option.</p>
<h3 id="the-stack-frame-and-the-call-stack">The Stack Frame and the Call Stack</h3>
<p>Whenever a function is called in any programming language, a stack frame is created. A stack frame is a certain amount of memory that the program sets aside for the function to use. A stack frame contains arguments given to the function to use, the functions local variables, and the address that the function is located at. The stack frame also allows your computer to hand off control of the program back to function that called the called function and returns the values that the called function computes.</p>
<p>The sequence of stack frames that are created and executed exists inside the call stack. The call stack organizes the stack frames in a LIFO (last in first out) manner. The last stack frame that is put inside the call stack will be executed and removed from the call stack, handing off control of the program to the stack frame right below it. Imagine a function one that calls two that calls three which will return a value.</p>
<pre><code>Current Function		Call Stack
one()					|one|
two()					|one|two|
three()					|one|two|three|
three() returns				|one|two|
two() returns				|one|
</code></pre>
<p>The above illustrates the call stack during the execution of the one function. When three is called, the call stack contains all three functions. When three returns a value, the three stack frame is removed from the call stack, transitioning control to the two function and leaving only one and two in the call stack. And when two returns, the two stack frame is removed from the call stack, leaving one.</p>
<p>So why is this important in relation to recursion? Well, calling a function recursively is no different than calling a function normally, at least when it pertains to the call stack and the function’s stack frame. Every time a function is called, a stack frame will be created and pushed onto a call stack, complete with all the arguments, local variables, pointers, addresses, and space in the memory that a stack frame would normally be complete with. Normally, this amount of memory allocation is fine. If a function can operate correctly without recursion, it would only take up a single stack frame in the call stack. Only one stack frame will be pushed onto the stack and only one will be popped. But a recursive function, that works by calling itself over and over again, will push any number of stack frames to the call stack over and over again.</p>
<p>Take this simple code that calculates the number of square roots less than a given number.</p>
<pre><code>def roots(num):
    if (num == 0):
	    return 0
	elif (sqrt(num).is_integer()):
		return 1 + roots(num - 1)
	else:
		return roots(num - 1)
</code></pre>
<p>This is what the stack frame looks like with an initial call to the function with an argument of 6:</p>
<pre><code>roots(6) | roots(5) | roots(4) | roots(3) | roots(2) | roots(1) | roots(0)
</code></pre>
<p>In cases like this, the call stack will grow proportional to the size of the input. In many other case, such as our countLeaves function early where we traversed a binary tree, the call stack will grow exponentially to the size of the input.</p>
<p>Is is important to note, as well, that when root(0) is finished executing and returns 0, not all the stack frames below it will continue to return a value down to roots(6). The call to the function roots(4), for instance, passes an argument of 4 to the function. This triggers the first recursive case, which adds a 1 to the value of the next recursive call. So when roots(3) finishes executing and returns a value, that value has to be added on to 1 before that value is returned.</p>
<h3 id="efficiency-of-a-recursive-function">Efficiency of a Recursive Function</h3>
<p>So why is all of this important in regards to efficiency? Like we mentioned before, calling a function recursively is no different to the system than calling a function normally. And for each call of the function, it takes a small amount of time for the call to be initialize and the stack frame set up. Even a simple recursive function can take up significant system resources if the function is called too much. It’s important to keep in mind the efficient of your function in relation to the amount of work your function is doing. If you’re planning on recursively calling a function many times, and your function’s job can be done inside of a loop, it’s likely that implementing a loop will be take up less system resources than recursion.</p>
<p>Another important idea to consider is that the amount of memory that’s available to you is not infinite. As a result, the maximum size of your call stack will not be infinite. Take a look at what might happen if you recursively call a function too many time.</p>
<pre><code>def recursiveFactorial(n):
    if (n == 1):
        return 1
    else:
        return n * recursiveFactorial(n - 1)

def main():
    print(recursiveFactorial(1000))
</code></pre>
<p>Output:</p>
<pre><code>RecursionError: maximum recursion depth exceeded in comparison
</code></pre>
<p>It’s unlikely that you would need to implement a recursive function that would ever need to call itself 1000 times, but limitations like these are important to keep in mind. You may never have to code a single function that would extend the call stack by 1000 stack frames, but in a large program that uses a number of different functions, the call stack may eventually reach its limit if you’re not too careful. Nonetheless, the factorial code above would not necessarily need to implemented recursively. A better implementation would be to loop over the values leading up to n and multiply the values to an accumulator.</p>
<h3 id="tail-recursion">Tail Recursion</h3>
<p>There is, however, one very important and very useful exception in regards to a recursive function growing the call stack. You would recall that during the recursiveFactorial() function we wrote earlier, during each recursive case of the each call of the function, we needed to multiply n to the next recursive function call. Because of this, the compiler to the program needed to make sure that each function call will grow the call stack, because there is still something each call of the function needs to do once the next recursive call returns.</p>
<p>With this, we are able to avoid growing the call stack by implementing our recursive functions in such a way so as to make sure that the recursive call is the very last thing done by the function before returning (This is not the case in recursiveFactorial(). In recursiveFactorial(), multiplying n is the last thing done to the function before returning). Take a look at the following implementation of recursiveFactorial() using tail recursion.</p>
<pre><code>def recursiveFactorial(n, acc):
    if (n == 1):
        return acc
    else:
        return recursiveFactorial(n - 1, n * acc)

def main():
	print(recursiveFactorial(5, 1)
</code></pre>
<p>Tail recursion is possible in this implementation of recursiveFactorial because we are using an accumulator, represented by the second argument in the function call, to keep track of the value of the result. In the first initial call to recursiveFactorial in main, we pass in an initial accumulator of 1. In the first execution of recursiveFactorial, the recursive case is triggered, calling the function again, this time with an accumulator value of 5. During the execution of the next recursive call, the accumulator is 20. Once the base case is triggered, we are ready to return the value of the accumulator, which will be 120, the value of 5!.</p>
<p>The reason why tail recursion avoids growing the call stack is because, once the next recursive call is done, there is nothing left to do in the current function call, so the stack frame for the call of the current function is no use. Once recursiveFunction(5, 1) calls recursiveFunction(4, 5), recursiveFunction(4, 5) will yield the same result as recursiveFunction(5, 1), which means that recursiveFunction(5, 1) is no longer necessary. Note that this is only possible because the call to the next function is the last thing done by the recursive case. If we, for whatever reason, needed to add 3 to the result of recursiveFunction(4, 5) once it returns, we would still need recursiveFunction(5, 1) and by extention, its stack frame, because it still has work to do.</p>
<p>A final note to make of tail recursion is the importance of the initial accumulator and how the accumulator is handled. In the case of factorial, we needed to multiply add the decrementing values of n together. That is why we multiplied n by the accumulator inside the next recursive call. The initial accumulator is 1 because the values of n multiplied to 1 is will be the product of all the n values. If the initial accumulator is 0, the final result will always be 0.</p>
<h2 id="conclusion">Conclusion</h2>
<p>Recursion is one of the most important concepts in computer science. It can be an extremely useful tool in countless problems you will encounter and has been implemented in many of the most well known established computer science solutions out there. But like most other computer science tools, recursion can get extremely complicated on a conceptual level, and extremely dangerous on a technical level, which is why being able to understand recursion is one of the most important steps you can take.</p>

