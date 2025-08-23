# Java 8 Streams – Stream Intermediate Operations (201–216)

Each method includes a code sample and a sample input/output block.

---

## 201. Filter even numbers

```java
public static List<Integer> filterEvenNumbers(List<Integer> numbers) {
    return numbers.stream()
            .filter(n -> n % 2 == 0)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);
System.out.println(StreamIntermediate.filterEvenNumbers(nums));

// Sample Output:
[2, 4, 6]
```

---

## 202. Map to double each number

```java
public static List<Integer> mapToDouble(List<Integer> numbers) {
    return numbers.stream()
            .map(n -> n * 2)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3);
System.out.println(StreamIntermediate.mapToDouble(nums));

// Sample Output:
[2, 4, 6]
```

---

## 203. Distinct elements

```java
public static List<Integer> distinctElements(List<Integer> numbers) {
    return numbers.stream()
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 3, 3, 4);
System.out.println(StreamIntermediate.distinctElements(nums));

// Sample Output:
[1, 2, 3, 4]
```

---

## 204. Sorted (ascending)

```java
public static List<Integer> sortedAscending(List<Integer> numbers) {
    return numbers.stream()
            .sorted()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(5, 2, 8, 1, 3);
System.out.println(StreamIntermediate.sortedAscending(nums));

// Sample Output:
[1, 2, 3, 5, 8]
```

---

## 205. Sorted (descending)

```java
public static List<Integer> sortedDescending(List<Integer> numbers) {
    return numbers.stream()
            .sorted(Collections.reverseOrder())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(5, 2, 8, 1, 3);
System.out.println(StreamIntermediate.sortedDescending(nums));

// Sample Output:
[8, 5, 3, 2, 1]
```

---

## 206. Limit elements

```java
public static List<Integer> limitElements(List<Integer> numbers, int limit) {
    return numbers.stream()
            .limit(limit)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
System.out.println(StreamIntermediate.limitElements(nums, 3));

// Sample Output:
[1, 2, 3]
```

---

## 207. Skip elements

```java
public static List<Integer> skipElements(List<Integer> numbers, int skip) {
    return numbers.stream()
            .skip(skip)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
System.out.println(StreamIntermediate.skipElements(nums, 2));

// Sample Output:
[3, 4, 5]
```

---

## 208. FlatMap example (list of lists to single list)

```java
public static List<Integer> flatMapListOfLists(List<List<Integer>> listOfLists) {
    return listOfLists.stream()
            .flatMap(Collection::stream)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<List<Integer>> lol = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4));
System.out.println(StreamIntermediate.flatMapListOfLists(lol));

// Sample Output:
[1, 2, 3, 4]
```

---

## 209. Peek for debugging

```java
public static List<Integer> peekDebug(List<Integer> numbers) {
    return numbers.stream()
            .peek(n -> System.out.println("Processing: " + n))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3);
StreamIntermediate.peekDebug(nums);
// Output:
Processing: 1
Processing: 2
Processing: 3
// Returned value: [1, 2, 3]
```

---

## 210. Remove null elements

```java
public static List<String> removeNullElements(List<String> strings) {
    return strings.stream()
            .filter(Objects::nonNull)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("a", null, "b", null, "c");
System.out.println(StreamIntermediate.removeNullElements(words));

// Sample Output:
[a, b, c]
```

---

## 211. Filter non-empty strings

```java
public static List<String> filterNonEmptyStrings(List<String> strings) {
    return strings.stream()
            .filter(s -> s != null && !s.trim().isEmpty())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("a", "", "b", "   ", "c");
System.out.println(StreamIntermediate.filterNonEmptyStrings(words));

// Sample Output:
[a, b, c]
```

---

## 212. Filter using multiple conditions

```java
public static List<Integer> filterMultipleConditions(List<Integer> numbers) {
    return numbers.stream()
            .filter(n -> n > 2 && n < 10 && n % 2 == 0)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 6, 8, 10, 12);
System.out.println(StreamIntermediate.filterMultipleConditions(nums));

// Sample Output:
[4, 6, 8]
```

---

## 213. Map to string lengths

```java
public static List<Integer> mapToStringLengths(List<String> strings) {
    return strings.stream()
            .map(String::length)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "pie", "java");
System.out.println(StreamIntermediate.mapToStringLengths(words));

// Sample Output:
[5, 3, 4]
```

---

## 214. FlatMap string to chars

```java
public static List<Character> flatMapStringToChars(List<String> strings) {
    return strings.stream()
            .flatMap(str -> str.chars().mapToObj(c -> (char) c))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("hi", "ok");
System.out.println(StreamIntermediate.flatMapStringToChars(words));

// Sample Output:
[h, i, o, k]
```

---

## 215. Remove duplicates (distinct)

```java
public static List<String> distinctStrings(List<String> strings) {
    return strings.stream()
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("a", "b", "a", "c", "b");
System.out.println(StreamIntermediate.distinctStrings(words));

// Sample Output:
[a, b, c]
```

---

## 216. Sort strings alphabetically

```java
public static List<String> sortStringsAlphabetically(List<String> strings) {
    return strings.stream()
            .sorted()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "apple", "banana");
System.out.println(StreamIntermediate.sortStringsAlphabetically(words));

// Sample Output:
[apple, banana, pear]
```

---