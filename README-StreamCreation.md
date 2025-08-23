# Java 8 Streams – Stream Creation & Sources (183–190)

Each method includes a code sample and a sample input/output block.

---

## 183. Create stream from array

```java
public static Stream<Integer> streamFromArray(Integer[] arr) {
    return Arrays.stream(arr);
}
```
#### Sample Input/Output
```java
// Sample Input:
Integer[] arr = {1, 2, 3, 4};
System.out.println(StreamCreation.streamFromArray(arr).collect(Collectors.toList()));

// Sample Output:
[1, 2, 3, 4]
```

---

## 184. Create stream from collection

```java
public static Stream<String> streamFromCollection(Collection<String> collection) {
    return collection.stream();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> list = Arrays.asList("a", "b", "c");
System.out.println(StreamCreation.streamFromCollection(list).collect(Collectors.toList()));

// Sample Output:
[a, b, c]
```

---

## 185. Create stream using Stream.of

```java
public static Stream<String> streamOfStrings() {
    return Stream.of("apple", "banana", "cherry");
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamCreation.streamOfStrings().collect(Collectors.toList()));

// Sample Output:
[apple, banana, cherry]
```

---

## 186. Create infinite stream with iterate

```java
public static List<Integer> infiniteStreamIterate(int seed, int step, int limit) {
    return Stream.iterate(seed, n -> n + step)
            .limit(limit)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamCreation.infiniteStreamIterate(0, 2, 5));

// Sample Output:
[0, 2, 4, 6, 8]
```

---

## 187. Create infinite stream with generate

```java
public static List<Double> infiniteStreamGenerate(int limit) {
    return Stream.generate(Math::random)
            .limit(limit)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamCreation.infiniteStreamGenerate(3));

// Sample Output:
[0.123456789, 0.987654321, 0.456789123] // (actual values will vary)
```

---

## 188. Stream from file lines (Java 8+)

```java
public static List<String> streamFromFileLines(String filePath) throws IOException {
    try (Stream<String> lines = Files.lines(Paths.get(filePath))) {
        return lines.collect(Collectors.toList());
    }
}
```
#### Sample Input/Output
```java
// Sample Input:
String filePath = "test.txt"; // file contains: "line1\nline2\nline3"
System.out.println(StreamCreation.streamFromFileLines(filePath));

// Sample Output:
[line1, line2, line3]
```

---

## 189. Stream of characters from String

```java
public static List<Character> streamOfChars(String input) {
    return input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "abc";
System.out.println(StreamCreation.streamOfChars(s));

// Sample Output:
[a, b, c]
```

---

## 190. Stream of words from String

```java
public static List<String> streamOfWords(String input) {
    return Arrays.stream(input.split("\\s+"))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "Java streams are powerful";
System.out.println(StreamCreation.streamOfWords(s));

// Sample Output:
[Java, streams, are, powerful]
```

---