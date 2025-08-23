# Java 8 Streams – Stream Terminal Operations (191–200)

Each method includes a code sample and a sample input/output block.

---

## 191. forEach to print all elements

```java
public static void printAllElements(List<Integer> numbers) {
    numbers.forEach(System.out::println);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
StreamTerminal.printAllElements(nums);

// Sample Output:
1
2
3
4
```

---

## 192. Collect to a List

```java
public static List<Integer> collectToList(Stream<Integer> stream) {
    return stream.collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
Stream<Integer> s = Stream.of(1, 2, 3);
System.out.println(StreamTerminal.collectToList(s));

// Sample Output:
[1, 2, 3]
```

---

## 193. Collect to a Set

```java
public static Set<Integer> collectToSet(Stream<Integer> stream) {
    return stream.collect(Collectors.toSet());
}
```
#### Sample Input/Output
```java
// Sample Input:
Stream<Integer> s = Stream.of(1, 2, 2, 3);
System.out.println(StreamTerminal.collectToSet(s));

// Sample Output:
[1, 2, 3] // Set does not guarantee order
```

---

## 194. Collect to a Map

```java
public static Map<Integer, String> collectToMap(List<String> words) {
    return words.stream()
            .collect(Collectors.toMap(String::length, w -> w, (w1, w2) -> w1));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "dog", "bird");
System.out.println(StreamTerminal.collectToMap(words));

// Sample Output:
{3=dog, 4=bird} // "dog" overwrites "cat" due to same length key
```

---

## 195. Reduce to sum

```java
public static int reduceToSum(List<Integer> numbers) {
    return numbers.stream().reduce(0, Integer::sum);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
System.out.println(StreamTerminal.reduceToSum(nums));

// Sample Output:
10
```

---

## 196. Reduce to product

```java
public static int reduceToProduct(List<Integer> numbers) {
    return numbers.stream().reduce(1, (a, b) -> a * b);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 3, 4);
System.out.println(StreamTerminal.reduceToProduct(nums));

// Sample Output:
24
```

---

## 197. Find first element

```java
public static Optional<Integer> findFirstElement(Stream<Integer> stream) {
    return stream.findFirst();
}
```
#### Sample Input/Output
```java
// Sample Input:
Stream<Integer> s = Stream.of(10, 20, 30);
System.out.println(StreamTerminal.findFirstElement(s).get());

// Sample Output:
10
```

---

## 198. Find any element

```java
public static Optional<Integer> findAnyElement(Stream<Integer> stream) {
    return stream.findAny();
}
```
#### Sample Input/Output
```java
// Sample Input:
Stream<Integer> s = Stream.of(100, 200, 300);
System.out.println(StreamTerminal.findAnyElement(s).get());

// Sample Output:
100 // or 200 or 300 (especially with parallel streams)
```

---

## 199. Count elements

```java
public static long countElements(Stream<?> stream) {
    return stream.count();
}
```
#### Sample Input/Output
```java
// Sample Input:
Stream<String> s = Stream.of("a", "b", "c");
System.out.println(StreamTerminal.countElements(s));

// Sample Output:
3
```

---

## 200. Match operations (anyMatch, allMatch, noneMatch)

```java
public static boolean anyMatchEven(List<Integer> numbers) {
    return numbers.stream().anyMatch(n -> n % 2 == 0);
}
public static boolean allMatchPositive(List<Integer> numbers) {
    return numbers.stream().allMatch(n -> n > 0);
}
public static boolean noneMatchNegative(List<Integer> numbers) {
    return numbers.stream().noneMatch(n -> n < 0);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 4, 6);
System.out.println(StreamTerminal.anyMatchEven(nums));      // Output: true
System.out.println(StreamTerminal.allMatchPositive(nums));  // Output: true
System.out.println(StreamTerminal.noneMatchNegative(nums)); // Output: true
```

---