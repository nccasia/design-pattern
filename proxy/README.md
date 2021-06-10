# Proxy
## 1. Khái niệm
`Proxy Pattern` là một trong những Pattern thuộc nhóm cấu trúc (Structural Pattern). 

`Proxy Pattern` là mẫu thiết kế mà ở đó tất cả các truy cập trực tiếp đến một đối tượng nào đó sẽ được chuyển hướng vào một đối tượng trung gian (Proxy Class). Mẫu Proxy (người đại diện) đại diện cho một đối tượng khác thực thi các phương thức, phương thức đó có thể được định nghĩa lại cho phù hợp với múc đích sử dụng.

## 2. Phân loại Proxy
- `Virtual Proxy`: Virtual Proxy tạo ra một đối tượng trung gian mỗi khi có yêu cầu tại thời điểm thực thi ứng dụng, nhờ đó làm tăng hiệu suất của ứng dụng.
- `Protection Proxy`: Phạm vi truy cập của các client khác nhau sẽ khác nhau. Protection proxy sẽ kiểm tra các quyền truy cập của client khi có một dịch vụ được yêu cầu.
- `Remote Proxy`: Client truy cập qua Remote Proxy để chiếu tới một đối tượng được bảo về nằm bên ngoài ứng dụng (trên cùng máy hoặc máy khác).
- `Monitor Proxy`: Monitor Proxy sẽ thiết lập các bảo mật trên đối tượng cần bảo vệ, ngăn không cho client truy cập một số trường quan trọng của đối tượng. Có thể theo dõi, giám sát, ghi log việc truy cập, sử dụng đối tượng.
- `Firewall Proxy`: bảo vệ đối tượng từ chối các yêu cầu xuất xứ từ các client không tín nhiệm.
- `Cache Proxy`: Cung cấp không gian lưu trữ tạm thời cho các kết quả trả về từ đối tượng nào đó, kết quả này sẽ được tái sử dụng cho các client chia sẻ chung một yêu cầu gửi đến. Loại Proxy này hoạt động tương tự như Flyweight Pattern.
- `Smart Reference Proxy`: Là nơi kiểm soát các hoạt động bổ sung mỗi khi đối tượng được tham chiếu.
- `Synchronization Proxy`: Đảm bảo nhiều client có thể truy cập vào cùng một đối tượng mà không gây ra xung đột. Khi một client nào đó chiếm dụng khóa khá lâu khiến cho số lượng các client trong danh sách hàng đợi cứ tăng lên, và do đó hoạt động của hệ thống bị ngừng trệ, có thể dẫn đến hiện tượng “tắc nghẽn”.
- `Copy-On-Write Proxy`: Loại này đảm bảo rằng sẽ không có client nào phải chờ vô thời hạn. Copy-On-Write Proxy là một thiết kế rất phức tạp.

## 3. Sử dụng
`Proxy Pattern` có những đặc điểm chung sau đây:

- Cung cấp mức truy cập gián tiếp vào một đối tượng.
- Tham chiếu vào đối tượng đích và chuyển tiếp các yêu cầu đến đối tượng đó.
- Cả Proxy và đối tượng đích đều kế thừa hoặc thực thi chung một lớp giao diện. Mã máy dịch cho lớp giao diện thường “nhẹ” hơn các lớp cụ thể và do đó có thể giảm được thời gian tải dữ liệu giữa server và client.

![Proxy pattern diagram](https://gpcoder.com/wp-content/uploads/2018/11/design-patterns-proxy-diagram.png)

Các thành phần tham gia vào mẫu `Proxy Pattern`:

- `Subject`: là một interface định nghĩa các phương thực để giao tiếp với client. Đối tượng này xác định giao diện chung cho RealSubject và Proxy để Proxy có thể được sử dụng bất cứ nơi nào mà RealSubject mong đợi.
- `Proxy`: là một class sẽ thực hiện các bước kiểm tra và gọi tới đối tượng của class service thật để thực hiện các thao tác sau khi kiểm tra. Nó duy trì một tham chiếu đến RealSubject để Proxy có thể truy cập nó. Nó cũng thực hiện các giao diện tương tự như RealSubject để Proxy có thể được sử dụng thay cho RealSubject. Proxy cũng điều khiển truy cập vào RealSubject và có thể tạo hoặc xóa đối tượng này.
- `RealSubject`: là một class service sẽ thực hiện các thao tác thực sự. Đây là đối tượng chính mà proxy đại diện.
- `Client`: Đối tượng cần sử dụng RealSubject nhưng thông qua Proxy.

> Ví dụ: Virtual Proxy

>Image.java
```java
    public interface Image {
    void display();
    }
```
>RealImage.java
RealImage.java
```java
    public class RealImage implements Image {

        private String fileName;

        public RealImage(String fileName){
            this.fileName = fileName;
            loadFromDisk(fileName);
        }

        @Override
        public void display() {
            System.out.println("Displaying " + fileName);
        }

        private void loadFromDisk(String fileName){
            System.out.println("Loading " + fileName);
        }
    }
```
>ProxyImage.java
```java
    public class ProxyImage implements Image{

        private RealImage realImage;
        private String fileName;

        public ProxyImage(String fileName){
            this.fileName = fileName;
        }

        @Override
        public void display() {
            if(realImage == null){
                realImage = new RealImage(fileName);
            }else{
                System.out.println("Image existed: " + fileName);
            }
            realImage.display();
        }
    }
```
> Client.java
```java
    public class Client {
        
        public static void main(String[] args) {
            Image image = new ProxyImage("test.jpg");

            //image will be loaded from disk
            image.display(); 
            System.out.println("");
            
            //image will not be loaded from disk
            image.display(); 	
        }
    }
```

>Output
```
    Loading test.jpg
    Displaying test.jpg

    Image existed: test.jpg
    Displaying test.jpg
```

## 3. Lợi ích
- Cãi thiện Performance thông qua lazy loading, chỉ tải các tài nguyên khi chúng được yêu cầu.
- Nó cung cấp sự bảo vệ cho đối tượng thực từ thế giới bên ngoài.
- Giảm chi phí khi có nhiều truy cập vào đối tượng có chi phí khởi tạo ban đầu lớn.
- Dễ nâng cấp, bảo trì.

## Tham khảo

https://gpcoder.com/4644-huong-dan-java-design-pattern-proxy/