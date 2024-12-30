---
layout: post
title: "Sorting Algorithms"
excerpt: "My attempt on sorting out the sorts."
date: 2024-12-25 00:00:00 +0500
categories: post
tags:
- data-structures
- algorithms
- sorting
- search 
usemathjax: true
---

Long time ago I've heard someone say:

> Today's programmers are incompetent. Most of them can't even write the quicksort from memory.

And for a long time this bothered me. It felt like I can't call myself a real programmer if I didn't remember every sorting algorithms there is, which I didn't, and still don't. Because in reality you don't really have to, unless you are taking a course in programming. Almost every programming language has these things already implemented and built in, all you have to know is the name of the function that does what you want.

But there must be a valid reason to teach this, right? Learning it certainly wouldn't hurt. However, I was surprised to discover that for something that is taught so commonly and frequently – there is no single reliable and complete source on the topic (or maybe I just didn't search well enough). Information is scattered around, and often different sources contradict each other. 

So, after some research, and couple prompts to ChatGPT later I tried to structure what was out there, trying to ensure factual accuracy and clarity. Also note that there is two searching algorithms mentioned at the end.

Sources I used are [DSA Tutorial from w3schools](https://www.w3schools.com/dsa/index.php) and from [Programiz.com](https://www.programiz.com/dsa/bubble-sort). Reference them for visuals and more details, but be careful, because they are not great sources either.

If you find factual errors in this article, or want to contribute – feel free to propose a change on [github](https://github.com/sagyzdop/blog/blob/main/_posts/2024-12-25-Sorting-Algorithms.markdown?plain=1).

**Table of contents**

---

* TOC
{:toc}

## Categorization of Sorting Algorithms

---

Sorting algorithms can be categorized as follows (note that the list of examples in the tables are just the ones present in this article, there are more examples of algorithms you can put there that are not mentioned, like [Heap Sort](https://www.programiz.com/dsa/heap-sort)): 

### Data Location (RAM vs. Disk)

| Internal Sorting                                                                                                                                                                                 | External Sorting          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------- |
| All data fits in RAM.                                                                                                                                                                            | Requires disk storage.    |
| [Bubble Sort](#bubble-sort)<br>[Selection Sort](#selection-sort)<br>[Insertion Sort](#insertion-sort)<br>[Quicksort](#quicksort)<br>[Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort) | [Merge Sort](#merge-sort) |

### Memory Usage (In-Place vs. Extra Memory)

| In-Place Sorting                                                                                                                 | Out-of-Place Sorting                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Modifies the input data structure without significant extra memory.                                                              | Requires extra memory to store data.                                                      |
| [Bubble Sort](#bubble-sort)<br>[Selection Sort](#selection-sort)<br>[Insertion Sort](#insertion-sort)<br>[Quicksort](#quicksort) | [Merge Sort](#merge-sort)<br>[Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort) |

### Stability of Sorting

| Stable Algorithms                                                                                                                                             | Unstable Algorithms                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Maintain the relative order of equal elements.                                                                                                                | May not preserve the relative order of equal elements.       |
| [Bubble Sort](#bubble-sort)<br>[Insertion Sort](#insertion-sort)<br>[Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort)<br>[Merge Sort](#merge-sort) | [Quicksort](#quicksort)<br>[Selection Sort](#selection-sort) |

### Comparison vs. Non-Comparison

| Comparison-Based Sorting                                                                                                                                      | Non-Comparison-Based Sorting                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Compare elements to decide order.                                                                                                                             | Do not directly compare elements but use other properties (like keys). |
| [Bubble Sort](#bubble-sort)<br>[Selection Sort](#selection-sort)<br>[Insertion Sort](#insertion-sort)<br>[Quicksort](#quicksort)<br>[Merge Sort](#merge-sort) | [Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort)           |

### Performance with Sorted/Unsorted Data

| Adaptive Sorting                                 | Non-Adaptive Sorting                                                                                                                                                                     |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Perform better if the input is partially sorted. | Performance is independent of input order.                                                                                                                                               |
| [Insertion Sort](#insertion-sort)                | [Bubble Sort](#bubble-sort)<br>[Selection Sort](#selection-sort)<br>[Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort)<br>[Quicksort](#quicksort)<br>[Merge Sort](#merge-sort) |

### Algorithm Structure

| Recursive Sorting                                    | Iterative Sorting                                                                                                                                                     |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Use recursion for divide-and-conquer strategies.     | Use loops instead of recursion.                                                                                                                                       |
| [Quicksort](#quicksort)<br>[Merge Sort](#merge-sort) | [Bubble Sort](#bubble-sort)<br>[Selection Sort](#selection-sort)<br>[Insertion Sort](#insertion-sort)<br>[Counting Sort](#counting-sort)<br>[Radix Sort](#radix-sort) |


### Computational Complexity

> Look in the **Characteristics** of each algorithm for more detail.

| Time Complexity                                                                                                                       | Space Complexity                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Considers best-case, worst-case, and average-case runtime                                                                             | Considers the amount of auxiliary memory used                                |
| Faster ($O(n*log(n))$): [Merge Sort](#merge-sort)<br>Slower ($O(n^2)$): [Bubble Sort](#bubble-sort), [Selection Sort](#selection-sort) | Less space: [Quicksort](#quicksort)<br>More space: [Merge Sort](#merge-sort) |


## Bubble Sort

---

The word "Bubble" comes from how this algorithm works, it makes the highest values "bubble up".

### How it works

1. Go through the array, one value at a time.
2. For each value, compare the value with the next value.
3. If the value is higher than the next one, swap the values so that the highest value comes last.
4. Go through the array as many times as there are values in the array.

### Code

```python
def bubbleSort(array):
    
  # Loop through each element of array
  for i in range(len(array)):
        
    # Keep track of swapping
    swapped = False
    
    # Loop to compare array elements
    for j in range(0, len(array) - i - 1):

      # Compare two adjacent elements
      # Change > to < to sort in descending order
      if array[j] > array[j + 1]:

        # Swapping occurs if elements
        # Are not in the intended order
        array[j], array[j+1] = array[j+1], array[j]
        swapped = True
          
    # No swapping means the array is already sorted
    # So no need for further comparison
    if not swapped:
	    break

data = [-2, 45, 0, 11, -9]
print("Unsorted:", data)
bubbleSort(data)
print("Sorted:", data)
```

### Characteristics

| Time Complexity  |          |
| ---------------- | -------- |
| Best             | $O(n)$   |
| Worst            | $O(n^2)$ |
| Average          | $O(n^2)$ |
| Space Complexity | $O(1)$   |
| Stability        | Yes      |

The best case for Bubble Sort is $O(n)$ because of the trick with `swapped` flag. If the array is already sorted the algorithm only has to perform $n$ number of comparisons.

While swapping two elements, we need some extra space to store temporary values. Other than that, the sorting can be done in-place. Hence space complexity is $O(1)$ or constant space.

The algorithm is trivially stable.

## Selection Sort

---

Basically, it can be understood as an inverse of a [Bubble Sort](#bubble-sort).

### How it works

1. Go through the array to find the lowest value.
2. Move the lowest value to the front of the unsorted part of the array.
3. Go through the array again as many times as there are values in the array.

### Code

```python
def selectionSort(array, size):
    for step in range(size):
        min_idx = step

        for i in range(step + 1, size):
            # To sort in descending order, change > to < in this line
            # Select the minimum element in each loop
            if array[i] < array[min_idx]:
                min_idx = i
         
        # Put min at the correct position
        (array[step], array[min_idx]) = (array[min_idx], array[step])


data = [-2, 45, 0, 11, -9]
print('Unsorted:', data)
size = len(data)
selectionSort(data, size)
print('Sorted:', data)
```

### Characteristics

| Time Complexity  |          |
| ---------------- | -------- |
| Best             | $O(n^2)$ |
| Worst            | $O(n^2)$ |
| Average          | $O(n^2)$ |
| Space Complexity | $O(1)$   |
| Stability        | Yes      |

The most significant difference from [Bubble Sort](#bubble-sort) that we can notice in this simulation is that best and worst case is actually almost the same for Selection Sort – $O(n^2)$, but for [Bubble Sort](#bubble-sort) the best case runtime is only $O(n)$. Why is that?It is because Selection Sort compares each element with all the elements for if it is the smallest, no matter if the array is sorted or not.

But there is still a slight difference between best and worst case for Selection Sort, and it is mainly the number of swaps. In the best case scenario Selection Sort does not have to swap any of the values because the array is already sorted. And in the worst case scenario, where the array already sorted, but in the wrong order, Selection Sort must do as many swaps as there are values in array. But because the swaps are done with the comparison, it does not significantly increase the average time it takes.

Partially it is also because of the fact that the Selection Sort is an In-Place and Internal algorithm, which minimizes the time it takes to swap elements.

As with [Bubble Sort](#bubble-sort), while swapping two elements, we need some extra space to store temporary values. Other than that, the sorting can be done in-place. Hence space complexity is $O(1)$ or constant space.

And the algorithm is also trivially stable.

## Insertion Sort

---

The Insertion Sort algorithm uses one part of the array to hold the sorted values, and the other part of the array to hold values that are not sorted yet.

### How it works

1. Take the first value from the unsorted part of the array.
2. Move the value into the correct place in the sorted part of the array.
3. Go through the unsorted part of the array again as many times as there are values.

### Code

```python
def insertionSort(array):
	for step in range(1, len(array)): 
        currentElem = array[step]
		# Check from the second element of the array, 
		# assuming the first one is sorted
        j = step - 1
		# Compare currentElem with each element on the left 
		# of it until an element smaller than it is found
		# For descending order, 
		# change key < array[j] to key > array[j]    
        while j >= 0 and currentElem < array[j]: 
            array[j + 1] = array[j]
            j = j - 1
			# Place currentElem at after the element 
			# just smaller than it
        array[j + 1] = currentElem 
        # If the element is alreasdy in place, 
        # the array[j + 1] is the same as array[step]


data = [9, 5, 1, 4, 3]
print("Unsorted:", data)
insertionSort(data)
print("Sorted:", data)
```

To get this more clearly:

```python
# Initial 3 steps of this sorting algorithm

# Step 1
# currentElem = array[1] = 5
data = [9, 5, 1, 4, 3] # j = 0, array[0] = 9 > 5 -> array[1] = 9
data = [9, 9, 1, 4, 3] # j = -1 < 0 ->
data = [5, 9, 1, 4, 3] # j + 1 = 0, array[0] = 5

# Step 2
# currentElem = array[2] = 1
data = [5, 9, 1, 4, 3] # j = 1, array[1] = 9 > 1 -> array[2] = 9
data = [5, 9, 9, 4, 3] # j = 0, array[0] = 5 > 1 -> array[1] = 5
data = [5, 5, 9, 4, 3] # j = -1 < 0 ->
data = [1, 5, 9, 4, 3] # j + 1 = 0, array[0] = 1

# Step 3
# currentElem = array[3] = 4
data = [1, 5, 9, 4, 3] # j = 2, array[2] = 9 > 4 -> array[3] = 9
data = [1, 5, 9, 9, 3] # j = 1, array[1] = 5 > 4 -> array[2] = 5
data = [1, 5, 5, 9, 3] # j = 0, array[0] = 1 < 4 ->

# Notice how the value of j does not go to -1 because the 
# "sorted" place of 4 is not at the very start of the array

data = [1, 4, 5, 9, 3] # j + 1 = 1, array[1] = 4
```

### Characteristics

| Time Complexity  |          |
| ---------------- | -------- |
| Best             | $O(n)$   |
| Worst            | $O(n^2)$ |
| Average          | $O(n^2)$ |
| Space Complexity | $O(1)$   |
| Stability        | Yes      |

## Quicksort

---

The Quicksort algorithm takes an array of values, chooses one of the values as the 'pivot' element, and moves the other values so that lower values are on the left of the pivot element, and higher values are on the right of it.

### How it works

1. Choose a value in the array to be the pivot element.
2. Order the rest of the array so that lower values than the pivot element are on the left, and higher values are on the right.
3. Swap the pivot element with the first element of the higher values so that the pivot element lands in between the lower and higher values.
4. Do the same operations (recursively) for the sub-arrays on the left and right side of the pivot element.

### Code

```python
# function to find the partition position
# in other words, function to find the position of the rightmost
# pivot after sorting all lower elements on the left and
# all greater elements on the right
def partition(array, low, high):

	# choose the rightmost element as pivot
	pivot = array[high]
	# i is a pointer for greater element
	# but actually, i points to the element
	# that is equal or less than the pivot
	# the element greater than the pivot is actually at i + 1
	# i starts with -1 because it is incremented in the loop,
	# and initilaly it must be empty 
	i = low - 1
	
	# traverse through all elements
	# compare each element with pivot
	for j in range(low, high):
		if array[j] <= pivot:
			# if element smaller than pivot is found
			# swap it with the greater element pointed by i
			i = i + 1
			
			# swapping the current element being checked
			# (which is less than or equal to the pivot)
			# with the element that is greater than the pivot
			# (which is at I + 1)
			(array[i], array[j]) = (array[j], array[i])
		
	# swapping the pivot element with the 
	# greater element specified by i + 1
	(array[i + 1], array[high]) = (array[high], array[i + 1])
	
	# return the position from where partition is done
	# in other words, return the position of the pivot
	return i + 1

# function to perform quicksort
def quickSort(array, low, high):
	# implicit check if the passed array has at least 2 elemets
	if low < high:
		# find pivot element such that
		# element smaller than pivot are on the left
		# element greater than pivot are on the right
		pi = partition(array, low, high)
		
		# recursive call on the left of pivot
		# notice that the range is from the leftmost position
		# of the partition up to the left of the pivot position
		quickSort(array, low, pi - 1)
		
		# recursive call on the right of pivot
		# notice that the range is from the right of the
		# pivot position up to the rightmost 
		# position of the partition
		quickSort(array, pi + 1, high)


data = [8, 7, 2, 1, 0, 9, 6]
print("Unsorted:", data)
size = len(data)
quickSort(data, 0, size - 1)
print("Sorted:", data)
```

### Characteristics

| Time Complexity  |               |
| ---------------- | ------------- |
| Best             | $O(n*log(n))$ |
| Worst            | $O(n^2)$      |
| Average          | $O(n*log(n))$ |
| Space Complexity | $O(log(n))$   |
| Stability        | No            |

## Counting Sort

---

The Counting Sort algorithm sorts an array by counting the number of times each value occurs.

- Only works on non-negative **integers**.
- Does not compare values.
- Stable sorting algorithm. Stable sort it is achieved by using LIFO when adding the elements to the counting array – meaning the elements are added to the counting array from first to last, and sorted array is constructed from the last to the first (by position, not by value) element.

### How it works

1. Create a new array for counting how many there are of the different values by getting the maximum value (+ 1 to include 0). Or you can do 0-9 if the elements are all single digit integers.
2. Go through the array that needs to be sorted.
3. For each value, count it by increasing the counting array at the corresponding index.
4. After counting the values, go through the counting array to create the sorted array.
5. For each count in the counting array, create the correct number of elements, with values that correspond to the counting array index.

### Code

```python
def countingSort(array):
	size = len(array)
    output = [0] * size
	
    # Initialize count array
    count = [0] * (max(array) + 1)
	
    # Store the count of each elements in count array
    for i in range(0, size):
        count[array[i]] += 1
		
    # Store the cumulative count
    for i in range(1, (max(array) + 1)):
        count[i] += count[i - 1]
		
    i = size - 1 
    # Processing the input array from 
    # right to left ensures stability
    
    while i >= 0:
        output[count[array[i]] - 1] = array[i]
        # 1. Fetching the last element of the input array
        # 2. Finding its corresponding index in the count array
        # 3. Placing what comes last of duplicate in its place
        count[array[i]] -= 1
        # 4. Decrementing the last available position for the 
        # element with that value
        i -= 1
        # 5. Moving to the next element to sort
		
    # Copy the sorted elements into original array
    for i in range(0, size):
        array[i] = output[i]


data = [4, 2, 2, 8, 3, 3, 1]
print("Unsorted:", data)
countingSort(data)
print("Sorted:", data)
```

To get this more clearly:
- Before sorting starts (after cumulative summing), `count` reflects the last position of each element in the output array. (Actually it stores `position + 1`, because of the decrementing logic.)
- During sorting, `count` is updated to reflect the **next available position** for that element.
- Processing the input array from right to left ensures stability of the sort.
- The final values in the `count` array are essentially useless after the sorting process is complete as they do not represent any useful information, in the example above it is: `count = [0, 0, 1, 3, 5, 6, 6, 6, 6]`

### Characteristics

| Time Complexity  |          |
| ---------------- | -------- |
| Best             | $O(n)$   |
| Worst            | $O(n^2)$ |
| Average          | $O(n+k)$ |
| Space Complexity | $O(k)$   |
| Stability        | Yes      |

Here:
- $n$ is the number of values
- $k$ is the range of possible different values.

In general, time complexity for Counting Sort is $O(n+k)$.

In a best case scenario, $k$ is very small compared to $n$ and Counting Sort has time complexity $O(n)$.

But in a worst case scenario, the range of possible different values k is very big compared to the number of values n and Counting Sort can have time complexity $O(n^2)$ or even worse.

## Radix Sort

---

The Radix Sort algorithm sorts an array by individual digits, starting with the least significant digit (the rightmost one).

- Only works on non-negative **integers**.
- Does not compare values.
- It is important for Radix Sort that the the sorting is done in a stable way. It works with any intermediate **stable** sorting algorithm, in this example it is [Counting Sort](#counting-sort).

### How it works

1. Start with the least significant digit (rightmost digit).
2. Sort the values based on the digit in focus by first putting the values in the correct bucket based on the digit in focus, and then put them back into array in the correct order.
3. Move to the next digit, and sort again, like in the step above, until there are no digits left.

### Code

```python 
# Using counting sort to sort the elements in the basis of significant places
def countingSort(array, place):
    size = len(array)
    output = [0] * size
    count = [0] * 10 # From 0 to 9
    
    # Calculate count of elements
    for i in range(0, size):
        elementSlice = array[i] // place
        # Slice of the element that we need in the scope
        # For example, 
        # if element = 763, place = 1, then elementSlice = 763
        # if element = 763, place = 10, then elementSlice = 76
        # if element = 763, place = 100, then elementSlice = 7
        index = elementSlice % 10
        # Actual index of the element in the count array
        # is the last digit of elementSlice, which is the 
        # remainder of elementSlice % 10 operation
        count[index] += 1 
		
    # Calculate cumulative count
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Place the elements in sorted order
    i = size - 1
    while i >= 0:
        elementSlice = array[i] // place
        index = elementSlice % 10
        output[count[index] - 1] = array[i]
        count[index] -= 1
        i -= 1

    for i in range(0, size):
        array[i] = output[i]


# Main function to implement radix sort
def radixSort(array):
    # Get maximum element
    max_element = max(array)

    # Apply counting sort to sort elements based on place value.
    place = 1
    while max_element // place > 0:
        countingSort(array, place)
        place *= 10


data = [121, 432, 564, 23, 1, 45, 788]
print("Unsorted:", data)
radixSort(data)
print("Sorted:", data)
```

### Characteristics

| Time Complexity  |          |
| ---------------- | -------- |
| Best             | $O(n)$   |
| Worst            | $O(n^2)$ |
| Average          | $O(n*k)$ |
| Space Complexity | $O(n+k)$ |
| Stability        | Yes      |

The time complexity for Radix Sort is:

$$
O(n*k)
$$

Here:
- $n$ is the number of values
- $k$ the number of digits in the highest value.

A best case scenario for Radix Sort is if there are lots of values to sort, but the values have few digits. For example if there are more than a million values to sort, and the highest value is 999, with just three digits. In such a case the time complexity $O(n*k)$ can be simplified to just $O(n)$.

A worst case scenario for Radix Sort would be if there are as many digits in the highest value as there are values to sort. This is perhaps not a common scenario, but the time complexity would be $O(n^2)$ in this case.

The most average or common case is perhaps for example if there are million values to sort, and the values have 6 digits. If so, Radix Sort gets time complexity $O(n*log(n))$.

## Merge Sort

---

The Merge Sort algorithm is a divide-and-conquer algorithm that sorts an array by first breaking it down into smaller arrays, and then building the array back together the correct way so that it is sorted.

- **Divide:** The algorithm starts with breaking up the array into smaller and smaller pieces until one such sub-array only consists of one element.
- **Conquer:** The algorithm merges the small pieces of the array back together by putting the lowest values first, resulting in a sorted array.

### How it works

1. Divide the unsorted array into two sub-arrays (half the size of the original if recursive approach is used).
2. Continue to divide the sub-arrays as long as the current piece of the array has more than one element.
3. Merge two sub-arrays together by always putting the lowest value first.
4. Keep merging until there are no sub-arrays left.

### Code

#### Recursive approach

```python
# Recursive implementation of Merge sort
def mergeSort(arr):
	# If the array has one or no elements there is
	# nothing to sort
    if len(arr) <= 1:
        return arr
        
    mid = len(arr) // 2
    # Middle element is found to divide the array into 2
    
    leftHalf = arr[:mid]
    rightHalf = arr[mid:]
    # Recursive call on both sides (left first)
    sortedLeft = mergeSort(leftHalf)
    sortedRight = mergeSort(rightHalf)
    
	# Calling merging function
    return merge(sortedLeft, sortedRight)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
		# The loop iterates through 2 arrays that are being 
		# compared and appends smaller to greater elements 
		# from both of them to the result array
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
            
    result.extend(left[i:])
    result.extend(right[j:])
    
    return result


data = [3, 7, 6, -10, 15, 23.5, 55, -13]
print("Unsorted:", data)
mergeSort(data)
print("Sorted:", sortedArr)
```

Elaboration:
- On line 6 `arr[:mid]` takes all values from the array up until, but not including, the value on index `mid`.
- On line 7 `arr[mid:]` takes all values from the array, starting at the value on index `mid` and all the next values.
- On lines 26-27 the first part of the merging is done. At this this point either the left sub-array or the right sub-array is empty, so the result array can just be filled with the remaining values from either the left or the right sub-array. These lines can be swapped, and the result will be the same.

#### Iterative approach

```python
def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
            
    result.extend(left[i:])
    result.extend(right[j:])
    
    return result

def mergeSort(arr):
    step = 1  # Starting with sub-arrays of length 1
    length = len(arr)
    
    while step < length:
        for i in range(0, length, 2 * step):
            left = arr[i:(i + step)]
            right = arr[(i + step):(i + 2 * step)]
            
            merged = merge(left, right)
            
            # Place the merged array back 
            # into the original array
            for j, val in enumerate(merged):
                arr[i + j] = val
                
        step *= 2  
        # Double the sub-array length for the next iteration
        
    return arr

data = [3, 7, 6, -10, 15, 23.5, 55, -13]
print("Unsorted:", data)
mergeSort(data)
print("Sorted:", sortedArr)
```

Elaboration:

You might notice that the merge functions are exactly the same in the two Merge Sort implementations above, but in the implementation right above here the while loop inside the mergeSort function is used to replace the recursion. The while loop does the splitting and merging of the array in place, and that makes the code a bit harder to understand.

To put it simply, the while loop inside the mergeSort function uses short step lengths to sort tiny pieces (sub-arrays) of the initial array using the merge function. Then the step length is increased to merge and sort larger pieces of the array until the whole array is sorted.

### Characteristics

| Time Complexity  |               |
| ---------------- | ------------- |
| Best             | $O(n*log(n))$ |
| Worst            | $O(n*log(n))$ |
| Average          | $O(n*log(n))$ |
| Space Complexity | $O(n)$        |
| Stability        | Yes           |

The time complexity of the Merge Sort is the same across the board because the algorithm divides and merges no matter if the input array is sorted or not.

While merging two arrays, we require an auxiliary space to temporarily store the merged array, before we plug this partially sorted array into the main array. Hence space complexity of Merge Sort is $O(n)$, as we require an auxiliary array as big as the main input array.

Merge sort is stable because if there is duplicates, the ones that come earlier in the array stay on the left and ones that come later in the array stay on the right. Their relative positions are preserved in the merging stage.

## Linear Search

---

The Linear Search algorithm searches through an array and returns the index of the value it searches for.

### How it works

1. Go through the array value by value from the start.
2. Compare each value to check if it is equal to the value we are looking for.
3. If the value is found, return the index of that value.
4. If the end of the array is reached and the value is not found, return `-1` to indicate that the value was not found.

### Code

```python
def linearSearch(arr, targetVal):
    for i in range(len(arr)):
        if arr[i] == targetVal:
            return i
    return -1

arr = [3, 7, 2, 9, 5]
targetVal = 9

result = linearSearch(arr, targetVal)

if result != -1:
    print("Value", targetVal, "found at index", result)
else:
    print("Value", targetVal, "not found")
```

### Characteristics

| Time Complexity  | $O(n)$ |
| ---------------- | ------ |
| Space Complexity | $O(1)$ |

## Binary Search

---

Binary Search is much faster than Linear Search, but requires a **sorted** array to work.

### How it works

1. Check the value in the center of the array.
2. If the target value is lower, search the left half of the array. If the target value is higher, search the right half.
3. Continue step 1 and 2 for the new reduced part of the array until the target value is found or until the search area is empty.
4. If the value is found, return the target value index. If the target value is not found, return -1.

### Code

```python
def binarySearch(arr, targetVal):
    left = 0
    right = len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == targetVal:
            return mid
        
        if arr[mid] < targetVal:
            left = mid + 1
        else:
            right = mid - 1
            
    return -1


myArray = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
myTarget = 15

result = binarySearch(myArray, myTarget)

if result != -1:
    print("Value", myTarget, "found at index", result)
else:
    print("Target not found in array.")
```

### Characteristics

| Time Complexity  | $O(log_2(n))$ |
| ---------------- | ------------- |
| Space Complexity | $O(1)$        |

When writing time complexity using Big-O notation we could also just have written $O(log(n))$, but $O(log_2(n))$ reminds us that the array search area is halved for every new comparison, which is the basic concept of Binary Search, so we will just keep the base 2 indication in this case.

