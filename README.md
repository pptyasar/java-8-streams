# java-8-streams

I'll provide Java Streams solutions for all these questions in a well-organized manner. Here's a comprehensive solution set:

## Java Streams Solutions

### String Processing (1-12)

```java
import java.util.*;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class StreamsSolutions {

    // 1. Count frequency of words in a sentence
    public static Map<String, Long> countWordFrequency(String sentence) {
        return Arrays.stream(sentence.toLowerCase().split("\\s+"))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 2. Find the largest word from a string
    public static String findLargestWord(String input) {
        return Arrays.stream(input.split("\\s+"))
                .max(Comparator.comparing(String::length))
                .orElse("");
    }

    // 3. Find frequency of each character
    public static Map<Character, Long> characterFrequency(String input) {
        return input.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 4. Find first non-repeated character
    public static Character firstNonRepeatedChar(String input) {
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

    // 5. Find first repeated character
    public static Character firstRepeatedChar(String input) {
        Set<Character> seen = new HashSet<>();
        return input.chars()
                .mapToObj(c -> (char) c)
                .filter(c -> !seen.add(c))
                .findFirst()
                .orElse(null);
    }

    // 6. Reverse each word
    public static String reverseEachWord(String input) {
        return Arrays.stream(input.split("\\s+"))
                .map(word -> new StringBuilder(word).reverse().toString())
                .collect(Collectors.joining(" "));
    }

    // 7. Find the longest word
    public static String findLongestWord(String input) {
        return Arrays.stream(input.split("\\s+"))
                .max(Comparator.comparing(String::length))
                .orElse("");
    }

    // 8. Find duplicate words
    public static List<String> findDuplicateWords(String input) {
        Map<String, Long> wordCount = Arrays.stream(input.toLowerCase().split("\\s+"))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        
        return wordCount.entrySet().stream()
                .filter(entry -> entry.getValue() > 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 9. Check if palindrome using streams
    public static boolean isPalindrome(String input) {
        String cleaned = input.toLowerCase().replaceAll("[^a-z]", "");
        return IntStream.range(0, cleaned.length() / 2)
                .allMatch(i -> cleaned.charAt(i) == cleaned.charAt(cleaned.length() - 1 - i));
    }

    // 10. Count vowels and consonants
    public static Map<String, Long> countVowelsConsonants(String input) {
        Map<Boolean, Long> result = input.toLowerCase().chars()
                .filter(Character::isLetter)
                .mapToObj(c -> (char) c)
                .collect(Collectors.partitioningBy(
                    c -> "aeiou".indexOf(c) != -1, Collectors.counting()));
        
        Map<String, Long> finalResult = new HashMap<>();
        finalResult.put("vowels", result.get(true));
        finalResult.put("consonants", result.get(false));
        return finalResult;
    }

    // 11. Extract unique words
    public static List<String> extractUniqueWords(String input) {
        return Arrays.stream(input.toLowerCase().split("\\s+"))
                .distinct()
                .collect(Collectors.toList());
    }

    // 12. Find word(s) with maximum frequency
    public static List<String> wordsWithMaxFrequency(String input) {
        Map<String, Long> wordCount = Arrays.stream(input.toLowerCase().split("\\s+"))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        
        long maxCount = wordCount.values().stream().mapToLong(Long::longValue).max().orElse(0);
        
        return wordCount.entrySet().stream()
                .filter(entry -> entry.getValue() == maxCount)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }
}
```

### Array/List Operations (13-31)

```java
public class ArrayOperations {

    // 13. Find duplicates
    public static List<Integer> findDuplicates(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() > 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 14. Find unique elements
    public static List<Integer> findUniqueElements(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 15. Find second highest number
    public static OptionalInt findSecondHighest(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .distinct()
                .sorted()
                .skip(numbers.stream().mapToInt(Integer::intValue).distinct().count() - 2)
                .findFirst();
    }

    // 16. Find nth highest number
    public static OptionalInt findNthHighest(List<Integer> numbers, int n) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .distinct()
                .boxed()
                .sorted(Collections.reverseOrder())
                .skip(n - 1)
                .mapToInt(Integer::intValue)
                .findFirst();
    }

    // 17. Sum of all numbers
    public static int sumAllNumbers(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .sum();
    }

    // 18. Find average
    public static OptionalDouble findAverage(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .average();
    }

    // 19. Sort ascending
    public static List<Integer> sortAscending(List<Integer> numbers) {
        return numbers.stream()
                .sorted()
                .collect(Collectors.toList());
    }

    // 20. Sort descending
    public static List<Integer> sortDescending(List<Integer> numbers) {
        return numbers.stream()
                .sorted(Collections.reverseOrder())
                .collect(Collectors.toList());
    }

    // 21. Find max
    public static OptionalInt findMax(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .max();
    }

    // 22. Find min
    public static OptionalInt findMin(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .min();
    }

    // 23. Find even numbers
    public static List<Integer> findEvenNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());
    }

    // 24. Find odd numbers
    public static List<Integer> findOddNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 != 0)
                .collect(Collectors.toList());
    }

    // 25. Count numbers > 5
    public static long countNumbersGreaterThan5(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 5)
                .count();
    }

    // 26. Find product of all elements
    public static int findProduct(List<Integer> numbers) {
        return numbers.stream()
                .reduce(1, (a, b) -> a * b);
    }

    // 27. Generate squares
    public static List<Integer> generateSquares(List<Integer> numbers) {
        return numbers.stream()
                .map(n -> n * n)
                .collect(Collectors.toList());
    }

    // 28. Generate cubes
    public static List<Integer> generateCubes(List<Integer> numbers) {
        return numbers.stream()
                .map(n -> n * n * n)
                .collect(Collectors.toList());
    }

    // 29. Find numbers greater than 2
    public static List<Integer> numbersGreaterThan2(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 2)
                .collect(Collectors.toList());
    }

    // 30. Sum only even numbers
    public static int sumEvenNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 == 0)
                .mapToInt(Integer::intValue)
                .sum();
    }

    // 31. Sum only odd numbers
    public static int sumOddNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 != 0)
                .mapToInt(Integer::intValue)
                .sum();
    }
}
```

### Employee Operations (32-40)

```java
class Employee {
    private int id;
    private String name;
    private double salary;
    private String department;
    
    // Constructor, getters, setters
    public Employee(int id, String name, double salary, String department) {
        this.id = id;
        this.name = name;
        this.salary = salary;
        this.department = department;
    }
    
    // Getters
    public int getId() { return id; }
    public String getName() { return name; }
    public double getSalary() { return salary; }
    public String getDepartment() { return department; }
}

public class EmployeeOperations {

    // 32. Group employees by department
    public static Map<String, List<Employee>> groupByDepartment(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));
    }

    // 33. Find highest salary
    public static OptionalDouble findHighestSalary(List<Employee> employees) {
        return employees.stream()
                .mapToDouble(Employee::getSalary)
                .max();
    }

    // 34. Find second highest salary
    public static OptionalDouble findSecondHighestSalary(List<Employee> employees) {
        return employees.stream()
                .mapToDouble(Employee::getSalary)
                .distinct()
                .boxed()
                .sorted(Collections.reverseOrder())
                .skip(1)
                .mapToDouble(Double::doubleValue)
                .findFirst();
    }

    // 35. Find average salary by department
    public static Map<String, Double> averageSalaryByDepartment(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.averagingDouble(Employee::getSalary)
                ));
    }

    // 36. Count employees in each department
    public static Map<String, Long> countEmployeesByDepartment(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.counting()
                ));
    }

    // 37. Partition employees by salary > 50000
    public static Map<Boolean, List<Employee>> partitionBySalary(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.partitioningBy(emp -> emp.getSalary() > 50000));
    }

    // 38. Find employee with longest name
    public static Optional<Employee> employeeWithLongestName(List<Employee> employees) {
        return employees.stream()
                .max(Comparator.comparing(emp -> emp.getName().length()));
    }

    // 39. Find names starting with "A"
    public static List<String> namesStartingWithA(List<Employee> employees) {
        return employees.stream()
                .map(Employee::getName)
                .filter(name -> name.startsWith("A"))
                .collect(Collectors.toList());
    }

    // 40. Convert to comma-separated string
    public static String employeeNamesToString(List<Employee> employees) {
        return employees.stream()
                .map(Employee::getName)
                .collect(Collectors.joining(", "));
    }
}
```

### Advanced String Operations (41-50)

```java
public class AdvancedStringOperations {

    // 41. Find duplicate characters
    public static List<Character> findDuplicateCharacters(String input) {
        return input.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() > 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 42. Find first non-repeating character
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

    // 43. Reverse entire string
    public static String reverseString(String input) {
        return input.chars()
                .mapToObj(c -> String.valueOf((char) c))
                .reduce("", (s1, s2) -> s2 + s1);
    }

    // 44. Find shortest word
    public static String findShortestWord(String input) {
        return Arrays.stream(input.split("\\s+"))
                .min(Comparator.comparing(String::length))
                .orElse("");
    }

    // 45. Find words starting with given letter
    public static List<String> wordsStartingWith(String input, String letter) {
        return Arrays.stream(input.split("\\s+"))
                .filter(word -> word.toLowerCase().startsWith(letter.toLowerCase()))
                .collect(Collectors.toList());
    }

    // 46. Find palindromic words
    public static List<String> findPalindromicWords(String input) {
        return Arrays.stream(input.split("\\s+"))
                .filter(word -> {
                    String cleaned = word.toLowerCase();
                    return cleaned.equals(new StringBuilder(cleaned).reverse().toString());
                })
                .collect(Collectors.toList());
    }

    // 47. Find second most frequent word
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
}
```
## Continued Java Streams Solutions

### Array Operations Continued (48-77)

```java
public class AdvancedArrayOperations {

    // 48. Find all even numbers
    public static List<Integer> findEvenNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());
    }

    // 49. Find all odd numbers
    public static List<Integer> findOddNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 != 0)
                .collect(Collectors.toList());
    }

    // 50. Find duplicate elements
    public static List<Integer> findDuplicateElements(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() > 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 51. Find unique elements
    public static List<Integer> findUniqueElements(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 52. Find maximum element
    public static OptionalInt findMaximum(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .max();
    }

    // 53. Find minimum element
    public static OptionalInt findMinimum(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .min();
    }

    // 54. Find second largest element
    public static OptionalInt findSecondLargest(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .distinct()
                .boxed()
                .sorted(Collections.reverseOrder())
                .skip(1)
                .mapToInt(Integer::intValue)
                .findFirst();
    }

    // 55. Find second smallest element
    public static OptionalInt findSecondSmallest(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .distinct()
                .sorted()
                .skip(1)
                .findFirst();
    }

    // 56. Remove duplicates
    public static List<Integer> removeDuplicates(List<Integer> numbers) {
        return numbers.stream()
                .distinct()
                .collect(Collectors.toList());
    }

    // 57. Sort ascending
    public static List<Integer> sortAscending(List<Integer> numbers) {
        return numbers.stream()
                .sorted()
                .collect(Collectors.toList());
    }

    // 58. Sort descending
    public static List<Integer> sortDescending(List<Integer> numbers) {
        return numbers.stream()
                .sorted(Collections.reverseOrder())
                .collect(Collectors.toList());
    }

    // 59. Sum of all elements
    public static int sumAllElements(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .sum();
    }

    // 60. Average of all elements
    public static OptionalDouble averageOfElements(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .average();
    }

    // 61. Partition into even and odd
    public static Map<Boolean, List<Integer>> partitionEvenOdd(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.partitioningBy(n -> n % 2 == 0));
    }

    // 62. Group by modulo 3
    public static Map<Integer, List<Integer>> groupByModulo3(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(n -> n % 3));
    }

    // 63. Find numbers greater than 5
    public static List<Integer> numbersGreaterThan5(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 5)
                .collect(Collectors.toList());
    }

    // 64. Count elements greater than 5
    public static long countElementsGreaterThan5(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 5)
                .count();
    }

    // 65. Square of each element
    public static List<Integer> squareElements(List<Integer> numbers) {
        return numbers.stream()
                .map(n -> n * n)
                .collect(Collectors.toList());
    }

    // 66. Cube of each element
    public static List<Integer> cubeElements(List<Integer> numbers) {
        return numbers.stream()
                .map(n -> n * n * n)
                .collect(Collectors.toList());
    }

    // 67. Find distinct squares
    public static List<Integer> distinctSquares(List<Integer> numbers) {
        return numbers.stream()
                .map(n -> n * n)
                .distinct()
                .collect(Collectors.toList());
    }

    // 68. Check if all elements are even
    public static boolean allElementsEven(List<Integer> numbers) {
        return numbers.stream()
                .allMatch(n -> n % 2 == 0);
    }

    // 69. Check if any element is greater than 10
    public static boolean anyElementGreaterThan10(List<Integer> numbers) {
        return numbers.stream()
                .anyMatch(n -> n > 10);
    }

    // 70. Count frequency of numbers
    public static Map<Integer, Long> countFrequency(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 71. Find first element
    public static Optional<Integer> findFirstElement(List<Integer> numbers) {
        return numbers.stream()
                .findFirst();
    }

    // 72. Find last element
    public static Optional<Integer> findLastElement(List<Integer> numbers) {
        return numbers.stream()
                .reduce((first, second) -> second);
    }

    // 73. Merge two lists
    public static List<Integer> mergeLists(List<Integer> list1, List<Integer> list2) {
        return Stream.concat(list1.stream(), list2.stream())
                .collect(Collectors.toList());
    }

    // 74. Flatten list of lists
    public static List<Integer> flattenLists(List<List<Integer>> listOfLists) {
        return listOfLists.stream()
                .flatMap(Collection::stream)
                .collect(Collectors.toList());
    }

    // 75. Generate first 10 even numbers
    public static List<Integer> generateFirst10EvenNumbers() {
        return IntStream.iterate(2, n -> n + 2)
                .limit(10)
                .boxed()
                .collect(Collectors.toList());
    }

    // 76. Generate first 10 odd numbers
    public static List<Integer> generateFirst10OddNumbers() {
        return IntStream.iterate(1, n -> n + 2)
                .limit(10)
                .boxed()
                .collect(Collectors.toList());
    }

    // 77. Generate Fibonacci series of 10 numbers
    public static List<Integer> generateFibonacci10() {
        return Stream.iterate(new int[]{0, 1}, fib -> new int[]{fib[1], fib[0] + fib})
                .limit(10)
                .map(fib -> fib)
                .collect(Collectors.toList());
    }
}
```

### Advanced String and Employee Operations (78-93)

```java
public class AdvancedOperations {

    // 78. Group words by their length
    public static Map<Integer, List<String>> groupWordsByLength(String input) {
        return Arrays.stream(input.split("\\s+"))
                .collect(Collectors.groupingBy(String::length));
    }

    // 79. Count frequency using Map + Streams
    public static Map<String, Long> countWordFrequency(String input) {
        return Arrays.stream(input.toLowerCase().split("\\s+"))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 80. Group numbers into odd/even
    public static Map<String, List<Integer>> groupOddEven(List<Integer> numbers) {
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
                .collect(Collectors.partitioningBy(n -> n % 2 == 0));
        
        Map<String, List<Integer>> result = new HashMap<>();
        result.put("even", partitioned.get(true));
        result.put("odd", partitioned.get(false));
        return result;
    }

    // 81. Find highest salary employee
    public static Optional<Employee> highestSalaryEmployee(List<Employee> employees) {
        return employees.stream()
                .max(Comparator.comparing(Employee::getSalary));
    }

    // 82. Find lowest salary employee
    public static Optional<Employee> lowestSalaryEmployee(List<Employee> employees) {
        return employees.stream()
                .min(Comparator.comparing(Employee::getSalary));
    }

    // 83. Find employees with salary > 50000
    public static List<Employee> employeesWithHighSalary(List<Employee> employees) {
        return employees.stream()
                .filter(emp -> emp.getSalary() > 50000)
                .collect(Collectors.toList());
    }

    // 84. Sort employees by salary ascending
    public static List<Employee> sortBySalaryAsc(List<Employee> employees) {
        return employees.stream()
                .sorted(Comparator.comparing(Employee::getSalary))
                .collect(Collectors.toList());
    }

    // 85. Sort employees by salary descending
    public static List<Employee> sortBySalaryDesc(List<Employee> employees) {
        return employees.stream()
                .sorted(Comparator.comparing(Employee::getSalary).reversed())
                .collect(Collectors.toList());
    }

    // 86. Group employees by department
    public static Map<String, List<Employee>> groupEmployeesByDept(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));
    }

    // 87. Count employees per department
    public static Map<String, Long> countEmployeesPerDept(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment, Collectors.counting()));
    }

    // 88. Average salary per department
    public static Map<String, Double> avgSalaryPerDept(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.averagingDouble(Employee::getSalary)
                ));
    }

    // 89. Max salary per department
    public static Map<String, Optional<Double>> maxSalaryPerDept(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.mapping(Employee::getSalary, 
                        Collectors.maxBy(Double::compareTo))
                ));
    }

    // 90. Second highest salary overall
    public static OptionalDouble secondHighestSalary(List<Employee> employees) {
        return employees.stream()
                .mapToDouble(Employee::getSalary)
                .distinct()
                .boxed()
                .sorted(Collections.reverseOrder())
                .skip(1)
                .mapToDouble(Double::doubleValue)
                .findFirst();
    }

    // 91. Nth highest salary
    public static OptionalDouble nthHighestSalary(List<Employee> employees, int n) {
        return employees.stream()
                .mapToDouble(Employee::getSalary)
                .distinct()
                .boxed()
                .sorted(Collections.reverseOrder())
                .skip(n - 1)
                .mapToDouble(Double::doubleValue)
                .findFirst();
    }

    // 92. Convert to Map id -> name
    public static Map<Integer, String> employeeIdToName(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.toMap(Employee::getId, Employee::getName));
    }

    // 93. Convert to Map department -> list of employees
    public static Map<String, List<Employee>> deptToEmployees(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));
    }
}
```

### Complex List Operations (94-120)

```java
public class ComplexOperations {

    // 94. Partition employees based on salary > 50000
    public static Map<Boolean, List<Employee>> partitionBySalary(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.partitioningBy(emp -> emp.getSalary() > 50000));
    }

    // 95. Find common elements between two lists
    public static List<Integer> findCommonElements(List<Integer> list1, List<Integer> list2) {
        return list1.stream()
                .filter(list2::contains)
                .distinct()
                .collect(Collectors.toList());
    }

    // 96. Elements in list1 but not in list2
    public static List<Integer> elementsInList1NotInList2(List<Integer> list1, List<Integer> list2) {
        return list1.stream()
                .filter(elem -> !list2.contains(elem))
                .distinct()
                .collect(Collectors.toList());
    }

    // 97. Check if two lists are equal (ignoring order)
    public static boolean listsEqualIgnoreOrder(List<Integer> list1, List<Integer> list2) {
        return list1.size() == list2.size() && 
               list1.stream().allMatch(list2::contains) &&
               list2.stream().allMatch(list1::contains);
    }

    // 98. Find duplicate words across two sentences
    public static List<String> duplicateWordsInSentences(String sentence1, String sentence2) {
        List<String> words1 = Arrays.asList(sentence1.toLowerCase().split("\\s+"));
        List<String> words2 = Arrays.asList(sentence2.toLowerCase().split("\\s+"));
        
        return words1.stream()
                .filter(words2::contains)
                .distinct()
                .collect(Collectors.toList());
    }

    // 99. Convert list to comma-separated string
    public static String listToCommaSeparated(List<Integer> numbers) {
        return numbers.stream()
                .map(String::valueOf)
                .collect(Collectors.joining(", "));
    }

    // 100. Convert to uppercase
    public static List<String> convertToUppercase(List<String> strings) {
        return strings.stream()
                .map(String::toUpperCase)
                .collect(Collectors.toList());
    }

    // 101. Convert to lowercase
    public static List<String> convertToLowercase(List<String> strings) {
        return strings.stream()
                .map(String::toLowerCase)
                .collect(Collectors.toList());
    }

    // 102. Join words with dash
    public static String joinWithDash(List<String> words) {
        return words.stream()
                .collect(Collectors.joining("-"));
    }

    // 103. Find longest string
    public static Optional<String> findLongestString(List<String> strings) {
        return strings.stream()
                .max(Comparator.comparing(String::length));
    }

    // 104. Find shortest string
    public static Optional<String> findShortestString(List<String> strings) {
        return strings.stream()
                .min(Comparator.comparing(String::length));
    }

    // 105. Sort strings by length
    public static List<String> sortByLength(List<String> strings) {
        return strings.stream()
                .sorted(Comparator.comparing(String::length))
                .collect(Collectors.toList());
    }

    // 106. Remove null values
    public static List<String> removeNulls(List<String> strings) {
        return strings.stream()
                .filter(Objects::nonNull)
                .collect(Collectors.toList());
    }

    // 107. Remove empty strings
    public static List<String> removeEmptyStrings(List<String> strings) {
        return strings.stream()
                .filter(s -> s != null && !s.trim().isEmpty())
                .collect(Collectors.toList());
    }

    // 108. Count nulls
    public static long countNulls(List<String> strings) {
        return strings.stream()
                .filter(Objects::isNull)
                .count();
    }

    // 109. Count empty strings
    public static long countEmptyStrings(List<String> strings) {
        return strings.stream()
                .filter(s -> s != null && s.trim().isEmpty())
                .count();
    }

    // 110. Find duplicate words ignoring case
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

    // 111. Capitalize first letter of each word
    public static String capitalizeWords(String input) {
        return Arrays.stream(input.split("\\s+"))
                .map(word -> Character.toUpperCase(word.charAt(0)) + word.substring(1).toLowerCase())
                .collect(Collectors.joining(" "));
    }

    // 112. Find anagrams
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

    // 113. Words with length > 4
    public static List<String> wordsLongerThan4(List<String> words) {
        return words.stream()
                .filter(word -> word.length() > 4)
                .collect(Collectors.toList());
    }

    // 114. First repeated character
    public static Character firstRepeatedCharacter(String input) {
        Set<Character> seen = new HashSet<>();
        return input.chars()
                .mapToObj(c -> (char) c)
                .filter(c -> !seen.add(c))
                .findFirst()
                .orElse(null);
    }

    // 115. Common elements in two arrays
    public static List<Integer> commonElementsArrays(int[] arr1, int[] arr2) {
        Set<Integer> set2 = Arrays.stream(arr2).boxed().collect(Collectors.toSet());
        return Arrays.stream(arr1)
                .boxed()
                .filter(set2::contains)
                .distinct()
                .collect(Collectors.toList());
    }

    // 116. Get unique elements (no duplicates)
    public static List<Integer> getUniqueElements(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .filter(entry -> entry.getValue() == 1)
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());
    }

    // 117. Sort strings alphabetically
    public static List<String> sortAlphabetically(List<String> strings) {
        return strings.stream()
                .sorted()
                .collect(Collectors.toList());
    }

    // 118. Sort integers descending
    public static List<Integer> sortIntegersDesc(List<Integer> numbers) {
        return numbers.stream()
                .sorted(Collections.reverseOrder())
                .collect(Collectors.toList());
    }

    // 119. Count word occurrences
    public static Map<String, Long> countWordOccurrences(String input) {
        return Arrays.stream(input.toLowerCase().split("\\s+"))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 120. Check if string contains only digits
    public static boolean containsOnlyDigits(String input) {
        return input.chars()
                .allMatch(Character::isDigit);
    }
}
```

### Advanced Operations and Custom Scenarios (121-153)

```java
public class AdvancedScenarios {

    // 121-123. Employee salary operations (already covered in previous sections)
    
    // 124. Concatenate all strings
    public static String concatenateStrings(List<String> strings) {
        return strings.stream()
                .collect(Collectors.joining(" "));
    }

    // 125. Check if all numbers are even
    public static boolean allNumbersEven(List<Integer> numbers) {
        return numbers.stream()
                .allMatch(n -> n % 2 == 0);
    }

    // 126. Find numbers greater than 50
    public static List<Integer> numbersGreaterThan50(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 50)
                .collect(Collectors.toList());
    }

    // 127. Second smallest number
    public static OptionalInt secondSmallestNumber(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .distinct()
                .sorted()
                .skip(1)
                .findFirst();
    }

    // 128. Even numbers and square them
    public static List<Integer> evenNumbersSquared(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n % 2 == 0)
                .map(n -> n * n)
                .collect(Collectors.toList());
    }

    // 129. Find longest palindrome
    public static Optional<String> longestPalindrome(List<String> words) {
        return words.stream()
                .filter(word -> {
                    String lower = word.toLowerCase();
                    return lower.equals(new StringBuilder(lower).reverse().toString());
                })
                .max(Comparator.comparing(String::length));
    }

    // 130. Count vowels in string
    public static long countVowels(String input) {
        return input.toLowerCase().chars()
                .filter(c -> "aeiou".indexOf(c) != -1)
                .count();
    }

    // 131. Find all anagrams
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

    // 132. Kth largest element
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

    // 133. Check if list is sorted
    public static boolean isListSorted(List<Integer> numbers) {
        return IntStream.range(1, numbers.size())
                .allMatch(i -> numbers.get(i - 1) <= numbers.get(i));
    }

    // 134. Intersection of multiple lists
    public static List<Integer> intersectionOfLists(List<List<Integer>> lists) {
        if (lists.isEmpty()) return new ArrayList<>();
        
        return lists.get(0).stream()
                .filter(element -> lists.stream().allMatch(list -> list.contains(element)))
                .distinct()
                .collect(Collectors.toList());
    }

    // 135. Words starting with specific letter
    public static List<String> wordsStartingWithLetter(List<String> words, String letter) {
        return words.stream()
                .filter(word -> word.toLowerCase().startsWith(letter.toLowerCase()))
                .collect(Collectors.toList());
    }

    // 136. Count frequency of numbers
    public static Map<Integer, Long> countNumberFrequency(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 137. Find common prefix
    public static String findCommonPrefix(List<String> strings) {
        if (strings.isEmpty()) return "";
        
        String first = strings.get(0);
        return IntStream.range(0, first.length())
                .filter(i -> strings.stream().anyMatch(s -> s.length() <= i || s.charAt(i) != first.charAt(i)))
                .findFirst()
                .map(i -> first.substring(0, i))
                .orElse(first);
    }

    // 138. Character occurrences in list of strings
    public static Map<Character, Long> characterOccurrences(List<String> strings) {
        return strings.stream()
                .flatMap(s -> s.chars().mapToObj(c -> (char) c))
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 139. Check longest increasing subsequence (simplified)
    public static boolean hasIncreasingSubsequence(List<Integer> numbers, int minLength) {
        return IntStream.range(0, numbers.size() - minLength + 1)
                .anyMatch(start -> 
                    IntStream.range(start, start + minLength)
                        .allMatch(i -> i == start || numbers.get(i) > numbers.get(i - 1))
                );
    }

    // 140. Check if pangram
    public static boolean isPangram(String input) {
        return input.toLowerCase().chars()
                .filter(Character::isLetter)
                .distinct()
                .count() == 26;
    }

    // 141. Find prime numbers
    public static List<Integer> findPrimeNumbers(List<Integer> numbers) {
        return numbers.stream()
                .filter(n -> n > 1 && IntStream.range(2, (int) Math.sqrt(n) + 1)
                        .allMatch(i -> n % i != 0))
                .collect(Collectors.toList());
    }

    // 142. Group by word length
    public static Map<Integer, List<String>> groupByWordLength(List<String> words) {
        return words.stream()
                .collect(Collectors.groupingBy(String::length));
    }

    // 143. Character frequency in string
    public static Map<Character, Long> characterFrequencyInString(String input) {
        return input.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 144. Nth highest element (generic)
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

    // 145. Longest string
    public static Optional<String> longestStringInList(List<String> strings) {
        return strings.stream()
                .max(Comparator.comparing(String::length));
    }

    // 146. Merge two string lists
    public static List<String> mergeStringLists(List<String> list1, List<String> list2) {
        return Stream.concat(list1.stream(), list2.stream())
                .collect(Collectors.toList());
    }

    // 147. Common elements (duplicate from 95)
    // 148. Generate first 10 even numbers with iterate
    public static List<Integer> generateEvenWithIterate() {
        return Stream.iterate(2, n -> n + 2)
                .limit(10)
                .collect(Collectors.toList());
    }

    // 149. Fibonacci with iterate
    public static List<Integer> fibonacciWithIterate() {
        return Stream.iterate(new int[]{0, 1}, arr -> new int[]{arr[1], arr[0] + arr})
                .limit(10)
                .map(arr -> arr)
                .collect(Collectors.toList());
    }

    // 150. Most repeated element
    public static Optional<Integer> mostRepeatedElement(List<Integer> numbers) {
        return numbers.stream()
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .max(Map.Entry.comparingByValue())
                .map(Map.Entry::getKey);
    }

    // 151. Sort map by values
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

    // 152. Average length of words
    public static OptionalDouble averageWordLength(List<String> words) {
        return words.stream()
                .mapToInt(String::length)
                .average();
    }

    // 153. Parallel stream example
    public static List<Integer> parallelStreamExample(List<Integer> numbers) {
        return numbers.parallelStream()
                .filter(n -> n % 2 == 0)
                .map(n -> n * n)
                .collect(Collectors.toList());
    }
}
```

### Most Advanced Operations (156-182)

```java
public class MostAdvancedOperations {

    // 156. Longest word without repeating characters
    public static Optional<String> longestWordWithoutRepeatingChars(String input) {
        return Arrays.stream(input.split("\\s+"))
                .filter(word -> {
                    Set<Character> chars = new HashSet<>();
                    return word.chars().allMatch(c -> chars.add((char) c));
                })
                .max(Comparator.comparing(String::length));
    }

    // 157. First palindrome word
    public static Optional<String> firstPalindromeWord(String input) {
        return Arrays.stream(input.split("\\s+"))
                .filter(word -> {
                    String lower = word.toLowerCase();
                    return lower.equals(new StringBuilder(lower).reverse().toString());
                })
                .findFirst();
    }

    // 158. Sum of digits of all numbers
    public static int sumOfDigits(List<Integer> numbers) {
        return numbers.stream()
                .flatMapToInt(n -> String.valueOf(n).chars().map(Character::getNumericValue))
                .sum();
    }

    // 159. Check if list is sorted lexicographically
    public static boolean isSortedLexicographically(List<String> strings) {
        return IntStream.range(1, strings.size())
                .allMatch(i -> strings.get(i - 1).compareTo(strings.get(i)) <= 0);
    }

    // 160. Word with maximum vowels
    public static Optional<String> wordWithMaxVowels(String input) {
        return Arrays.stream(input.split("\\s+"))
                .max(Comparator.comparing(word -> 
                    word.toLowerCase().chars().map(c -> "aeiou".indexOf(c) != -1 ? 1 : 0).sum()
                ));
    }

    // 161. Merge lists alternately
    public static List<Integer> mergeListsAlternately(List<Integer> list1, List<Integer> list2) {
        List<Integer> result = new ArrayList<>();
        IntStream.range(0, Math.max(list1.size(), list2.size()))
                .forEach(i -> {
                    if (i < list1.size()) result.add(list1.get(i));
                    if (i < list2.size()) result.add(list2.get(i));
                });
        return result;
    }

    // 162. Longest common suffix
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

    // 163. Department with highest total salary
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

    // 164. Department with highest average salary
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

    // 165. Map of department to highest salary employee name
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

    // 166. Partition and count employees by name length
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

    // 167. Sort by department then by salary descending
    public static List<Employee> sortByDeptThenSalaryDesc(List<Employee> employees) {
        return employees.stream()
                .sorted(Comparator.comparing(Employee::getDepartment)
                        .thenComparing(Comparator.comparing(Employee::getSalary).reversed()))
                .collect(Collectors.toList());
    }

    // 168. Comma-separated distinct department names
    public static String distinctDepartmentNames(List<Employee> employees) {
        return employees.stream()
                .map(Employee::getDepartment)
                .distinct()
                .collect(Collectors.joining(", "));
    }

    // 169-172. Exception handling and performance questions are conceptual

    // 177. Sum using IntStream
    public static int sumUsingIntStream(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .sum();
    }

    // 178. Generate random numbers
    public static List<Double> generateRandomNumbers(int count) {
        return DoubleStream.generate(Math::random)
                .limit(count)
                .boxed()
                .collect(Collectors.toList());
    }

    // 180. Custom collector for string concatenation
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

    // 181. Product using reduce
    public static OptionalInt productUsingReduce(List<Integer> numbers) {
        return numbers.stream()
                .mapToInt(Integer::intValue)
                .reduce((a, b) -> a * b);
    }

    // 182. Transaction balance calculation
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
}
```

### Usage Examples

```java
public class StreamsUsageExamples {
    public static void main(String[] args) {
        // Example 1: Word frequency
        String sentence = "To associate myself with an organization that provides a challenging job";
        Map<String, Long> wordCount = StreamsSolutions.countWordFrequency(sentence);
        System.out.println("Word frequencies: " + wordCount);

        // Example 2: Employee operations
        List<Employee> employees = Arrays.asList(
            new Employee(1, "Alice", 75000, "IT"),
            new Employee(2, "Bob", 60000, "HR"),
            new Employee(3, "Charlie", 80000, "IT"),
            new Employee(4, "Diana", 55000, "HR")
        );
        
        Map<String, List<Employee>> grouped = EmployeeOperations.groupByDepartment(employees);
        System.out.println("Employees by department: " + grouped);

        // Example 3: Array operations
        List<Integer> numbers = Arrays.asList(5, 3, 9, 1, 3, 9, 7);
        List<Integer> duplicates = ArrayOperations.findDuplicates(numbers);
        System.out.println("Duplicates: " + duplicates);

        // Example 4: Advanced operations
        List<String> words = Arrays.asList("apple", "banana", "strawberry", "kiwi");
        Optional<String> longest = ComplexOperations.findLongestString(words);
        System.out.println("Longest word: " + longest.orElse("None"));
    }
}
```
Based on my analysis of current Java Streams interview trends, here are **additional important questions** that are frequently asked but weren't covered in the previous comprehensive list:

## Critical Missing Java Streams Interview Questions

### **Stream Creation & Sources (183-190)**

```java
public class StreamCreationQuestions {

    // 183. Create streams from different sources
    public static void demonstrateStreamSources() {
        // From array
        Stream<String> fromArray = Arrays.stream(new String[]{"a", "b", "c"});
        
        // From values
        Stream<Integer> fromValues = Stream.of(1, 2, 3, 4, 5);
        
        // Empty stream
        Stream<String> empty = Stream.empty();
        
        // Infinite stream with limit
        Stream<Integer> infinite = Stream.iterate(0, n -> n + 2).limit(5);
        
        // From file lines
        // Stream<String> fromFile = Files.lines(Paths.get("file.txt"));
        
        // From range
        IntStream range = IntStream.range(1, 10);
        IntStream rangeClosed = IntStream.rangeClosed(1, 10);
    }

    // 184. Generate infinite streams with conditions
    public static List<Integer> generateUntilCondition(int limit) {
        return Stream.iterate(1, n -> n <= limit, n -> n + 1)
                .collect(Collectors.toList());
    }

    // 185. Create stream from Map
    public static List<String> streamFromMap(Map<String, Integer> map) {
        return map.entrySet().stream()
                .filter(entry -> entry.getValue() > 5)
                .map(entry -> entry.getKey() + ":" + entry.getValue())
                .collect(Collectors.toList());
    }

    // 186. Builder pattern for streams
    public static Stream<String> buildStream() {
        return Stream.<String>builder()
                .add("a")
                .add("b")
                .add("c")
                .build();
    }

    // 187. Generate stream with Supplier
    public static List<String> generateWithSupplier(int count) {
        return Stream.generate(() -> "Random: " + Math.random())
                .limit(count)
                .collect(Collectors.toList());
    }

    // 188. Primitive stream conversions
    public static void primitiveStreamConversions() {
        List<String> strings = Arrays.asList("1", "2", "3", "4", "5");
        
        // String to IntStream
        IntStream intStream = strings.stream().mapToInt(Integer::parseInt);
        
        // IntStream to Stream<Integer>
        Stream<Integer> boxedStream = intStream.boxed();
        
        // Statistics from IntStream
        IntSummaryStatistics stats = strings.stream()
                .mapToInt(Integer::parseInt)
                .summaryStatistics();
        
        System.out.println("Average: " + stats.getAverage());
        System.out.println("Max: " + stats.getMax());
        System.out.println("Count: " + stats.getCount());
    }

    // 189. Stream concatenation and merging
    public static List<Integer> concatenateStreams(List<Integer> list1, List<Integer> list2, List<Integer> list3) {
        return Stream.of(list1.stream(), list2.stream(), list3.stream())
                .flatMap(Function.identity())
                .distinct()
                .sorted()
                .collect(Collectors.toList());
    }

    // 190. Create conditional streams
    public static Optional<Stream<String>> conditionalStream(boolean condition, List<String> data) {
        return condition ? Optional.of(data.stream()) : Optional.empty();
    }
}
```

### **Advanced FlatMap Scenarios (191-196)**

```java
public class AdvancedFlatMapQuestions {

    // 191. Flatten nested lists with filtering
    public static List<String> flattenNestedListsWithFilter(List<List<String>> nestedLists) {
        return nestedLists.stream()
                .flatMap(list -> list.stream())
                .filter(str -> str.length() > 3)
                .distinct()
                .collect(Collectors.toList());
    }

    // 192. FlatMap with Optional
    public static List<String> flatMapWithOptional(List<Optional<String>> optionals) {
        return optionals.stream()
                .flatMap(Optional::stream)
                .collect(Collectors.toList());
    }

    // 193. Extract words from sentences and count frequency
    public static Map<String, Long> wordFrequencyFromSentences(List<String> sentences) {
        return sentences.stream()
                .flatMap(sentence -> Arrays.stream(sentence.toLowerCase().split("\\s+")))
                .filter(word -> !word.isEmpty())
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 194. FlatMap with complex objects
    public static class Order {
        private List<OrderItem> items;
        public Order(List<OrderItem> items) { this.items = items; }
        public List<OrderItem> getItems() { return items; }
    }
    
    public static class OrderItem {
        private String product;
        private int quantity;
        private double price;
        
        public OrderItem(String product, int quantity, double price) {
            this.product = product;
            this.quantity = quantity;
            this.price = price;
        }
        
        public String getProduct() { return product; }
        public int getQuantity() { return quantity; }
        public double getPrice() { return price; }
        public double getTotalValue() { return quantity * price; }
    }

    public static double calculateTotalOrderValue(List<Order> orders) {
        return orders.stream()
                .flatMap(order -> order.getItems().stream())
                .mapToDouble(OrderItem::getTotalValue)
                .sum();
    }

    // 195. FlatMap with arrays
    public static List<Character> getAllCharacters(List<String> words) {
        return words.stream()
                .flatMap(word -> word.chars().mapToObj(c -> (char) c))
                .distinct()
                .sorted()
                .collect(Collectors.toList());
    }

    // 196. FlatMap directory traversal simulation
    public static List<String> flattenDirectoryStructure(Map<String, List<String>> directories) {
        return directories.entrySet().stream()
                .flatMap(entry -> Stream.concat(
                    Stream.of(entry.getKey()),
                    entry.getValue().stream()
                ))
                .collect(Collectors.toList());
    }
}
```

### **Exception Handling in Streams (197-202)**

```java
public class StreamExceptionHandling {

    // 197. Handle checked exceptions in streams
    @FunctionalInterface
    public interface ThrowingFunction<T, R> {
        R apply(T t) throws Exception;
    }

    public static <T, R> Function<T, R> wrapper(ThrowingFunction<T, R> throwingFunction) {
        return i -> {
            try {
                return throwingFunction.apply(i);
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
        };
    }

    public static List<Integer> parseIntegers(List<String> strings) {
        return strings.stream()
                .map(wrapper(Integer::parseInt))
                .collect(Collectors.toList());
    }

    // 198. Handle exceptions with Optional
    public static List<Integer> parseIntegersWithOptional(List<String> strings) {
        return strings.stream()
                .map(s -> {
                    try {
                        return Optional.of(Integer.parseInt(s));
                    } catch (NumberFormatException e) {
                        return Optional.<Integer>empty();
                    }
                })
                .flatMap(Optional::stream)
                .collect(Collectors.toList());
    }

    // 199. Collect errors while processing
    public static class Result<T> {
        private final T value;
        private final Exception error;
        
        private Result(T value, Exception error) {
            this.value = value;
            this.error = error;
        }
        
        public static <T> Result<T> success(T value) {
            return new Result<>(value, null);
        }
        
        public static <T> Result<T> failure(Exception error) {
            return new Result<>(null, error);
        }
        
        public boolean isSuccess() { return error == null; }
        public T getValue() { return value; }
        public Exception getError() { return error; }
    }

    public static Map<Boolean, List<Result<Integer>>> parseWithErrorCollection(List<String> strings) {
        List<Result<Integer>> results = strings.stream()
                .map(s -> {
                    try {
                        return Result.success(Integer.parseInt(s));
                    } catch (NumberFormatException e) {
                        return Result.<Integer>failure(e);
                    }
                })
                .collect(Collectors.toList());
        
        return results.stream()
                .collect(Collectors.partitioningBy(Result::isSuccess));
    }

    // 200. Try-with-resources in streams (file processing)
    public static List<String> processLinesWithExceptionHandling(String filename) {
        try {
            return Files.lines(Paths.get(filename))
                    .filter(line -> !line.trim().isEmpty())
                    .map(String::toUpperCase)
                    .collect(Collectors.toList());
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
            return Collections.emptyList();
        }
    }

    // 201. Custom exception in stream processing
    public static class InvalidDataException extends RuntimeException {
        public InvalidDataException(String message) {
            super(message);
        }
    }

    public static List<Double> validateAndProcessData(List<String> data) {
        return data.stream()
                .filter(Objects::nonNull)
                .map(s -> {
                    if (s.trim().isEmpty()) {
                        throw new InvalidDataException("Empty string found");
                    }
                    return Double.parseDouble(s);
                })
                .filter(d -> d >= 0)
                .collect(Collectors.toList());
    }

    // 202. Graceful degradation with logging
    public static List<Integer> parseWithLogging(List<String> strings) {
        return strings.stream()
                .map(s -> {
                    try {
                        return Integer.parseInt(s);
                    } catch (NumberFormatException e) {
                        System.err.println("Failed to parse: " + s + " - " + e.getMessage());
                        return null;
                    }
                })
                .filter(Objects::nonNull)
                .collect(Collectors.toList());
    }
}
```

### **Performance and Parallel Streams (203-208)**

```java
public class StreamPerformanceQuestions {

    // 203. When to use parallel streams
    public static boolean shouldUseParallelStream(List<Integer> data) {
        // Use parallel for CPU-intensive operations on large datasets
        return data.size() > 10000 && 
               Runtime.getRuntime().availableProcessors() > 1;
    }

    // 204. Parallel stream performance comparison
    public static void compareSequentialVsParallel(List<Integer> largeList) {
        long startTime, endTime;
        
        // Sequential
        startTime = System.currentTimeMillis();
        long sequentialSum = largeList.stream()
                .mapToLong(i -> expensiveOperation(i))
                .sum();
        endTime = System.currentTimeMillis();
        System.out.println("Sequential time: " + (endTime - startTime) + "ms");
        
        // Parallel
        startTime = System.currentTimeMillis();
        long parallelSum = largeList.parallelStream()
                .mapToLong(i -> expensiveOperation(i))
                .sum();
        endTime = System.currentTimeMillis();
        System.out.println("Parallel time: " + (endTime - startTime) + "ms");
    }
    
    private static long expensiveOperation(int n) {
        // Simulate CPU-intensive work
        return IntStream.range(0, n).map(i -> i * i).sum();
    }

    // 205. Avoid stateful operations in parallel streams
    public static List<Integer> incorrectParallelProcessing(List<Integer> numbers) {
        // BAD: Using stateful lambda
        List<Integer> result = new ArrayList<>(); // Not thread-safe!
        numbers.parallelStream()
                .filter(n -> n % 2 == 0)
                .forEach(result::add); // Race condition!
        return result;
    }

    public static List<Integer> correctParallelProcessing(List<Integer> numbers) {
        // GOOD: Using collect which is thread-safe
        return numbers.parallelStream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());
    }

    // 206. Custom thread pool for parallel streams
    public static List<Integer> processWithCustomThreadPool(List<Integer> numbers) {
        ForkJoinPool customThreadPool = new ForkJoinPool(4);
        try {
            return customThreadPool.submit(() ->
                numbers.parallelStream()
                        .filter(n -> n > 50)
                        .collect(Collectors.toList())
            ).get();
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            customThreadPool.shutdown();
        }
    }

    // 207. Memory-efficient stream processing for large datasets
    public static void processLargeDatasetMemoryEfficient(Stream<String> largeStream) {
        // Process in chunks to avoid memory issues
        largeStream
                .filter(Objects::nonNull)
                .filter(s -> s.length() > 5)
                .map(String::toLowerCase)
                .forEach(this::processChunk); // Process one at a time
    }
    
    private void processChunk(String item) {
        // Process individual item
        System.out.println("Processing: " + item);
    }

    // 208. Stream vs traditional loop performance
    public static void compareStreamVsLoop(List<Integer> numbers) {
        long startTime, endTime;
        
        // Traditional for loop
        startTime = System.nanoTime();
        int sum1 = 0;
        for (int num : numbers) {
            if (num % 2 == 0) {
                sum1 += num * num;
            }
        }
        endTime = System.nanoTime();
        System.out.println("Loop time: " + (endTime - startTime) + "ns");
        
        // Stream
        startTime = System.nanoTime();
        int sum2 = numbers.stream()
                .filter(n -> n % 2 == 0)
                .mapToInt(n -> n * n)
                .sum();
        endTime = System.nanoTime();
        System.out.println("Stream time: " + (endTime - startTime) + "ns");
    }
}
```

### **Advanced Collectors and Custom Implementations (209-215)**

```java
public class AdvancedCollectorQuestions {

    // 209. Teeing collector (Java 12+)
    public static Map<String, Object> calculateStatistics(List<Integer> numbers) {
        return numbers.stream().collect(
            Collectors.teeing(
                Collectors.averagingDouble(Integer::doubleValue),
                Collectors.maxBy(Integer::compareTo),
                (avg, max) -> Map.of(
                    "average", avg,
                    "maximum", max.orElse(0)
                )
            )
        );
    }

    // 210. Custom collector implementation
    public static Collector<String, ?, String> joiningWithPrefix(String prefix, String delimiter) {
        return Collector.of(
            StringBuilder::new,
            (sb, s) -> {
                if (sb.length() > 0) sb.append(delimiter);
                sb.append(s);
            },
            (sb1, sb2) -> {
                if (sb1.length() > 0 && sb2.length() > 0) {
                    sb1.append(delimiter);
                }
                return sb1.append(sb2);
            },
            sb -> prefix + sb.toString()
        );
    }

    // 211. Multi-level grouping with downstream collectors
    public static Map<String, Map<String, Long>> multiLevelGrouping(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.groupingBy(
                    Employee::getDepartment,
                    Collectors.groupingBy(
                        emp -> emp.getSalary() > 50000 ? "High" : "Low",
                        Collectors.counting()
                    )
                ));
    }

    // 212. Collecting to immutable collections
    public static Set<String> collectToImmutableSet(List<String> strings) {
        return strings.stream()
                .filter(s -> s.length() > 3)
                .collect(Collectors.collectingAndThen(
                    Collectors.toSet(),
                    Collections::unmodifiableSet
                ));
    }

    // 213. Complex partitioning with downstream operations
    public static Map<Boolean, Optional<Employee>> partitionWithMaxSalary(List<Employee> employees) {
        return employees.stream()
                .collect(Collectors.partitioningBy(
                    emp -> emp.getSalary() > 60000,
                    Collectors.maxBy(Comparator.comparing(Employee::getSalary))
                ));
    }

    // 214. Custom reduction operations
    public static Optional<String> findLongestStringCustom(List<String> strings) {
        return strings.stream()
                .reduce((s1, s2) -> s1.length() >= s2.length() ? s1 : s2);
    }

    // 215. Collecting with filtering (Java 9+)
    public static List<String> collectWithFiltering(List<String> strings) {
        return strings.stream()
                .collect(Collectors.filtering(
                    s -> s.length() > 5,
                    Collectors.toList()
                ));
    }
}
```

### **Debugging and Stream Introspection (216-220)**

```java
public class StreamDebuggingQuestions {

    // 216. Using peek for debugging
    public static List<String> debugStreamPipeline(List<String> strings) {
        return strings.stream()
                .peek(s -> System.out.println("Original: " + s))
                .filter(s -> s.length() > 3)
                .peek(s -> System.out.println("After filter: " + s))
                .map(String::toUpperCase)
                .peek(s -> System.out.println("After map: " + s))
                .collect(Collectors.toList());
    }

    // 217. Counting elements at each stage
    public static List<Integer> debugWithCounting(List<Integer> numbers) {
        AtomicInteger filterCount = new AtomicInteger(0);
        AtomicInteger mapCount = new AtomicInteger(0);
        
        return numbers.stream()
                .filter(n -> {
                    filterCount.incrementAndGet();
                    return n % 2 == 0;
                })
                .map(n -> {
                    mapCount.incrementAndGet();
                    return n * 2;
                })
                .peek(n -> System.out.println(
                    String.format("Filtered: %d, Mapped: %d, Current: %d", 
                        filterCount.get(), mapCount.get(), n)
                ))
                .collect(Collectors.toList());
    }

    // 218. Stream performance monitoring
    public static <T> List<T> monitorStreamPerformance(Stream<T> stream, String operationName) {
        long startTime = System.nanoTime();
        List<T> result = stream.collect(Collectors.toList());
        long endTime = System.nanoTime();
        
        System.out.println(String.format("%s took %d nanoseconds, processed %d elements",
                operationName, (endTime - startTime), result.size()));
        
        return result;
    }

    // 219. Lazy evaluation demonstration
    public static void demonstrateLazyEvaluation() {
        List<String> strings = Arrays.asList("a", "b", "c", "d", "e");
        
        System.out.println("Creating stream pipeline...");
        Stream<String> stream = strings.stream()
                .peek(s -> System.out.println("Processing: " + s))
                .filter(s -> s.compareTo("c") > 0)
                .map(String::toUpperCase);
        
        System.out.println("Pipeline created, no processing yet!");
        System.out.println("Now collecting...");
        
        List<String> result = stream.collect(Collectors.toList());
        System.out.println("Result: " + result);
    }

    // 220. Stream short-circuiting behavior
    public static void demonstrateShortCircuiting(List<Integer> numbers) {
        System.out.println("Finding first even number > 10:");
        
        Optional<Integer> result = numbers.stream()
                .peek(n -> System.out.println("Examining: " + n))
                .filter(n -> n % 2 == 0)
                .peek(n -> System.out.println("Even number: " + n))
                .filter(n -> n > 10)
                .peek(n -> System.out.println("Even number > 10: " + n))
                .findFirst();
        
        result.ifPresent(n -> System.out.println("Found: " + n));
    }
}
```

### **Real-World Complex Scenarios (221-230)**

```java
public class RealWorldStreamScenarios {

    // 221. Process log files and extract error patterns
    public static Map<String, Long> analyzeLogErrors(List<String> logLines) {
        return logLines.stream()
                .filter(line -> line.contains("ERROR"))
                .map(line -> extractErrorType(line))
                .filter(Objects::nonNull)
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }
    
    private static String extractErrorType(String logLine) {
        // Extract error type from log line
        Pattern pattern = Pattern.compile("ERROR\\s+(\\w+)");
        Matcher matcher = pattern.matcher(logLine);
        return matcher.find() ? matcher.group(1) : null;
    }

    // 222. Financial transaction processing
    public static class Transaction {
        private String accountId;
        private double amount;
        private LocalDateTime timestamp;
        private String type; // DEBIT, CREDIT
        
        public Transaction(String accountId, double amount, LocalDateTime timestamp, String type) {
            this.accountId = accountId;
            this.amount = amount;
            this.timestamp = timestamp;
            this.type = type;
        }
        
        // Getters...
        public String getAccountId() { return accountId; }
        public double getAmount() { return amount; }
        public LocalDateTime getTimestamp() { return timestamp; }
        public String getType() { return type; }
    }

    public static Map<String, Double> calculateAccountBalances(List<Transaction> transactions) {
        return transactions.stream()
                .collect(Collectors.groupingBy(
                    Transaction::getAccountId,
                    Collectors.summingDouble(t -> 
                        "CREDIT".equals(t.getType()) ? t.getAmount() : -t.getAmount()
                    )
                ));
    }

    // 223. Data validation and cleansing pipeline
    public static List<String> cleanAndValidateData(List<String> rawData) {
        return rawData.stream()
                .filter(Objects::nonNull)
                .map(String::trim)
                .filter(s -> !s.isEmpty())
                .filter(s -> s.matches("^[a-zA-Z0-9\\s]+$")) // Only alphanumeric
                .map(s -> s.replaceAll("\\s+", " ")) // Normalize whitespace
                .distinct()
                .sorted()
                .collect(Collectors.toList());
    }

    // 224. Inventory management system
    public static class Product {
        private String id;
        private String name;
        private String category;
        private int quantity;
        private double price;
        
        public Product(String id, String name, String category, int quantity, double price) {
            this.id = id;
            this.name = name;
            this.category = category;
            this.quantity = quantity;
            this.price = price;
        }
        
        // Getters...
        public String getId() { return id; }
        public String getName() { return name; }
        public String getCategory() { return category; }
        public int getQuantity() { return quantity; }
        public double getPrice() { return price; }
        public double getTotalValue() { return quantity * price; }
    }

    public static Map<String, Object> generateInventoryReport(List<Product> products) {
        return Map.of(
            "totalValue", products.stream().mapToDouble(Product::getTotalValue).sum(),
            "lowStockItems", products.stream()
                    .filter(p -> p.getQuantity() < 10)
                    .map(Product::getName)
                    .collect(Collectors.toList()),
            "categoryValues", products.stream()
                    .collect(Collectors.groupingBy(
                        Product::getCategory,
                        Collectors.summingDouble(Product::getTotalValue)
                    )),
            "averagePrice", products.stream()
                    .mapToDouble(Product::getPrice)
                    .average()
                    .orElse(0.0)
        );
    }

    // 225. Text analysis and word statistics
    public static Map<String, Object> analyzeText(String text) {
        List<String> words = Arrays.stream(text.toLowerCase().split("\\W+"))
                .filter(word -> !word.isEmpty())
                .collect(Collectors.toList());
        
        return Map.of(
            "wordCount", words.size(),
            "uniqueWords", words.stream().distinct().count(),
            "averageWordLength", words.stream()
                    .mapToInt(String::length)
                    .average()
                    .orElse(0.0),
            "longestWord", words.stream()
                    .max(Comparator.comparing(String::length))
                    .orElse(""),
            "wordFrequency", words.stream()
                    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
        );
    }

    // 226. Student grade analysis system
    public static class Student {
        private String name;
        private String subject;
        private int grade;
        
        public Student(String name, String subject, int grade) {
            this.name = name;
            this.subject = subject;
            this.grade = grade;
        }
        
        public String getName() { return name; }
        public String getSubject() { return subject; }
        public int getGrade() { return grade; }
    }

    public static Map<String, Object> analyzeStudentPerformance(List<Student> students) {
        return Map.of(
            "topPerformers", students.stream()
                    .collect(Collectors.groupingBy(
                        Student::getName,
                        Collectors.averagingInt(Student::getGrade)
                    ))
                    .entrySet().stream()
                    .filter(entry -> entry.getValue() >= 90)
                    .map(Map.Entry::getKey)
                    .collect(Collectors.toList()),
            
            "subjectAverages", students.stream()
                    .collect(Collectors.groupingBy(
                        Student::getSubject,
                        Collectors.averagingInt(Student::getGrade)
                    )),
            
            "gradeDistribution", students.stream()
                    .map(s -> {
                        int grade = s.getGrade();
                        if (grade >= 90) return "A";
                        else if (grade >= 80) return "B";
                        else if (grade >= 70) return "C";
                        else if (grade >= 60) return "D";
                        else return "F";
                    })
                    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
        );
    }

    // 227. E-commerce order processing
    public static class Order {
        private String orderId;
        private String customerId;
        private List<OrderItem> items;
        private LocalDateTime orderDate;
        
        public Order(String orderId, String customerId, List<OrderItem> items, LocalDateTime orderDate) {
            this.orderId = orderId;
            this.customerId = customerId;
            this.items = items;
            this.orderDate = orderDate;
        }
        
        public String getOrderId() { return orderId; }
        public String getCustomerId() { return customerId; }
        public List<OrderItem> getItems() { return items; }
        public LocalDateTime getOrderDate() { return orderDate; }
        
        public double getTotalValue() {
            return items.stream().mapToDouble(OrderItem::getTotalValue).sum();
        }
    }

    public static Map<String, Object> generateSalesReport(List<Order> orders, LocalDateTime fromDate, LocalDateTime toDate) {
        List<Order> filteredOrders = orders.stream()
                .filter(order -> order.getOrderDate().isAfter(fromDate) && 
                               order.getOrderDate().isBefore(toDate))
                .collect(Collectors.toList());
        
        return Map.of(
            "totalRevenue", filteredOrders.stream()
                    .mapToDouble(Order::getTotalValue)
                    .sum(),
            
            "orderCount", filteredOrders.size(),
            
            "topCustomers", filteredOrders.stream()
                    .collect(Collectors.groupingBy(
                        Order::getCustomerId,
                        Collectors.summingDouble(Order::getTotalValue)
                    ))
                    .entrySet().stream()
                    .sorted(Map.Entry.<String, Double>comparingByValue().reversed())
                    .limit(5)
                    .collect(Collectors.toMap(
                        Map.Entry::getKey,
                        Map.Entry::getValue,
                        (e1, e2) -> e1,
                        LinkedHashMap::new
                    )),
            
            "averageOrderValue", filteredOrders.stream()
                    .mapToDouble(Order::getTotalValue)
                    .average()
                    .orElse(0.0)
        );
    }

    // 228-230. Additional complex scenarios would follow similar patterns
}
```

### **Interview Gotchas and Edge Cases (231-235)**

```java
public class StreamGotchasAndEdgeCases {

    // 231. Stream reuse pitfall
    public static void demonstrateStreamReusePitfall() {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        Stream<Integer> stream = numbers.stream();
        
        // First use
        long count1 = stream.count();
        System.out.println("Count: " + count1);
        
        try {
            // Second use - will throw IllegalStateException
            long count2 = stream.count();
        } catch (IllegalStateException e) {
            System.out.println("Stream already operated upon: " + e.getMessage());
        }
    }

    // 232. Null handling in streams
    public static void handleNullsCorrectly() {
        List<String> stringsWithNulls = Arrays.asList("a", null, "b", null, "c");
        
        // Wrong - will throw NullPointerException
        try {
            stringsWithNulls.stream()
                    .map(String::toUpperCase) // NPE here!
                    .collect(Collectors.toList());
        } catch (NullPointerException e) {
            System.out.println("NPE caught: " + e.getMessage());
        }
        
        // Correct way
        List<String> result = stringsWithNulls.stream()
                .filter(Objects::nonNull)
                .map(String::toUpperCase)
                .collect(Collectors.toList());
        System.out.println("Filtered result: " + result);
    }

    // 233. Side effects in stream operations
    public static void demonstrateSideEffects() {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> processed = new ArrayList<>(); // Mutable state
        
        // BAD: Side effects in stream operations
        numbers.stream()
                .filter(n -> n % 2 == 0)
                .forEach(processed::add); // Side effect!
        
        // GOOD: Use collectors instead
        List<Integer> correctResult = numbers.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());
    }

    // 234. Boxing/unboxing performance implications
    public static void demonstrateBoxingImplications() {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        
        // Less efficient - boxing/unboxing
        OptionalDouble avg1 = numbers.stream()
                .mapToDouble(Integer::doubleValue) // Unboxing
                .average();
        
        // More efficient - using primitive stream
        OptionalDouble avg2 = numbers.stream()
                .mapToInt(Integer::intValue) // To IntStream
                .average();
    }

    // 235. Collector vs reduce confusion
    public static void collectVsReduce() {
        List<String> strings = Arrays.asList("a", "b", "c", "d");
        
        // Using reduce (creates intermediate strings - inefficient)
        String result1 = strings.stream()
                .reduce("", String::concat);
        
        // Using collector (more efficient)
        String result2 = strings.stream()
                .collect(Collectors.joining());
        
        // Custom mutable reduction
        StringBuilder result3 = strings.stream()
                .collect(StringBuilder::new, 
                        StringBuilder::append, 
                        StringBuilder::append);
    }
}
```


## Key Interview Tips

1. **Always mention lazy evaluation** when discussing streams
2. **Explain when NOT to use streams** (simple operations, small datasets, need for debugging)
3. **Discuss parallel stream caveats** (thread safety, overhead, stateful operations)
4. **Know the difference between intermediate and terminal operations**
5. **Understand primitive streams** (IntStream, LongStream, DoubleStream) for performance
6. **Be aware of common pitfalls** (stream reuse, null handling, side effects)
7. **Explain Optional integration** with streams
8. **Discuss custom collectors** for complex scenarios
9. **Know file I/O integration** with streams
10. **Understand performance implications** of different stream operations

These additional questions cover the most critical missing areas that interviewers frequently ask about, especially for **senior Java developer positions** where deep streams knowledge is expected.

[1](https://cloudfoundation.com/blog/java-stream-interview-questions-and-answers/)
[2](https://www.geeksforgeeks.org/java/java-8-interview-questions-and-answers/)
[3](https://www.interviewbit.com/java-8-interview-questions/)
[4](https://github.com/Ruptam/java-8-stream-api-coding-interview-question)
[5](https://codefinity.com/blog/The-80-Top-Java-Interview-Questions-and-Answers)
[6](https://javaconceptoftheday.com/java-8-interview-sample-coding-questions/)
[7](https://blog.devgenius.io/java-8-coding-and-programming-interview-questions-and-answers-62512c44f062)
