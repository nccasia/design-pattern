# Prototype
## 1. Khái niệm
`Prototype Pattern` là một trong những Creational pattern. Nó có nhiệm vụ khởi tạo một đối tượng bằng cách clone một đối tượng đã tồn tại thay vì khởi tạo với từ khoá `new`. Đối tượng mới là một bản sao có thể giống 100% với đối tượng gốc, chúng ta có thể thay đổi dữ liệu của nó mà không ảnh hưởng đến đối tượng gốc.
## 2. Cách sử dụng
![alt](https://gpcoder.com/wp-content/uploads/2018/09/design-patterns-prototype-diagram.png)

Trong Java cung cấp mẫu `Prototype Pattern` này bằng việc implement interface `Cloneable` và sử dụng method `clone()` để tạo object có đầy đủ thuộc tính của đối tượng ban đầu.


Một Prototype Pattern gồm các thành phần cơ bản sau:

- `Prototype`   : khai báo một class, interface hoặc abtract class cho việc clone chính nó.
- `ConcretePrototype` class: các lớp này thực thi interface (hoặc kế thừa từ lớp abstract) được cung cấp bởi `Prototype` để copy (nhân bản) chính bản thân nó. Các lớp này chính là thể hiện cụ thể phương thức `clone()`. Lớp này có thể không cần thiết nếu: Prototype là một class và nó đã implement việc clone chính nó.
- `Client` class : tạo mới object bằng cách gọi Prototype thực hiện clone chính nó.

> Ví dụ:

>Computer
```java
    public class Computer implements Cloneable {
        private String os;
        private String office;
        private String antivirus;
        private String browser;
        private String others;
    
        public Computer(String os, String office, String antivirus, String browser, String other) {
            super();
            this.os = os;
            this.office = office;
            this.antivirus = antivirus;
            this.browser = browser;
            this.others = other;
        }
    
        @Override
        protected Computer clone() {
            try {
                return (Computer) super.clone();
            } catch (CloneNotSupportedException e) {
                e.printStackTrace();
            }
            return null;
        }
    
        @Override
        public String toString() {
            return "Computer [os=" + os + ", office=" + office + ", antivirus=" + antivirus + ", browser=" + browser
                    + ", others=" + others + "]";
        }
    
        public void setOthers(String others) {
            this.others = others;
        }
    }
```

>App
```java
    public class ITApp {
    
        public static void main(String[] args) {
            Computer computer1 = new Computer("Window 10", "Word 2013", "BKAV", "Chrome", "Skype");
            Computer computer2 = computer1.clone();
            computer2.setOthers("Skype, Teamviewer, FileZilla Client");
    
            System.out.println(computer1);
            System.out.println(computer2);
        }
    }
```
> Output
```
    Computer [os=Window 10, office=Word 2013, antivirus=BKAV, browser=Chrome v69, other=Skype]
    Computer [os=Window 10, office=Word 2013, antivirus=BKAV, browser=Chrome v69, other=Skype, Teamviewer, FileZilla Client]
```
## 3. Lợi ích
- Cãi thiện performance: giảm chi phí để tạo ra một đối tượng mới theo chuẩn, điều này sẽ làm tăng hiệu suất so với việc sử dụng từ khóa new để tạo đối tượng mới.
- Giảm độ phức tạp cho việc khởi tạo đối tượng: do mỗi lớp chỉ implement cách clone của chính nó.
- Giảm việc phân lớp, tránh việc tạo nhiều lớp con cho việc khởi tạo đối tượng


## Tham khảo

https://gpcoder.com/4413-huong-dan-java-design-pattern-prototype/