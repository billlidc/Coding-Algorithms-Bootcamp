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


# Lecture 2 - Computational Complexity / Parsing and String Manipulation

- Additional resources can be found [here](https://billlidc.github.io/Data-Structures/lectures/lecture1.html).


---

## Computational Complexity
- Describes the "difficulty" of a problem
- States resource usage as a function of the given problem's "size"
    - Usually time or memory


### Big-O Notation

- Describes the asymptotic behavior of a function
- can be arbitrarily "loose"
    - If $f(x)$ is $O(n^2)$, it is also $O(n^3)$, $O(n^4)$, $O(2^n)$, etc.

- Definition
$$
f(n) = O(g(n)) \text{ if there exist constants } c > 0 \text{ and } n_0 > 0 \text{ such that } 0 \leq f(n) \leq c \cdot g(n) \text{ for all } n \geq n_0
$$


<div style="border: 1px solid black; padding: 10px; margin: 10px;">
  <p>

  - $O(1)$: **Constant** time
    - The algorithm does NOT depend on the input size.
  - $O(\log n)$: **Logarithmic** time
    - The algorithm gets slightly slower as $n$ grows.
  - $O(n)$: **Linear** time
    - The runtime grows as much as $n$ grows (When $n$ doubles, runtime doubles).
  - $O(n \cdot \log n)$: **Linearithmic** time
    - Usually the result of performing $O(\log n)$ operation $n$ times or performing $O(n)$ operation $log n$ times.
  - $O(n^c)$: **Polynomial** time
    - $O(n^2)$: **Quadratic** time
    - $O(n^3)$ **Cubic** time
  - $O(2^n)$: **Exponential** time
  - $O(n!)$: **Factorial** time

  </p>
</div>


### When is `O(n²)` Better than `O(n)`?

- `4n² < 1000n` whenever `n < 250`.
    - **When `n` is known to be small** and the `O(n²)` algorithm has a lower constant factor than the `O(n)` algorithm.
    - In such cases, even though `O(n²)` grows faster with larger `n`, the actual performance for small `n` can be better than the `O(n)` algorithm due to a smaller constant factor.


### Big-O Examples

- Checking whether an item is present in a linked list: `O(n)`
    - Scan through the entire list until the item is found (on average `n/2` checks)

- Checking whether an item is present in an unordered binary tree: `O(n)`

- Checking whether an item is present in a binary search tree: `O(H)`
    - If the tree is degenerate (like a linked list), `H = n`
    - If the tree is balanced, `H = log n`


### Big-O Sanity-Checking

- Determine **the least conceivable** work or space needed to accomplish the task
    - Can **NOT** be `O(log n)` or faster than `O(n)` to examine every single item of input
    - Can **NOT** be faster than `O(n²)` for quadratic working memory


---


## Amortized Time

- Additional resources can be found [here](https://billlidc.github.io/Data-Structures/lectures/lecture4.html).


---



## Parsing and String Manipulation


### Java String Functions: Access

| **Code** | **Explanation** |
| --- | --- |
| `char charAt(int index)` | Return the character at the given position. |
| `int codePointAt(int index)` | Return the Unicode code point at the specified position. |
| `int length()` | Return the length of the string. |
| `int codePointCount(int b, int e)` | Return the number of Unicode code points in the range from index `b` to `e`. |


### Java String Functions: Testing

| **Code** | **Explanation** |
| --- | --- |
| `s.contains(CharSequence cs)` | Return `True` if `cs` is a subsequence of `s`. |
| `s.startsWith(String pre)` | Return `True` if `s` starts with the prefix `pre`. |
| `s.endsWith(String suf)` | Return `True` if `s` ends with the suffix `suf`. |
| `int s1.indexOf(int ch)` | Return the index of the first occurrence of `ch`. |
| `int s1.indexOf(String s2)` | Return the index of the first occurrence of the string `s2`. |
| `int s1.lastIndexOf(ch/s2)` | Return the index of the last occurrence of `ch` or `s2`. |


### Java String Functions: Modification

| **Code** | **Explanation** |
| --- | --- |
| `s.replace(c1, c2)` | Replace all occurrences of `c1` with `c2`. |
| `s.toLowerCase()` | Convert all characters in `s` to lowercase. |
| `s.toUpperCase()` | Convert all characters in `s` to uppercase. |


### Java String Functions: Assembly/Disassembly

| **Code** | **Explanation** |
| --- | --- |
| `s1.concat(s2)`<br>`s1 += s2` | Append `s2` to the end of `s1`. |
| `String.valueOf(char[] arr)` | Return a new string containing the characters in `arr`. |
| `s.substring(int b, int e)` | Return a new string containing the substring from index `b` to `e`. |
| `s.trim()` | Return `s` without leading and trailing whitespace. |
| `String[] s.split(String regex)` | Split `s` around occurrences of the regex pattern. |


### Java String Functions: Comparison

| **Code** | **Explanation** |
| --- | --- |
| `string1 == string2` | Returns `True` if `string1` and `string2` reference the same instance. |
| `string1.equals(string2)` | Returns `True` if `string1` and `string2` have the same content. |
| `string1.compareTo(string2)` | Returns `0` if equal, `-1` if `string1` is lexically before `string2`, `+1` if after. |
| `string1.compareToIgnoreCase(string2)` | Returns `0` if `string1` and `string2` have the same content, ignoring case. |
| `s.matches(String regex)` | Returns `True` if `s` matches the regular expression `regex`. |


---


## Regular Expressions


### Building Blocks of Regular Expressions

1. **Character Literal**: Matches a specific character
   - `"a"`: Matches the letter `a`

2. **Character Wildcard (`.`)**: Matches any single character
   - `"."`: Matches any character

3. **Character Set (`[...]`)**: Matches any one of the characters within the brackets
   - `"[aeiou]"`: Matches any vowel
   - (`[^...]`): Matches anything not in the set
   - `[^0-9]`: Matches any character that is not a digit

4. **Repetition**:
   - `X?`: Matches `0` or `1` occurrence of `X` (X is optional)
   - `X*`: Matches `0` or more occurrences of `X`
   - `X+`: Matches `1` or more occurrences of `X`

5. **Concatenation**: Combines multiple expressions
   - `XY`: Matches X followed by Y

6. **Alternation (`|`)**: Matches either the expression before or after `|`
   - `X|Y`: Matches `X` or `Y`


### Anchors

- **`^` (Caret)**: Matches the start of the string
    - `^abc`: Matches `abc` only at the start

- **`$` (Dollar)**: Matches the end of the string
    - `abc$`: Matches `abc` only at the end


### Extended Regular Expressions

1. **Finer Control Over Repetition**:
   - `X{m,n}`: Matches at least `m` and at most `n` occurrences of `X`
   - `X{m,}`: Matches at least `m` consecutive occurrences of `X`
   - `X{,n}`: Matches at most `n` consecutive occurrences of `X`

2. **Grouping and Capture**:
   - `(X...)`: Groups expressions to be treated as a single unit
   - `...(X)...`: Captures matched text for later reference


### Special Use of Backslash (`\`)

1. **Escape Special Characters**: Makes a special character literal
   - `\[ `: Matches `[`

2. **Referencing Matches**:
   - `\1`, `\2`, etc., refer to previously captured groups
  
3. **Shortcut Expressions**:
   - `\s`: Matches any whitespace
   - `\d`: Matches any digit (`[0-9]`)
   - `\D`: Matches any non-digit
   - `\w`: Matches any word character (`[a-zA-Z0-9_]`)

4. **Literal Backslash**: 
   - Use `\\` to match a single backslash


### Regular Expression Examples

| **Expression** | **Matches**                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------|
| `abc`          | `abc` only                                                                                        |
| `ab*c`         | `ac`, `abc`, `abbc`, `abbbc`, `abbbbc`, etc.                                                      |
| `.\.`          | Any character followed by a period                                                                |
| `(a\|bc)d`      | `acd` and `bcd`                                                                                   |
| `(a\|(bc))d`    | `ad` and `bcd`                                                                                    |
| `x[aeiou]?z`   | `xz`, `xaz`, `xez`, `xiz`, `xoz`, and `xuz`                                                       |
| `b{3,4}`       | `bbb` and `bbbb`                                                                                  |
| `^a`           | `a` only — multiple leading carets all anchor to start                                            |
| `^\^a`         | `^a`                                                                                              |
| `[A-Z]`        | `A`, `B`, ..., `Z`                                                                                |
| `[^0-9]`       | Any character except a digit                                                                      |
| `\d{3}-\d{2}-\d{4}` | `123-45-6789`                                                                               |
| `\bword\b`     | `word`                                                                                           |
| `X+`           | `X`, `XX`, `XXX`, etc.                                                                            |
| `^abc$`        | `abc`                                                                                             |
| `foo\|bar`      | `foo` or `bar`                                                                                    |
| `a(bc)*d`      | `ad`, `abcd`, `abcbcd`, etc.                                                                      |
| `\w+@\w+\.\w+` | `example@domain.com`                                                                              |
| `\s`           | A single whitespace character                                                                     |
| `(\d{3})`      | Captures three digits (e.g., `123`)                                                               |


## Regex Functions in Java

- `String.split`
  - `String.split` is a convenience function that internally uses `Pattern.compile(re).split(str)`.
    ```java
    String[] parts = "a,b,c".split(",");
    ```

- Efficient Re-use of Regex
  - More efficient to compile once and reuse the `Pattern` object.
    ```java
    Pattern p = Pattern.compile(regex);
    ```

- Processing Multiple Matches
  - Create a `Matcher` object to find multiple matches within a string.
    ```java
    Pattern p = Pattern.compile(regex);
    Matcher m = p.matcher(string);
    ```

    - `m.matches()`:
      - Equivalent to `string.matches(regex)`, checks if the **entire** string matches the pattern.
    - `m.find()`:
      - Looks for the next match in the string, returns `true` if found.
    - `m.group()`:
      - Returns the string that was matched by the most recent `find()`.


- Usage Example
    ```java
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;

    public class RegexTest {
        public static void main(String[] args) {
            // Define the regex pattern
            String regex = "\\bword\\b"; // "\\b" represents word boundary
            
            // Compile the pattern
            Pattern pattern = Pattern.compile(regex);
            
            // Input string to match against
            String input = "This is a word in a sentence. Another word appears here.";

            // Create a Matcher object
            Matcher matcher = pattern.matcher(input);
            
            // Check if the entire string matches the pattern
            if (matcher.matches()) {
                System.out.println("The entire string matches the pattern.");
            } else {
                System.out.println("The entire string does not match the pattern.");
            }

            // Find and print all occurrences of the pattern
            while (matcher.find()) {
                System.out.println("Found a match: " + matcher.group() + " at position " + matcher.start());
            }
        }
    }

    /*
    Outputs:
    Found a match: word at position 10
    Found a match: word at position 38
    */
    ```


---

[Back to Home](../index.html)
[Next Lecture](./lecture3.html)