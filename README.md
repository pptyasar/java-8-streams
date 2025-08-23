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

I'll continue with the remaining solutions in the next parts. Would you like me to continue with solutions 48-182? The pattern follows similar stream operations with increasing complexity for collections, file I/O, and custom collectors.

**Key Patterns Used:**
- `collect(Collectors.groupingBy())` for frequency counting
- `filter()` and `map()` for transformations
- `sorted()` with custom comparators
- `partitioningBy()` for boolean-based grouping
- `reduce()` for aggregations
- `flatMap()` for flattening operations

Would you like me to continue with the remaining solutions?
