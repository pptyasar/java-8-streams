# Java 8 Streams – Advanced Intermediate Operations (217–235)

Each method includes a code sample and a sample input/output block.

---

## 217. Filter strings starting with a letter

```java
public static List<String> filterStringsStartingWith(List<String> strings, String prefix) {
    return strings.stream()
            .filter(s -> s != null && s.startsWith(prefix))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana", "apricot", "cherry");
System.out.println(StreamAdvanced.filterStringsStartingWith(words, "a"));

// Sample Output:
[apple, apricot]
```

---

## 218. Remove strings shorter than n

```java
public static List<String> removeShorterThan(List<String> strings, int n) {
    return strings.stream()
            .filter(s -> s != null && s.length() >= n)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "elephant", "dog");
System.out.println(StreamAdvanced.removeShorterThan(words, 4));

// Sample Output:
[elephant]
```

---

## 219. Map to uppercase and sort

```java
public static List<String> mapToUppercaseAndSort(List<String> strings) {
    return strings.stream()
            .map(String::toUpperCase)
            .sorted()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "banana", "apple");
System.out.println(StreamAdvanced.mapToUppercaseAndSort(words));

// Sample Output:
[APPLE, BANANA, PEAR]
```

---

## 220. FlatMap to list of words from sentences

```java
public static List<String> flatMapSentencesToWords(List<String> sentences) {
    return sentences.stream()
            .flatMap(sentence -> Arrays.stream(sentence.split("\\s+")))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> sentences = Arrays.asList("hello world", "java streams");
System.out.println(StreamAdvanced.flatMapSentencesToWords(sentences));

// Sample Output:
[hello, world, java, streams]
```

---

## 221. Filter and map custom objects

```java
public static List<String> getNamesOfEmployeesWithHighSalary(List<Employee> employees, double minSalary) {
    return employees.stream()
            .filter(e -> e.getSalary() > minSalary)
            .map(Employee::getName)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamAdvanced.getNamesOfEmployeesWithHighSalary(employees, 60000));

// Sample Output:
[Carol]
```

---

## 222. Remove duplicate words from sentences

```java
public static List<String> removeDuplicateWords(List<String> sentences) {
    return sentences.stream()
            .flatMap(sentence -> Arrays.stream(sentence.split("\\s+")))
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> sentences = Arrays.asList("hello world", "world of java");
System.out.println(StreamAdvanced.removeDuplicateWords(sentences));

// Sample Output:
[hello, world, of, java]
```

---

## 223. Sort custom objects by two fields

```java
public static List<Employee> sortByDeptThenName(List<Employee> employees) {
    return employees.stream()
            .sorted(Comparator.comparing(Employee::getDepartment)
                    .thenComparing(Employee::getName))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamAdvanced.sortByDeptThenName(employees));

// Sample Output:
[Employee{id=2, name='Bob', ...}, Employee{id=4, name='Diana', ...}, Employee{id=1, name='Alice', ...}, Employee{id=3, name='Carol', ...}]
```

---

## 224. Group by first letter

```java
public static Map<Character, List<String>> groupByFirstLetter(List<String> strings) {
    return strings.stream()
            .filter(s -> s != null && !s.isEmpty())
            .collect(Collectors.groupingBy(s -> s.charAt(0)));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "apricot", "banana", "cherry");
System.out.println(StreamAdvanced.groupByFirstLetter(words));

// Sample Output:
{a=[apple, apricot], b=[banana], c=[cherry]}
```

---

## 225. Join sorted strings with a delimiter

```java
public static String joinSortedStrings(List<String> strings, String delimiter) {
    return strings.stream()
            .sorted()
            .collect(Collectors.joining(delimiter));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("pear", "banana", "apple");
System.out.println(StreamAdvanced.joinSortedStrings(words, ","));

// Sample Output:
apple,banana,pear
```

---

## 226. Filter, map, and collect summary statistics

```java
public static IntSummaryStatistics salaryStatistics(List<Employee> employees, String department) {
    return employees.stream()
            .filter(e -> department.equals(e.getDepartment()))
            .mapToInt(e -> (int) e.getSalary())
            .summaryStatistics();
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(StreamAdvanced.salaryStatistics(employees, "IT"));

// Sample Output:
IntSummaryStatistics{count=2, sum=150000, min=70000, average=75000.000000, max=80000}
```

---

## 227. Remove null and empty strings

```java
public static List<String> removeNullAndEmpty(List<String> strings) {
    return strings.stream()
            .filter(s -> s != null && !s.trim().isEmpty())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("a", null, "", "b", " ");
System.out.println(StreamAdvanced.removeNullAndEmpty(words));

// Sample Output:
[a, b]
```

---

## 228. Map strings to their lengths and group by length

```java
public static Map<Integer, List<String>> groupByStringLength(List<String> strings) {
    return strings.stream()
            .collect(Collectors.groupingBy(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "dog", "apple");
System.out.println(StreamAdvanced.groupByStringLength(words));

// Sample Output:
{3=[cat, dog], 5=[apple]}
```

---

## 229. Filter, sort, and join numbers as string

```java
public static String filterSortJoinNumbers(List<Integer> numbers, int min) {
    return numbers.stream()
            .filter(n -> n > min)
            .sorted()
            .map(Object::toString)
            .collect(Collectors.joining(","));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(5, 2, 9, 1, 7);
System.out.println(StreamAdvanced.filterSortJoinNumbers(nums, 4));

// Sample Output:
5,7,9
```

---

## 230. Remove duplicates and sort (case-insensitive)

```java
public static List<String> distinctAndSortIgnoreCase(List<String> strings) {
    return strings.stream()
            .map(String::toLowerCase)
            .distinct()
            .sorted()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("Apple", "banana", "APPLE", "Banana", "pear");
System.out.println(StreamAdvanced.distinctAndSortIgnoreCase(words));

// Sample Output:
[apple, banana, pear]
```

---

## 231. Filter by pattern using regex

```java
public static List<String> filterByPattern(List<String> strings, String regex) {
    Pattern pattern = Pattern.compile(regex);
    return strings.stream()
            .filter(s -> s != null && pattern.matcher(s).matches())
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "bat", "rat", "mat", "dog");
System.out.println(StreamAdvanced.filterByPattern(words, ".*at"));

// Sample Output:
[cat, bat, rat, mat]
```

---

## 232. Remove duplicates from list of lists

```java
public static List<Integer> flattenAndDistinct(List<List<Integer>> listOfLists) {
    return listOfLists.stream()
            .flatMap(Collection::stream)
            .distinct()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<List<Integer>> lol = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(2, 3, 4));
System.out.println(StreamAdvanced.flattenAndDistinct(lol));

// Sample Output:
[1, 2, 3, 4]
```

---

## 233. Find max by custom comparator

```java
public static Optional<String> maxByCustomComparator(List<String> strings) {
    return strings.stream()
            .max((s1, s2) -> s1.length() - s2.length());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "elephant", "dog");
System.out.println(StreamAdvanced.maxByCustomComparator(words).get());

// Sample Output:
elephant
```

---

## 234. Find min by custom comparator

```java
public static Optional<String> minByCustomComparator(List<String> strings) {
    return strings.stream()
            .min((s1, s2) -> s1.length() - s2.length());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("cat", "elephant", "dog");
System.out.println(StreamAdvanced.minByCustomComparator(words).get());

// Sample Output:
cat
```

---

## 235. Remove elements by value

```java
public static List<Integer> removeElementsByValue(List<Integer> numbers, int value) {
    return numbers.stream()
            .filter(n -> n != value)
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 4, 2, 5);
System.out.println(StreamAdvanced.removeElementsByValue(nums, 2));

// Sample Output:
[1, 3, 4, 5]
```

---