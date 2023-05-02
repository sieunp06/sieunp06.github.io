---
title:  "☕ [Java] 까먹지말자 stream 총정리"
search: false
categories: 
  - Java
tag:
  - Java
toc: true
---

> 까먹지 말자 Java stream

<br>

# java.util.stream

Java 8부터 추가된 stream 클래스입니다. 

## Method

## stream 생성하기
### 배열 스트림
`Stream.of()`나 `Arrays.stream()`을 사용하여 만들 수 있습니다.
- Stream.of()
  ```java
  Stream<String> streamOfArray = Stream.of("a", "b", "c");
  ```
  
- Arrays.stream()
  ```java
  String[] arr = new String[]{"a", "b", "c"};

  Stream<String> streamOfArrayFull = Arrays.stream(arr);
  Stream<String> streamOfArrayPart = Arrays.stream(arr, 1, 3);    // [b, c]
  ```

### 컬렉션 스트림
`Collection 인터페이스`에는 `stream`이 정의되어 있기 떄문에 Collection 타입에는 `stream`을 사용할 수 있습니다.
```java
Collection<String> collection = Arrays.asList("a", "b", "c");
Stream<String> streamOfCollection = collection.stream();
```

### 비어 있는 스트림 생성
```java
Stream<String> streamEmpty = Stream.empty();
```

### Stream.builder();
`Stream.builder()`를 사용하여 원하는 값을 stream에 넣을 수 있습니다.
```java
Stream<String> streamBuilder = 
      Stream.<String>builder().add("a").add("b").add("c").build();
```

### Stream.generate()
`stream.generate()`은 람다식을 사용해서 stream을 생성한다.

하지만 `stream.generate()`를 사용하면 무한대로 만들어지기 때문에 `limit()`을 사용하여 크기를 제한해야 합니다.
```java
Stream<String> streamGenerated = 
      Stream.generate(() -> "element").limit(5);
```
`element`를 5개 생성하는 코드입니다.

### Stream.iterate()
`iterate()`는 초기값과 스트림에 들어갈 요소를 만듭니다.
```java
Stream<Integer> streamIterated = Stream.iterate(40, n -> n + 2).limit(20);
```
초기값을 40을 가지고 초기값에서 2씩 커지는 요소들이 들어갑니다.

무한대로 만들어지기 때문에 `limit()`을 통해 크기를 제한해야합니다.

### 원시 Stream 생성
Stream 외에도 `int`, `long`, `double` 같은 원시 자료형들을 사용하기 위해 `IntStream`, `LongStream`, `DoubleStream`을 사용하면 됩니다.

```java
IntStream stream = IntStream.range(1, 5); // [1, 2, 3, 4]
LongStream longStream = LongStream.range(1, 3); // [1, 2]
LongStream longStreamRangeClosed = LongStream.rangeClose(1, 3); // [1, 2, 3]
```
- `range(int StartInclusive, int endExclusive)`
- `range(int startInclusive, int endInclusive)`

```java
Random random = new Random();
DoubleStream doubleStream = random.doubles(3);
```
3개의 난수를 생성할 수도 있습니다.

### 문자열 스트림
```java
IntStream streamOfChars = "abc".chars(); // [97, 98, 99] 
```
`chars()`를 사용해서 문자열을 분리해 stream에 넣습니다.

이때 `IntStream`으로 변환됩니다.

```java
Stream<String> streamOfString = 
      Pattern.compile(", ").splitAsStream("a, b, c");
```
`a, b, c`을 `, `로 스플릿해 stream으로 넣습니다.

### 파일 스트림
```java
Path path = Paths.get("C:\\file.txt");
Stream<String> streamOfStrings = Files.lines(path);
Stream<String> streamWithCharset = 
      Files.lines(path, Charset.forName("UTF-8"));
```
`lines()`를 사용해 `file.txt`을 각 라인을 스트링 타입 스트링으로 만듭니다.

## stream 가공하기
### Concating
`concat()`을 사용하면 두 개의 스트림을 연결할 수 있습니다.
```java
Stream<String> stream1 = stream.of("a", "b", "c");
Steram<String> stream2 = stream.of("d", "e", "f");

Stream<String> concat = Steam.concat(steam1, stream2);
```

### Iterating
```java
for (String string : list) {
  if (string.contains("a"))
    return true;
}
```
이 코드를 stream을 사용하면 한 줄로 바꿀 수 있습니다.
```java
boolean isExist = list.stream().anyMatch(element -> element.contains("a"));
```
### Filtering
`filter()`를 사용하면 특정 요소를 찾을 수 있습니다.
```java
ArrayList<String> list = new ArrayList<>();
list.add("One");
list.add("OneAndOnly");
list.add("Derek");
list.add("Change");
list.add("factory");
list.add("justBefore");
list.add("Italy");
list.add("Italy");
list.add("Thursday");
list.add("");
list.add("");
```
이 `ArrayList`에서 `d`를 포함하는 요소를 걸러내 새 스트림을 만들 수 있습니다.
```java
Stream<String> stream = list.stream().filter(element -> element.contains("d"));
```

### Mapping
```java
Stream<String> stream = 
            names.stream()
            .map(String::toUpperCase);
```
스트림 내의 `String`에 `toUpperCase()`를 실행해서 stream으로 리턴합니다.

```java
Stream<Integer> stream = IntStream.range(1, 10).boxed();
stream.filter(element -> (element % 2 == 0))
      .map(element -> v * 10)
      .forEach(System.out::println);
```
1부터 9까지 `filter()`를 이용해 짝수만 뽑아내고, `map()`을 통해 10배를 한 후 이를 출력합니다.

### Matching
`Matching`은 조건에 맞는 요소가 있는지 확인하고 `boolean`을 리턴합니다.

- `anyMatch` : 하나라도 조건을 만족하는 요소가 있는지 확인함.
- `allMatch` : 모든 요소가 조건을 만족하는지 확인함.
- `noneMatch` : 모든 요소가 조건을 만족하지 않는지 확인함.

```java
boolean isValid = list.stream().anyMatch(element -> element.contains("h")); // true
boolean isValidOne = list.stream().allMatch(element -> element.contains("h")) // false
boolean isValidTwo = list.stream().noneMatch(element -> element.contains("h"));  // flase
```

빈 스트림에 `allMatch()`를 사용하면 항상 `true`를 리턴합니다.

### Sorting
- `오름차순` 정렬
  
  인자가 없으면 오름차순 정렬을 합니다.
  ```java
  Intstream.of(18, 14, 15, 11, 40)
           .sorted() 
           .boxed()
           .collect(Collectors.toList());
  ```
- `내림차순` 정렬
  ```java
  Intstream.of(18, 14, 15, 11, 40)
           .sorted(Comparator.reverseOrder()) 
           .boxed()
           .collect(Collectors.toList());
  ```

문자열 길이로 정렬하는 코드입니다.
```java
List<String> language = Arrays.asList("Java", "Scala", "Groovy", "Python", "Go", "Swift");

language.steam()
        .sorted(Comparator.comparingInt(String::length))
        .collect(Collectors.toList());
```

```java
language.steam() 
        .sorted((s1, s2) -> s2.length() - s1.length())
        .collect(Collectors.toList());
```

### Peek
`map`과 같은 역할을 하지만, stream을 리턴하는 `map`과 다르게 `peek`은 작업을 수행만 하고 이를 반영하지는 않습니다.

```java
int sum = IntStream.of(1, 3, 5, 7, 9)
                   .peek(System.out::println)
                   .sum();
```

## stream 결과 만들기
### Calculating
- `count` & `sum`
  빈 스트림인 경우 `0`을 리턴합니다.
  ```java
  long count = IntStream.of(1, 3, 5).count();
  long sum = IntStream.of(1, 3, 5).sum();
  ```
- `min` & `max` & `average`
  빈 스트림인 경우 Optional을 사용해 리턴합니다.
  ```java
  int min = IntStream.of(1, 3, 5).min();
  int max = IntStream.of(1, 3, 5).max();
  int average = IntStream.of(1, 3, 5).average();
  ```

### Reduce
`reduce()`를 사용해서 stream의 결과를 만들 수 있습니다.

`reduce()`는 파라미터에 따라 세 가지로 나눌 수 있습니다.

```java
// 1개 (accumulator)
Optional<T> reduce(BinaryOperator<T> accumulator)

// 2개 (identity)
T reduce(T identity, BinaryOperator<T> accumulator)
```

- 인자가 `1개`인 경우
  ```java
  Optional<T> reduce(BinaryOperator<T> accumulator)
  ```
  ```java
  OptionalInt reduced = IntStream.range(1, 10)
                                 .reduce((a, b) -> {
                                    return Integer.sum(a, b);
                                 })
  ```
- 인자가 `2개`인 경우
  ```java
  T reduce(T identity, BinaryOperator<T> accumulator)
  ```
  ```java
  int reducedTwoParams = IntStream.range(1, 10)
                                  .reduce(10, Integer::sum);
  ```

## Collect
### Collectors.toList()
스트림을 리스트로 변환합니다.

### Collectors.joining()
스트림에서 작업한 결과를 하나의 스트링으로 이어 붙일 수 있습니다.
```java
List<String> languages = Arrays.asList("Banana", "Apple", "Melon");
String languageJoining = language.stream()
                                 .collect(Collectors.joining());
```
```
BananaAppleMelon
```

`Collections.joining`에는 세 개의 파라미터를 사용할 수 있습니다.

- `delimiter` : 각 요소 중간에 들어갈 구분자
- `prefix` : 결과 맨 앞에 붙는 문자
- `suffix` : 결과 맨 뒤에 분는 문자

```java
List<String> languages = Arrays.asList("Banana", "Apple", "Melon");
String languageJoining = language.stream()
                                 .collect(Collectors.joining(", ", "<", ">"));
```
```
<Banana, Apple, Melon>
```

### Collectors.counting()
`Collectors.counting()`을 사용해 스트림 요소들의 개수를 셀 수 있습니다.
```java
Long result = givenList.stream()
                       .collect(Collectors.counting());
```

### Collectors.summarizingDouble/Long/Int()
스트림의 통계적인 수치들(평균, 개수, 최대, 최소, 합)을 확인할 수 있습니다.
```java
DoubleSummaryStatistics result = givenList.stream()
                                          .collect(summarizingDouble(String::length));
```
```java
assertThat(result.getAverage()).isEqualTo(2);
assertThat(result.getCount()).isEqualTo(4);
assertThat(result.getMax()).isEqualTo(3);
assertThat(result.getMin()).isEqualTo(1);
assertThat(result.getSum()).isEqualTo(8);
```

### Collectors.avergingDouble/Long/Int()
스트림 내 요소들의 평균값을 알 수 있습니다.
```java
Double averageAmount = givenList.stream()
                                .collect(Collectors.averageInt())
```

### Collections.summingDouble/Long/Int()
스트림 내 요소들의 합을 알 수 있습니다.
```java
Double result = givenList.stream()
                         .collect(summingDouble(String::length));
```

# Reference
- https://www.baeldung.com/java-8-streams
- https://www.baeldung.com/java-8-streams-introduction
- https://www.baeldung.com/java-8-collectors
- https://futurecreator.github.io/2018/08/26/java-8-streams/
- https://hbase.tistory.com/171
