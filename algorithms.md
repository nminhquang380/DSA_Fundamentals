# Data Structure and Algorithms

Start: 03/07/2023
Status: In progress

# Essential Algorithms for Interview

## Algorithms

- **Sorting algorithms:**
    
    Here is a list of common sorting algorithms with explanations and Python implementations:
    
    - **Bubble Sort**: Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.
        
        ```
        def bubble_sort(arr):
            n = len(arr)
        
            for i in range(n):
                for j in range(n-i-1):
                    if arr[j] > arr[j+1]:
                        arr[j], arr[j+1] = arr[j+1], arr[j]
        
            return arr
        
        ```
        
    - **Selection Sort**: Selection Sort is a simple sorting algorithm that works by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning. The algorithm maintains two subarrays in a given array.
        
        ```
        def selection_sort(arr):
            n = len(arr)
        
            for i in range(n):
                min_index = i
                for j in range(i+1, n):
                    if arr[j] < arr[min_index]:
                        min_index = j
        
                arr[i], arr[min_index] = arr[min_index], arr[i]
        
            return arr
        
        ```
        
    - **Insertion Sort**: Insertion Sort is a simple sorting algorithm that builds the final sorted array one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort.
    
    ```
    def insertion_sort(arr):
        n = len(arr)
    
        for i in range(1, n):
            key = arr[i]
            j = i-1
            while j >=0 and key < arr[j] :
                    arr[j+1] = arr[j]
                    j -= 1
            arr[j+1] = key
    
        return arr
    
    ```
    
    - **Merge Sort**: Merge Sort is a divide and conquer algorithm that was invented by John von Neumann in 1945. It is a comparison-based algorithm that works by dividing an array into two halves, sorting the two halves independently, and then merging the sorted halves back together.
        
        ```
        def merge_sort(arr):
            if len(arr) > 1:
                mid = len(arr)//2
                L = arr[:mid]
                R = arr[mid:]
        
                merge_sort(L)
                merge_sort(R)
        
                i = j = k = 0
        
                while i < len(L) and j < len(R):
                    if L[i] < R[j]:
                        arr[k] = L[i]
                        i+=1
                    else:
                        arr[k] = R[j]
                        j+=1
                    k+=1
        
                while i < len(L):
                    arr[k] = L[i]
                    i+=1
                    k+=1
        
                while j < len(R):
                    arr[k] = R[j]
                    j+=1
                    k+=1
        
            return arr
        
        ```
        
    - **Quick Sort**: Quick Sort is a divide and conquer algorithm that was invented by Tony Hoare in 1959. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.
        
        ```
        def quick_sort(arr):
            if len(arr) <= 1:
                return arr
        
            pivot = arr[len(arr)//2]
            left = [x for x in arr if x < pivot]
            middle = [x for x in arr if x == pivot]
            right = [x for x in arr if x > pivot]
        
            return quick_sort(left) + middle + quick_sort(right)
        
        ```
        
    
    Remember, it's important to have a good understanding of these algorithms and be able to implement them in code. Practice makes perfect, so make sure to keep practicing these algorithms until you feel comfortable with them. Good luck with your interviews!
    
- **Searching algorithms:**
    - **Sequential Search**: Linear Search,…
        
        ```
        def linear_search(arr, x):
            for i in range(len(arr)):
                if arr[i] == x:
                    return i
            return -1
        ```
        
    - **Interval Search**: Binary Search, Ternary Search,…
        
        Binary search is an algorithm used to find the position of a specific value within a sorted array. The algorithm works by repeatedly dividing the search interval in half until the target value is found or the search interval is empty.
        
        This process is repeated until the target value is found or the search interval is empty. Because the search interval is divided in half at each step, the time complexity of binary search is O(log n), where n is the size of the array.
        
        ```
        def binary_search(arr, x):
            low = 0
            high = len(arr) - 1
            while low <= high:
                mid = (low + high) // 2
                if arr[mid] < x:
                    low = mid + 1
                elif arr[mid] > x:
                    high = mid - 1
                else:
                    return mid
            return -1
        ```
        
    - **DFS**
        
        DFS stands for Depth-First Search, which is a way to traverse a graph or tree data structure. The algorithm starts at a root node and explores as far as possible along each branch before backtracking. This means it goes as deep as possible into the graph before exploring other branches.
        
        Here is an implementation of DFS in Python:
        
        ```
        def dfs(graph, start):
            visited = set()
            stack = [start]
        
            while stack:
                vertex = stack.pop()
        
                if vertex not in visited:
                    visited.add(vertex)
                    stack.extend(graph[vertex] - visited)
        
            return visited
        
        ```
        
    - **BFS**
        
        BFS stands for Breadth-First Search, which is a way to traverse a graph or tree data structure. The algorithm starts at a root node and explores all the neighboring nodes at the present depth before moving on to the nodes at the next depth level. This means it explores all the nodes at one level before moving on to the next level.
        
        Here's an implementation of BFS in Python:
        
        ```
        def bfs(graph, start):
            visited = set()
            queue = [start]
        
            while queue:
                vertex = queue.pop(0)
        
                if vertex not in visited:
                    visited.add(vertex)
                    queue.extend(graph[vertex] - visited)
        
            return visited
        
        ```
        
- **Divide and conquer:**
    
    > **Divide:** This involves dividing the problem into smaller sub-problems.
    > 
    
    > **Conquer:** Solve sub-problems by calling recursively until solved.
    > 
    
    > **Combine:** Combine the sub-problems to get the final solution of the whole problem.
    > 
    
    Standard algorithms that follow divide and conquer algorithm:
    
    1. **Quicksort**: The algorithm picks a pivot element and rearranges the array elements so that all elements smaller than the picked pivot element move to the left side of the pivot, and all greater elements move to the right side. Finally, the algorithm recursively sorts the subarrays on the left and right of the pivot element.
    2. **Merge sort:**  is also a sorting algorithm. The algorithm divides the array into two halves, recursively sorts them, and finally merges the two sorted halves.
    3. **Closest Pair of Points:**
        
        Following are the detailed steps of a O(n (Logn)^2) algorithm. *Input:* An array of n points *P[]* *Output:* The smallest distance between two points in the given array.As a pre-processing step, the input array is sorted according to x coordinates.
        
        **1)** Find the middle point in the sorted array, we can take *P[n/2]* as middle point.
        
        **2)** Divide the given array in two halves. The first subarray contains points from P[0] to P[n/2]. The second subarray contains points from P[n/2+1] to P[n-1].
        
        **3)** Recursively find the smallest distances in both subarrays. Let the distances be dl and dr. Find the minimum of dl and dr. Let the minimum be d.
        
        ![https://media.geeksforgeeks.org/wp-content/uploads/mindis.png](https://media.geeksforgeeks.org/wp-content/uploads/mindis.png)
        
        **4)** From the above 3 steps, we have an upper bound d of minimum distance. Now we need to consider the pairs such that one point in pair is from the left half and the other is from the right half. Consider the vertical line passing through P[n/2] and find all points whose x coordinate is closer than d to the middle vertical line. Build an array strip[] of all such points.
        
        ![https://media.geeksforgeeks.org/wp-content/uploads/closepair.png](https://media.geeksforgeeks.org/wp-content/uploads/closepair.png)
        
        **5)** Sort the array strip[] according to y coordinates. This step is O(nLogn). It can be optimized to O(n) by recursively sorting and merging. 
        
        **6)** Find the smallest distance in strip[]. This is tricky. From the first look, it seems to be a O(n^2) step, but it is actually O(n). It can be proved geometrically that for every point in the strip, we only need to check at most 7 points after it (note that strip is sorted according to Y coordinate). See **[this](http://people.csail.mit.edu/indyk/6.838-old/handouts/lec17.pdf)** for more analysis.
        
        **7)** Finally return the minimum of d and distance calculated in the above step (step 6)
        
        ```python
        import math
        
        class Point:
        	def __init__(self, x, y):
        		self.x = x
        		self.y = y
        
        def compareX(p1, p2):
        	return (p1.x - p2.x)
        
        def compareY(p1, p2):
        	return (p1.y - p2.y)
        
        def dist(p1, p2):
        	return math.sqrt((p1.x-p2.x)**2 + (p1.y-p2.y)**2)
        
        def bruteForce(P, n):
        	min_dist = float("inf")
        	for i in range(n):
        		for j in range(i+1, n):
        			if dist(P[i], P[j]) < min_dist:
        				min_dist = dist(P[i],P[j])
        	return min_dist
        
        def min(x, y):
        	return x if x < y else y
        
        def stripClosest(strip, size, d):
        	min_dist = d
        	strip = sorted(strip, key= lambda point: point.y)
        
        	for i in range(size):
        		for j in range(i+1, size):
        			if (strip[j].y - strip[i]) >= min_dist:
        				break
        			if dist(strip[j], strip[i]) < min_dist:
        				min_dist = dist(strip[j], strip[i])
        	return min_dist
        
        def closestUtil(P, n):
        		if n <= 3:
                return bruteForce(P, n)
            mid = n//2
            midPoint = P[mid]
            dl = closestUtil(P, mid)
            dr = closestUtil(P[mid:], n - mid)
            d = min(dl, dr)
            strip = []
            for i in range(n):
                if abs(P[i].x - midPoint.x) < d:
                    strip.append(P[i])
            return min(d, stripClosest(strip, len(strip), d))
        
        def clocest(P, n):
        	P = sorted(P, key=lambda point: point.x)
        	return (clocestUtil(P,n))
        
        ```
        
    4. Regularized Divide and Conquer Algorithms:
        
        ```python
        def DAC(a, i, j): # a is array, i is start point, j is end point
        	if small(a,i,j):
        		return basicSolution(a,i,j)
        	else:
        		mid = divide(a, i ,j)
        		b = DAC(a, i, mid)
        		c = DAC(a, mid, j)
        		d = combine(b, c)
        	return d
        ```
        
- **Greedy Algorithms:**
    
    > Greedy Algorithms are used to solve optimization problems by making the locally optimal choice at each step. Some of the most commonly used greedy algorithms include the Activity Selection problem, the Fractional Knapsack problem, and Huffman Encoding.
    > 
    
    Here's an example implementation of a greedy algorithm in Python, which solves the problem of finding the minimum number of coins needed to make change for a given amount:
    
    ```python
    def greedy_coin_change(coins, amount):
        """
        Given a list of coin denominations and an amount, returns the minimum number of coins needed to make change for that
        amount using a greedy algorithm.
        """
        coins = sorted(coins, reverse=True)
        num_coins = 0
        for coin in coins:
            while amount >= coin:
                amount -= coin
                num_coins += 1
        return num_coins
    
    ```
    
    In this implementation, we first sort the list of coin denominations in descending order. We then iterate over the list of coins, starting with the largest denomination. At each step, we subtract as many coins as possible from the remaining amount, and add the number of coins used to our running total. Once we've exhausted all the available coins, we return the total number of coins used.
    
    Note that while this algorithm is often effective at producing good solutions to optimization problems, it is not guaranteed to find the optimal solution in all cases. In some cases, a brute-force approach (such as dynamic programming) may be necessary to ensure the optimal solution is found.
    
- **Dynamic Programming:**
    
    > Dynamic Programming is an algorithmic technique that is used to solve problems by breaking them down into smaller sub-problems. Some of the most commonly used dynamic programming algorithms include the Knapsack problem, the Longest Common Subsequence problem, and the Fibonacci sequence.
    > 
- **Graph Algorithms:**
    
    > Graph Algorithms are used to solve problems that involve graphs or networks. Some of the most commonly used graph algorithms include Breadth-First Search (BFS), Depth-First Search (DFS), Dijkstra's Algorithm, and the Minimum Spanning Tree (MST).
    > 
- **String Algorithms:**
    
    > String Algorithms are used to solve problems that involve strings or text. Some of the most commonly used string algorithms include the Knuth-Morris-Pratt Algorithm (KMP), the Rabin-Karp Algorithm, and the Longest Common Prefix (LCP) problem.
    > 
- **Backtracking Algorithms:**

## Data Structutes

- **Linear Data Structures:**
    - Static DS
        - Array
    - Dynamic DS
        - Queue
        - Stack
        - Linked list
- **Non-linear Data Structures:**
    - Tree
    - Graph

Remember, it's important to have a good understanding of these algorithms and be able to implement them in code. Practice makes perfect, so make sure to keep practicing these algorithms until you feel comfortable with them. Good luck with your interviews!