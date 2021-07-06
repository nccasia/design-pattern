# Command
## 1. Khái niệm
`Command Pattern` là một trong những Pattern thuộc nhóm hành vi (Behavior Pattern). Nó cho phép tất cả những Request gửi đến object được lưu trữ trong chính object đó dưới dạng một object Command. Khái niệm Command Object giống như một class trung gian được tạo ra để lưu trữ các câu lệnh và trạng thái của object tại một thời điểm nào đó.
## 2. Cách sử dụng
![Command diagram](https://gpcoder.com/wp-content/uploads/2018/12/design-patterns-command-diagram.png)
Các thành phần tham gia trong Command Pattern:

- `Command`: là một interface hoặc abstract class, chứa một phương thức trừu tượng thực thi (execute) một hành động (operation). Request sẽ được đóng gói dưới dạng Command.
- `ConcreteCommand` : là các implementation của Command. Định nghĩa một sự gắn kết giữa một đối tượng Receiver và một hành động. Thực thi execute() bằng việc gọi operation đang hoãn trên Receiver. Mỗi một ConcreteCommand sẽ phục vụ cho một case request riêng.
- `Client` : tiếp nhận request từ phía người dùng, đóng gói request thành ConcreteCommand thích hợp và thiết lập receiver của nó.
- `Invoker` : tiếp nhận ConcreteCommand từ Client và gọi execute() của ConcreteCommand để thực thi request.
- `Receiver` : đây là thành phần thực sự xử lý business logic cho case request. Trong phương execute() của ConcreteCommand chúng ta sẽ gọi method thích hợp trong Receiver.
  
Như vậy, `Client` và `Invoker` sẽ thực hiện việc tiếp nhận request. Còn việc thực thi request sẽ do `Command`, `ConcreteCommand` và `Receiver` đảm nhận.

>Ví dụ: Hệ thống đóng / mở tài khoản trực tuyến của Ngân hàng
![Command example](https://gpcoder.com/wp-content/uploads/2018/12/design-patterns-command-example1.png)

- `Account` : là một request class.
- `Command` : là một interface của Command Pattern, cung cấp phương thức execute().
- `OpenAccount`, `CloseAccount` : là các ConcreteCommand, cài đặt các phương thức của Command, sẽ thực hiện các xử lý thực tế.
- `BankApp` : là một class, hoạt động như Invoker, gọi execute() của ConcreteCommand để thực thi request.
- `Client` : tiếp nhận request từ phía người dùng, đóng gói request thành ConcreteCommand thích hợp và gọi thực thi các Command.

> ACcount.java
```java
    public class Account {
        private String name;
    
        public Account(String name) {
            this.name = name;
        }
    
        public void open() {
            System.out.println("Account [" + name + "] Opened\n");
        }
    
        public void close() {
            System.out.println("Account [" + name + "] Closed\n");
        }
    }
```

> Command.java

```java
 
    public interface Command {
        
        void execute();
    }
```
> OpenAccount.java
```java
    public class OpenAccount implements Command {
    
        private Account account;
    
        public OpenAccount(Account account) {
            this.account = account;
        }
    
        @Override
        public void execute() {
            account.open();
        }
    }
```

> CloseAccount.java
```java
    public class CloseAccount implements Command {
    
        private Account account;
    
        public CloseAccount(Account account) {
            this.account = account;
        }
    
        @Override
        public void execute() {
            account.close();
        }
    }
```
> BankApp.java
```java
    public class BankApp {
    
        private Command openAccount;
        private Command closeAccount;
    
        public BankApp(Command openAccount, Command closeAccount) {
            this.openAccount = openAccount;
            this.closeAccount = closeAccount;
        }
        
        public void clickOpenAccount() {
            System.out.println("User click open an account");
            openAccount.execute();
        }
        
        public void clickCloseAccount() {
            System.out.println("User click close an account");
            closeAccount.execute();
        }
    }
```
> Client.java
```java
    public class Client {
    
        public static void main(String[] args) {
            Account account = new Account("Admin");
    
            Command open = new OpenAccount(account);
            Command close = new CloseAccount(account);
            BankApp bankApp = new BankApp(open, close);
    
            bankApp.clickOpenAccount();
            bankApp.clickCloseAccount();
        }
    }
```
>Output
```
    User click open an account
    Account [Admin] Opened
    
    User click close an account
    Account [Admin] Closed
```
## 3. Lợi ích
- Dễ dàng thêm các Command mới trong hệ thống mà không cần thay đổi trong các lớp hiện có. Đảm bảo Open/Closed Principle.
- Tách đối tượng gọi operation từ đối tượng thực sự thực hiện operation. - Giảm kết nối giữa Invoker và Receiver.
- Cho phép tham số hóa các yêu cầu khác nhau bằng một hành động để thực hiện.
- Cho phép lưu các yêu cầu trong hàng đợi.
- Đóng gói một yêu cầu trong một đối tượng. Dễ dàng chuyển dữ liệu dưới dạng đối tượng giữa các thành phần hệ thống.

## 4. Sử dụng Command Pattern khi nào?
- Khi cần tham số hóa các đối tượng theo một hành động thực hiện.
- Khi cần tạo và thực thi các yêu cầu vào các thời điểm khác nhau.
- Khi cần hỗ trợ tính năng undo, log , callback hoặc transaction.

## Tham khảo

https://gpcoder.com/4686-huong-dan-java-design-pattern-command/