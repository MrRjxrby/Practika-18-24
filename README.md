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

# Задание 2
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

```
package com.mycompany.onlinepurchase;

import java.util.Scanner;

class InvalidInn extends Exception {
    public InvalidInn(String message) {
        super(message);
    }
}

public class OnlinePurchase {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            System.out.print("Enter your full name: ");
            String fullName = scanner.nextLine();

            System.out.print("Enter your INN: ");
            String inn = scanner.nextLine();

            
            validateINN(inn);

            System.out.println("Purchase completed successfully for " + fullName);
        } catch (InvalidInn e) {
            System.out.println("Error: " + e.getMessage());
        } finally {
            scanner.close();
        }
    }

    public static void validateINN(String inn) throws InvalidInn {
        if (inn == null || !inn.matches("\\d{12}")) {
            throw new InvalidInn("Invalid INN, please enter Correct IN.");
        }
    }
}
```
# Практика 20: 
Задание 1 и 2:
```
package com.mycompany.triple;
public class Triple<T, V, K> {
    private T first;
    private V second;
    private K third;

    public Triple(T first, V second, K third) {
        this.first = first;
        this.second = second;
        this.third = third;
    }

    public T getFirst() {
        return first;
    }

    public V getSecond() {
        return second;
    }

    public K getThird() {
        return third;
    }

    // Метод для вывода имён классов
    public void printClassNames() {
        System.out.println("Type of T: " + first.getClass().getName());
        System.out.println("Type of V: " + second.getClass().getName());
        System.out.println("Type of K: " + third.getClass().getName());
    }

    // Пример использования
    public static void main(String[] args) {
        Triple<Integer, String, Double> triple = new Triple<>(42, "Hello", 3.14);
        System.out.println("First: " + triple.getFirst());
        System.out.println("Second: " + triple.getSecond());
        System.out.println("Third: " + triple.getThird());
        triple.printClassNames();
    }
}
```
Задание 5:
```
import java.util.Arrays;

public class Matrix<T extends Number> {
    private T[][] data;

    public Matrix(T[][] data) {
        this.data = data;
    }

    public int getRows() {
        return data.length;
    }

    public int getColumns() {
        return data[0].length;
    }

    public T getElement(int row, int col) {
        return data[row][col];
    }

    public Matrix<T> add(Matrix<T> other) {
        if (this.getRows() != other.getRows() || this.getColumns() != other.getColumns()) {
            throw new IllegalArgumentException("Matrices must have the same dimensions for addition.");
        }

        Number[][] result = new Number[getRows()][getColumns()];
        for (int i = 0; i < getRows(); i++) {
            for (int j = 0; j < getColumns(); j++) {
                result[i][j] = this.getElement(i, j).doubleValue() + other.getElement(i, j).doubleValue();
            }
        }
        return new Matrix<>((T[][]) result);
    }

    public Matrix<T> multiply(Matrix<T> other) {
        if (this.getColumns() != other.getRows()) {
            throw new IllegalArgumentException("Matrices dimensions do not match for multiplication.");
        }

        Number[][] result = new Number[getRows()][other.getColumns()];
        for (int i = 0; i < getRows(); i++) {
            for (int j = 0; j < other.getColumns(); j++) {
                double sum = 0.0;
                for (int k = 0; k < this.getColumns(); k++) {
                    sum += this.getElement(i, k).doubleValue() * other.getElement(k, j).doubleValue();
                }
                result[i][j] = sum;
            }
        }
        return new Matrix<>((T[][]) result);
    }

    public void printMatrix() {
        for (T[] row : data) {
            System.out.println(Arrays.toString(row));
        }
    }

    public static void main(String[] args) {
        Integer[][] data1 = {{1, 2, 3}, {4, 5, 6}};
        Integer[][] data2 = {{7, 8}, {9, 10}, {11, 12}};
        Integer[][] data3 = {{1, 1, 1}, {1, 1, 1}};

        Matrix<Integer> matrix1 = new Matrix<>(data1);
        Matrix<Integer> matrix2 = new Matrix<>(data2);
        Matrix<Integer> matrix3 = new Matrix<>(data3);

        System.out.println("Matrix 1:");
        matrix1.printMatrix();

        System.out.println("Matrix 2:");
        matrix2.printMatrix();

        System.out.println("Matrix 3:");
        matrix3.printMatrix();

        System.out.println("Matrix 1 * Matrix 2:");
        Matrix<Integer> result1 = matrix1.multiply(matrix2);
        result1.printMatrix();

        System.out.println("Matrix 1 + Matrix 3:");
        Matrix<Integer> result2 = matrix1.add(matrix3);
        result2.printMatrix();
    }
}
```
# Практика 22 
Задание 1
```
package com.mycompany.rpncalculator;

import java.util.Stack;
import java.util.Scanner;

public class RPNCalculator {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter expression:");
        String input = scanner.nextLine();

        try {
            double result = evaluateRPN(input);
            System.out.println("Result: " + result);
        } catch (IllegalArgumentException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }

    public static double evaluateRPN(String expression) {
        Stack<Double> stack = new Stack<>();
        String[] tokens = expression.split(" ");

        for (String token : tokens) {
            if (isNumber(token)) {
                stack.push(Double.parseDouble(token));
            } else if (isOperator(token)) {
                if (stack.size() < 2) {
                    throw new IllegalArgumentException("Not enought numbers: " + token);
                }
                double b = stack.pop();
                double a = stack.pop();
                double result = applyOperation(a, b, token);
                stack.push(result);
            } else {
                throw new IllegalArgumentException("Incorrect input: " + token);
            }
        }

        if (stack.size() != 1) {
            throw new IllegalArgumentException("Incorrect input.");
        }

        return stack.pop();
    }

    private static boolean isNumber(String token) {
        try {
            Double.parseDouble(token);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }

    private static boolean isOperator(String token) {
        return token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/");
    }

    private static double applyOperation(double a, double b, String operator) {
        switch (operator) {
            case "+":
                return a + b;
            case "-":
                return a - b;
            case "*":
                return a * b;
            case "/":
                if (b == 0) {
                    throw new IllegalArgumentException("Division by Zero.");
                }
                return a / b;
            default:
                throw new IllegalArgumentException("Unknown operator: " + operator);
        }
    }
}
```
# Практика 23
Задание 1
Файл ArrayQueueModule(очередь с использованием статических переменных):
```
package com.mycompany.queue;

public class ArrayQueue {
    private Object[] elements;
    private int size;
    private int head;
    private int tail;

    public ArrayQueue() {
        elements = new Object[10];
        size = 0;
        head = 0;
        tail = 0;
    }

    public void enqueue(Object element) {
        assert element != null;
        ensureCapacity(size + 1);
        elements[tail] = element;
        tail = (tail + 1) % elements.length;
        size++;
    }

    public Object element() {
        assert size > 0;
        return elements[head];
    }

    public Object dequeue() {
        assert size > 0;
        Object result = elements[head];
        elements[head] = null;
        head = (head + 1) % elements.length;
        size--;
        return result;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void clear() {
        elements = new Object[10];
        size = 0;
        head = 0;
        tail = 0;
    }

    private void ensureCapacity(int capacity) {
        if (capacity > elements.length) {
            Object[] newElements = new Object[2 * elements.length];
            for (int i = 0; i < size; i++) {
                newElements[i] = elements[(head + i) % elements.length];
            }
            elements = newElements;
            head = 0;
            tail = size;
        }
    }
}
```
Файл ArrayQueueADT(очередь, как абстрактный типа данных):
```
package com.mycompany.queue;

public class ArrayQueueADT {
    private Object[] elements;
    private int size;
    private int head;
    private int tail;

    public ArrayQueueADT() {
        elements = new Object[10];
        size = 0;
        head = 0;
        tail = 0;
    }

    public static void enqueue(ArrayQueueADT queue, Object element) {
        assert element != null;
        ensureCapacity(queue, queue.size + 1);
        queue.elements[queue.tail] = element;
        queue.tail = (queue.tail + 1) % queue.elements.length;
        queue.size++;
    }

    public static Object element(ArrayQueueADT queue) {
        assert queue.size > 0;
        return queue.elements[queue.head];
    }

    public static Object dequeue(ArrayQueueADT queue) {
        assert queue.size > 0;
        Object result = queue.elements[queue.head];
        queue.elements[queue.head] = null;
        queue.head = (queue.head + 1) % queue.elements.length;
        queue.size--;
        return result;
    }

    public static int size(ArrayQueueADT queue) {
        return queue.size;
    }

    public static boolean isEmpty(ArrayQueueADT queue) {
        return queue.size == 0;
    }

    public static void clear(ArrayQueueADT queue) {
        queue.elements = new Object[10];
        queue.size = 0;
        queue.head = 0;
        queue.tail = 0;
    }

    private static void ensureCapacity(ArrayQueueADT queue, int capacity) {
        if (capacity > queue.elements.length) {
            Object[] newElements = new Object[2 * queue.elements.length];
            for (int i = 0; i < queue.size; i++) {
                newElements[i] = queue.elements[(queue.head + i) % queue.elements.length];
            }
            queue.elements = newElements;
            queue.head = 0;
            queue.tail = queue.size;
        }
    }
}
```
Файл ArrayQueue(очередь, как объектно-ориентированный класс):
```
package com.mycompany.queue;

public class ArrayQueue {
    private Object[] elements;
    private int size;
    private int head;
    private int tail;

    public ArrayQueue() {
        elements = new Object[10];
        size = 0;
        head = 0;
        tail = 0;
    }

    public void enqueue(Object element) {
        assert element != null;
        ensureCapacity(size + 1);
        elements[tail] = element;
        tail = (tail + 1) % elements.length;
        size++;
    }

    public Object element() {
        assert size > 0;
        return elements[head];
    }

    public Object dequeue() {
        assert size > 0;
        Object result = elements[head];
        elements[head] = null;
        head = (head + 1) % elements.length;
        size--;
        return result;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void clear() {
        elements = new Object[10];
        size = 0;
        head = 0;
        tail = 0;
    }

    private void ensureCapacity(int capacity) {
        if (capacity > elements.length) {
            Object[] newElements = new Object[2 * elements.length];
            for (int i = 0; i < size; i++) {
                newElements[i] = elements[(head + i) % elements.length];
            }
            elements = newElements;
            head = 0;
            tail = size;
        }
    }
}
```
Файл Queue(Main):
```
package com.mycompany.queue;

public class Queue {
    public static void main(String[] args) {
        // Пример использования ArrayQueueModule
        ArrayQueueModule.enqueue("AC");
        ArrayQueueModule.enqueue("BT");
        System.out.println(ArrayQueueModule.dequeue()); 
        System.out.println(ArrayQueueModule.element()); 

        // Пример использования ArrayQueueADT
        ArrayQueueADT queueADT = new ArrayQueueADT();
        ArrayQueueADT.enqueue(queueADT, "XS");
        ArrayQueueADT.enqueue(queueADT, "YZ");
        System.out.println(ArrayQueueADT.dequeue(queueADT)); 
        System.out.println(ArrayQueueADT.element(queueADT)); 

        // Пример использования ArrayQueue
        ArrayQueue queue = new ArrayQueue();
        queue.enqueue("21");
        queue.enqueue("25");
        System.out.println(queue.dequeue()); 
        System.out.println(queue.element()); 
    }
}
```
# Практика 24
Задание 1
Файл Complex:
```
package com.mycompany.factory;

public class Complex {
    private int real;  
    private int imaginary; 

    public Complex(int real, int imaginary) {
        this.real = real;
        this.imaginary = imaginary;
    }

    public int getReal() {
        return real;
    }

    public int getImaginary() {
        return imaginary;
    }

    @Override
    public String toString() {
        return real + " + " + imaginary + "i";
    }
}
```
Файл ConcreteFactory:
```
package com.mycompany.factory;

public class ConcreteFactory implements ComplexAbstractFactory {

    @Override
    public Complex createComplex() {
        return new Complex(0, 0);
    }

    @Override
    public Complex createComplex(int real, int imaginary) {
        return new Complex(real, imaginary);
    }
}
```
Файл ComplexAbstractFactory:
```
package com.mycompany.factory;

public interface ComplexAbstractFactory {
    Complex createComplex();
    Complex createComplex(int real, int imaginary);
}
```
Файл Factory(Main):
```
package com.mycompany.factory;

public class Factory {
    public static void main(String[] args) {
        ComplexAbstractFactory factory = new ConcreteFactory();

        Complex defaultComplex = factory.createComplex();
        System.out.println("Default Complex Number: " + defaultComplex);

        Complex customComplex = factory.createComplex(9, 2);
        System.out.println("Custom Complex Number: " + customComplex);
    }
}
```
