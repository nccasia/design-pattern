# Design Pattern
## 1. Khái niệm
**Design Pattern** là một kỹ thuật trong lập trình hướng đối tượng, nó sẽ cung cấp các "mẫu thiết kế", giải pháp tối ưu để giải quyết các vấn đề chung, thường gặp trong lập trình.
## 2. Lợi ích
- Design pattern cung cấp giải pháp ở dạng tổng quát, giúp tăng tốc độ phát triển phần mềm bằng cách đưa ra các mô hình test, mô hình phát triển đã qua kiểm nghiệm.
- Dùng lại các design pattern giúp tránh được các vấn đề tiềm ẩn có thể gây ra những lỗi lớn, dễ dàng nâng cấp, bảo trì về sau.
- Giúp cho các lập trình viên có thể hiểu code của người khác 1 cách nhanh chóng (có thể hiểu là tính communicate). Mọi thành viên trong team có thể dễ dàng trao đổi với nhau để cùng xây dựng dự án mà không mất quá nhiều thời gian.
## 3. Phân loại
Design pattern hiện có 23 mẫu được định nghĩa trong cuốn `Design patterns Elements of Reusable Object Oriented Software` và được chia thành 3 nhóm:
### 3.1. Creational Pattern (Nhóm Khởi Tạo)
Nhóm này gồm có 5 mẫu: `Factory Method`, `Abstract Factory`, `Builder`, `Prototype`, `Singleton`. Những Design pattern loại này cung cấp một giải pháp để tạo ra các object và che giấu được logic của việc tạo ra nó, thay vì tạo ra object một cách trực tiếp bằng cách sử dụng method new. Điều này giúp cho chương trình trở nên mềm dẻo hơn trong việc quyết định object nào cần được tạo ra trong những tình huống được đưa ra.

![alt](https://images.viblo.asia/db99da2e-7eee-45b2-90ee-8e599f975a29.png)

#### [Singleton](singleton/README.md)

#### [Factory Method](factory-method/README.md)

#### Abstract Factory

#### [Builder](builder/README.md)

#### [Prototype](prototype/README.md)

### 3.2. Structural Pattern (Nhóm Cấu Trúc)
Nhóm này gồm 7 mẫu: `Adapter`, `Bridge`, `Composite`, `Decorator`, `Facade`, `Flyweight` và `Proxy`. Những Design pattern loại này liên quan tới class và các thành phần của object. Nó dùng để thiết lập, định nghĩa quan hệ giữa các đối tượng.
![alt](https://images.viblo.asia/d32eddff-6ff8-4e3c-a2f2-9aa0185312a7.png)

#### [Adapter](adapter/README.md)

#### Bridge

#### [Composite](composite/README.md)

#### Decorator

#### [Facade](facade/README.md)

#### Flyweight

#### [Proxy](proxy/README.md)

### 3.3 Behavioral Pattern (Nhóm Tương Tác / Hành Vi)
Nhóm này có 11 mẫu: `Interpreter`, `Template Method`, `Chain of Responsibility`, `Command`, `Iterator`, `Mediator`, `Memento`, `Observer`, `State`, `Strategy` và `Visitor`. Nhóm này dùng trong thực hiện các hành vi của đối tượng, sự giao tiếp giữa các object với nhau.

![alt](https://gpcoder.com/wp-content/uploads/2018/08/Behavioral.png)

#### Interpreter

#### Template Method

#### Chain of Responsibility

#### [Command](command/README.md)

#### Iterator

#### Mediator

#### Memento

#### [Observer](observer/README.md)

#### [State](state/README.md)

#### [Strategy](strategy/README.md)

#### Visitor

## Tham khảo

https://gpcoder.com/4164-gioi-thieu-design-patterns/