# Java 8 Streams – Advanced String Operations (41–50)

Each method below includes a code sample and a sample input/output block.

---

## 41. Find duplicate characters

```java
public static List<Character> findDuplicateCharacters(String input) {
    return input.chars()
            .mapToObj(c -> (char) c)
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
String s = "programming";
System.out.println(AdvancedStringOperations.findDuplicateCharacters(s));

// Sample Output:
[r, g, m]
```

---

## 42. Find first non-repeating character

```java
public static Character firstNonRepeatingChar(String input) {
    Map<Character, Long> charCount = input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(Function.identity(), 
                    LinkedHashMap::new, Collectors.counting()));
    return charCount.entrySet().stream()
            .filter(entry -> entry.getValue() == 1)
            .map(Map.Entry::getKey)
            .findFirst()
            .orElse(null);
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "success";
System.out.println(AdvancedStringOperations.firstNonRepeatingChar(s));

// Sample Output:
u
```

---

## 43. Reverse entire string

```java
public static String reverseString(String input) {
    return input.chars()
            .mapToObj(c -> String.valueOf((char) c))
            .reduce("", (s1, s2) -> s2 + s1);
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "hello";
System.out.println(AdvancedStringOperations.reverseString(s));

// Sample Output:
olleh
```

---

## 44. Find shortest word

```java
public static String findShortestWord(String input) {
    return Arrays.stream(input.split("\\s+"))
            .min(Comparator.comparing(String::length))
            .orElse("");
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "the quick brown fox";
System.out.println(AdvancedStringOperations.findShortestWord(s));

// Sample Output:
the
```

---

## 45. Find words starting with given letter

```java
public static List<String> wordsStartingWith(String input, String letter) {
    return Arrays.stream(input.split("\\s+"))
            .filter(word -> word.toLowerCase().startsWith(letter.toLowerCase()))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "apple apricot banana avocado";
System.out.println(AdvancedStringOperations.wordsStartingWith(s, "a"));

// Sample Output:
[apple, apricot, avocado]
```

---

## 46. Find palindromic words

```java
public static List<String> findPalindromicWords(String input) {
    return Arrays.stream(input.split("\\s+"))
            .filter(word -> {
                String cleaned = word.toLowerCase();
                return cleaned.equals(new StringBuilder(cleaned).reverse().toString());
            })
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "madam level noon civic kayak";
System.out.println(AdvancedStringOperations.findPalindromicWords(s));

// Sample Output:
[madam, level, noon, civic, kayak]
```

---

## 47. Find second most frequent word

```java
public static String secondMostFrequentWord(String input) {
    Map<String, Long> wordCount = Arrays.stream(input.toLowerCase().split("\\s+"))
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    return wordCount.entrySet().stream()
            .sorted(Map.Entry.<String, Long>comparingByValue().reversed())
            .skip(1)
            .map(Map.Entry::getKey)
            .findFirst()
            .orElse("");
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "a b a c b a b d";
System.out.println(AdvancedStringOperations.secondMostFrequentWord(s));

// Sample Output:
b
```

---
