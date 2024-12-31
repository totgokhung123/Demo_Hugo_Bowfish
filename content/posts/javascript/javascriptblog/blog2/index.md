---
title: "Gửi HTTP Request trong JavaScript: Hướng dẫn toàn diện cho người mới bắt đầu"
date: 2024-11-12
description: "Có một số phương thức bạn có thể sử dụng để gửi HTTP request và mỗi phương thức phục vụ một mục đích khác nhau, như được hiển thị bên dưới"
tags: ["javascript","http"]
categories: ["javascript","http"]
series_order: 2
---

Ngày nay, sự tương tác giữa các ứng dụng web dựa trên HTTP. Ví dụ, giả sử bạn có một ứng dụng cửa hàng trực tuyến và bạn muốn tạo một sản phẩm mới. Bạn phải điền tất cả thông tin cần thiết và có thể nhấp vào nút "Tạo".

Hành động này sẽ gửi một HTTP request đến backend cùng với tất cả dữ liệu cần thiết và ứng dụng backend sẽ sử dụng dữ liệu đó để thực hiện các thay đổi đối với cơ sở dữ liệu. Sau khi hành động hoàn tất, cho dù thành công hay không, một HTTP response sẽ được gửi lại cho frontend, nơi nó sẽ hoạt động tương ứng dựa trên trạng thái của phản hồi đó.

Khi các request và response này được truyền qua và lại, chúng cần tuân theo một định dạng nhất định để cả hai đầu có thể hiểu nhau. HTTP được tạo ra cho mục đích này. Nó là một giao thức mạng tiêu chuẩn cho phép các ứng dụng web hiểu và giao tiếp với nhau.

## Các phương thức HTTP Request phổ biến

Có một số phương thức bạn có thể sử dụng để gửi HTTP request và mỗi phương thức phục vụ một mục đích khác nhau, như được hiển thị bên dưới:

### 1. Phương thức GET

Phương thức GET được sử dụng để yêu cầu dữ liệu và tài nguyên từ máy chủ. Khi bạn gửi yêu cầu GET, các tham số truy vấn được nhúng trong URL theo các cặp name/value như thế này:
```
http://example.com/index.html?name1=value1&name2=value2
```
Lưu ý rằng dấu hỏi chấm (?) biểu thị phần đầu của danh sách các tham số. Mỗi tham số tạo thành một cặp key/value (name=value) và dấu và (&) được sử dụng để phân chia hai tham số khác nhau.

### 2. Phương thức POST

Phương thức POST được sử dụng để gửi dữ liệu đến máy chủ, cho dù là thêm một tài nguyên mới hay cập nhật một tài nguyên hiện có. Các tham số được lưu trữ trong phần thân của HTTP request.

```
POST /index.html HTTP/1.1
Host: example.com
name1=value1&name2=value2
```
### 3. Phương thức DELETE

Phương thức này xóa một tài nguyên khỏi máy chủ.

### 4. Phương thức HEAD

Phương thức HEAD hoạt động giống như GET ngoại trừ việc HTTP response được gửi từ máy chủ sẽ chỉ chứa phần đầu nhưng không phải phần thân. Điều này có nghĩa là nếu máy chủ "OK" với yêu cầu, nó sẽ cung cấp cho bạn phản hồi 200 OK nhưng không phải là tài nguyên bạn đã yêu cầu. Bạn chỉ có thể truy xuất tài nguyên bằng phương thức GET.

Điều này rất hữu ích khi bạn đang kiểm tra xem máy chủ có hoạt động hay không. Đôi khi, tài nguyên có thể mất nhiều thời gian để được truyền tải và cho mục đích thử nghiệm, bạn chỉ cần phản hồi 200 OK để biết rằng mọi thứ hoạt động bình thường.

### 5. Phương thức PUT

Phương thức PUT được sử dụng để cập nhật các tài nguyên hiện có và nó tương tự như phương thức POST với một điểm khác biệt nhỏ.

Khi bạn PUT một tài nguyên đã tồn tại, tài nguyên cũ sẽ bị ghi đè. Và việc thực hiện nhiều yêu cầu PUT giống hệt nhau sẽ có tác dụng như thực hiện một lần.

Khi bạn POST các tài nguyên giống hệt nhau, tài nguyên đó sẽ bị nhân đôi mỗi khi yêu cầu được thực hiện.

## Fetch API Trong JavaScript

Trong một thời gian dài, cộng đồng JavaScript thiếu một cách tiêu chuẩn để gửi HTTP request. Một số người đã sử dụng XMLHttpRequest, hay còn gọi là AJAX, trong khi những người khác lại thích các thư viện bên ngoài như Axios hoặc jQuery.

Fetch API được giới thiệu vào năm 2015 như một cách hiện đại, đơn giản hóa và tiêu chuẩn để tạo HTTP request bằng JavaScript. Nó được hỗ trợ nguyên bản, vì vậy không cần phải cài đặt bất kỳ thư viện của bên thứ ba nào.

## Gửi GET Request Với JavaScript

Fetch API dựa trên cơ chế promise, điều này có nghĩa là nó cung cấp một cú pháp rõ ràng và ngắn gọn để viết các hoạt động không đồng bộ. Ví dụ, đây là cách bạn có thể gửi yêu cầu GET bằng Fetch API.
```javascript
fetch("https://jsonplaceholder.typicode.com/users")
  .then((response) => {
    // If the response is not 2xx, throw an error
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }

    // If the response is 200 OK, return the response in JSON format.
    return response.json();
  })
  .then((data) => console.log(data)) // You can continue to do something to the response.
  .catch((error) => console.error("Fetch error:", error)); // In case of an error, it will be captured and logged
```
Bạn cũng có thể bao gồm các tùy chọn tùy chỉnh với yêu cầu, chẳng hạn như tiêu đề tùy chỉnh, mã thông báo ủy quyền, v.v.
```javascript
fetch("https://jsonplaceholder.typicode.com/users", {
  headers: {
    "Content-Type": "application/json",
    "Authorization": "your-token-here",
  },
  credentials: "same-origin",
})
  .then(. . .);
```
## Gửi POST Request với JavaScript

Khi gửi yêu cầu POST, mọi thứ trở nên phức tạp hơn một chút vì bạn cần gửi dữ liệu đến máy chủ với phần thân yêu cầu. Điều này có thể trở nên phức tạp tùy thuộc vào loại dữ liệu bạn đang gửi và trường hợp sử dụng cụ thể của bạn.

Ví dụ, đoạn mã sau gửi dữ liệu JSON đến backend:
```javascript
fetch("https://jsonplaceholder.typicode.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "John Doe",
    email: "johndoe@example.com",
  }),
});
```
Có một vài điều bạn phải chú ý ở đây. Trước hết, bạn phải chỉ định rõ ràng phương thức yêu cầu. Nếu bạn bỏ qua điều này, phương thức GET mặc định sẽ được sử dụng.

Ngoài ra, phần thân yêu cầu chỉ chấp nhận dữ liệu chuỗi, vì vậy bạn phải sử dụng phương thức stringify() để chuyển đổi JSON thành chuỗi trước khi gán nó cho phần thân yêu cầu.

Đây cũng là lý do tại sao điều quan trọng là phải bao gồm tiêu đề Content-Type, cho phép bất kỳ ai ở phía nhận biết cách phân tích cú pháp phần thân yêu cầu.

Tuy nhiên, mọi thứ thường phức tạp hơn trong thực tế. Ví dụ, khi làm việc với các biểu mẫu web, thay vì JSON, bạn có thể đang sử dụng mã hóa biểu mẫu x-www-form-urlencoded, trong trường hợp này, yêu cầu có thể được gửi như thế này.

Ví dụ sau giả định rằng bạn hiểu trình xử lý sự kiện là gì.
```javascript
document.addEventListener("DOMContentLoaded", function () {
  const form = document.querySelector("form");
  const usernameInput = document.getElementById("username");
  const emailInput = document.getElementById("email");

  const formData = new URLSearchParams();

  usernameInput.addEventListener("input", function () {
    formData.set("username", usernameInput.value);
  });

  emailInput.addEventListener("input", function () {
    formData.set("email", emailInput.value);
  });

  form.addEventListener("submit", async function (event) {
    event.preventDefault(); // Prevent the default form submission action

    await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      body: formData.toString(),
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
      },
    });
  });
});
```
Nếu bạn cần tải tệp lên backend, bạn sẽ cần mã hóa biểu mẫu multipart/form-data.
```javascript
document.addEventListener("DOMContentLoaded", function () {
  const form = document.getElementById("myForm");
  const usernameInput = document.getElementById("username");
  const emailInput = document.getElementById("email");
  const pictureInput = document.getElementById("picture");

  const formData = new FormData();

  usernameInput.addEventListener("input", function () {
    formData.set("username", usernameInput.value);
  });

  emailInput.addEventListener("input", function () {
    formData.set("email", emailInput.value);
  });

  pictureInput.addEventListener("change", function () {
    formData.set("picture", pictureInput.files[0]);
  });

  form.addEventListener("submit", async function (event) {
    event.preventDefault(); // Prevent the default form submission

    await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      body: formData,
    });
  });
});
```
Lưu ý rằng khi sử dụng FormData() để tạo phần thân yêu cầu, Content-Type sẽ bị khóa thành multipart/form-data. Trong trường hợp này, không cần thiết phải đặt tiêu đề Content-Type tùy chỉnh.

## Gửi PUT và DELETE Request với JavaScript

Yêu cầu PUT hoạt động tương tự như POST, nhưng bạn phải nhớ đặt method thành PUT.
```javascript
fetch("https://jsonplaceholder.typicode.com/users", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    id: "123"
    name: "John Doe",
    email: "johndoe@example.com",
  }),
});
```
Thực tế, bạn sẽ phải cung cấp id hoặc bất kỳ khóa nào khác cho phép bạn xác định vị trí bản ghi cần cập nhật trong backend.

Yêu cầu DELETE hoạt động tương tự như PUT, nhưng hãy nhớ đặt method thành DELETE.
```javascript
fetch("https://jsonplaceholder.typicode.com/users/123", {
  method: "DELETE",
});
```
Và tương tự, hãy nhớ cung cấp một id để ứng dụng backend biết bản ghi nào cần xóa.

## Cách gửi yêu cầu bằng XMLHttpRequest (AJAX)

Ngoài fetch() ra, chúng ta cũng có thể thực hiện HTTP Request bằng cách sử dụng XMLHttpRequest. Ví dụ sau đây minh họa cách yêu cầu thực hiện đến điểm cuối https://jsonplaceholder.typicode.com
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://jsonplaceholder.typicode.com/users", true);
xhr.onload = function () {
  if (xhr.status >= 200 && xhr.status < 300) {
    console.log(JSON.parse(xhr.responseText));
  } else {
    console.error("Error:", xhr.statusText);
  }
};
xhr.onerror = function () {
  console.error("Request failed");
};
xhr.send();
```
Cú pháp phức tạp hơn một chút vì XMLHttpRequest dựa vào các hàm gọi lại để làm việc với các hoạt động không đồng bộ, nghĩa là dễ dẫn đến tình trạng được gọi là callback hell, nơi bạn có nhiều lớp hàm gọi lại, khiến cơ sở mã của bạn khó đọc và bảo trì.

Tuy nhiên, XMLHttpRequest có một số ưu điểm. Do thực tế là XMLHttpRequest cũ hơn nhiều so với fetch(), nên nó được hỗ trợ rộng rãi hơn. Bạn nên cân nhắc sử dụng XMLHttpRequest khi ứng dụng web của bạn cần tương thích với các trình duyệt cũ hơn.

## Cách gửi Request sử dụng thư viện bên ngoài

Ngoài các phương thức tích hợp, bạn cũng có thể gửi HTTP Request bằng các thư viện của bên thứ ba. Ví dụ, đây là cách bạn có thể gửi yêu cầu GET bằng jQuery:
```javascript
$.get("https://api.example.com/data", function (data) {
  console.log(data);
}).fail(function (error) {
  console.error("Error:", error);
});
```
jQuery là một trong những thư viện JavaScript phổ biến nhất. Nó nhằm mục đích sửa phần JavaScript khó sử dụng và đã khá thành công.

Trong những năm gần đây, jQuery đã mất đi một số sự phổ biến vì JavaScript đã liên tục được cải thiện qua nhiều năm và các vấn đề từng làm phiền mọi người đến nay đã được khắc phục. Nó không còn là lựa chọn hàng đầu để tạo ứng dụng JavaScript, đặc biệt là đối với các lập trình viên mới.

Ngoài ra, bạn có thể sử dụng Axios, một trình khách HTTP dựa trên promise-based HTTP giống như fetch(), và đã được mọi người ưa chuộng trong một thời gian rất dài trước khi fetch()ra mắt.
```javascript
axios
  .get("https://api.example.com/data")
  .then((response) => console.log(response.data))
  .catch((error) => console.error("Axios error:", error));

```
Axios và fetch() có cú pháp rất giống nhau vì cả hai đều dựa trên promise-based. Sự khác biệt chính giữa chúng là fetch() được tích hợp sẵn, trong khi Axios yêu cầu bạn phải cài đặt một thư viện bên ngoài. Tuy nhiên, Axios có nhiều tính năng hơn nhiều vì nó đi kèm với các trình chặn yêu cầu/phản hồi, xử lý JSON tự động và thời gian chờ tích hợp sẵn.

Hy vọng qua bài viết này, bạn đã biết cách để gửi HTTP Request trong JavaScript bằng nhiều cách khác nhau. Cảm ơn các bạn đã theo dõi.


<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>