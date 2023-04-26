# Big O
Big 0 time is the language and metric we use to describe the efficiency of algorithms. Not understanding 
it thoroughly can really hurt you in developing an algorithm. Not only might you be judged harshly for 
not really understanding big 0, but you will also struggle to judge when your algorithm is getting faster or 
slower. 

In my opinion, it seems quite similar to LIM in Math.
## Time Complexity
We could describe the data transfer algorithm runtime as:
- Electronic Transfer: 0(s) , where s is the size of the file. This means that the time to transfer the file 
increases linearly with the size of the file. (Yes, this is a bit of a simplification, but that's okay for these 
purposes.) 
- Airplane Transfer: 0(1 ) with respect to the size of the file. As the size of the file increases, it won't take 
any longer to get the file to your friend. The time is constant.

There are many more runtimes than this. Some of the most common ones are 0( log N),0(N log N), 
0(N), O(N^). There's no fixed list of possible runtimes, though. 
You can also have multiple variables in your runtime. For example, the time to paint a fence that's w meters 
wide and h meters high could be described as 0(wh).

## Best Case, Worst Case, Expected Case
We can actually describe our runtime for an algorithm in three different ways. 
- Best Case: If all elements are equal, then quick sort will, on average, just traverse through the array once. 
This is 0(N). (This actually depends slightly on the implementation of quick sort. There are implementa￾tions, though, that will run very quickly on a sorted array.) 
- Worst Case: What if we get really unlucky and the pivot is repeatedly the biggest element in the array? 
(Actually, this can easily happen. If the pivot is chosen to be the first element in the subarray and the 
array is sorted in reverse order, we'll have this situation.) In this case, our recursion doesn't divide the 
array in half and recurse on each half. It just shrinks the subarray by one element. This will degenerate 
to anO(N^) runtime. 
- Expected Case: Usually, though, these wonderful or terrible situations won't happen. Sure, sometimes 
the pivot will be very low or very high, but it won't happen over and over again. We can expect a runtime 
of0( N log N).
## Space Complexity
Time is not the only thing that matters in an algorithm. We might also care about the amount of memory— 
or space—required by an algorithm. 
Space complexity is a parallel concept to time complexity. If we need to create an array of size n, this will 
require 0(n ) space. If we need a two-dimensional array of size nxn, this will require 0(n^2) space.
## Drop the constants
It is very possible for 0(N ) code to run faster than 0(1 ) code for specific inputs. Sig 0 just describes the 
rate of increase. 
For this reason, we drop the constants in runtime. An algorithm that one might have described as 0( 2N) 
isactuallyO(N). 
Many people resist doing this. They will see code that has two (non-nested) for loops and continue this 
0(2N). They think they're being more "precise." They're not.
## Drop the non-dominant terms
What do you do about ari expression such as 0(N^3 + N)?That second N isn't exactly a constant. But it's not especially important. 
We already said that we drop constants.Therefore, 0(N^J + N^2) would be (N^?)- If we don't care about that 
latter NJ term, why would we care about N? We don't. 
You should drop the non-dominant terms, 
- 0(N^2 + N) becomes O(N2). 
- 0(N + log N) becomes O(M). 
- 0(5*2^N + ie00N100) becomes 0(2^S). 
## Multi-Part Algorithms: Add vs Multiply
- If your algorithm is in the form "do this, then, when you're all done, do that" then you add the runtimes. 
- If your algorithm is in the form "do this for each time you do that" then you multiply the runtimes. 
## Amortized Time

## Log N Runtimes
This is a good takeaway for you to have. When you see a problem where the number of elements in the 
problem space gets halved each time, that will likely be a 0( lo g N) runtime. 
This is the same reason why finding an element in a balanced binary search tree is O(lo g N). With each 
comparison, we go either left or right. Half the nodes are on each side, so we cut the problem space in half 
each time.
## Recursive Runtimes
Try to remember this pattern. When you have a recursive function that makes multiple calls, the runtime will 
often (but not always) took like O(branchest^i), where branches is the number of times each recursive 
call branches.

