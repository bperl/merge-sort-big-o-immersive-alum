# Big O of Merge Sort

## Objectives
* Understand how to calculate the big O of merge sort
* Review merge sort

## Review
So the merge sort function is written like this:

```javascript

function mergeSort(array){
  let midpoint = array.length/2
  let firstHalf = array.slice(0, midpoint)
  let secondHalf = array.slice(midpoint, array.length)

  if(array.length < 2){
    return array
  } else {

    merge(mergeSort(firstHalf), mergeSort(secondHalf))
  }
}
```
And we can think of it as doing the following:

```javascript
let array =  [1, 2, 6, 7, 8, 3, 4, 5]
mergeSort(array)

// 1. Splitting up
// [2, 1, 7, 6]      [8, 3, 4, 5]
// [2, 1] [7, 6]   [8, 3] [4, 5]
// [2] [1] [7] [6] [8] [3] [4] [5]

// 2. Merge
// merge([2], [1]) merge([7],[6])  merge([8], [3])  merge([4], [5])
// merge([1, 2], [6, 7]) merge([3, 8], [4, 5])
// merge([1, 2, 6, 7], [3, 4, 5, 8])
```

### Calculating Big O

**The cost of merging**

So how costly is something like this.  Well let's calculate the merging section first.  Notice that for an array of length 8, our merge section has three levels.  So notice that it's three levels because we split our array in half until the length is one.  So how many times do you have to split an array in half until the length is one?  log(n).  

> We said that the definition of log(n) is the number of times you have to press divide by 2 on a calculator until you get to one.  

Ok so the height of this merge section is log(n).  Now what is the cost at our first level.  

```javascript
// merge([2], [1]) merge([7],[6])  merge([8], [3])  merge([4], [5])
```

Well remember we said that the cost of merge is `firstHalf.length + secondHalf.length`.  So at the first level that merge operation occurs four times for a cost of two each.  At the second level merge occurs twice for a cost of four each, and at the final level merge happens once for a cost of eight.  In other words, the cost at each level is n.  

```javascript

// merge([2], [1]) merge([7],[6])  merge([8], [3])  merge([4], [5])
  2 + 2 + 2 + 2 = 8
// merge([1, 2], [6, 7]) merge([3, 8], [4, 5])
  4 + 4 = 8
// merge([1, 2, 6, 7], [3, 4, 5, 8])
  8
```

So each level costs n, and we said there are log n levels.  So the cost of merging is n*log n.  

**The cost of splitting**

Now we still didn't cover the cost of splitting.  Let's look at the splitting stage again.

```javascript
let array =  [1, 2, 6, 7, 8, 3, 4, 5, 9, 10]
mergeSort(array)

// 1. Splitting up
// [2, 1, 7, 6]      [8, 3, 4, 5]
// [2, 1] [7, 6]   [8, 3] [4, 5]
// [2] [1] [7] [6] [8] [3] [4] [5]

```

So splitting occurs three times, and splitting an array in half does not cost n.  It costs the same regardless of the size of the array.  How many times does the splitting operation occur?  log n times.  This is because we continue to split the array in half until the array's length is one. So the cost of splitting is log n.  

So we can say that the big o of merge sort is the total cost of splitting plus the total cost of merging or log n + n log n.  Now in big o we only consider the largest exponent, and because n * log n is larger than log n the big o is n log n.

### So what?

Compare the big o of merge sort with that of selection sort.  Remember that selection sort cost us n^2.  Well in this example of sorting an array of eight elements n log n = 24 while n^2 = 64.  Once we arrive at a size where n = 1000 then n^2 = 1,000,000 while n log n = 9,965.  So when is one thousand selection sort takes over a hundred times longer than merge sort.  That's significant.

Going forward, you can assume that the cost of sorting an array is n log n.  And now you know the steps involved in sorting an array.

### Summary

We calculate the big O of mergeSort by remembering that the big O of merging is equal to the length of our two subarrays combined.  And that number of times we need to incur the merge operation is equal to the number of times we need to split the length of our array in two to get down to one.  So the big o of merge sort is n log n.  
