# Adapter
## 1. Khái niệm
`Adapter Pattern` là một trong những Pattern thuộc nhóm cấu trúc (Structural Pattern. `Adapter Pattern` cho phép các inteface (giao diện) không liên quan tới nhau có thể làm việc cùng nhau. Đối tượng giúp kết nối các interface gọi là Adapter.
## 2. Cách sử dụng
Một Adapter Pattern bao gồm các thành phần cơ bản sau:

- `Adaptee`: định nghĩa interface không tương thích, cần được tích hợp vào.
- `Adapter`: lớp tích hợp, giúp interface không tương thích tích hợp được với interface đang làm việc. Thực hiện việc chuyển đổi interface cho `Adaptee` và kết nối `Adaptee` với `Client`.
- `Target`: một interface chứa các chức năng được sử dụng bởi `Client` (domain specific).
- `Client`: lớp sử dụng các đối tượng có interface `Target`.
![Adapter diagram](https://gpcoder.com/wp-content/uploads/2018/10/design-patterns-object-adapter-diagram.png)

Trong mô hình này, một lớp mới (`Adapter`) sẽ tham chiếu đến một (hoặc nhiều) đối tượng của lớp có sẵn với interface không tương thích (`Adaptee`), đồng thời cài đặt interface mà người dùng mong muốn (`Target`). Trong lớp mới này, khi cài đặt các phương thức của interface người dùng mong muốn, sẽ gọi phương thức cần thiết thông qua đối tượng thuộc lớp có interface không tương thích.

>Ví dụ
Một người Việt muốn trao đổi với một người Nhật. Tuy nhiên, 2 người này không biết ngôn ngữ của nhau nên cần phải có một người để chuyển đổi từ ngôn ngữ tiếng Việt sang ngôn ngữ tiếng Nhật. Chúng ta sẽ mô hình hóa trường hợp này với Adapter Pattern như sau:

- `Client`: người Việt sẽ là Client trong ví dụ này,vì anh ta cần gửi một số message cho người Nhật.
- `Target`: đây là nội dung message được Client cung cấp cho thông dịch viên (Translator / Adapter).
- `Adapter`: thông dịch viên (Translator) sẽ là Adapter, nhận message tiếng Việt từ Client và chuyển đổi nó sang tiếng Nhật trước khi gởi cho người Nhật.
- `Adaptee`: đây là interface hoặc class được người Nhật sử dụng để nhận message được chuyển đổi từ thông dịch viên (Translator).

![Adapter diagram example](https://gpcoder.com/wp-content/uploads/2018/10/design-patterns-adapter-diagram-translator-example.png)

> VietnameseTarget
```java
    public interface VietnameseTarget {
    
        void send(String words);
    
    }
```
> JapaneseAdaptee
```java
    public class JapaneseAdaptee {
    
        public void receive(String words) {
            System.out.println("Retrieving words from Adapter ...");
            System.out.println(words);
        }
    }
```
> TranslatorAdapter
```java
    public class TranslatorAdapter implements VietnameseTarget {
    
        private JapaneseAdaptee adaptee;
    
        public TranslatorAdapter(JapaneseAdaptee adaptee) {
            this.adaptee = adaptee;
        }
    
        @Override
        public void send(String words) {
            System.out.println("Reading Words ...");
            System.out.println(words);
            String vietnameseWords = this.translate(words);
            System.out.println("Sending Words ...");
            adaptee.receive(vietnameseWords);
        }
    
        private String translate(String vietnameseWords) {
            System.out.println("Translated!");
            return "こんにちは";
        }
    }
```
> VietnameseClient
```java
    public class VietnameseClient {
    
        public static void main(String[] args) {
            VietnameseTarget client = new TranslatorAdapter(new JapaneseAdaptee());
            client.send("Xin chào");
        }
```
> Output
```
    Reading Words ...
    Xin chào
    Translated!
    Sending Words ...
    Retrieving words from Adapter ...
    こんにちは
```
## 3. Lợi ích
- Cho phép nhiều đối tượng có interface giao tiếp khác nhau có thể tương tác và giao tiếp với nhau.
- Tăng khả năng sử dụng lại thư viện với interface không thay đổi do không có mã nguồn.

## Tham Khảo

https://gpcoder.com/4483-huong-dan-java-design-pattern-adapter/