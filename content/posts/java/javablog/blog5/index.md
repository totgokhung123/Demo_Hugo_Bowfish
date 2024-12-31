---
title: "Các tính năng của từ khóa protected trong Java"
date: 2024-06-23
description: "Các tính năng của từ khóa protected trong Java"
tags: ["Java"]
categories: ["Java"]
series: ["Java"]
series_order: 5

---

## Tìm hiểu về tính năng protected trong Java

Tính năng protected trong Java cho phép các thành phần của một lớp được truy cập bởi các lớp con của nó.

Điều này có nghĩa là các lớp con có thể sử dụng và mở rộng các thành phần protected của lớp cha. Điều này rất hữu ích khi chúng ta muốn tạo ra các lớp con có tính kế thừa từ lớp cha mà không cần phải viết lại code.

Để sử dụng tính năng protected trong Java, chúng ta có thể sử dụng cú pháp sau:

```java
protected [kiểu dữ liệu] [tên biến];
protected [kiểu trả về] [tên phương thức]([tham số]);
```

 Các thành phần được đánh dấu là protected có thể được truy cập bởi:

- Bản thân lớp sở hữu các thành phần protected
- Các lớp con của lớp cha
- Các lớp trong cùng một gói với lớp cha (nếu không có modifier truy cập nào khác được chỉ định)

## Cách sử dụng từ khóa protected trong Java

Để minh hoạ cách sử dụng tính năng protected trong Java, chúng ta sẽ tạo ra một ví dụ đơn giản về lớp cha và lớp con. Trong ví dụ này, chúng ta sẽ tạo ra một lớp cha có tên là Shape và một lớp con là Rectangle.

```java
public class Shape {
    protected int width;
    protected int height;
    public Shape(int width, int height) {
        this.width = width;
        this.height = height;
    }
    protected int calculateArea() {
        return this.width * this.height;
    }
}
public class Rectangle extends Shape {
    private String color;

    public Rectangle(int width, int height, String color) {
        super(width, height);
        this.color = color;
    }
    public void printArea() {
        System.out.println("Area of rectangle is: " + calculateArea());
    }
}
```

Trong ví dụ trên, chúng ta có một lớp cha Shape với hai thuộc tính là width và height, cùng với một phương thức tính diện tích là calculateArea(). Lớp con Rectangle kế thừa từ lớp cha Shape và sử dụng các thuộc tính và phương thức protected của nó.

Chúng ta có thể thấy rằng trong lớp con Rectangle, chúng ta không cần phải khai báo lại các thuộc tính và phương thức đã có sẵn trong lớp cha. Thay vào đó, chúng ta chỉ cần gọi các phương thức và thuộc tính đó thông qua từ khóa super.

```java
public void printArea() {
    System.out.println("Area of rectangle is: " + calculateArea());
} 
```

## Phân biệt giữa private và protected trong Java

Sự khác biệt chính giữa private và protected là phạm vi truy cập:

- Private: Các thành phần private chỉ có thể được truy cập từ bên trong lớp sở hữu chúng.
- Protected: Các thành phần protected có thể được truy cập bởi lớp sở hữu chúng, các lớp con và các lớp khác trong cùng một gói.
Điều này có nghĩa là khi chúng ta sử dụng từ khóa private, các thành phần đó chỉ có thể được truy cập bởi lớp sở hữu của chúng. Trong khi đó, khi sử dụng từ khóa protected, các thành phần có thể được truy cập bởi nhiều lớp hơn, bao gồm cả lớp con và các lớp trong cùng một gói.

## Lợi ích của việc sử dụng protected trong Java

Sử dụng tính năng protected mang lại một số lợi ích:

- Tính kế thừa dễ dàng: Cho phép các lớp con tiếp tục sử dụng và mở rộng các thành phần protected của lớp cha.
- Giảm thiểu code: Không cần phải viết lại code cho các thành phần đã có sẵn trong lớp cha.
- Bảo mật dữ liệu: Các thành phần protected chỉ có thể được truy cập bởi các lớp có quyền truy cập tương đương, giúp bảo vệ dữ liệu của lớp cha.

## Các quy tắc và hạn chế khi sử dụng protected trong Java

Khi sử dụng tính năng protected trong Java, chúng ta cần lưu ý một số quy tắc và hạn chế sau:

- Các thành phần protected không thể được truy cập từ bên ngoài gói chứa lớp cha, trừ khi lớp con của nó cũng nằm trong gói đó.
- Các thành phần protected không thể được truy cập từ bên ngoài lớp con, trừ khi lớp con đó là lớp con của lớp cha đó.
- Các thành phần protected không thể được truy cập từ bên ngoài lớp con của lớp con, trừ khi lớp con đó là lớp con của lớp cha và nằm trong cùng một gói với lớp cha.

## Bảo mật dữ liệu với tính năng protected trong Java

Một trong những ứng dụng quan trọng của tính năng protected trong Java là để bảo mật dữ liệu. Với tính năng này, chúng ta có thể giới hạn quyền truy cập vào các thành phần của lớp chỉ cho các lớp có quyền truy cập tương đương. Điều này giúp bảo vệ dữ liệu của lớp cha khỏi việc bị sửa đổi hoặc truy cập trái phép.

Ví dụ, trong lớp Shape ở ví dụ trước, chúng ta có thể sử dụng tính năng protected để bảo vệ các thuộc tính width và height của lớp. Điều này đảm bảo rằng chỉ có các lớp con của Shape mới có thể truy cập và sử dụng các thuộc tính này.

## Ví dụ minh họa về cách sử dụng protected trong Java

Để hiểu rõ hơn về cách sử dụng tính năng protected trong Java, chúng ta sẽ xem xét một ví dụ khác. Trong ví dụ này, chúng ta sẽ tạo ra một lớp Employee và một lớp con là Manager.

```java
public class Employee {
    protected String name;
    protected int salary;
    public Employee(String name, int salary) {
        this.name = name;
        this.salary = salary;
    }
    protected void printInfo() {
        System.out.println("Name: " + this.name);
        System.out.println("Salary: " + this.salary);
    }
}
public class Manager extends Employee {
    private int bonus;

    public Manager(String name, int salary, int bonus) {
        super(name, salary);
        this.bonus = bonus;
    }
    public void printInfo() {
        super.printInfo();
        System.out.println("Bonus: " + this.bonus);
    }
}
```

Trong ví dụ này, chúng ta có một lớp Employee với hai thuộc tính là name và salary, cùng với một phương thức in thông tin là printInfo(). Lớp con Manager kế thừa từ lớp cha Employee và sử dụng các thuộc tính và phương thức protected của nó.

Chúng ta có thể thấy rằng trong lớp con Manager, chúng ta không cần phải khai báo lại các thuộc tính và phương thức đã có sẵn trong lớp cha. Thay vào đó, chúng ta chỉ cần gọi các phương thức và thuộc tính đó thông qua từ khóa super.

```java
public void printInfo() {
    super.printInfo();
    System.out.println("Bonus: " + this.bonus);
}
```

## Các lỗi thường gặp khi sử dụng protected trong Java

Khi sử dụng tính năng protected trong Java, chúng ta cần lưu ý một số lỗi thường gặp sau:

- Lỗi truy cập: Khi chúng ta cố gắng truy cập các thành phần protected từ bên ngoài lớp cha hoặc lớp con không hợp lệ, chúng ta sẽ nhận được lỗi truy cập.
- Lỗi kế thừa: Khi chúng ta cố gắng kế thừa từ một lớp có các thành phần private hoặc default, chúng ta sẽ nhận được lỗi kế thừa.
- Lỗi định nghĩa: Khi chúng ta cố gắng định nghĩa một thành phần protected với cùng tên nhưng kiểu dữ liệu khác với một thành phần đã có trong lớp cha, chúng ta sẽ nhận được lỗi định nghĩa.

## Cách truy cập các thành phần protected trong Java

Để truy cập các thành phần protected của một lớp, chúng ta có thể sử dụng các phương thức và thuộc tính đó thông qua từ khóa super trong lớp con. Ngoài ra, chúng ta cũng có thể sử dụng các getter và setter để truy cập và thay đổi giá trị của các thuộc tính protected.

Ví dụ:

```java
public class Rectangle extends Shape {
    private String color;
    public Rectangle(int width, int height, String color) {
        super(width, height);
        this.color = color;
    }
    public void printArea() {
        System.out.println("Area of rectangle is: " + calculateArea());
    }
    public void setColor(String color) {
        this.color = color;
    }
    public String getColor() {
        return this.color;
    }
}
```
Trong ví dụ này, chúng ta đã tạo ra các getter và setter cho thuộc tính color của lớp Rectangle, cho phép chúng ta truy cập và thay đổi giá trị của thuộc tính này từ bên ngoài lớp.

## Tài liệu tham khảo

1. [Các tính năng của từ khóa protected trong Java](https://topdev.vn/blog/cac-tinh-nang-cua-tu-khoa-protected-trong-java/#tim-hieu-ve-tinh-nang-protected-trong-java)


<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>