# Facade
## 1. Khái niệm
`Facade Pattern` là một trong những Pattern thuộc nhóm cấu trúc (Structural Pattern). Pattern này cung cấp một giao diện chung đơn giản thay cho một nhóm các giao diện có trong một hệ thống con (subsystem). Facade Pattern định nghĩa một giao diện ở một cấp độ cao hơn để giúp cho người dùng có thể dễ dàng sử dụng hệ thống con này.

`Facade Pattern` cho phép các đối tượng truy cập trực tiếp giao diện chung này để giao tiếp với các giao diện có trong hệ thống con. Mục tiêu là che giấu các hoạt động phức tạp bên trong hệ thống con, làm cho hệ thống con dễ sử dụng hơn.

|![Without Facade](https://gpcoder.com/wp-content/uploads/2018/11/facade-1.png)|![With facade](https://gpcoder.com/wp-content/uploads/2018/11/facade-2.png)|
|:--------------:|:-----------:|
| Without Facade | With Facade |

## 2. Cách sử dụng
![facade diagram](https://gpcoder.com/wp-content/uploads/2018/11/design-patterns-facade-diagram.png)

Các thành phần cơ bản của một `Facade Pattern`:

- `Facade`: biết rõ lớp của hệ thống con nào đảm nhận việc đáp ứng yêu cầu của client, sẽ chuyển yêu cầu của client đến các đối tượng của hệ thống con tương ứng.
- `Subsystems`: cài đặt các chức năng của hệ thống con, xử lý công việc được gọi bởi Facade. Các lớp này không cần biết Facade và không tham chiếu đến nó.
- `Client`: đối tượng sử dụng Facade để tương tác với các subsystem.

Các đối tượng `Facade` thường là `Singleton` bởi vì chỉ cần duy nhất một đối tượng Facade.

> Ví dụ

> Shape.java
```java
    public interface Shape {
    void draw();
    }
```
>Tạo Subsystem

>Rectangle.java
```java
    public class Rectangle implements Shape {

    @Override
    public void draw() {
        System.out.println("Rectangle::draw()");
    }
    }
```
>Square.java
```java
    public class Square implements Shape {

    @Override
    public void draw() {
        System.out.println("Square::draw()");
    }
    }
```
>Circle.java
```java
    public class Circle implements Shape {

    @Override
    public void draw() {
        System.out.println("Circle::draw()");
    }
    }
```
>ShapeFacade.java
```java
    public class ShapeFace {
        private static final ShapeFacade INSTANCE = new ShapeFacade();

        private Shape circle;
        private Shape rectangle;
        private Shape square;
    
        public ShapeFacade() {
            circle = new Circle();
            rectangle = new Rectangle();
            square = new Square();
        }
        public static ShapeFacade getInstance() {
            return INSTANCE;
        }

        public void drawCircle(){
            circle.draw();
        }
        public void drawRectangle(){
            rectangle.draw();
        }
        public void drawSquare(){
            square.draw();
        }
    }
```
> Client.java

```java
    public class Client {
        public static void main(String[] args) {
            ShapeFacade.getInstance().drawCircle();
            ShapeFacade.getInstance().drawRectangle();
            ShapeFacade.getInstance().drawSquare();		
        }
    }
```
>Output
```
    Circle::draw()
    Rectangle::draw()
    Square::draw()
```
## 3. Lợi ích
- Tạo ra một giao diện đơn giản cho người sử dụng một hệ thống phức tạp.
- Tăng khả năng độc lập và khả chuyển.
- Giảm sự phụ thuộc.
- Che dấu tính phức tạp.

## Tham khảo

https://gpcoder.com/4604-huong-dan-java-design-pattern-facade/