# Observer
## 1. Khái niệm
`Observer Pattern` là một trong những Pattern thuộc nhóm hành vi (Behavior Pattern). Nó định nghĩa mối phụ thuộc một – nhiều giữa các đối tượng để khi mà một đối tượng có sự thay đổi trạng thái, tất các thành phần phụ thuộc của nó sẽ được thông báo và cập nhật một cách tự động.

## 2. Cách sử dụng
![Obserber diagram](https://gpcoder.com/wp-content/uploads/2018/12/design-patterns-observer-diagram.png)

Các thành phần tham gia `Observer Pattern`:

- `Subject` : chứa danh sách các observer,  cung cấp phương thức để có thể thêm và loại bỏ observer.
- `Observer` : định nghĩa một phương thức update() cho các đối tượng sẽ được subject thông báo đến khi có sự thay đổi trạng thái.
- `ConcreteSubject` : cài đặt các phương thức của Subject, lưu trữ trạng thái danh sách các ConcreateObserver, gửi thông báo đến các observer của nó khi có sự thay đổi trạng thái.
- `ConcreteObserver` : cài đặt các phương thức của Observer, lưu trữ trạng thái của subject, thực thi việc cập nhật để giữ cho trạng thái đồng nhất với subject gửi thông báo đến.

>Ví dụ

>Subject.java
```java
    public interface Subject {

        int getState() {
        }

        void setState(int state) {
        }

        void attach(Observer observer){	
        }

        void notifyAllObservers(){
        } 	
    }
```

>ConcreteSubject.java   
```java
    public class ConcreteSubject implements Subject{
        
    private List<Observer> observers = new ArrayList<Observer>();
    private int state;

    @Override
    public int getState() {
        return state;
    }
    @Override
    public void setState(int state) {
        this.state = state;
        notifyAllObservers();
    }
    @Override
    public void attach(Observer observer){
        observers.add(observer);		
    }
    @Override
    public void notifyAllObservers(){
        for (Observer observer : observers) {
            observer.update();
        }
    } 	
    }
```

>Observer.java
```java
    public abstract class Observer {
        protected Subject subject;
        public abstract void update();
        }
```

>ConcreteObserver

>BinaryObserver.java
```java
    public class BinaryObserver extends Observer{

    public BinaryObserver(Subject subject){
        this.subject = subject;
        this.subject.attach(this);
    }

    @Override
    public void update() {
        System.out.println( "Binary String: " + Integer.toBinaryString( subject.getState() ) ); 
    }
    }
```
>OctalObserver.java
```java
    public class OctalObserver extends Observer{

    public OctalObserver(Subject subject){
        this.subject = subject;
        this.subject.attach(this);
    }

    @Override
    public void update() {
        System.out.println( "Octal String: " + Integer.toOctalString( subject.getState() ) ); 
    }
    }
```
>HexaObserver.java
```java
    public class HexaObserver extends Observer{

    public HexaObserver(Subject subject){
        this.subject = subject;
        this.subject.attach(this);
    }

    @Override
    public void update() {
        System.out.println( "Hex String: " + Integer.toHexString( subject.getState() ).toUpperCase() ); 
    }
    }
```

>ObserverPatternDemo.java
```java
    public class ObserverPatternDemo {
        public static void main(String[] args) {
            Subject subject = new ConcreteSubject();

            new HexaObserver(subject);
            new OctalObserver(subject);
            new BinaryObserver(subject);

            System.out.println("First state change: 15");	
            subject.setState(15);
            System.out.println("Second state change: 10");	
            subject.setState(10);
        }
    }
```
>Output
```
    First state change: 15
    Hex String: F
    Octal String: 17
    Binary String: 1111
    Second state change: 10
    Hex String: A
    Octal String: 12
    Binary String: 1010
```
## 3. Lợi ích
- Dễ dàng mở rộng với ít sự thay đổi : mẫu này cho phép thay đổi Subject và Observer một cách độc lập. Chúng ta có thể tái sử dụng các Subject mà không cần tái sử dụng các Observer và ngược lại. Nó cho phép thêm Observer mà không sửa đổi Subject hoặc Observer khác. Vì vậy, nó đảm bảo nguyên tắc Open/Closed Principle (OCP).
- Sự thay đổi trạng thái ở 1 đối tượng có thể được thông báo đến các đối tượng khác mà không phải giữ chúng liên kết quá chặt chẽ.
- Một đối tượng có thể thông báo đến một số lượng không giới hạn các đối tượng khác.

# Tham khảo

https://gpcoder.com/4747-huong-dan-java-design-pattern-observer/

https://www.tutorialspoint.com/design_pattern/observer_pattern.htm