# Java 8 Streams – Complex List Operations (94–120)

Each method includes a code sample and a sample input/output block.

---

## 94. Partition employees based on salary > 50000

```java
public static Map<Boolean, List<Employee>> partitionBySalary(List<Employee> employees) {
    return employees.stream()
            .collect(Collectors.partitioningBy(emp -> emp.getSalary() > 50000));
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(ComplexOperations.partitionBySalary(employees));

// Sample Output:
{true=[Employee{id=1, ...}, Employee{id=2, ...}, Employee{id=3, ...}], false=[Employee{id=4, ...}]}
```

---

## 95. Find common elements between two lists

```java
public static List<Integer> findCommonElements(List<Integer> list1, List<Integer> list2) {
    return list1.stream()
            .filter(list2::contains)
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> l1 = Arrays.asList(1, 2, 3, 4);
List<Integer> l2 = Arrays.asList(3, 4, 5, 6);
System.out.println(ComplexOperations.findCommonElements(l1, l2));

// Sample Output:
[3, 4]
```

---

## 96. Elements in list1 but not in list2

```java
public static List<Integer> elementsInList1NotInList2(List<Integer> list1, List<Integer> list2) {
    return list1.stream()
            .filter(elem -> !list2.contains(elem))
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> l1 = Arrays.asList(1, 2, 3, 4);
List<Integer> l2 = Arrays.asList(3, 4, 5, 6);
System.out.println(ComplexOperations.elementsInList1NotInList2(l1, l2));

// Sample Output:
[1, 2]
```

---

## 97. Check if two lists are equal (ignoring order)

```java
public static boolean listsEqualIgnoreOrder(List<Integer> list1, List<Integer> list2) {
    return list1.size() == list2.size() && 
           list1.stream().allMatch(list2::contains) &&
           list2.stream().allMatch(list1::contains);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> l1 = Arrays.asList(1, 2, 3);
List<Integer> l2 = Arrays.asList(3, 2, 1);
System.out.println(ComplexOperations.listsEqualIgnoreOrder(l1, l2));

// Sample Output:
true
```

---

## 98. Find duplicate words across two sentences

```java
public static List<String> duplicateWordsInSentences(String sentence1, String sentence2) {
    List<String> words1 = Arrays.asList(sentence1.toLowerCase().split("\\s+"));
    List<String> words2 = Arrays.asList(sentence2.toLowerCase().split("\\s+"));
    return words1.stream()
            .filter(words2::contains)
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s1 = "apple banana orange";
String s2 = "banana orange grape";
System.out.println(ComplexOperations.duplicateWordsInSentences(s1, s2));

// Sample Output:
[banana, orange]
```

---

## 99. Convert list to comma-separated string

```java
public static String listToCommaSeparated(List<Integer> numbers) {
    return numbers.stream()
            .map(String::valueOf)
            .collect(Collectors.joining(", "));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
System.out.println(ComplexOperations.listToCommaSeparated(nums));

// Sample Output:
1, 2, 3, 4
```

---

## 100. Convert to uppercase

```java
public static List<String> convertToUppercase(List<String> strings) {
    return strings.stream()
            .map(String::toUpperCase)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana");
System.out.println(ComplexOperations.convertToUppercase(words));

// Sample Output:
[APPLE, BANANA]
```

---

## 101. Convert to lowercase

```java
public static List<String> convertToLowercase(List<String> strings) {
    return strings.stream()
            .map(String::toLowerCase)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("APPLE", "BANANA");
System.out.println(ComplexOperations.convertToLowercase(words));

// Sample Output:
[apple, banana]
```

---

## 102. Join words with dash

```java
public static String joinWithDash(List<String> words) {
    return words.stream()
            .collect(Collectors.joining("-"));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana", "cherry");
System.out.println(ComplexOperations.joinWithDash(words));

// Sample Output:
apple-banana-cherry
```

---

## 103. Find longest string

```java
public static Optional<String> findLongestString(List<String> strings) {
    return strings.stream()
            .max(Comparator.comparing(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "elephant", "dog");
System.out.println(ComplexOperations.findLongestString(words).get());

// Sample Output:
elephant
```

---

## 104. Find shortest string

```java
public static Optional<String> findShortestString(List<String> strings) {
    return strings.stream()
            .min(Comparator.comparing(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "elephant", "dog");
System.out.println(ComplexOperations.findShortestString(words).get());

// Sample Output:
cat
```

---

## 105. Sort strings by length

```java
public static List<String> sortByLength(List<String> strings) {
    return strings.stream()
            .sorted(Comparator.comparing(String::length))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "banana", "fig");
System.out.println(ComplexOperations.sortByLength(words));

// Sample Output:
[fig, pear, banana]
```

---

## 106. Remove null values

```java
public static List<String> removeNulls(List<String> strings) {
    return strings.stream()
            .filter(Objects::nonNull)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> data = Arrays.asList("a", null, "b", null, "c");
System.out.println(ComplexOperations.removeNulls(data));

// Sample Output:
[a, b, c]
```

---

## 107. Remove empty strings

```java
public static List<String> removeEmptyStrings(List<String> strings) {
    return strings.stream()
            .filter(s -> s != null && !s.trim().isEmpty())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> data = Arrays.asList("a", "", "b", "   ", "c");
System.out.println(ComplexOperations.removeEmptyStrings(data));

// Sample Output:
[a, b, c]
```

---

## 108. Count nulls

```java
public static long countNulls(List<String> strings) {
    return strings.stream()
            .filter(Objects::isNull)
            .count();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> data = Arrays.asList("a", null, "b", null, "c");
System.out.println(ComplexOperations.countNulls(data));

// Sample Output:
2
```

---

## 109. Count empty strings

```java
public static long countEmptyStrings(List<String> strings) {
    return strings.stream()
            .filter(s -> s != null && s.trim().isEmpty())
            .count();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> data = Arrays.asList("a", "", "b", "   ", "c");
System.out.println(ComplexOperations.countEmptyStrings(data));

// Sample Output:
2
```

---

## 110. Find duplicate words ignoring case

```java
public static List<String> duplicateWordsIgnoreCase(String input) {
    List<String> words = Arrays.asList(input.split("\\s+"));
    return words.stream()
            .map(String::toLowerCase)
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
            .entrySet().stream()
            .filter(entry -> entry.getValue() > 1)
            .map(Map.Entry::getKey)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "Apple apple Banana banana apple";
System.out.println(ComplexOperations.duplicateWordsIgnoreCase(s));

// Sample Output:
[apple, banana]
```

---

## 111. Capitalize first letter of each word

```java
public static String capitalizeWords(String input) {
    return Arrays.stream(input.split("\\s+"))
            .map(word -> Character.toUpperCase(word.charAt(0)) + word.substring(1).toLowerCase())
            .collect(Collectors.joining(" "));
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "hello world java";
System.out.println(ComplexOperations.capitalizeWords(s));

// Sample Output:
Hello World Java
```

---

## 112. Find anagrams

```java
public static Map<String, List<String>> findAnagrams(List<String> words) {
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
System.out.println(ComplexOperations.findAnagrams(words));

// Sample Output:
{eilnst=[listen, silent, enlist], art=[rat, tar, art]}
```

---

## 113. Words with length > 4

```java
public static List<String> wordsLongerThan4(List<String> words) {
    return words.stream()
            .filter(word -> word.length() > 4)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "banana", "fig", "melon");
System.out.println(ComplexOperations.wordsLongerThan4(words));

// Sample Output:
[banana, melon]
```

---

## 114. First repeated character

```java
public static Character firstRepeatedCharacter(String input) {
    Set<Character> seen = new HashSet<>();
    return input.chars()
            .mapToObj(c -> (char) c)
            .filter(c -> !seen.add(c))
            .findFirst()
            .orElse(null);
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "abca";
System.out.println(ComplexOperations.firstRepeatedCharacter(s));

// Sample Output:
a
```

---

## 115. Common elements in two arrays

```java
public static List<Integer> commonElementsArrays(int[] arr1, int[] arr2) {
    Set<Integer> set2 = Arrays.stream(arr2).boxed().collect(Collectors.toSet());
    return Arrays.stream(arr1)
            .boxed()
            .filter(set2::contains)
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
int[] a1 = {1, 2, 3, 4};
int[] a2 = {3, 4, 5, 6};
System.out.println(ComplexOperations.commonElementsArrays(a1, a2));

// Sample Output:
[3, 4]
```

---

## 116. Get unique elements (no duplicates)

```java
public static List<Integer> getUniqueElements(List<Integer> numbers) {
    return numbers.stream()
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
            .entrySet().stream()
            .filter(entry -> entry.getValue() == 1)
            .map(Map.Entry::getKey)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 3, 2, 4, 5, 5, 6);
System.out.println(ComplexOperations.getUniqueElements(nums));

// Sample Output:
[3, 4, 6]
```

---

## 117. Sort strings alphabetically

```java
public static List<String> sortAlphabetically(List<String> strings) {
    return strings.stream()
            .sorted()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "banana", "apple");
System.out.println(ComplexOperations.sortAlphabetically(words));

// Sample Output:
[apple, banana, pear]
```

---

## 118. Sort integers descending

```java
public static List<Integer> sortIntegersDesc(List<Integer> numbers) {
    return numbers.stream()
            .sorted(Collections.reverseOrder())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(3, 1, 4, 2);
System.out.println(ComplexOperations.sortIntegersDesc(nums));

// Sample Output:
[4, 3, 2, 1]
```

---

## 119. Count word occurrences

```java
public static Map<String, Long> countWordOccurrences(String input) {
    return Arrays.stream(input.toLowerCase().split("\\s+"))
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "cat dog cat bird cat";
System.out.println(ComplexOperations.countWordOccurrences(s));

// Sample Output:
{cat=3, dog=1, bird=1}
```

---

## 120. Check if string contains only digits

```java
public static boolean containsOnlyDigits(String input) {
    return input.chars()
            .allMatch(Character::isDigit);
}
```
#### Sample Input/Output
```java
// Sample Input:
String s1 = "12345";
System.out.println(ComplexOperations.containsOnlyDigits(s1));
// Output: true

String s2 = "123a5";
System.out.println(ComplexOperations.containsOnlyDigits(s2));
// Output: false
```

---