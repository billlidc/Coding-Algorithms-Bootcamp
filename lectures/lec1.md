<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>


# Lecture 1 - Java Strings and Arrays


## Strings versus Character Arrays

- Strings are represented as an array of characters.

- Strings have a means of determining length:
  - Explicit length field or sentinel character.

- Arrays in Java also have an explicit length attribute.

- The difference between strings and character arrays is mainly **conceptual**:
  - Strings are treated as **single** objects.
  - Arrays are treated as **collections** of objects.

- Strings also have string-specific operations such as:
  - Comparison
  - Insert/delete substrings, substring extraction


## String Representations
- Pointer to an array terminated by a sentinel such as NUL (the "C" model):
  - Drawbacks: Cannot use sentinel value as data, `strlen()` is O(n).
- Pointer to a length field, followed by an array of characters (the "Pascal" model):
  - Explicit length makes `strlen()` O(1), but may take more space or limit string length.
- Pointer to an array of characters, preceded by a length field:
  - May be more efficient to access; negative index can be used to access the length field.
- Pointer to a structure containing a length field and a pointer to the array of characters:
  - Takes more space than any of the above; accessing string value is slower due to extra indirection.
  - Extra indirection allows data sharing.


## String Conversions in Java
- **String to character array**:
  - `String.toCharArray()`
- **Extract character from String**:
  - `String.charAt(int N)` where `0 <= N < string length`
- **Character array to String**:
  - `String.valueOf(char a[])` (static function)
- **Character to String**:
  - `Character.toString(char c)` (static function)
  - `String.valueOf(char c)` (static function)


## Basic String Operations
- **Check the length**:
  - `Integer len = s.length();`
- **Concatenate two strings**:
  - `String result = s1 + s2;`
  - `String result = s1 + "text";`


## Building a String

- **Char by char**:
    ```java
    String s = new String("");
    for (...) {
        s += ' ';  // O(n²) since each addition involves copying the partial result.
    }
    ```

- **StringBuilder**:
    ```java
    StringBuilder sb = new StringBuilder();
    for (...) {
        sb.append(' ');  // O(n) since `StringBuilder` updates a buffer in place.
    }
    ```


## Duplicate Check
- **IsUnique** – Determines if a string contains any duplicate characters.
  - Recursively check the rest of the string: O(n²)
  - Sort and check adjacent characters: O(n log n)
  - Use a HashMap of counts: O(n)
  - Use an int[] or bool[]: O(n)


---

[Back to Home](../index.html)
[Next Lecture](./lecture2.html)