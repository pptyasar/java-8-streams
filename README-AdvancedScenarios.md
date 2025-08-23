# Java 8 Streams – Advanced Operations and Custom Scenarios (121–153)

Each method includes a code sample and a sample input/output block.

---

## 124. Concatenate all strings

```java
public static String concatenateStrings(List<String> strings) {
    return strings.stream()
            .collect(Collectors.joining(" "));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("Java", "8", "Streams");
System.out.println(AdvancedScenarios.concatenateStrings(words));

// Sample Output:
Java 8 Streams
```

---

## 125. Check if all numbers are even

```java
public static boolean allNumbersEven(List<Integer> numbers) {
    return numbers.stream()
            .allMatch(n -> n % 2 == 0);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 4, 6, 8);
System.out.println(AdvancedScenarios.allNumbersEven(nums));

// Sample Output:
true
```

---

## 126. Find numbers greater than 50

```java
public static List<Integer> numbersGreaterThan50(List<Integer> numbers) {
    return numbers.stream()
            .filter(n -> n > 50)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(25, 60, 75, 20, 100);
System.out.println(AdvancedScenarios.numbersGreaterThan50(nums));

// Sample Output:
[60, 75, 100]
```

---

## 127. Second smallest number

```java
public static OptionalInt secondSmallestNumber(List<Integer> numbers) {
    return numbers.stream()
            .mapToInt(Integer::intValue)
            .distinct()
            .sorted()
            .skip(1)
            .findFirst();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(7, 3, 9, 3, 4);
System.out.println(AdvancedScenarios.secondSmallestNumber(nums).getAsInt());

// Sample Output:
4
```

---

## 128. Even numbers and square them

```java
public static List<Integer> evenNumbersSquared(List<Integer> numbers) {
    return numbers.stream()
            .filter(n -> n % 2 == 0)
            .map(n -> n * n)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
System.out.println(AdvancedScenarios.evenNumbersSquared(nums));

// Sample Output:
[4, 16]
```

---

## 129. Find longest palindrome

```java
public static Optional<String> longestPalindrome(List<String> words) {
    return words.stream()
            .filter(word -> {
                String lower = word.toLowerCase();
                return lower.equals(new StringBuilder(lower).reverse().toString());
            })
            .max(Comparator.comparing(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("racecar", "madam", "level", "noon", "apple");
System.out.println(AdvancedScenarios.longestPalindrome(words).get());

// Sample Output:
racecar
```

---

## 130. Count vowels in string

```java
public static long countVowels(String input) {
    return input.toLowerCase().chars()
            .filter(c -> "aeiou".indexOf(c) != -1)
            .count();
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "Java Streams";
System.out.println(AdvancedScenarios.countVowels(s));

// Sample Output:
4
```

---

## 131. Find all anagrams

```java
public static Map<String, List<String>> findAllAnagrams(List<String> words) {
    return words.stream()
            .collect(Collectors.groupingBy(word -> {
                char[] chars = word.toLowerCase().toCharArray();
                Arrays.sort(chars);
                return new String(chars);
            }))
            .entrySet().stream()
            .filter(entry -> entry.getValue().size() > 1)
            .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("listen", "silent", "enlist", "rat", "tar", "art");
System.out.println(AdvancedScenarios.findAllAnagrams(words));

// Sample Output:
{eilnst=[listen, silent, enlist], art=[rat, tar, art]}
```

---

## 132. Kth largest element

```java
public static OptionalInt kthLargestElement(List<Integer> numbers, int k) {
    return numbers.stream()
            .mapToInt(Integer::intValue)
            .distinct()
            .boxed()
            .sorted(Collections.reverseOrder())
            .skip(k - 1)
            .mapToInt(Integer::intValue)
            .findFirst();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(3, 1, 4, 4, 2, 5);
System.out.println(AdvancedScenarios.kthLargestElement(nums, 3).getAsInt());

// Sample Output:
3
```

---

## 133. Check if list is sorted

```java
public static boolean isListSorted(List<Integer> numbers) {
    return IntStream.range(1, numbers.size())
            .allMatch(i -> numbers.get(i - 1) <= numbers.get(i));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 4, 5);
System.out.println(AdvancedScenarios.isListSorted(nums));

// Sample Output:
true
```

---

## 134. Intersection of multiple lists

```java
public static List<Integer> intersectionOfLists(List<List<Integer>> lists) {
    if (lists.isEmpty()) return new ArrayList<>();
    return lists.get(0).stream()
            .filter(element -> lists.stream().allMatch(list -> list.contains(element)))
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<List<Integer>> lol = Arrays.asList(
    Arrays.asList(1,2,3,4),
    Arrays.asList(2,3,4,5),
    Arrays.asList(0,2,3,4)
);
System.out.println(AdvancedScenarios.intersectionOfLists(lol));

// Sample Output:
[2, 3, 4]
```

---

## 135. Words starting with specific letter

```java
public static List<String> wordsStartingWithLetter(List<String> words, String letter) {
    return words.stream()
            .filter(word -> word.toLowerCase().startsWith(letter.toLowerCase()))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana", "apricot", "blueberry");
System.out.println(AdvancedScenarios.wordsStartingWithLetter(words, "a"));

// Sample Output:
[apple, apricot]
```

---

## 136. Count frequency of numbers

```java
public static Map<Integer, Long> countNumberFrequency(List<Integer> numbers) {
    return numbers.stream()
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 3, 2, 4, 3, 2);
System.out.println(AdvancedScenarios.countNumberFrequency(nums));

// Sample Output:
{2=3, 3=2, 4=1}
```

---

## 137. Find common prefix

```java
public static String findCommonPrefix(List<String> strings) {
    if (strings.isEmpty()) return "";
    String first = strings.get(0);
    return IntStream.range(0, first.length())
            .filter(i -> strings.stream().anyMatch(s -> s.length() <= i || s.charAt(i) != first.charAt(i)))
            .findFirst()
            .map(i -> first.substring(0, i))
            .orElse(first);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("flower", "flow", "flight");
System.out.println(AdvancedScenarios.findCommonPrefix(words));

// Sample Output:
fl
```

---

## 138. Character occurrences in list of strings

```java
public static Map<Character, Long> characterOccurrences(List<String> strings) {
    return strings.stream()
            .flatMap(s -> s.chars().mapToObj(c -> (char) c))
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana");
System.out.println(AdvancedScenarios.characterOccurrences(words));

// Sample Output:
{a=4, p=2, l=1, e=1, b=1, n=2}
```

---

## 139. Check longest increasing subsequence (simplified)

```java
public static boolean hasIncreasingSubsequence(List<Integer> numbers, int minLength) {
    return IntStream.range(0, numbers.size() - minLength + 1)
            .anyMatch(start -> 
                IntStream.range(start, start + minLength)
                    .allMatch(i -> i == start || numbers.get(i) > numbers.get(i - 1))
            );
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 3, 5, 2, 4, 6);
System.out.println(AdvancedScenarios.hasIncreasingSubsequence(nums, 3));

// Sample Output:
true
```

---

## 140. Check if pangram

```java
public static boolean isPangram(String input) {
    return input.toLowerCase().chars()
            .filter(Character::isLetter)
            .distinct()
            .count() == 26;
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "The quick brown fox jumps over the lazy dog";
System.out.println(AdvancedScenarios.isPangram(s));

// Sample Output:
true
```

---

## 141. Find prime numbers

```java
public static List<Integer> findPrimeNumbers(List<Integer> numbers) {
    return numbers.stream()
            .filter(n -> n > 1 && IntStream.range(2, (int) Math.sqrt(n) + 1)
                    .allMatch(i -> n % i != 0))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 3, 4, 5, 6, 7, 8);
System.out.println(AdvancedScenarios.findPrimeNumbers(nums));

// Sample Output:
[2, 3, 5, 7]
```

---

## 142. Group by word length

```java
public static Map<Integer, List<String>> groupByWordLength(List<String> words) {
    return words.stream()
            .collect(Collectors.groupingBy(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "dog", "parrot", "lion");
System.out.println(AdvancedScenarios.groupByWordLength(words));

// Sample Output:
{3=[cat, dog], 4=[lion], 6=[parrot]}
```

---

## 143. Character frequency in string

```java
public static Map<Character, Long> characterFrequencyInString(String input) {
    return input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "test";
System.out.println(AdvancedScenarios.characterFrequencyInString(s));

// Sample Output:
{t=2, e=1, s=1}
```

---

## 144. Nth highest element (generic)

```java
public static OptionalInt nthHighestElement(List<Integer> numbers, int n) {
    return numbers.stream()
            .mapToInt(Integer::intValue)
            .distinct()
            .boxed()
            .sorted(Collections.reverseOrder())
            .skip(n - 1)
            .mapToInt(Integer::intValue)
            .findFirst();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(3, 5, 1, 2, 4);
System.out.println(AdvancedScenarios.nthHighestElement(nums, 2).getAsInt());

// Sample Output:
4
```

---

## 145. Longest string

```java
public static Optional<String> longestStringInList(List<String> strings) {
    return strings.stream()
            .max(Comparator.comparing(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("dog", "elephant", "cat");
System.out.println(AdvancedScenarios.longestStringInList(words).get());

// Sample Output:
elephant
```

---

## 146. Merge two string lists

```java
public static List<String> mergeStringLists(List<String> list1, List<String> list2) {
    return Stream.concat(list1.stream(), list2.stream())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> l1 = Arrays.asList("a", "b");
List<String> l2 = Arrays.asList("c", "d");
System.out.println(AdvancedScenarios.mergeStringLists(l1, l2));

// Sample Output:
[a, b, c, d]
```

---

## 148. Generate first 10 even numbers with iterate

```java
public static List<Integer> generateEvenWithIterate() {
    return Stream.iterate(2, n -> n + 2)
            .limit(10)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(AdvancedScenarios.generateEvenWithIterate());

// Sample Output:
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

---

## 149. Fibonacci with iterate

```java
public static List<Integer> fibonacciWithIterate() {
    return Stream.iterate(new int[]{0, 1}, arr -> new int[]{arr[1], arr[0] + arr[1]})
            .limit(10)
            .map(arr -> arr[0])
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(AdvancedScenarios.fibonacciWithIterate());

// Sample Output:
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

---

## 150. Most repeated element

```java
public static Optional<Integer> mostRepeatedElement(List<Integer> numbers) {
    return numbers.stream()
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
            .entrySet().stream()
            .max(Map.Entry.comparingByValue())
            .map(Map.Entry::getKey);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 2, 4);
System.out.println(AdvancedScenarios.mostRepeatedElement(nums).get());

// Sample Output:
2
```

---

## 151. Sort map by values

```java
public static <K, V extends Comparable<? super V>> Map<K, V> sortMapByValues(Map<K, V> map) {
    return map.entrySet().stream()
            .sorted(Map.Entry.comparingByValue())
            .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (e1, e2) -> e1,
                LinkedHashMap::new
            ));
}
```
#### Sample Input/Output
```java
// Sample Input:
Map<String, Integer> map = new HashMap<>();
map.put("a", 2); map.put("b", 1); map.put("c", 3);
System.out.println(AdvancedScenarios.sortMapByValues(map));

// Sample Output:
{b=1, a=2, c=3}
```

---

## 152. Average length of words

```java
public static OptionalDouble averageWordLength(List<String> words) {
    return words.stream()
            .mapToInt(String::length)
            .average();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("Java", "Streams", "API");
System.out.println(AdvancedScenarios.averageWordLength(words).getAsDouble());

// Sample Output:
5.0
```

---

## 153. Parallel stream example

```java
public static List<Integer> parallelStreamExample(List<Integer> numbers) {
    return numbers.parallelStream()
            .filter(n -> n % 2 == 0)
            .map(n -> n * n)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);
System.out.println(AdvancedScenarios.parallelStreamExample(nums));

// Sample Output:
[4, 16, 36]    // Note: order may vary due to parallel processing
```

---