---
title: "JavaScript căn bản"
date: 2024-11-12
description: "Chương đầu tiên này sẽ trình bày về những khái niệm căn bản nhất trong JavaScript.
Bài viết này là một phần của series JavaScript dành cho người mới tiếp cận javascript, giúp các bạn đã có kinh nghiệm code trong các ngôn ngữ khác nhanh chóng làm quen với JS."
tags: ["JavaScript"]
categories: ["JavaScript"]
series: ["JavaScript"]
series_order: 1
---

## JavaScript series
Chương đầu tiên này sẽ trình bày về những khái niệm căn bản nhất trong JavaScript.
Bài viết này là một phần của series JavaScript dành cho người mới tiếp cận javascript, giúp các bạn đã có kinh nghiệm code trong các ngôn ngữ khác nhanh chóng làm quen với JS.
Nếu được rất mong nhận được sự ủng hộ và đóng góp ý kiến của mọi người để hoàn thiện series.
## A. JS introduction
### 1. Introduction
JavaScript (JS) là một ngôn ngữ lập trình client side, được dùng trong trang web bên cạnh HTML và CSS. HTML dùng tạo bộ xương cho trang web, CSS trang trí và tạo layout cho trang web lung linh hơn, thì JS lập trình để có những hành vi, tương tác với người dùng.

Hiện nay, JS không chỉ có thể viết client side mà còn mở rộng ra nhiều lĩnh vực khác, có thể kể tới như viết app với Electron hoặc web service với Node.js. Các thư viện, framework cho JS phát triển rất mạnh, như jquery, React, Angular, Vue,...

Lưu ý, JS không phải Java.

Trong series này chỉ nói tới JS ở khía cạnh cơ bản nhất, là tạo tương tác cho trang web. JS được chạy trong trình duyệt và hầu hết trình duyệt hiện nay đều support tốt JS.
> JS là ngôn ngữ có phân biệt hoa thường.
### 2. Đặt code ở đâu?
**Script tag trong HTML**

Code JS có thể được đặt trong một tag script, và HTML document có thể chứa nhiều script như vậy.

```html
  <script>
    // Đây là đoạn mã JavaScript
    console.log("Hello, Hugo garnacho!");
  </script>
```
Các đoạn code JS trong cùng document có thể được gọi, sử dụng lẫn nhau.
**External JS**

Code JS cũng có thể chứa trong một file riêng, và được liên kết vào HTML cũng bằng thẻ script.
```html
<script src="script.js"></script>
```
**HTML event**

Các thuộc tính event của các HTML tag cũng có thể chứa script. Và code được gọi khi event xảy ra (fire - được bắn ra).

```html
<button type="button" onclick="...">Click me</button>
```
Code JS trong event dạng này thường chỉ dùng để gọi các function đã định nghĩa trong các script khác (script tag hoặc external js), chứ không phù hợp cho các đoạn code quá dài.

**Head or body?**

Script có thể đặt trong cả head lẫn body. Trước đây người ta khuyến khích đặt ở cuối cùng của body, như sau để cải thiện tốc độ tải trang (vì hạn chế script làm delay việc hiển thị).
```html
<html>
  <head></head>
  <body>
      ...
      // Script here
  </body>
</html>
```
Tuy nhiên, nhờ có thêm thuộc tính defer của tag script nên ta không còn bận tâm vấn đề này nữa. Nhờ có defer, code JS sẽ chỉ thực thi khi trang web đã phân tích xong. Chú ý defer chỉ dành cho tệp JS external.
### 3. Output
Có nhiều cách để đưa kết quả ra màn hình để xem. Ví dụ như xem value của biến chẳng hạn. Giống như C++ dùng `cout`, Java dùng `System.out.print()` thì JS cũng có những cách riêng để hiển thị output ra bên ngoài.
**Console.log**

Đưa output ra console của chrome devtools. Cách này khá nhanh và cũng tiện, nó tương tự `cout` trong C++. Nhược điểm duy nhất là bạn phải nhấn F12 để mở console ra xem.

Mỗi lần gọi, console sẽ in ra theo từng dòng nên bạn không cần quan tâm vấn đề xuống dòng. Và nếu in liên tiếp nhiều giá trị, thì console tự động thêm space tách chúng ra. Bạn không cần làm thủ công.
```javascript
  console.log(10 + 5);
```
Tùy vào loại dữ liệu, khi đưa ra console sẽ được hiển thị khác nhau. Và một điểm rất hay là những loại phức tạp như array, object sẽ được hiển thị trực quan, đầy đủ thông tin cần thiết. Ví dụ, thay vì dùng vòng lặp để in ra mảng như sau.
```javascript
let a = [1, 2, 3, 4];
for (let i = 0; i < a.length; i++)
    console.log(a[i]);
```
Thì chỉ cần
```javascript
console.log(a);
```
Console sẽ hiển thị đầy đủ dữ liệu, không chỉ có các phần tử mà còn gồm độ dài mảng. Đối với object thì là các key và value thuộc tính.
**Document.write**

Dùng để ghi một đoạn text, hoặc một đoạn HTML ra trang web.
```javascript
document.write("Hello<br>");
```
Nhược điểm là phải ghi đúng HTML format, nếu muốn xuống dòng phải thêm chuỗi `<br>`. Và chú ý quan trọng, không dùng method này khi trang web tải xong, vì nó sẽ xóa toàn bộ những gì đang có và write lại từ đầu.

**Write to HTML element**

Ngoài ra còn có thể đưa output ra một element nào đó. Ví dụ bạn có một thẻ p, và bạn đưa output ra thẻ này (làm nó hiển thị nội dung output), và bạn có thể đọc được nhờ sự thay đổi trên trang web.
```javascript
document.getElementById("test").innerHTML = 10 + 5;
```
Nhược điểm cách này là khá rườm rà, phải "select" các element, rồi thay đổi thuộc tính `innerHTML` của nó. Nó yêu cầu phải tạo thêm một element, với id hay cái gì đó để xác định, nên gây phức tạp cho chương trình.

**Window.alert()**

Ngoài ra có thể dùng method `alert()` để đưa ra một popup thông báo. Nhưng không được dùng nhiều khi mới học code.
```javascript
alert("Hello world");
```
Nhược điểm là không hiển thị nhiều dữ liệu được, và không hiển thị cùng lúc (vì bị chặn).

## B. JS basic
### 1. Statement

Statement hiểu là một câu lệnh. Trong chương trình có nhiều lệnh, và cuối mỗi lệnh nên đặt dấu chấm phẩy để tách ra. Nếu không đặt cũng không sao, thường thì JS không bắt buộc, nhưng khi bạn viết nhiều lệnh trên cùng một dòng thì nên dùng chấm phẩy tách chúng ra. Ví dụ.
```javascript
console.log(a)
console.log(b)
```
Mặc dù không cần chấm phẩy, các lệnh trên vẫn hoạt động bình thường, vì nằm trên các dòng khác nhau. Nhưng code sau là sai.
```javascript
console.log(a) console.log(b)  // Sai
console.log(a); console.log(b);  // Ok
```
Quy tắc chúng là nên thêm chấm phấy cuối mỗi lệnh, để tránh rắc rối như sau.
```javascript
function ABC() {
    return
        10;  // Trả về là undefined, chứ không phải 10
}
```
JS sẽ hiểu code trên là như sau, dẫn tới việc sai kết quả.
```javascript
function ABC() {
    return;
    10;
}
```
### 2. Comment

Comment bị bỏ qua khi thực thi JS, và có thể dùng comment để giải thích code cho dễ hiểu hơn.

JS có 2 loại comment là single line comment và multi-line comment (block).
```javascript
// This is single line comment
/* This is
    block comment */
```
Comment dạng 1 comment từ vị trí dấu `//` cho tới hết dòng. Comment dạng 2 có thể trải rộng trên nhiều dòng, chỉ cần nằm trong cặp` /* */ `sẽ được coi là comment.

Single line comment phổ biến hơn, trong khi block comment thường dùng trong documentation.
### 3. Variable, constant

Có hai từ khóa khai báo biến là let và var. Vì JS là ngôn ngữ weak type nên không cần chỉ định rõ kiểu của biến, mà được tự động xác định và thay đổi dựa theo value (giá trị) chứa bên trong.
```javascript
let x = 10;
var y = 1.2;
let z;  // z = undefined
```
Biến không khởi tạo giá trị sẽ có value là undefined.

Mặc dù cả let và var đều dùng khai báo biến được, nhưng nên dùng let hơn. Chi tiết sẽ được đề cập trong phần cuối chương này.
```javascript
let a = 10, b = 1.5, c = "John";
var name =
    "Mickey";
```
Biến có thể khai báo trên nhiều dòng, hoặc nhiều biến trên một dòng đều được.
```javascript
const pi = 3.14;
```
Đối với hằng số (constant) thì dùng từ khóa const như trên để khai báo.

### 4. Operators

Toán tử (operator) là những phép tính thực hiện trên các số (biến, hằng, giá trị,...) gọi là các toán hạng (operand). Kết hợp của toán tử và toán hạng tạo ra những biểu thức (expression) và trả về giá trị nào đó.

Tùy số lượng toán hạng tham gia, được chia thành 3 loại toán tử chính:
* Toán tử một ngôi (unary operator): chỉ có một toán hạng, gồm phép thuận `+x`, phép đối `-x` và phủ định `!x`.
* Toán tử hai ngôi (binary operator): có hai toán hạng, và hầu hết các phép tính số học đều là hai ngôi, như phép * cộng `a + b`,...
* Toán tử ba ngôi (ternary operator): nhận 3 toán hạng, dựa vào toán hạng 1 mà lựa chọn trả về toán hạng 2 hoặc 3.

Ngoài ra còn có các toán tử khác, như gán (assignment), logic (logical), so sánh (comparison), thao tác bit (bitwise),...

**Arithmetic operators**

Các phép toán số học trong JS tương tự các ngôn ngữ khác, gồm:

* Toán tử một ngôi: `+x`, lấy số đối `-x`, tăng `++x`, `x++`, giảm `--x`, `x--`.
* Toán tử hai ngôi: cộng `a + b`, trừ `a - b`, nhân `a * b`, chia nguyên `a / b`, chia dư `a & b`.
Ngoài ra từ phiên bản ES6 trở đi có phép lũy thừa `a ** b` để tính số mũ.

**Assignment operators**

Toán tử gán `x = 5` tương tự các ngôn ngữ khác. Ngoài ra JS cũng hỗ trợ các phép gán rút gọn như `x += 5`, `x /= 5`,...

Đặc biệt, JS cho phép gán nhiều giá trị cùng lúc, ví dụ như `a = b = c = 5` thì cả 3 biến a, b, c đều mang giá trị 5.

**Comparison operators**

Gồm các phép so sánh bằng `x == 5`, khác `x != 10` lớn bé, lớn hơn hoặc bằng, bé hơn hoặc bằng như trong các ngôn ngữ khác.

Các toán tử comparison luôn trả về kết quả boolean.

Ngoài ra JS còn có hai phép so sánh mới là strict comparison `x === 10` và `x !== 10`. Điểm khác biệt ở chỗ strict comparison yêu cầu hai vế phải cùng kiểu dữ liệu thì mới so sánh, nếu khác kiểu thì kết quả là false. Trong khi đó loose comparison `x == 10` sẽ tự động convert kiểu phù hợp rồi mới so sánh.

**Logical operators**

Dùng cho các toán hạng boolean. Gồm and `a && b`, or `a || b` và not `!a`.

**Bitwise operators**

Dùng cho các phép thao tác bit, gồm hai dạng.

Dạng 1 dùng biến đổi bit, gồm 3 toán tử hai ngôi (and `x & y`, or `x | y`, xor `x ^ y`) và một toán tử một ngôi (not !x).

Chú ý các phép trên chỉ sử dụng một dấu, thay vì hai dấu như comparison.

Loại thứ 2 dùng dịch chuyển bit (bit shifting), gồm left shift (zero fill) `x << n`, signed right shift `x >> n` và zero fill right shift `x >>> n`.

Trong JS thì thao tác bit ít dùng.

## C. Data types
### 1. Overview

Kiểu dữ liệu (data type) dùng định nghĩa loại dữ liệu mà biến (hoặc hằng) lưu trữ. JS là một ngôn ngữ weak type, nên kiểu dữ liệu không được chỉ định rõ ràng, kiểu được tự động xác định dựa trên giá trị (value) mà nó chứa.

Kiểu dữ liệu của một biến trong JS có thể thay đổi, điều này là không được phép trong các ngôn ngữ strong type.
```javascript
let x = 5;  // number
x = x * 1.5;  // number
x = x + " VND";  // string
```
Trong JS có một số kiểu như sau:
* Number: chứa số nguyên và thực
* Boolean: đúng sai
* String: chuỗi
* Object: đối tượng
* Null
* Undefined
ES6 bổ sung thêm kiểu Symbol nữa. Ngoài ra các kiểu như array, date thực chất cũng là object.

**Typeof operator**

Dùng toán tử typeof để xem kiểu của đối tượng. Kết quả trả về là một string.

**Undefined value**

Biến khi chưa được gán giá trị thì mang value là undefined, và typeof cũng là undefined.

**Empty value**

Các value rỗng như 0, chuỗi rỗng "", null vẫn giữ được kiểu dữ liệu của nó. Ví dụ như sau.
```javascript
typeof 0;  // number
typeof "";  // string
typeof null;  // object
```
**Function type**

Các hàm (function), phương thức (method) cũng là kiểu function, và được xem như các biến. Cả kiểu function và object thuộc loại kiểu phức (complex type).
```javascript
function ABC() {}
typeof ABC;  // function
```
### 2. Type casting

Chuyển đổi kiểu, hay còn gọi là ép kiểu (type casting) là chuyển từ một kiểu này sang kiểu khác. Trong JS, phần nhiều trường hợp sẽ được tự động chuyển (ngầm định - implicit casting), nhưng bạn cũng có thể tự tay ép kiểu theo cách thủ công, rõ ràng (explicit casting).

Cú pháp mặc định cho type casting như sau.
```javascript
Type(old_var);
```
Ví dụ.
```javascript
let x = Number("100");  // string > number
let s1 = String(10);  // number > string
let s2 = 10.toString();  // number > string
```
Về cơ bản là vậy, bên cạnh đó các kiểu cụ thể sẽ có những method chi tiết hơn để thực hiện chuyển đổi. Ví dụ như từ number sang string thì có những method như `toString()`, `toFixed()`, `toPrecision()` chuyển kiểu nhưng với chức năng khác nhau.

Một vài lưu ý:

* Khi xuất biến ra console, hoặc element,... thì JS tự động chuyển thành một string.
* Trong các biểu thức (expression) tính toán thì JS chuyển kiểu theo một số quy tắc nhất định.
Nói chung nên hạn chế type casting, và khi cần thiết nên tránh để JS tự động thực hiện. Hạn chế việc thao tác khác kiểu dữ liệu, vì JS có thể tự động ép kiểu và cho ra kết quả không như mong đợi.

## D. Basic commands
### 1. Conditional statements

**If else statement**

Lệnh if else trong JS khá giống với các ngôn ngữ khác nên mình không bàn nhiều ở đây.
```javascript
if (<condition>)
    ...;
if (<condition>)
    ...
else
    ...
```
`condition` là một biểu thức boolean, có được từ phép so sánh hoặc lấy trực tiếp từ biến, hàm. Nếu biểu thức đúng (true), lệnh đầu tiên sẽ được thực hiện, ngược lại thực hiện lệnh thứ 2 (nếu có).

Đặc biệt, câu lệnh trước `else` trong JS không cần chấm phẩy cũng được.

Các cặp if else có thể lồng nhau (nested) như sau, chú ý `else` `if` là hai từ riêng biệt.
```javascript
if (<condition1>) ...
else if (<condition2>) ...
else if (<condition3>) ...
...
else ...
```
Các statement nếu là lệnh đơn thì không cần ngoặc, nếu từ 2 lệnh trở lên cần có ngoặc {} bao lại.

**Ternary operator**

JS hỗ trợ toán tử ba ngôi (ternary operator) như sau.
```javascript
<condition> ? <true_value> : <false_value>;
```
Toán tử trả về kết quả là một trong hai value đã cho, dựa theo điều kiện `condition`. Nếu điều kiện đúng trả về `true_value`, ngược lại trả về `false_value`.

Toán tử ternary có thể viết liên tiếp nhau như sau.
```javascript
let x = 10;
console.log(x > 0 ? 'So duong' : x < 0 ? 'So am' : 'So khong');
```
Như code trên so sánh x với 0 và báo x là số dương, số âm hay là 0. Câu lệnh trên dùng hai ternary operator liên tiếp nhau vẫn được.

**Switch case**

Dùng so sánh một biểu thức với nhiều nhóm giá trị khác nhau, mỗi giá trị là một case. Nếu khớp với case nào, thì lệnh trong case sẽ được thực hiện. Còn không có case nào khớp thì default sẽ được gọi (nếu có, vì default có thể bỏ qua)
```javascript
switch (1 + 2) {
    case 1: case 2:
        ...
        break;
    case 3:
        ...
        break;
    default:
        ...
}
```
Sau mỗi case nên có break để ngắt, nếu không sẽ bị trôi case, tương tự các ngôn ngữ khác.

Chú ý, switch case sử dụng strict comparison (dấu ===) để so sánh, vì thế nên kiểu dữ liệu của case và expresssion phải giống nhau.

### 2. Loop statements
**While loop**

```javascript
while (<condition>) {
    ...
}
```
Lặp lại một công việc với số lần xác định. Nếu điều kiện `condition` đúng thì lặp lại lần nữa, nếu không thì thoát.

Điều kiện dừng cần phải khả thi, để tránh vòng lặp chạy vô hạn sẽ gây crash trình duyệt.

**Do while loop**
```javascript
do {
    ...
} while (<condition>);
```
Tương tự `while` loop, nhưng thực hiện ít nhất 1 lần, thực hiện xong lệnh mới kiểm tra điều kiện.

**For loop**
```javascript
for (<init>; <condition>; <increment>)
    ...
```
Tương tự trong ngôn ngữ khác, nên mình không bàn nhiều ở đây. Ngoài ra JS cho phép các statement bên trong có thể được bỏ qua (omitting).

**Other loop**

Hai vòng lặp for nữa trong JS là `for of` và `for in`. Ở đây mình ghi ra để làm quen với cú pháp, các bạn có thể bỏ qua, các chương sau sẽ có nhắc tới.

`For of` dùng để duyệt qua lần lượt các element (e) trong một iterable (mảng, chuỗi, map,...)
<textarea id="code-input" rows="5" cols="50">// Viết mã của bạn ở đây</textarea>
<button onclick="runCode()">Run</button>
<pre id="output"></pre>
```javascript
let list = [1, 2, 3, 4];
for (e of list)
    console.log(e);
```
`For in`dùng lặp qua các thuộc tính của object.
```javascript
let obj = {
    name: "John",
    age: 20
}
for (p in obj)
    console.log(p + ": " + obj[p]);
```
**Break & continue**

Lệnh `break` dùng để ngắt một vòng lặp, còn `continue` để dừng lần lặp hiện tại và đi tiếp vòng lặp tiếp theo, tương tự các ngôn ngữ khác.

Ngoải ra `break` còn dùng cho label để break một label block.

<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>
<script>
    function runCode() {
        const code = document.getElementById('code-input').value;
        const outputElement = document.getElementById('output');
        try {
            const result = eval(code);
            outputElement.textContent = result !== undefined ? result : 'Code executed successfully!';
        } catch (error) {
            outputElement.textContent = 'Error: ' + error.message;
        }
    }
</script>