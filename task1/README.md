# Задача 1: Калькулятор

## Класс 'Main'
```java
public class Main {
    public static void main(String[] args) {
        Calculator calc = Calculator.instance.get();

        int a = calc.plus.apply(1, 2);
        int b = calc.minus.apply(1, 1);
        int c = calc.devide.apply(a, b); // ошибка 'деление на ноль'

        calc.println.accept(c);

    }
}
```

## Класс 'Calculator' 
```java
import java.util.function.*;

public class Calculator {



    static Supplier<Calculator> instance = Calculator::new;
    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x*y;
    BinaryOperator<Integer> devide = (x, y) -> x/y;
    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;
    Predicate<Integer> isPositive = x -> x > 0;
    Consumer<Integer> println = System.out::println;
}
```
## Реализация с обработкой ошибки:
```java
import java.util.function.*;

public class Calculator {



    static Supplier<Calculator> instance = Calculator::new;
    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x*y;
    BinaryOperator<Integer> devide = (x, y) -> {
        try {
            return x / y;
        } catch (Exception e) {
            System.out.println("Делить на ноль нельзя!");
            return 0;
        }
    };
    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;
    Predicate<Integer> isPositive = x -> x > 0;
    Consumer<Integer> println = System.out::println;
}
```