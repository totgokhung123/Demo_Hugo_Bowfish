---
title: "Quản lý và Tối ưu hóa Memory trong JavaScript"
date: 2024-12-12
description: "Tìm hiểu cách JavaScript quản lý memory, các vấn đề phổ biến và kỹ thuật tối ưu để bạn có thể tạo ra những ứng dụng hiệu quả nhất."
tags: ["javascript","http","optimization"]
categories: ["javascript","http","optimization"]
series_order: 4
---
![optimazation](opti.webp "")
Khi phát triển ứng dụng JavaScript, việc quản lý bộ nhớ đóng vai trò quan trọng trong việc đảm bảo hiệu suất. Tối ưu hóa bộ nhớ giúp cải thiện tốc độ, mang đến trải nghiệm tốt hơn cho người dùng. Vấn đề này, mình nghĩ chắc nhiều bạn cũng đã và đang mắc phải, ngay cả bản thân mình cũng vậy.

Bài viết này, mình sẽ hướng dẫn chi tiết dựa trên kinh nghiệm cá nhân về cách JavaScript quản lý memory, các vấn đề phổ biến và kỹ thuật tối ưu để bạn có thể tạo ra những ứng dụng hiệu quả nhất. Đừng lo lắng, vì nó không quá khó khăn như bạn nghĩ đâu, làm là bị cuốn á.

## 1. Hiểu rõ về JavaScript’s Memory Lifecycle

JavaScript quản lý memory thông qua cơ chế Garbage Collection (GC), giúp các developer không cần trực tiếp thao tác cấp phát và giải phóng memory.
Tuy nhiên, để hiểu rõ cách tối ưu hóa, bạn cần nắm rõ ba giai đoạn trong memory lifecycle:

* Cấp phát (Allocation): JavaScript cấp phát memory khi bạn tạo các variables, object và function.
* Cách sử dụng (Usage): Memory được sử dụng khi các variables, object hoặc function còn cần trong code.
* Giải phóng (Garbage Collection): GC sẽ tự động giải phóng memory của các object không còn tham chiếu nào.
Ví dụ như:
```javascript
function allocateMemory() {
    let data = new Array(1000000).fill("memory");
}
```
Khi mà `allocateMemory` chạy, một array lớn sẽ được cấp phát. Khi function hoàn thành, mảng không còn tham chiếu đến data thì GC sẽ giải phóng memory.

Nhưng giả sử mình giữ lại tham chiếu thì sẽ như thế nào?
```javascript
let leakedData;
function allocateMemory() {
    leakedData = new Array(1000000).fill('memory');
}
allocateMemory();
```
Ở đây, biến toàn cục `leakedData` vẫn giữ tham chiếu đến mảng, khiến GC không thể giải phóng được memory.

## 2. Memory Leaks phổ biến trong JavaScript

Mặc dù JavaScript có cơ chế Garbage Collection, một số lỗi code vẫn khiến memory không được giải phóng, dẫn đến rò rỉ. Dưới đây, là các trường hợp phổ biến và cách phát hiện.
![mem](memory.webp "")

### 2.1 Biến toàn cục

Biến toàn cục sẽ tồn tại trong suốt vòng đời của ứng dụng và rất hiếm khi được Garbage Collection. Nếu như không cần thiết, việc sử dụng biến toàn cục sẽ gây lãng phí memory.
```javascript
function myFunc() {
    globalVar = "I'm a memory leak!";
}
myFunc();
```
Ở đây, `globalVar` được khai báo không đúng cách (không có let, const hoặc var), vô hình chung sẽ trở thành biến toàn cục.

Cách khắc phục: luôn khai báo biến với let, const, var
```javascript
function myFunc() {
    let localVar = "I'm safe!";
}
myFunc();
```
### 2.2 Tách biệt DOM Nodes

Khi **DOM** nodes bị xóa khỏi DOM nhưng vẫn còn được tham chiếu đến, chúng sẽ không bị giải phóng.
```javascript
let element = document.getElementById('myElement');
document.body.removeChild(element);
// biến 'element' vẫn giữ tham chiếu đến DOM nodes
```
Thường thì để tránh, bạn nên xóa tham chiếu bằng cách gán null.
```javascript
let element = document.getElementById("myElement");
document.body.removeChild(element);
```
### 2.3 Timers và Callbacks Không Được Giải Phóng
Các setInterval, setTimeout giữ lại tham chiếu nếu không được xóa.

Mình để ý thấy nhiều bạn sẽ viết như thế này:
```javascript
function startTimer() {
    setInterval(() => {
        // Thực hiện một số công việc
    }, 1000);
}
startTimer();
// Timer chạy vô thời hạn mà không thấy dừng
```
Để khắc phục điểm này, bạn nên lưu lại ID của timer và xóa khi không còn cần thiết.
```javascript
function startTimer() {
    let timerId = setInterval(() => {
        // Thực hiện một số công việc
    }, 1000);
    // clear khi không cần
    clearInterval(timerId);
}
startTimer();
```
### 2.4 Closures Không Được Giải Phóng

Closures lưu trữ các biến từ func ngoài. Nếu không cẩn thận, closures có thể giữ lại dữ liệu lớn không cần thiết.
```javascript
function outer() {
    let bigData = new Array(1000000).fill('data');
    return function inner() {
        console.log(bigData[0]);
    };
}
let closureFunc = outer();
// 'bigData' vẫn tồn tại vì 'inner' giữ tham chiếu
```
Khắc phục điểm này bằng cách giảm phạm vi của biến hoặc tránh giữ lại tham chiếu không còn dùng.
```javascript
function outer() {
    let bigData = new Array(1000000).fill('data');
    function inner() {
        console.log(bigData[0]);
    }
    inner();
}
outer();
// 'bigData' sẽ được giải phóng sau khi 'outer' hoàn thành
```
## 3. Cách phòng và khắc phục Memory Leaks

Memory leaks xảy ra khi ứng dụng tiếp tục sử dụng bộ nhớ mà không giải phóng nó sau khi không còn dùng. Điều này sẽ dẫn đến việc sử dụng bộ nhớ tăng dần theo thời gian, có thể giảm hiệu suất hoặc treo ứng dụng. Dưới đây là các kỹ thuật phổ biến để ngăn và xử lý memory leaks trong JavaScript.

### 3.1 Giảm thiểu biến toàn cục

Biến toàn cục tồn tại trong suốt vòng đời của ứng dụng và không được thu gom bởi Garbage Collector (GC) cho đến khi ứng dụng kết thúc. Việc sử dụng quá nhiều biến toàn cục có thể dẫn đến tiêu tốn bộ nhớ không cần thiết. Bạn hãy cùng theo dõi ví dụ sau:
```javascript
function createLeak() {
  globalVar = 'I am a global variable';
}

createLeak();
```
Trong ví dụ này, `globalVar` được khai báo mà không sử dụng let, const hoặc var, do đó nó trở thành một biến toàn cục. Vậy vấn đề ở đây là gì?

* Biến toàn cục `globalVar` sẽ tồn tại cho đến khi ứng dụng kết thúc.
* Nếu biến này lưu trữ lượng dữ liệu lớn, nó sẽ chiếm nhiều bộ nhớ không dùng.
Cách khắc phục vấn đề này khá là đơn giản, bạn hãy nhớ luôn sử dụng let, const hoặc var để giới hạn lại phạm vi của biến.
```javascript
function scopedFunction() {
    let localVar = "This is local";
    // Sử dụng 'localVar' trong phạm vi func
}
scopedFunction();
// 'localVar' không tồn tại bên ngoài func
```
### 3.2 Xóa tham chiếu DOM Nodes

Khi bạn thao tác với DOM (Document Object Model), việc tạo và xóa các nút (nodes) là thường xuyên. Nếu bạn không xóa các tham chiếu đến các nút DOM đã bị loại bỏ khỏi cây DOM, bộ nhớ sẽ không được giải phóng.
```javascript
let element = document.getElementById('myElement');

// Xóa phần tử khỏi DOM
document.body.removeChild(element);

// Nhưng biến 'element' vẫn giữ tham chiếu đến nút DOM đã bị xóa
```
* Biến element vẫn giữ tham chiếu đến nút DOM đã bị xóa khỏi cây DOM.
* GC không thể giải phóng bộ nhớ của nút DOM này.
Bạn nên gán null cho biến để đảm bảo xóa các tham chiếu đến DOM nodes khi không còn sử dụng.

Ví dụ như:
```javascript
// Xóa phần tử khỏi DOM
document.body.removeChild(element);

// Xóa tham chiếu
element = null;
```
* Khi bạn tiến hành gán null cho element, bạn sẽ loại bỏ tham chiếu đến nút DOM.
* GC sẽ xác định rằng nút DOM không còn được tham chiếu ở bất kỳ đâu và giải phóng memory.
Lưu ý chút nha, nếu biến element của bạn được tham chiếu ở nhiều nơi khác, bạn cần đảm bảo xóa tất cả các tham chiếu để GC có thể giải phóng memory.

### 3.3 Quản Lý Event Listeners và Timers

#### 3.3.1 Timers

Các bộ đếm thời gian (setInterval, setTimeout) và event listeners nếu không được xóa khi không cần thiết sẽ giữ lại các tham chiếu đến hàm callback và các biến liên quan.

Đối với setInterval, thường bạn sẽ sử dụng thế này đúng không?
```javascript
function startAutoRefresh() {
  setInterval(() => {
    // Thực hiện một số công việc
  }, 1000);
}

startAutoRefresh();
// Timer sẽ chạy vô thời hạn nếu không được dừng
```
Nếu bạn đang sử dụng như thế này, sẽ xảy ra vấn đề:

* setInterval tiếp tục chạy mãi mãi, ngay cả khi không còn sử dụng.
* Điều này gây lãng phí tài nguyên và bộ nhớ.
Vậy nên, bạn hãy kiểm tra và sử dụng clearInterval để dừng bộ đếm thời gian khi không còn cần thiết. Ví dụ như sau:
```javascript
let intervalId;

function startAutoRefresh() {
  intervalId = setInterval(() => {
    // TODO: ...
  }, 1000);
}

function stopAutoRefresh() {
  clearInterval(intervalId);
}

startAutoRefresh();

// Khi không còn cần thiết
stopAutoRefresh();
```
Giải thích một chút về ví dụ trên:

* Mình lưu lại ID của bộ đếm để có thể dừng nó sau này, khi mà không còn sử dụng nữa
* Gọi clearInterval(intervalId) để dừng bộ đếm thời gian và giải phóng memory.

#### 3.3.2 Event Listeners

Bạn hãy theo dõi ví dụ này:
```javascript
function attachEvent() {
  let element = document.getElementById('myButton');
  element.addEventListener('click', function handleClick() {
    // Xử lý sự kiện
  });
}

attachEvent();
// Listener sẽ tồn tại ngay cả khi 'element' bị xóa khỏi DOM
```
* Event listener giữ tham chiếu đến element và hàm handleClick.
* Nếu không gỡ bỏ listener, memory sẽ không được giải phóng.
Chú ý sử dụng `removeEventListener` để gỡ bỏ listener khi không còn sử dụng
```javascript
function attachEvent() {
  let element = document.getElementById('myButton');

  function handleClick() {
    // Xử lý sự kiện
  }

  element.addEventListener('click', handleClick);

  // Khi không còn cần thiết
  element.removeEventListener('click', handleClick);
}

attachEvent();
```
* Luôn lưu trữ hàm callback trong một biến hoặc hàm đặt tên để có thể gỡ bỏ sau này.
* Gọi removeEventListener với cùng loại sự kiện và hàm callback để gỡ bỏ listener.
Một lưu ý nhỏ khi bạn làm việc với ứng dụng Single Page (SPA):

Ở trong SPA, các component có thể được thêm và xóa động, việc quản lý event listeners và timers sẽ càng quan trọng để ngăn ngừa memory leaks. Ví dụ trong React Component:
```javascript
import React, { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    const intervalId = setInterval(() => {
      // Thực hiện một số công việc
    }, 1000);

    return () => {
      // Hàm cleanup
      clearInterval(intervalId);
    };
  }, []);

  return <div>My Component</div>;
}

export default MyComponent;
```
* Sử dụng hàm cleanup trong useEffect để dọn dẹp timers khi component bị unmount.
* Giúp ngăn ngừa memory leaks khi component không còn hiển thị.
  
## 4. Các kỹ thuật tối ưu (Optimization) memory

Ngoài việc tránh rò rỉ memory, tối ưu hóa bộ nhớ sẽ giúp cải thiện hiệu suất ứng dụng. Dưới đây là một số kỹ thuật bạn nên biết đến

### 4.1 Sử dụng Weak References (WeakMap, WeakSet)

Weak References là các tham chiếu yếu đến đối tượng, cho phép Garbage Collector - GC giải phóng bộ nhớ khi không còn tham chiếu mạnh nào đến đối tượng đó.

* Trong JavaScript, WeakMap và WeakSet là hai cấu trúc dữ liệu hỗ trợ Weak References.
* WeakMap lưu trữ cặp key-value, trong đó key là một đối tượng và value có thể là bất kỳ loại dữ liệu nào.
* WeakSet lưu trữ các đối tượng duy nhất.
Ví dụ khi bạn sử dụng Map
```javascript
let map = new Map();
let obj = { name: 'Object 1' };
map.set(obj, 'Some metadata');

// Xóa tham chiếu gốc
obj = null;

// Đối tượng 'obj' vẫn tồn tại trong 'map', ngăn GC giải phóng bộ nhớ
```
Mặc dù mình đã gán obj = null, đối tượng vẫn được giữ lại trong map. Bạn nên sử dụng WeakMap để khắc phục vấn đề này:
```javascript
let weakMap = new WeakMap();
let obj = { name: 'Object 1' };
weakMap.set(obj, 'Some metadata');

// Xóa tham chiếu gốc
obj = null;
```
Khi obj không còn được tham chiếu ở nơi nào khác ngoài weakMap, GC sẽ tự động giải phóng bộ nhớ của obj.

Nhưng hãy cẩn thận, cân nhắc khi sử dụng WeakMap:

* WeakMap chỉ chấp nhận các keys là đối tượng, không phải là giá trị nguyên thủy như số hay chuỗi.
* Không thể lặp qua WeakMap hoặc WeakSet bằng cách sử dụng vòng lặp for...of hoặc các phương thức như forEach, vì các keys có thể biến mất bất cứ lúc nào do GC.
Theo mình, thì chỉ nên sử dụng khi: cần lưu trữ dữ liệu phụ liên quan đến đối tượng mà không muốn ngăn cản việc GC giải phóng đối tượng đó. Ví dụ: lưu trữ trạng thái, metadata hoặc các thông tin tạm thời khác.

### 4.2 Lazy Loading

Lazy Loading là kỹ thuật trì hoãn việc khởi tạo hoặc tải dữ liệu cho đến khi thực sự cần thiết. Mục đích là giảm thiểu việc sử dụng tài nguyên hệ thống (bộ nhớ, băng thông) và cải thiện hiệu suất.

Các lợi ích khi sử dụng Lazy Loading:

* Tiết kiệm bộ nhớ: chỉ sử dụng bộ nhớ khi cần thiết.
* Tăng tốc độ khởi động ứng dụng: tránh tải các tài nguyên không cần thiết ngay lập tức.
* Cải thiện trải nghiệm người dùng: ứng dụng phản hồi nhanh hơn.
```javascript
// Tải dữ liệu lớn ngay khi ứng dụng khởi động
let heavyData = loadHeavyData();

function loadHeavyData() {
  // Giả sử đây là hàm tải dữ liệu lớn
  return new Array(1000000).fill('data');
}

function processData() {
  // Sử dụng 'heavyData' để xử lý
}
```
* `heavyData` được tải ngay cả khi `processData` chưa được gọi.
* Lãng phí bộ nhớ nếu `heavyData` không được sử dụng.
```javascript
let heavyData = null;

function getHeavyData() {
  if (!heavyData) {
    heavyData = loadHeavyData();
  }
  return heavyData;
}

function loadHeavyData() {
  // Giả sử đây là hàm tải dữ liệu lớn
  return new Array(1000000).fill('data');
}

function processData() {
  let data = getHeavyData();
  // Sử dụng 'data' để xử lý
}
```
* heavyData chỉ được khởi tạo khi getHeavyData được gọi lần đầu tiên.
* Nếu như processData không bao giờ được gọi, heavyData sẽ không bao giờ được load.
Trong thực tế bạn cũng dễ dàng thấy được:

* Tải hình ảnh hoặc video khi người dùng cuộn đến (ví dụ: trên các trang web dài).
* Tải module hoặc component khi cần thiết trong các ứng dụng SPA (Single Page Application).
* Kết nối cơ sở dữ liệu hoặc thư viện bên ngoài chỉ khi cần sử dụng.
Đừng quá lạm dụng lazy loading, bạn cần đảm bảo việc trì hoãn sẽ không ảnh hưởng đến trải nghiệm người dùng (ví dụ: không gây ra độ trễ đáng kể khi người dùng thực sự cần dữ liệu).

### 4.3 Cấu trúc Dữ liệu Map, Set

Map và Set là các cấu trúc dữ liệu được cung cấp trong ES6, cung cấp hiệu suất và tính năng vượt trội so với Object và Array trong một số trường hợp.

* Map: lưu trữ cặp key-value, keys có thể là bất kỳ loại dữ liệu nào (bao gồm cả object, function).
* Set: lưu trữ các giá trị duy nhất, không trùng lặp.
Lợi ích:

* Hiệu suất cao hơn: các thao tác thêm, xóa, tìm kiếm nhanh hơn với dữ liệu lớn.
* Linh hoạt: keys trong Map có thể là bất kỳ giá trị nào, không chỉ là string.
* Tránh trùng lặp: Set đảm bảo mỗi giá trị chỉ xuất hiện duy nhất một lần.
```javascript
let data = {};
for (let i = 0; i < 1000000; i++) {
  data['key' + i] = 'value' + i;
}

// Kiểm tra sự tồn tại của một key
if (data.hasOwnProperty('key500000')) {
  // Thực hiện công việc
}
```
* Các thao tác với Object có thể chậm khi số lượng keys lớn.
* Keys trong Object chỉ có thể là chuỗi hoặc symbol.
* Các phương thức kế thừa từ Object.prototype có thể gây ra xung đột.
Bạn có thể cải thiện đoạn code trên với Map
```javascript
let data = new Map();
for (let i = 0; i < 1000000; i++) {
  data.set('key' + i, 'value' + i);
}

// Kiểm tra sự tồn tại của một key
if (data.has('key500000')) {
  // Thực hiện công việc
}
```
Hay bạn có thể sử dụng Set để loại bỏ sự trùng lặp trong dữ liệu
```javascript
let arrayWithDuplicates = [1, 2, 3, 2, 1, 4, 5];

let uniqueArray = Array.from(new Set(arrayWithDuplicates));

console.log(uniqueArray); // Kết quả: [1, 2, 3, 4, 5]
```
### 4.4 Pooling

Object Pooling là kỹ thuật tái sử dụng các đối tượng đã tạo thay vì tạo mới mỗi lần cần. Phù hợp khi việc khởi tạo đối tượng tốn kém về tài nguyên (CPU, bộ nhớ) và bạn cần tạo nhiều đối tượng tương tự trong suốt quá trình chạy ứng dụng.

* Tránh việc tạo và hủy đối tượng liên tục.
* Giảm thiểu việc cấp phát và giải phóng bộ nhớ.
* Ứng dụng chạy mượt hơn, đặc biệt trong các trò chơi hoặc các ứng dụng đồ họa.
```javascript
function createParticle() {
  return {
    x: 0,
    y: 0,
    velocityX: Math.random(),
    velocityY: Math.random(),
    // Các thuộc tính khác
  };
}

function simulate() {
  let particles = [];
  for (let i = 0; i < 1000; i++) {
    particles.push(createParticle());
  }
  // Thực hiện mô phỏng với particles
  // Sau khi xong, particles sẽ được GC thu gom
}
```
Bạn có thể nhận thấy:

* Mỗi lần `simulate` được gọi, 1000 đối tượng mới sẽ được tạo.
* Gây áp lực lên GC khi phải thu gom nhiều đối tượng ngắn hạn.
```javascript
const particlePool = [];

function getParticle() {
  if (particlePool.length > 0) {
    return particlePool.pop();
  } else {
    return {
      x: 0,
      y: 0,
      velocityX: 0,
      velocityY: 0,
      // Các thuộc tính khác
    };
  }
}

function releaseParticle(particle) {
  // Đặt lại trạng thái của particle nếu cần
  particle.x = 0;
  particle.y = 0;
  particle.velocityX = 0;
  particle.velocityY = 0;
  particlePool.push(particle);
}

function simulate() {
  let particles = [];
  for (let i = 0; i < 1000; i++) {
    let particle = getParticle();
    particle.velocityX = Math.random();
    particle.velocityY = Math.random();
    particles.push(particle);
  }
  // Thực hiện mô phỏng với particles

  // Sau khi xong, đưa các particles trở lại pool
  for (let particle of particles) {
    releaseParticle(particle);
  }
}
```
`getParticle`:

* Kiểm tra xem có đối tượng nào trong pool không.
* Nếu có, sẽ lấy ra và sử dụng. Nếu không, tạo mới một đối tượng.
`releaseParticle`:

* Đặt lại trạng thái của đối tượng để chuẩn bị cho lần sử dụng tiếp theo.
* Đưa đối tượng trở lại pool.
`simulate`:

* Sử dụng các đối tượng từ pool thay vì tạo mới.
* Sau khi sử dụng xong, trả lại đối tượng vào pool.
Lưu ý:

* Cần cẩn thận khi tái sử dụng đối tượng để tránh giữ lại dữ liệu cũ không mong muốn.
* Đảm bảo reset hoặc khởi tạo lại các thuộc tính của đối tượng trước khi sử dụng lại.
* Object Pooling có thể không phù hợp với mọi trường hợp. Cân nhắc trước giữa lợi ích và sự phức tạp trước khi triển khai.

## 5. Kết luận
Quản lý bộ nhớ hiệu quả không phải là một nhiệm vụ dễ dàng, nhưng lại có sức hút mạnh mẽ, bạn sẽ thấy nó trở thành một phần tự nhiên trong quy trình phát triển của mình. Đừng ngần ngại thử nghiệm và áp dụng những gì bạn đã học vào dự án thực tế. Những cải tiến nhỏ trong cách bạn quản lý bộ nhớ hôm nay có thể mang lại những lợi ích lớn về hiệu suất và trải nghiệm của người dùng.
<style>
    .max-w-prose {
        max-width: 825px;
        justify-content: center;
        margin-left: auto;
        margin-right: auto;
    }
</style>