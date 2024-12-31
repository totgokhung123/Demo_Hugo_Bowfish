---
title: "Java là gì? Tổng quan về ngôn ngữ lập trình Java"
date: 2024-06-23
description: "Java là gì? Tổng quan về ngôn ngữ lập trình Java."
tags: ["Java"]
categories: ["Java"]
series: ["Java"]
series_order: 1
---
## Java là gì?

Java là một trong những ngôn ngữ lập trình hướng đối tượng. Ngôn ngữ Java được sử dụng phổ biến trong phát triển phần mềm, trang web, game hay ứng dụng trên các thiết bị di động.

Java được khởi đầu bởi James Gosling và bạn đồng nghiệp ở Sun MicroSystem năm 1991. Ban đầu Java được tạo ra nhằm mục đích viết phần mềm cho các sản phẩm gia dụng, và có tên là Oak. Java được chính thức phát hành năm 1994, đến năm 2010 được Oracle mua lại từ Sun MicroSystem.

## Đặc điểm của ngôn ngữ lập trình Java là gì?

### Tương tự C++, hướng đối tượng hoàn toàn

Trong quá trình tạo ra một ngôn ngữ mới phục vụ cho mục đích chạy được trên nhiều nền tảng, các kỹ sư của Sun MicroSystem muốn tạo ra một ngôn ngữ dễ học và quen thuộc với đa số người lập trình. Vì vậy họ đã sử dụng lại các cú pháp của C và C++.

Tuy nhiên, trong Java thao tác với con trỏ bị lược bỏ nhằm đảo bảo tính an toàn và dễ sử dụng hơn. Các thao tác overload, goto hay các cấu trúc như struct và union cũng được loại bỏ khỏi Java.

### Độc lập phần cứng và hệ điều hành

Một chương trình viết bằng ngôn ngữ Java có thể chạy tốt ở nhiều môi trường khác nhau. Gọi là khả năng “cross-platform”. Khả năng độc lập phần cứng và hệ điều hành được thể hiện ở 2 cấp độ là cấp độ mã nguồn và cấp độ nhị phân.

Ở cấp độ mã nguồn: Kiểu dữ liệu trong Java nhất quán cho tất cả các hệ điều hành và phần cứng khác nhau. Java có riêng một bộ thư viện để hỗ trợ vấn đề này. Chương trình viết bằng ngôn ngữ Java có thể biên dịch trên nhiều loại máy khác nhau mà không gặp lỗi.

Ở cấp độ nhị phân: Một mã biên dịch có thể chạy trên nhiều nền tảng khác nhau mà không cần dịch lại mã nguồn. Tuy nhiên cần có Java Virtual Machine để thông dịch đoạn mã này.

### Ngôn ngữ thông dịch

Ngôn ngữ lập trình thường được chia ra làm 2 loại (tùy theo các hiện thực hóa ngôn ngữ đó) là ngôn ngữ thông dịch và ngôn ngữ biên dịch.

Thông dịch (Interpreter) : Nó dịch từng lệnh rồi chạy từng lệnh, lần sau muốn chạy lại thì phải dịch lại.
Biên dịch (Compiler): Code sau khi được biên dịch sẽ tạo ra 1 file thường là .exe, và file .exe này có thể đem sử dụng lại không cần biên dịch nữa.
Ngôn ngữ lập trình Java thuộc loại ngôn ngữ thông dịch. Chính xác hơn, Java là loại ngôn ngữ vừa biên dịch vừa thông dịch. Cụ thể như sau

Khi viết mã, hệ thống tạo ra một tệp .java. Khi biên dịch mã nguồn của chương trình sẽ được biên dịch ra mã byte code. Máy ảo Java (Java Virtual Machine) sẽ thông dịch mã byte code này thành machine code  (hay native code) khi nhận được yêu cầu chạy chương trình.

Ưu điểm : Phương pháp này giúp các đoạn mã viết bằng Java có thể chạy được trên nhiều nền tảng khác nhau. Với điều kiện là JVM có hỗ trợ chạy trên nền tảng này.

Nhược điểm : Cũng như các ngôn ngữ thông dịch khác, quá trình chạy các đoạn mã Java là chậm hơn các ngôn ngữ biên dịch khác (tuy nhiên vẫn ở trong một mức chấp nhận được).

### Cơ chế thu gom rác tự động

Khi tạo ra các đối tượng trong Java, JRE sẽ tự động cấp phát không gian bộ nhớ cho các đối tượng ở trên heap.

Với ngôn ngữ như C/C++, bạn sẽ phải yêu cầu hủy vùng nhớ mà bạn đã  cấp phát, để tránh việc thất thoát vùng nhớ. Tuy nhiên vì một lý do nào đó, bạn không hủy một vài vùng nhớ, dẫn đến việc thất thoát và làm giảm hiệu năng chương trình.

Ngôn ngữ lập trình Java hỗ trợ cho bạn điều đó, nghĩa là bạn không phải  tự gọi hủy các vùng nhớ. Bộ thu dọn rác của Java sẽ theo vết các tài nguyên đã được cấp. Khi không có tham chiếu nào đến vùng nhớ, bộ thu dọn rác sẽ tiến hành thu hồi vùng nhớ đã được cấp phát.

### Đa luồng

Java hỗ trợ lập trình đa tiến trình (multithread) để thực thi các công việc đồng thời. Đồng thời cũng cung cấp giải pháp đồng bộ giữa các tiến trình (giải pháp sử dụng priority…).

### Tính an toàn và bảo mật

#### Tính an toàn

- Ngôn ngữ lập trình Java yêu cầu chặt chẽ về kiểu dữ liệu.
- Dữ liệu phải được khai báo tường minh.
- Không sử dụng con trỏ và các phép toán với con trỏ.
- Java kiểm soát chặt chẽ việc truy nhập đến mảng, chuỗi. Không cho phép sử dụng các kỹ thuật tràn. Do đó các truy nhập sẽ không vượt quá kích thước của mảng hoặc chuỗi.
- Quá trình cấp phát và giải phóng bộ nhớ được thực hiện tự động.
- Cơ chế xử lý lỗi giúp việc xử lý và phục hồi lỗi dễ dàng hơn.

#### Tính bảo mật

Java cung cấp một môi trường quản lý chương trình với nhiều mức khác nhau.

- Mức 1 : Chỉ có thể truy xuất dữ liệu cũng như phương phức thông qua giao diện mà lớp cung cấp.
- Mức 2 : Trình biên dịch kiểm soát các đoạn mã sao cho tuân thủ các quy tắc của ngôn ngữ lập trình Java trước khi thông dịch.
- Mức 3 : Trình thông dịch sẽ kiểm tra mã byte code xem các đoạn mã này có đảm bảo được các quy định, quy tắc trước khi thực thi.
- Mức 4: Java kiểm soát việc nạp các lớp vào bộ nhớ để giám sát việc vi phạm giới hạn truy xuất trước khi nạp vào hệ thống.

## Các loại ứng dụng được phát triển sử dụng Java

Java là một ngôn ngữ lập trình phổ biến, mạnh mẽ và được sử dụng rộng rãi trong nhiều lĩnh vực khác nhau nhờ vào tính độc lập nền tảng, hiệu suất ổn định và bộ thư viện phong phú. Dưới đây là các ứng dụng chính của Java trong nhiều lĩnh vực:

### Phát triển Game

Java được sử dụng để phát triển nhiều game đơn giản cho cả máy tính và di động. Nhờ vào các thư viện như LibGDX và LWJGL (Lightweight Java Game Library), Java cung cấp môi trường phát triển mạnh mẽ cho các trò chơi 2D và 3D.

### Đám mây (Cloud Computing)

Java là ngôn ngữ chính được sử dụng trong các dịch vụ và hệ thống đám mây (cloud computing) do khả năng xử lý song song mạnh mẽ và bảo mật cao. Các hệ thống như Amazon Web Services (AWS), Google Cloud và Microsoft Azure đều hỗ trợ Java cho việc phát triển và triển khai các ứng dụng trên đám mây.

### Dữ liệu lớn (Big Data)

Trong lĩnh vực dữ liệu lớn (Big Data), Java đóng vai trò quan trọng nhờ vào các công cụ và framework mạnh mẽ như Apache Hadoop, Apache Spark. Những framework này chủ yếu được viết bằng Java và Scala, cho phép Java có thể xử lý và phân tích lượng dữ liệu lớn một cách hiệu quả.

### Phát triển Web

Java là lựa chọn hàng đầu trong phát triển ứng dụng web nhờ vào các framework như Spring, Hibernate, và Struts. Java giúp xây dựng các ứng dụng web mạnh mẽ, bảo mật và có khả năng mở rộng tốt.

### Trí tuệ nhân tạo (Artificial Intelligence – AI)

Java cũng được sử dụng trong trí tuệ nhân tạo (AI) nhờ vào tính năng đa luồng và khả năng mở rộng. Các thư viện Java hỗ trợ các mô hình học máy, xử lý ngôn ngữ tự nhiên và các thuật toán AI như Deeplearning4j, Weka, và Apache Mahout.

### Internet of Things (IoT)

Java là một ngôn ngữ phổ biến trong Internet of Things (IoT) nhờ vào khả năng tương thích với các thiết bị nhúng và hệ thống nhúng nhỏ gọn. Các hệ thống IoT yêu cầu tính bảo mật, độ ổn định, và khả năng hoạt động trên nhiều nền tảng, điều mà Java có thể đáp ứng tốt.

### Ứng dụng Doanh nghiệp

Java từ lâu đã là lựa chọn hàng đầu trong việc xây dựng các hệ thống quản lý doanh nghiệp như ERP, CRM, và các hệ thống quản lý quy trình kinh doanh phức tạp. Với Java Enterprise Edition (Java EE), các doanh nghiệp có thể phát triển các ứng dụng lớn, phức tạp và bảo mật.

## Tài liệu tham khảo

1. [Java là gì? Tổng quan về ngôn ngữ lập trình Java](https://topdev.vn/blog/tong-quan-ve-ngon-ngu-lap-trinh-java/#cac-loai-ung-dung-duoc-phat-trien-su-dung-java)


<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>