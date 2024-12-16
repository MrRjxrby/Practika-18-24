# Practika-18-24
# 18 практика
# Задание 1
Шаг 1 -  программа выдаст сбой, а именно выдаст ошибку "java.lang.ArithmeticException: / by zero", которая показывает, что деление целых чисел на ноль в Java не возможно (Она автоматических определяет это как недопустимую операцию), так же как и в простой математике.
Шаг 2:
```
public class Exception1 {  
    public void exceptionDemo() {  
        System.out.println(2.0 / 0.0);  
    }  
}
```
При запуске программа выведет - infinity (бесконечность). Если в Java используются числа с плавующей точкой, т.п double, она будет использовать стандарт IEEE 754 для выполнения арифметических действий.

Шаг 3:
```
public class Exception1 {  
    public void exceptionDemo() {  
        try {  
            System.out.println(2 / 0);  
        } catch (ArithmeticException e) {  
            System.out.println("Attempted division by zero");  
        }  
    }  
}
```
В этом случае, программа не выдаст сбой, а вместо этого выдаст в консоль: "Attempted division by zero". Блок Try-Catch будет перехватывать ошибку при делении на ноль и не давать программе завершится аварийно.

#Задание 2
Шаг 1:
```
import java.util.Scanner;

public class Exception2 {  
    public void exceptionDemo() {  
        Scanner myScanner = new Scanner(System.in);  
        System.out.print("Enter an integer: "); 
        String intString = myScanner.next(); 
        int i = Integer.parseInt(intString);  
        System.out.println(2 / i);  
    }  
}
```
Результат для различных входны данных:
1) Qwerty:
Исключение: java.lang.NumberFormatException
Причиной будет являться то, что Qwerty не может быть преобразовано в целое число.
2) 0:
Так же, как и с прошлым заданием, будет идти исключение: "java.lang.ArithmeticException: / by zero" и причиной этого, станет деление на ноль.
3) 1.2: 
Исключение: java.lang.NumberFormatException
"1.2" - не является допустимым целым числом.
4) 1:
Результат: 2, программа будет корректно выполнять деление.
Шаг 2:
```
import java.util.Scanner;

public class Exception2 {  
    public void exceptionDemo() {  
        Scanner myScanner = new Scanner(System.in);  
        System.out.print("Enter an integer: "); 
        try {  
            String intString = myScanner.next(); 
            int i = Integer.parseInt(intString);  
            System.out.println(2 / i);  
        } catch (NumberFormatException e) {  
            System.out.println("Invalid input. Please enter an integer.");  
        } catch (ArithmeticException e) {  
            System.out.println("Division by zero is not allowed.");  
        }  
    }  
}
```
Результат выполнений:
1) Qwerty:
Вывод: Invalid input. Please enter an integer
Исключение NumberFormatException обрабатывается блоком catch.
2) 0:
Вывод: Division by zero is not allowed.
Исключение ArithmeticException обрабатывается блоком catch.
3) 1.2: 
Вывод: Invalid input. Please enter an integer.
Исключение NumberFormatException обрабатывается блоком catch.
4) 1:
Результат: 2, программа будет корректно выполнять деление.

# Практика 19

