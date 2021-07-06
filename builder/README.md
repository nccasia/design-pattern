# Builder 
## 1. Khái niệm
`Builder pattern` là mẫu thiết kế đối tượng được tạo ra để xây dựng một đôi tượng phức tạp bằng cách sử dụng các đối tượng đơn giản và sử dụng tiếp cận từng bước, việc xây dựng các đối tượng đôc lập với các đối tượng khác.
## 2. Cách sử dụng
![alt](https://gpcoder.com/wp-content/uploads/2018/09/design-patterns-builder-diagram.png)

Một builder gồm các thành phần cơ bản sau:
- `Product`: đại diện cho đối tượng cần tạo, đối tượng này phức tạp, có nhiều thuộc tính.
- `Builder` : là abstract class hoặc interface khai báo phương thức tạo đối tượng.
- `ConcreteBuilder` : kế thừa Builder và cài đặt chi tiết cách tạo ra đối tượng. Nó sẽ xác định và nắm giữ các thể hiện mà nó tạo ra, đồng thời nó cũng cung cấp phương thức để trả các các thể hiện mà nó đã tạo ra trước đó.
- `Director/ Client`: là nơi sẽ gọi tới Builder để tạo ra đối tượng.

>Ví dụ:

>Product
```java
    public class Student {
        private int id;
        private String firstName;
        private String lastName;
        private String dayOfBirth;
        private String currentClass;
        private int phone;

        public Student(int id, String firstName, String lastName, String dayOfBirth, String currentClass, int phone) {
            this.id = id;
            this.firstName = firstName;
            this.lastName = lastName;
            this.dayOfBirth = dayOfBirth;
            this.currentClass = currentClass;
            this.phone = phone;
        }
    }

    // GETTER
```
> Builder
```java
public interface StudentBuilder {

    StudentBuilder setId(int id);

    StudentBuilder setFirstName(String firstName);

    StudentBuilder setLastName(String lastName);

    StudentBuilder setDayOfBirth(String dayOfBirth);

    StudentBuilder setCurrentClass(String currentClass);

    StudentBuilder setPhone(int phone);

    Student build();
}
```

```java
// ConcreteBuilder
public class StudentConcreteBuilder implements StudentBuilder {

    private int id;
    private String firstName;
    private String lastName;
    private String dayOfBirth;
    private String currentClass;
    private int phone;

    @Override
    public StudentBuilder setId(int id) {
        this.id = id;
        return this;
    }

    @Override
    public StudentBuilder setFirstName(String firstName) {
        this.firstName = firstName;
        return this;
    }

    @Override
    public StudentBuilder setLastName(String lastName) {
        this.lastName = lastName;
        return this;
    }

    @Override
    public StudentBuilder setDayOfBirth(String dayOfBirth) {
        this.dayOfBirth = dayOfBirth;
        return this;
    }

    @Override
    public StudentBuilder setCurrentClass(String currentClass) {
        this.currentClass = currentClass;
        return this;
    }

    @Override
    public StudentBuilder setPhone(int phone) {
        this.phone = phone;
        return this;
    }

    @Override
    public Student build() {
        return new Student(id, firstName, lastName, dayOfBirth, currentClass, phone);
    }
}
```
> Main
```java
    public static void main(String[] args) {

            StudentBuilder studentBuilder = new StudentConcreteBuilder()
                    .setFirstName("Thanh")
                    .setLastName("Pham Trong")
                    .setsetDayOfBirth("06/01/1999")
                    .setCurrentClass("ABC");

            System.out.println(studentBuilder.build());
        }
```
## 3. Lợi ích
- Hỗ trợ, loại bớt việc phải viết nhiều constructor.
- Code dễ đọc, dễ bảo trì hơn khi số lượng thuộc tính (propery) bắt buộc để tạo một object từ 4 hoặc 5 propery.
- Giảm bớt số lượng constructor, không cần truyền giá trị null cho các tham số không sử dụng.
- Ít bị lỗi do việc gán sai tham số khi mà có nhiều tham số trong constructor.
- Đối tượng được xây dựng an toàn hơn: bởi vì nó đã được tạo hoàn chỉnh trước khi sử dụng.
- Cung cấp cho bạn kiểm soát tốt hơn quá trình xây dựng: chúng ta có thể thêm xử lý kiểm tra ràng buộc trước khi đối tượng được trả về người dùng.

## Tham khảo

https://gpcoder.com/4434-huong-dan-java-design-pattern-builder/