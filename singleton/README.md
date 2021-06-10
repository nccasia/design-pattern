# Singleton
## 1. Khái niệm
`Singleton` đảm bảo chỉ duy nhất một thể hiện (instance) được tạo ra và nó sẽ cung cấp cho bạn một method để có thể truy xuất được thể hiện duy nhất đó mọi lúc mọi nơi trong chương trình.
## 2. Cách sử dụng
Có rất nhiều cách để implement `Singleton` Pattern. Nhưng dù cho việc implement bằng cách nào đi nữa cũng dựa vào nguyên tắc dưới đây cơ bản dưới đây:

- `private constructor` để hạn chế truy cập từ class bên ngoài.
- Đặt `private static final variable` đảm bảo biến chỉ được khởi tạo trong class.
- Có một method `public static` để `return instance` được khởi tạo ở trên.

>Ví dụ
```java
public class Singleton {
    private Singleton() {}

    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

## Tham Khảo

https://gpcoder.com/4190-huong-dan-java-design-pattern-singleton/