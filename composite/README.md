# Composite
## 1. Khái niệm
`Composite` là một mẫu thiết kế thuộc nhóm cấu trúc (Structural Pattern). `Composite Pattern` là một sự tổng hợp những thành phần có quan hệ với nhau để tạo ra thành phần lớn hơn. Nó cho phép thực hiện các tương tác với tất cả đối tượng trong mẫu tương tự nhau.

![Composite pattern struct](https://gpcoder.com/wp-content/uploads/2018/11/Composite.png)

## 2. Cách sử dụng
![Composite diagram](https://gpcoder.com/wp-content/uploads/2018/11/design-patterns-composite-diagram.png)

Một Composite Pattern bao gồm các thành phần cơ bản sau:

- `Base Component`: là một interface hoặc abstract class quy định các method chung cần phải có cho tất cả các thành phần tham gia vào mẫu này.
- `Leaf`: là lớp hiện thực (implements) các phương thức của Component. Nó là các object không có con.
- `Composite`: lưu trữ tập hợp các Leaf và cài đặt các phương thức của Base Component. Composite cài đặt các phương thức được định nghĩa trong interface Component bằng cách ủy nhiệm cho các thành phần con xử lý.
- `Client`: sử dụng Base Component để làm việc với các đối tượng trong Composite.

> Ví dụ: Sử dụng Composite Pattern cho chương trình quản lý một hệ thống tập tin

![example](https://gpcoder.com/wp-content/uploads/2018/11/design-patterns-composite-example.png)

> FileComponent
```java
    public interface FileComponent {
        void showProperty();
        long totalSize();
    }
```
>FileLeaf
```java
    public class FileLeaf implements FileComponent {
    
        private String name;
        private long size;
    
        public FileLeaf(String name, long size) {
            super();
            this.name = name;
            this.size = size;
        }
    
        @Override
        public long totalSize() {
            return size;
        }
    
        @Override
        public void showProperty() {
            System.out.println("FileLeaf [name=" + name + ", size=" + size + "]");
        }
    }
```
> FolderComposite
```java
    public class FolderComposite implements FileComponent {
    
        private List<FileComponent> files = new ArrayList<>();
    
        public FolderComposite(List<FileComponent> files) {
            this.files = files;
        }
    
        @Override
        public void showProperty() {
            for (FileComponent file : files) {
                file.showProperty();
            }
        }
    
        @Override
        public long totalSize() {
            long total = 0;
            for (FileComponent file : files) {
                total += file.totalSize();
            }
            return total;
        }
    }
```
> Client
```java
ublic class Client {
 
    public static void main(String[] args) {
        FileComponent file1 = new FileLeaf("file 1", 10);
        FileComponent file2 = new FileLeaf("file 2", 5);
        FileComponent file3 = new FileLeaf("file 3", 12);
 
        List<FileComponent> files = Arrays.asList(file1, file2, file3);
        FileComponent folder = new FolderComposite(files);
        folder.showProperty();
        System.out.println("Total Size: " + folder.totalSize());
    }
}
```
## 3. Lợi ích
Cung cấp cùng một cách sử dụng đối với từng đối tượng riêng lẻ hoặc nhóm các đối tượng với nhau.

## 4. Sử dụng
- Composite Pattern chỉ nên được áp dụng khi nhóm đối tượng phải hoạt động như một đối tượng duy nhất (theo cùng một cách).
- Composite Pattern có thể được sử dụng để tạo ra một cấu trúc giống như cấu trúc cây.

## Tham khảo

https://gpcoder.com/4554-huong-dan-java-design-pattern-composite/