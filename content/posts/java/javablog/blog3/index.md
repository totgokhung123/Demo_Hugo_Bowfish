---
title: "Các phương thức cắt chuỗi trong Java"
date: 2024-06-23
description: "Các phương thức cắt chuỗi trong Java"
tags: ["Java"]
categories: ["Java"]
series: ["Java"]
series_order: 3

---

## Cách cắt chuỗi trong Java

Cắt chuỗi là thao tác trích xuất một phần cụ thể của chuỗi dựa trên vị trí bắt đầu và (tùy chọn) vị trí kết thúc.

Trong Java, có hai cách chính để cắt chuỗi:

1. Sử dụng chỉ số: Sử dụng dấu ngoặc vuông ([]) với chỉ số bắt đầu và kết thúc để trích xuất phần chuỗi mong muốn.
2. Sử dụng phương thức substring(): Phương thức này cho phép bạn chỉ định vị trí bắt đầu và vị trí kết thúc tùy ý.

### Hàm cắt chuỗi

Java cung cấp nhiều hàm tích hợp sẵn để xử lý chuỗi, bao gồm cắt chuỗi:

1. substring(int startIndex): Trích xuất phần chuỗi từ vị trí bắt đầu đã chỉ định đến cuối chuỗi.
2. substring(int startIndex, int endIndex): Trích xuất phần chuỗi từ vị trí bắt đầu đến trước vị trí kết thúc đã chỉ định.
3. split(String delimiter): Chia chuỗi thành một mảng các chuỗi con dựa trên một ký tự phân cách.
4. replace(String oldChar, String newChar): Thay thế tất cả các lần xuất hiện của oldChar bằng newChar trong chuỗi.

### Ví dụ về cắt chuỗi trong Java

Để hiểu rõ hơn về cách cắt chuỗi trong Java, chúng ta hãy xem một ví dụ đơn giản. Giả sử chúng ta có một chuỗi “Hello World”, chúng ta muốn cắt chuỗi này để lấy ra từ “World”.

Sử dụng chỉ số:

```java
    String str = "Hello World";
    String result = str.substring(6); // result = "World" 
```

Ở đây, chúng ta sử dụng chỉ số 6 để chỉ định vị trí bắt đầu của chuỗi con mà chúng ta muốn trích xuất. Lưu ý rằng chỉ số bắt đầu từ 0, nên vị trí thứ 6 trong chuỗi sẽ là ký tự “W”.

Sử dụng phương thức substring():

```java
    String str = "Hello World";
    String result = str.substring(6, 11); // result = "World" 
```

Ở đây, chúng ta sử dụng hai tham số là 6 và 11 để chỉ định vị trí bắt đầu và kết thúc của chuỗi con mà chúng ta muốn trích xuất. Lưu ý rằng vị trí kết thúc không được bao gồm trong chuỗi con trả về, nên chúng ta cần chỉ định vị trí kết thúc là 11 để lấy được từ “World”.

### Thao tác cắt chuỗi 

Ngoài việc trích xuất một phần của chuỗi, chúng ta còn có thể thực hiện các thao tác khác trên chuỗi bằng cách cắt chuỗi. Ví dụ, chúng ta có thể chia chuỗi thành các chuỗi con dựa trên một ký tự phân cách hoặc thay thế một ký tự trong chuỗi bằng một ký tự khác.

Để minh họa cho các thao tác này, chúng ta sẽ sử dụng chuỗi “apple,banana,orange”.

Chia chuỗi thành một mảng các chuỗi con

Để chia chuỗi thành một mảng các chuỗi con dựa trên một ký tự phân cách, chúng ta sử dụng phương thức split().

```java
    String str = "apple,banana,orange";
    String[] fruits = str.split(","); // fruits = ["apple", "banana", "orange"]
```

Ở đây, chúng ta sử dụng ký tự , làm ký tự phân cách để chia chuỗi thành các chuỗi con. Kết quả trả về là một mảng các chuỗi con được lưu trong biến fruits.

Thay thế ký tự trong chuỗi

Để thay thế tất cả các lần xuất hiện của một ký tự trong chuỗi bằng một ký tự khác, chúng ta sử dụng phương thức replace().

```java
    String str = "apple,banana,orange";
    String newStr = str.replace(",", ";"); // newStr = "apple;banana;orange"
```

Ở đây, chúng ta thay thế tất cả các lần xuất hiện của ký tự , bằng ký tự ;. Kết quả trả về là một chuỗi mới được lưu trong biến newStr.

## Các phương thức cắt chuỗi

Trong phần trước, chúng ta đã tìm hiểu về các phương thức cắt chuỗi trong Java. Trong phần này, chúng ta sẽ đi sâu hơn vào các phương thức này và tìm hiểu cách sử dụng chúng.

### Cách sử dụng hàm cắt chuỗi trong Java

Để sử dụng các phương thức cắt chuỗi trong Java, chúng ta cần khởi tạo một đối tượng String từ chuỗi cần xử lý. Sau đó, chúng ta có thể gọi các phương thức trên đối tượng này để thực hiện các thao tác cắt chuỗi.

Ví dụ:

```java
    String str = "Hello World";
    String result = str.substring(6); // result = "World"
```

Ở đây, chúng ta đã khởi tạo đối tượng String từ chuỗi “Hello World” và gọi phương thức substring() để cắt chuỗi từ vị trí thứ 6 đến cuối chuỗi.

### Lưu ý khi cắt chuỗi

Khi sử dụng các phương thức cắt chuỗi trong Java, chúng ta cần lưu ý một số điểm sau:

1. Chỉ số bắt đầu từ 0: Khi sử dụng chỉ số để cắt chuỗi, chúng ta cần nhớ rằng chỉ số bắt đầu từ 0, nên vị trí thứ 6 trong chuỗi sẽ là ký tự thứ 7.
2. Vị trí kết thúc không được bao gồm: Khi sử dụng phương thức substring(), vị trí kết thúc không được bao gồm trong chuỗi con trả về. Vì vậy, chúng ta cần chỉ định vị trí kết thúc là một số lớn hơn vị trí thực tế một đơn vị.
3. Chuỗi là không thay đổi: Các phương thức cắt chuỗi trong Java không làm thay đổi chuỗi gốc, mà trả về một chuỗi mới. Vì vậy, nếu chúng ta muốn thay đổi chuỗi gốc, chúng ta cần gán lại giá trị trả về cho chuỗi gốc.

### Các ví dụ thực tế về cắt chuỗi trong Java

Để hiểu rõ hơn về cách sử dụng các phương thức cắt chuỗi trong Java, chúng ta sẽ xem một số ví dụ thực tế sau:

1. Lấy tên file từ đường dẫn đầy đủ:

```java
    String path = "/home/user/documents/report.pdf";
    String fileName = path.substring(path.lastIndexOf("/") + 1); // fileName = "report.pdf"
```

Ở đây, chúng ta sử dụng phương thức lastIndexOf() để tìm vị trí của ký tự / cuối cùng trong đường dẫn và cắt chuỗi từ vị trí đó đến cuối chuỗi để lấy ra tên file.

2. Chuyển đổi ngày tháng năm thành chuỗi ngày/tháng/năm:

```javascript
    String date = "2024-03-09";
    String[] parts = date.split("-");
    String newDate = parts[2] + "/" + parts[1] + "/" + parts[0]; // newDate = "09/03/2024"
```
Ở đây, chúng ta sử dụng phương thức split() để chia chuỗi thành một mảng các chuỗi con dựa trên ký tự -. Sau đó, chúng ta sử dụng các phần tử trong mảng này để tạo ra chuỗi mới có định dạng ngày/tháng/năm.

### So sánh các cách cắt chuỗi trong Java

Có hai cách chính để cắt chuỗi trong Java là sử dụng chỉ số và sử dụng phương thức substring(). Cả hai cách này đều có những ưu điểm và hạn chế riêng, vì vậy chúng ta cần cân nhắc để chọn cách phù hợp cho từng tình huống.

Sử dụng chỉ số:

- Ưu điểm: Đơn giản và dễ hiểu.
- Hạn chế: Chỉ có thể cắt chuỗi theo vị trí bắt đầu và kết thúc đã biết trước.
Sử dụng phương thức substring():

- Ưu điểm: Linh hoạt, có thể cắt chuỗi theo vị trí bất kỳ.
- Hạn chế: Phức tạp hơn khi cần cắt chuỗi theo nhiều vị trí khác nhau.
Vì vậy, chúng ta cần cân nhắc các yếu tố như tính đơn giản, tính linh hoạt và hiệu suất để chọn cách cắt chuỗi phù hợp cho từng tình huống.

## Tài liệu tham khảo

1. [Các phương thức cắt chuỗi trong Java](https://topdev.vn/blog/cac-phuong-thuc-cat-chuoi-trong-java/#thao-tac-cat-chuoi)


<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>