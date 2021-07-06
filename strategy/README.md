# Strategy
## 1. Khái niệm
`Strategy Pattern` là một trong những Pattern thuộc nhóm hành vi (Behavior Pattern). Nó cho phép định nghĩa tập hợp các thuật toán, đóng gói từng thuật toán lại, và dễ dàng thay đổi linh hoạt các thuật toán bên trong object. Strategy cho phép thuật toán biến đổi độc lập khi người dùng sử dụng chúng.
## 2. Cách sử dụng
![strategy diagram](https://gpcoder.com/wp-content/uploads/2019/01/design-patterns-strategy-diagram.png)
Các thành phần tham gia Strategy Pattern:

- `Strategy`: định nghĩa các hành vi có thể có của một Strategy.
- `ConcreteStrategy`: cài đặt các hành vi cụ thể của Strategy.
- `Context`: chứa một tham chiếu đến đối tượng Strategy và nhận các yêu cầu từ Client, các yêu cầu này sau đó được ủy quyền cho Strategy thực hiện.
> Ví dụ

>Strategy.java
```java
    public interface Strategy {
        public int algorithm(int num1, int num2);
    }
```

>AddStrategy.java
```java
    public class AddStrategy implements Strategy{
        @Override
        public int algorithm(int num1, int num2) {
            return num1 + num2;
        }
    }
```
>SubstractStrategy.java
```java
    public class SubstractStrategy implements Strategy{
        @Override
        public int algorithm(int num1, int num2) {
            return num1 - num2;
        }
    }
```
>MultiplyStrategy.java
```java
    public class MultiplyStrategy implements Strategy{
        @Override
        public int algorithm(int num1, int num2) {
            return num1 * num2;
        }
    }
```

>Context.java
```java
    public class Context {
        private Strategy strategy;

        public Context(Strategy strategy){
            this.strategy = strategy;
        }

        public int executeStrategy(int num1, int num2){
            return strategy.algorithm(num1, num2);
        }
    }
```
>StrategyPatternDemo.java
```java
    public class StrategyPatternDemo {
        public static void main(String[] args) {
            Context context = new Context(new AddStrategy());		
            System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

            context = new Context(new SubstractStrategy());		
            System.out.println("10 - 5 = " + context.executeStrategy(10, 5));

            context = new Context(new MultiplyStrategy());		
            System.out.println("10 * 5 = " + context.executeStrategy(10, 5));
        }
    }
```
>Output
```
    10 + 5 = 15
    10 - 5 = 5
    10 * 5 = 50
```

## 3. Lợi ích
- Đảm bảo nguyên tắc Single responsibility principle (SRP) : một lớp định nghĩa nhiều hành vi và chúng xuất hiện dưới dạng với nhiều câu lệnh có điều kiện. Thay vì nhiều điều kiện, chúng ta sẽ chuyển các nhánh có điều kiện liên quan vào lớp Strategy riêng lẻ của nó.
- Đảm bảo nguyên tắc Open/Closed Principle (OCP) : chúng ta dễ dàng mở rộng và kết hợp hành vi mới mà không thay đổi ứng dụng.
- Cung cấp một sự thay thế cho kế thừa.
## 4. Sử dụng Strategy Pattern khi nào?
- Khi muốn có thể thay đổi các thuật toán được sử dụng bên trong một đối tượng tại thời điểm run-time.
- Khi có một đoạn mã dễ thay đổi, và muốn tách chúng ra khỏi chương trình chính để dễ dàng bảo trì.
- Tránh sự rắc rối, khi phải hiện thực một chức năng nào đó qua quá nhiều lớp con.
- Cần che dấu sự phức tạp, cấu trúc bên trong của thuật toán.

## Tham khảo

https://gpcoder.com/4796-huong-dan-java-design-pattern-strategy/