# The Rise and Fall and Rise of Functional Programming (Composable Software)

Khi tôi khoảng độ 6 tuổi, tôi đã dành tất nhiều thời gian để chơ điện tử với người bạn thân của tôi. Nhà thằng bạn tôi có một cái phòng đầy những máy tính. Với tôi, nó rất khó cũng lại. Và điều kì diệu xảy ra, tôi dành rất nhiều giờ để khám phá rất nhiều trò chơi. Một ngày nọ tôi hỏi bạn tôi rằng: "Bằng cách nào chúng ta có thể tạo ra trò chơi được?"

Thằng bạn tôi nói không biết, vì vậy nó hỏi ba nó, ba nó với tay lên kệ kéo xuống cuốn sách của các trò chơi được lập trình một cách cơ bản nhất. Vì vậy, tôi đã bắt đầu con đường lập trình. Vào thời điểm trường công có dạy môn đại số, tôi đã rành về chủ đề này rồi, bởi vì lập trình cơ bản là đại số.

### The Rise of Functional Programming (Sự tăng trưởng của FP)

Khi khởi đầu với môn khoa học máy tính, trước khi khoa học máy tính được hiển thị thật sự trên máy vi tính, nó đã tồn tại 2 nhà toán học vĩ đại: Alonzo Churh và Alan Turing. Họ tạo ra 2 sự khác nhau, nhưng đó chỉ là mô hình tính toán tương đương. Cả hai mô hình có thể tính toán bất kỳ chức năng có thể tính toán được bằng máy Turing, nghĩa là, cho đầu vào n, có một máy Turing cuối cùng dừng lại và trả về f(n).

Alonzo Church đã phát minh ra phép tính lambda. Phép tính Lambda là một mô hình tính toán phổ quát dựa trên ứng dụng của function. Alan Turing được biết đến với cỗ máy Turing. Một cỗ máy Turing là một mô hình tính toán phổ quát xác định một thiết bị lý thuyết thao tác các ký hiệu trên một dải băng. Như Turing đã nói:

> “Một chức năng có thể tính toán một cách hiệu quả nếu các giá trị của nó có thể được tìm thấy bởi một số phương pháp thuần túy cơ học. tiến trình." ∼ AM Turing

The Church Turing Thesis cho thấy phép tính lambda và máy Turing là tương đương nhau.

Trong tính toán lamda, function là vua. Tất cả mọi thứ là một function, bao gồm cả số. Nghĩ đến việc hoạt động như các atomic building blocks (các mảnh ghép mà từ đó chúng ta xây dựng các tác phẩm của mình) là một cách compose software rất mạnh mẽ và phát triển cao. Trong sách này chúng ta sẽ thảo luận tầm quan trọng của Functional Composing trong thiết kế phần mềm.

Có ba điểm quan trọng làm cho phép tính lambda trở nên đặc biệt:

1. Functions là luôn là những Anonymous. Trong JS, vế phải của _const sum = (x, y) => x + y_ là biểu thức hàm ẩn danh _(x, y) => x + y_
2. Functions trong phép tính lambda luôn là đơn nguyên, nghĩa là chúng chỉ chấp nhận một tham số duy nhất. Nếu bạn có nhiều hơn một tham số, hàm sẽ nhận input và return một hàm mới ở hàm tiếp theo v.v. cho đến khi tất cả các tham số được thu thập và hàm ứng dụng có thể hoàn thành. Hàm _n-ary (x, y) => x + y_ có thể được biểu diễn dưới dạng một hàm như: _x => y => x + y_. Phép biến đổi này từ một hàm n-ary thành một chuỗi các hàm đơn nguyên chức năng được gọi là currying.
3. Functions là Class đầu tiên, nghĩa là các Functions có thể được sử dụng làm input đầu vào cho các function khác và function có thể return về function.

Tóm lại, các tính năng này tạo thành một từ vựng đơn giản nhưng đắt giá để composing software sử dụng hàm bằng cách xây dựng block chính. Trong JS, Anonymous function và Curries Functions là tính năng tuỳ chọn. Mặc dù, JS hỗ trợ phép tính quan trọng Lambda, nhưng không thực thi chúng.

The Classic Function lấy đầu ra ouput từ 1 function và sử dụng nó làm đầu vào input cho function khác. Ví dụ: hàm f . g có thể viết là:

```js
const compose = (f, g) => (x) => f(g(x));
```

Và bây giờ chúng ta sử dụng nó:

```js
const compose = (f, g) => (x) => f(g(x));

const double = (n) => n + 2;
const inc = (n) => n + 1;

const transform = compose(double, inc);

transform(3); // 8
```

Hàm _compose()_ lấy hàm _double_ làm tham số đầu tiên, và hàm _inc_ làm tham số thứ 2, và sau đó return lại 1 Hàm kết hợp cả 2. Bên trong hàm _compose()_ khi _transform()_ được gọi, _f_ là _double()_, _g_ là _inc()_ và _x_ là _3_

![alt](http://~)
