# Factory Method
## 1. Khái niệm
`Factory Method` là một pattern thuộc nhóm **Creational Patterns**. Định nghĩa interface giúp client tạo object nhưng ủy quyền cho các factory để xác định class nào được trả về cho client.
## 2. Cách sử dụng
Một `Factory Pattern` bao gồm các thành phần cơ bản sau:

- Super Class: môt supper class trong Factory Pattern có thể là một interface, abstract class hay một class thông thường.
- Sub Classes: các sub class sẽ implement các phương thức của supper class theo nghiệp vụ riêng của nó.
- Factory Class: một class chịu tránh nhiệm khởi tạo các đối tượng sub class dựa theo tham số đầu vào. (Lớp này là [Singleton](../singleton/README.md) hoặc cung cấp một `public static method `cho việc truy xuất và khởi tạo đối tượng. Factory class sử dụng if-else hoặc switch-case để xác định class con đầu ra.)

> **Ví dụ:** Tất cả hệ thống ngân hàng có cung cấp API để truy cập đến hệ thống của họ. Team được giao nhiệm vụ thiết kế một API để client có thể sử dụng dịch vụ của một ngân hàng bất kỳ. Hiện tại, phía client chỉ cần sử dụng dịch vụ của 2 ngân hàng là VietcomBank và TPBank. Tuy nhiên để dễ mở rộng sau này, và phía client mong muốn không cần phải thay đổi code của họ khi cần sử dụng thêm dịch vụ của ngân hàng khác. 

>Super Class
```java
    public interface Bank {
        String getBankName();
    }
```
>Sub Classes
```java
    public class TPBank implements Bank {
    
        @Override
        public String getBankName() {
            return "TPBank";
        }

    }
```

```java
    public class VietcomBank implements Bank {
    
        @Override
        public String getBankName() {
            return "VietcomBank";
        }
    
    }
```
> Factory Class
```java
    public class BankFactory {
    
        private BankFactory() {
        }
    
        public static final Bank getBank(BankType bankType) {
            switch (bankType) {
    
            case TPBANK:
                return new TPBank();
    
            case VIETCOMBANK:
                return new VietcomBank();
    
            default:
                throw new IllegalArgumentException("This bank type is unsupported");
            }
        }
    
    }
```
>Bank type
```java
public enum BankType {
 
    VIETCOMBANK, TPBANK;
 
}
```
> Client
```java
public class Client {
 
    public static void main(String[] args) {
        Bank bank = BankFactory.getBank(BankType.TPBANK);
        System.out.println(bank.getBankName()); // TPBank
    }
}
```
## 3. Lợi ích
- Giảm sự phụ thuộc giữa các Module.
- Mở rộng Code dễ dàng hơn.
- Khởi tạo các Objects mà che giấu đi xử lí logic của việc khởi tạo đấy. Người dùng không biết logic thực sực được khởi tạo bên dưới phương thức factory.

## Tham khảo

https://gpcoder.com/4352-huong-dan-java-design-pattern-factory-method/