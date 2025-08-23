# Java 8 Streams – Most Advanced Operations (156–182)

Each method below includes a code sample and a sample input/output block.

---

## 156. Longest word without repeating characters

```java
public static Optional<String> longestWordWithoutRepeatingChars(String input) {
    return Arrays.stream(input.split("\\s+"))
            .filter(word -> {
                Set<Character> chars = new HashSet<>();
                return word.chars().allMatch(c -> chars.add((char) c));
            })
            .max(Comparator.comparing(String::length));
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "apple orange dog";
System.out.println(MostAdvancedOperations.longestWordWithoutRepeatingChars(s).get());

// Sample Output:
orange
```

---

## 157. First palindrome word

```java
public static Optional<String> firstPalindromeWord(String input) {
    return Arrays.stream(input.split("\\s+"))
            .filter(word -> {
                String lower = word.toLowerCase();
                return lower.equals(new StringBuilder(lower).reverse().toString());
            })
            .findFirst();
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "hello madam noon";
System.out.println(MostAdvancedOperations.firstPalindromeWord(s).get());

// Sample Output:
madam
```

---

## 158. Sum of digits of all numbers

```java
public static int sumOfDigits(List<Integer> numbers) {
    return numbers.stream()
            .flatMapToInt(n -> String.valueOf(n).chars().map(Character::getNumericValue))
            .sum();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(12, 34, 5);
System.out.println(MostAdvancedOperations.sumOfDigits(nums));

// Sample Output:
15
// (1+2+3+4+5 = 15)
```

---

## 159. Check if list is sorted lexicographically

```java
public static boolean isSortedLexicographically(List<String> strings) {
    return IntStream.range(1, strings.size())
            .allMatch(i -> strings.get(i - 1).compareTo(strings.get(i)) <= 0);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana", "carrot");
System.out.println(MostAdvancedOperations.isSortedLexicographically(words));

// Sample Output:
true
```

---

## 160. Word with maximum vowels

```java
public static Optional<String> wordWithMaxVowels(String input) {
    return Arrays.stream(input.split("\\s+"))
            .max(Comparator.comparing(word -> 
                word.toLowerCase().chars().map(c -> "aeiou".indexOf(c) != -1 ? 1 : 0).sum()
            ));
}
```
#### Sample Input/Output
```java
// Sample Input:
String s = "sky apple orange";
System.out.println(MostAdvancedOperations.wordWithMaxVowels(s).get());

// Sample Output:
orange
```

---

## 161. Merge lists alternately

```java
public static List<Integer> mergeListsAlternately(List<Integer> list1, List<Integer> list2) {
    List<Integer> result = new ArrayList<>();
    IntStream.range(0, Math.max(list1.size(), list2.size()))
            .forEach(i -> {
                if (i < list1.size()) result.add(list1.get(i));
                if (i < list2.size()) result.add(list2.get(i));
            });
    return result;
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> l1 = Arrays.asList(1, 3, 5);
List<Integer> l2 = Arrays.asList(2, 4, 6, 8);
System.out.println(MostAdvancedOperations.mergeListsAlternately(l1, l2));

// Sample Output:
[1, 2, 3, 4, 5, 6, 8]
```

---

## 162. Longest common suffix

```java
public static String longestCommonSuffix(List<String> strings) {
    if (strings.isEmpty()) return "";
    String first = strings.get(0);
    int suffixLength = 0;
    for (int i = 1; i <= first.length(); i++) {
        String suffix = first.substring(first.length() - i);
        if (strings.stream().allMatch(s -> s.endsWith(suffix))) {
            suffixLength = i;
        } else {
            break;
        }
    }
    return suffixLength > 0 ? first.substring(first.length() - suffixLength) : "";
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("running", "ending", "sing");
System.out.println(MostAdvancedOperations.longestCommonSuffix(words));

// Sample Output:
ing
```

---

## 163. Department with highest total salary

```java
public static Optional<String> departmentWithHighestTotalSalary(List<Employee> employees) {
    return employees.stream()
            .collect(Collectors.groupingBy(
                Employee::getDepartment,
                Collectors.summingDouble(Employee::getSalary)
            ))
            .entrySet().stream()
            .max(Map.Entry.comparingByValue())
            .map(Map.Entry::getKey);
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.departmentWithHighestTotalSalary(employees).get());

// Sample Output:
IT
```

---

## 164. Department with highest average salary

```java
public static Optional<String> departmentWithHighestAvgSalary(List<Employee> employees) {
    return employees.stream()
            .collect(Collectors.groupingBy(
                Employee::getDepartment,
                Collectors.averagingDouble(Employee::getSalary)
            ))
            .entrySet().stream()
            .max(Map.Entry.comparingByValue())
            .map(Map.Entry::getKey);
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.departmentWithHighestAvgSalary(employees).get());

// Sample Output:
IT
```

---

## 165. Map of department to highest salary employee name

```java
public static Map<String, String> deptToHighestSalaryEmployeeName(List<Employee> employees) {
    return employees.stream()
            .collect(Collectors.groupingBy(
                Employee::getDepartment,
                Collectors.collectingAndThen(
                    Collectors.maxBy(Comparator.comparing(Employee::getSalary)),
                    opt -> opt.map(Employee::getName).orElse("N/A")
                )
            ));
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.deptToHighestSalaryEmployeeName(employees));

// Sample Output:
{IT=Carol, HR=Bob}
```

---

## 166. Partition and count employees by name length

```java
public static Map<String, Long> partitionAndCountByNameLength(List<Employee> employees) {
    Map<Boolean, Long> partitioned = employees.stream()
            .collect(Collectors.partitioningBy(
                emp -> emp.getName().length() > 5,
                Collectors.counting()
            ));
    Map<String, Long> result = new HashMap<>();
    result.put("longNames", partitioned.get(true));
    result.put("shortNames", partitioned.get(false));
    return result;
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.partitionAndCountByNameLength(employees));

// Sample Output:
{longNames=2, shortNames=2}
```

---

## 167. Sort by department then by salary descending

```java
public static List<Employee> sortByDeptThenSalaryDesc(List<Employee> employees) {
    return employees.stream()
            .sorted(Comparator.comparing(Employee::getDepartment)
                    .thenComparing(Comparator.comparing(Employee::getSalary).reversed()))
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.sortByDeptThenSalaryDesc(employees));

// Sample Output:
[Employee{id=2, name='Bob', ...}, Employee{id=4, name='Diana', ...}, Employee{id=3, name='Carol', ...}, Employee{id=1, name='Alice', ...}]
```

---

## 168. Comma-separated distinct department names

```java
public static String distinctDepartmentNames(List<Employee> employees) {
    return employees.stream()
            .map(Employee::getDepartment)
            .distinct()
            .collect(Collectors.joining(", "));
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.distinctDepartmentNames(employees));

// Sample Output:
IT, HR
```

---

## 177. Sum using IntStream

```java
public static int sumUsingIntStream(List<Integer> numbers) {
    return numbers.stream()
            .mapToInt(Integer::intValue)
            .sum();
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
System.out.println(MostAdvancedOperations.sumUsingIntStream(nums));

// Sample Output:
10
```

---

## 178. Generate random numbers

```java
public static List<Double> generateRandomNumbers(int count) {
    return DoubleStream.generate(Math::random)
            .limit(count)
            .boxed()
            .collect(Collectors.toList());
}
```
#### Sample Input/Output
```java
// Sample Input:
System.out.println(MostAdvancedOperations.generateRandomNumbers(3));

// Sample Output:
[0.123456789, 0.987654321, 0.456789123] // (actual values will vary)
```

---

## 180. Custom collector for string concatenation

```java
public static String customStringCollector(List<String> strings, String prefix, String suffix, String delimiter) {
    return strings.stream()
            .collect(Collector.of(
                StringBuilder::new,
                (sb, s) -> {
                    if (sb.length() > 0) sb.append(delimiter);
                    sb.append(s);
                },
                (sb1, sb2) -> sb1.append(delimiter).append(sb2),
                sb -> prefix + sb.toString() + suffix
            ));
}
```
#### Sample Input/Output
```java
// Sample Input:
List<String> words = Arrays.asList("apple", "banana", "cherry");
System.out.println(MostAdvancedOperations.customStringCollector(words, "[", "]", ";"));

// Sample Output:
[apple;banana;cherry]
```

---

## 181. Product using reduce

```java
public static OptionalInt productUsingReduce(List<Integer> numbers) {
    return numbers.stream()
            .mapToInt(Integer::intValue)
            .reduce((a, b) -> a * b);
}
```
#### Sample Input/Output
```java
// Sample Input:
List<Integer> nums = Arrays.asList(2, 3, 4);
System.out.println(MostAdvancedOperations.productUsingReduce(nums).getAsInt());

// Sample Output:
24
```

---

## 182. Transaction balance calculation

```java
public static class Transaction {
    private double amount;
    private String type; // "DEPOSIT" or "WITHDRAWAL"
    public Transaction(double amount, String type) {
        this.amount = amount;
        this.type = type;
    }
    public double getAmount() { return amount; }
    public String getType() { return type; }
}
public static double calculateBalance(List<Transaction> transactions) {
    return transactions.stream()
            .reduce(0.0,
                (balance, transaction) -> 
                    "DEPOSIT".equals(transaction.getType()) ? 
                        balance + transaction.getAmount() : 
                        balance - transaction.getAmount(),
                Double::sum
            );
}
```
#### Sample Input/Output
```java
// Sample Input:
List<MostAdvancedOperations.Transaction> txs = Arrays.asList(
    new MostAdvancedOperations.Transaction(100, "DEPOSIT"),
    new MostAdvancedOperations.Transaction(30, "WITHDRAWAL"),
    new MostAdvancedOperations.Transaction(50, "DEPOSIT")
);
System.out.println(MostAdvancedOperations.calculateBalance(txs));

// Sample Output:
120.0
```

---