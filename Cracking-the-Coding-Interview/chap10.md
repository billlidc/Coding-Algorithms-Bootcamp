# Chapter 10 - Sorting and Searching


## Table of Contents

Note: * means not yet completed.

- [10.1 Sorted Merge](#101)
- [10.2 Group Anagrams](#102)
- [10.3 Search in Rotated Array](#103)
- [10.4 Sorted Search, No Size](#104)
- [10.5 Sparse Search](#105)
- [10.6 Sort Big File](#106)
- [10.7 Missing Int*](#107)
- [10.8 Find Duplicates*](#108)
- [10.9 Sorted Matrix Search](#109)
- [10.10 Rank from Stream*](#1010)
- [10.11 Peaks and Valleys](#1011)


## 10.1

**Sorted Merge**: You are given two sorted arrays A and B, where A has a large enough buffer at the
end to hold B. Write a method to merge B into A in sorted order.

```
Input: [1, 3, 5, 0, 0, 0], [2, 4, 6]
Output: [1, 2, 3, 4, 5, 6]
```


```java
void merge(int[] a, int[] b, int lastA, int lastB) {
    int indexA = lastA - 1;  // Index of the last element in array A
    int indexB = lastB - 1;  // Index of the last element in array B
    int indexMerged = lastB + lastA - 1;  // Index of the last position in merged array

    // Merge a and b, starting from the last element in each array
    while (indexB >= 0) { 
        if (indexA >= 0 && a[indexA] > b[indexB]) {
            a[indexMerged] = a[indexA];  // Put larger element from A
            indexA--;
        } else {
            a[indexMerged] = b[indexB];  // Put larger element from B
            indexB--;
        }
        indexMerged--;  // Move indices
    }
}
```


```py
def merge(a, b, end1, end2):
    idxA = end1 - 1
    idxB = end2 - 1
    idxMerged = end1 + end2 - 1

    while idxB >= 0:
        if idxA >= 0 and a[idxA] > b[idxB]:
            a[idxMerged] = a[idxA]
            idxA -= 1
        else:
            a[idxMerged] = b[idxB]
            idxB -= 1
        idxMerged -= 1
```









## 10.2-Java

**Group Anagrams**: Write a method to sort an array of strings so that all the anagrams are next to each other.

An anagram is a word or phrase formed by rearranging the letters of another word or phrase, using all the original letters exactly once. For examples, "listen" and "silent", "triangle" and "integral".

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"]

Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

```java
import java.util.*;

public class GroupAnagrams {
    public static List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> anagramGroups = new HashMap<>();
        
        for (String s : strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String sorted = new String(chars); // The key
            anagramGroups.putIfAbsent(sorted, new ArrayList<>());
            anagramGroups.get(sorted).add(s);
        }
        
        // Return the values of the hashmap as a list of lists
        return new ArrayList<>(anagramGroups.values());
    }
}
```







## 10.3

**Search in Rotated Array**: Given a sorted array of n integers that has been rotated an unknown number of times, write code to find an element in the array. You may assume that the array was originally sorted in increasing order.

```
Input: [15, 16, 19, 20, 25, 1, 3, 4, 5, 7, 10, 14], 5
Output: 8 (the index of 5)
```

```
[5, 6, 7, 1, 2, 3, 4], 2
 0  1  2  3  4  5  6

l = 0, r = 6
mid = 3, 5 > 1, 2 > 1, 2 < 4, l = 4, r = 6
mid = 5 
```

```java
public class RotatedArraySearch {
    public static int search(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            // Check if the mid element is the target
            if (arr[mid] == target) {
                return mid;
            }

            if (arr[left] <= arr[mid]) { // left sorted
                if (target >= arr[left] && target < arr[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            else { // right sorted
                if (target > arr[mid] && target <= arr[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
}
```







## 10.4

**Sorted Search, No Size**: You are given an array-like data structure Listy which lacks a size method. It does, however, have an `elementAt(i)` method that returns the element at index i in 0(1) time, if i is beyond the bounds of the data structure, it returns -1. (For this reason, the data structure only supports positive integers.) Given a Listy which contains sorted, positive integers, find the index at which an element X occurs. If x occurs multiple times, you may return any index.

```java
public class ListySearch {
    
    public static int search(Listy listy, int x) {

        // Step 1: Find an upper bound
        int index = 1;
        while (listy.elementAt(index) != -1 && listy.elementAt(index) < x) {
            index *= 2; // Exponentially increase the index
        }

        // Step 2: Apply binary search
        return binarySearch(listy, x, 0, index);
    }

    private static int binarySearch(Listy listy, int x, int left, int right) {
        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (listy.elementAt(mid) == -1 || listy.elementAt(mid) > x) {
                right = mid - 1;
            
            } else if (listy.elementAt(mid) < x) {
                left = mid + 1;
            
            } else {
                return mid; // Found x
            }
        }
        return -1; // x not found
    }
}
```











## 10.5

**Sparse Search**: Given a sorted array of strings that is interspersed with empty strings, write a method to find the location of a given string.

```
Input: "ball", ["at", "", "", "", "ball", "", "", "car", "", "", "dad", ""]
Output: 4
```

Approach: Implement a simple modification of binary search: fix the comparison against mid, in case mid is an empty string by simply moving mid to the closest non-empty string.


```java
// O(log n)
public class SparseSearch {

    public static int search(String[] strings, String str) {

        if (strings == null || str == null || str.isEmpty()) {
            return -1;
        }

        return binarySearch(strings, str, 0, strings.length - 1);
    }

    private static int binarySearch(String[] strings, String str, int left, int right) {

        if (left > right) {
            return -1;  // String not found
        }

        int mid = left + (right - left) / 2;

        /*
            Modification: If mid is an empty string, find the closest non-empty string as the mid
        */
        if (strings[mid].isEmpty()) {
            int lp = mid - 1;
            int rp = mid + 1;

            // Move left or right
            while (true) {
                if (lp < left && rp > right) {
                    return -1; // No non-empty strings found
                } else if (rp <= right && !strings[rp].isEmpty()) {
                    mid = rp; // Closest non-empty string to the right
                    break;
                } else if (lp >= left && !strings[lp].isEmpty()) {
                    mid = lp; // Closest non-empty string to the left
                    break;
                }
                rp++;
                lp--;
            }
        }

        if (strings[mid].equals(str)) {
            return mid;

        } else if (strings[mid].compareTo(str) < 0) {
            return binarySearch(strings, str, mid + 1, right);  // Search the right half
        
        } else {
            return binarySearch(strings, str, left, mid - 1);  // Search the right half
        }
    }
}
```

```java
// O(n)
public class SparseSearchHashMap {

    // Function to preprocess the array and store non-empty strings in a HashMap
    public static HashMap<String, Integer> preprocess(String[] strings) {
        HashMap<String, Integer> map = new HashMap<>();
        for (int i = 0; i < strings.length; i++) {
            if (!strings[i].isEmpty()) {  // Ignore empty strings
                map.put(strings[i], i);
            }
        }
        return map;
    }

    // Main search function using HashMap for O(1) lookup
    public static int search(HashMap<String, Integer> map, String target) {
        return map.getOrDefault(target, -1); // Return -1 if target not found
    }
}
```







## 10.6-Java

**Sort Big File**: Imagine you have a 20 GB file with one string per line. Explain how you would sort the file.

External Sorting

1. **Divide the file into smaller chunks** that fit into memory. When 100 MB of memory is available, the file can be processed by dividing it into 100 MB chunks. Each chunk is loaded into memory, sorted individually, and then written back to disk.
   
2. **Merge the sorted chunks**. After all chunks are sorted, a merge process similar to the merge step of merge sort is used to combine the sorted chunks into the final, fully sorted file. This can be done efficiently by keeping only parts of each chunk in memory at a time.










## 10.7


**Missing Int**: Given an input file with four billion non-negative integers, provide an algorithm to generate an integer that is not contained in the file. Assume you have 1 GB of memory available.

FOLLOW UP: What if you have only 10 MB of memory? Assume that all the values are distinct and we now have no more than one billion non-negative integers.








## 10.8

**Find Duplicates**: You have an array with all the numbers from 1 to N, where N is at most 32,000. The array may have duplicate entries and you do not know what N is. With only 4 kilobytes of memory available, how would you print all duplicate elements in the array?






## 10.9

**Sorted Matrix Search**: Given an MxN matrix in which each row and each column is sorted in ascending order, write a method to find an element.

|  15  |  20  |  40  |  85  |
|------|------|------|------|
|  20  |  35  |  80  |  95  |
|  30  |  55  |  95  | 105  |
|  40  |  80  | 100  | 120  |


```java
boolean findElement(int[][] matrix, int elem) {
    int row = 0;
    int col = matrix[0].length - 1;

    while (row < matrix.length && col >= 0) {
        if (matrix[row][col] == elem) {
            return true;
        } else if (matrix[row][col] > elem) {
            col--;  // Move left
        } else {
            row++;  // Move down
        }
    }

    return false;  // Element not found
}
```


## 10.10

**Rank from Stream**: Imagine you are reading in a stream of integers. Periodically, you wish to be able to look up the rank of a number x (the number of values less than or equal to x).

Implement the data structures and algorithms to support these operations. That is, implement the method `track(int x)`, which is called when each number is generated, and the method `getRankOfNumber(int x)`, which returns the number of values tess than or equal to x (not including x itself).

```
Stream: 5, 1, 4, 4, 5, 9, 7, 13, 3

getRankOfNumber(1) = 0
getRankOfNumber(3) = 1
getRankOfNumber(4) = 3
```



## 10.11

**Peaks and Valleys**: In an array of integers, a "peak" is an element which is greater than or equal to the adjacent integers and a "valley" is an element which is less than or equal to the adjacent integers. For example, in the array [5, 8, 6, 2, 3, 4, 6], {8, 6} are peaks and {5, 2} are valleys. Given an array of integers, sort the array into an alternating sequence of peaks and valleys.

```
Input: [5, 3, 1, 2, 3]
Output: [5, 1, 3, 2, 3]
```

```
[0, 1, 2, 3, 4]
[1, 0, 3, 2, 4]
```

Approach:

1. Sort the array in ascending order.
2. Iterate through the elements, starting from index 1 (not 0) and jumping two elements at a time.
3. At each element, swap it with the previous element. Since every three elements appear in the order `small <= medium <= large`, swapping these elements will always put medium as a peak: `medium <= small <= large`.

```java
// O(n log n)
import java.util.Arrays;

public class Valley {

    public static void sortValleyPeak(int[] array) {
        Arrays.sort(array);

        for (int i = 1; i < array.length; i += 2) {
            swap(array, i - 1, i);
        }
    }

    // Helper method to swap elements in the array
    private static void swap(int[] array, int left, int right) {
        int temp = array[left];
        array[left] = array[right];
        array[right] = temp;
    }
}
```

```java
// O(n)
public class Valley {

    public static void sortValleyPeak(int[] array) {
        for (int i = 1; i < array.length; i += 2) {
            int biggestIndex = maxIndex(array, i - 1, i, i + 1);
            if (i != biggestIndex) {
                swap(array, i, biggestIndex);
            }
        }
    }

    // Helper method to find the maximum index among three elements
    private static int maxIndex(int[] array, int a, int b, int c) {
        int len = array.length;
        int aValue = (a >= 0 && a < len) ? array[a] : Integer.MIN_VALUE;
        int bValue = (b >= 0 && b < len) ? array[b] : Integer.MIN_VALUE;
        int cValue = (c >= 0 && c < len) ? array[c] : Integer.MIN_VALUE;

        int max = Math.max(aValue, Math.max(bValue, cValue));

        if (aValue == max) return a;
        else if (bValue == max) return b;
        else return c;
    }

    // Helper method to swap elements in the array
    private static void swap(int[] array, int left, int right) {
        int temp = array[left];
        array[left] = array[right];
        array[right] = temp;
    }
}
```
