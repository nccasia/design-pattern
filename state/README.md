# State
## 1. Khái niệm
`State Pattern` là một trong những Pattern thuộc nhóm hành vi (Behavior Pattern). Nó cho phép một đối tượng thay đổi hành vi của nó khi trạng thái nội bộ của nó thay đổi. Đối tượng sẽ xuất hiện để thay đổi lớp của nó.
## 2. Cách sử dụng
![State diagram](https://gpcoder.com/wp-content/uploads/2019/01/design-patterns-state-diagram.png)
Các thành phần tham gia State Pattern:

- `Context`: được sử dụng bởi Client. Client không truy cập trực tiếp đến State của đối tượng. Lớp Context này chứa thông tin của ConcreteState object, cho hành vi nào tương ứng với trạng thái nào hiện đang được thực hiện.
- `State`: là một interface hoặc abstract class xác định các đặc tính cơ bản của tất cả các đối tượng ConcreteState. Chúng sẽ được sử dụng bởi đối tượng Context để truy cập chức năng có thể thay đổi.
- `ConcreteState`: cài đặt các phương thức của State. Mỗi ConcreteState có thể thực hiện logic và hành vi của riêng nó tùy thuộc vào Context.

>Ví dụ:

>State.java
```java
    public interface State {
        public void handle();
    }
```

> Concrete State

> StartState.java
```java
public class StartState implements State{

    @Override
    public void handle(){
        System.out.println("Start State");
    }

}
```

> StopState.java
```java
    public class StopState implements State{

        @Override
        public void handle(){
            System.out.println("Stop State");
        }

    }
```

>Context.java
```java
    public class Context {
        private State state;

        public void setState(State state){
            this.state = state;		
        }

        public State applyState(){
            this.state.handle();
        }
    }
```

> StateExample.java
```java
public class StateExample{
    public static void main(String[] args) {
        Context context = new Context();

        context.setState(new StartState());
        context.applyState();        
        
        context.setState(new StopState());
        context.applyState();
    }
}
```
> Output
```
    Start State
    Stop State
```
## 3. Lợi ích:

- Đảm bảo nguyên tắc Single responsibility principle (SRP) : tách biệt mỗi State tương ứng với 1 class riêng biệt.
- Đảm bảo nguyên tắc Open/Closed Principle (OCP) : chúng ta có thể thêm một State mới mà không ảnh hưởng đến State khác hay Context hiện có.
- Giữ hành vi cụ thể tương ứng với trạng thái.
- Giúp chuyển trạng thái một cách rõ ràng.

## 4. Sử dụng
- Khi hành vi của đối tượng phụ thuộc vào trạng thái của nó và nó phải có khả năng thay đổi hành vi của nó lúc run-time theo trạng thái mới.
- Khi nhiều điều kiện phức tạp buộc đối tượng phụ thuộc vào trạng thái của nó.

## Tham khảo

https://gpcoder.com/4785-huong-dan-java-design-pattern-state/