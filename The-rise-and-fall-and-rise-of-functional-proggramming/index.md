### The Rise and Fall and Rise of Functional Programming (Composable Software)

Khi tôi khoảng độ 6 tuổi, tôi đã dành tất nhiều thời gian để chơi điện tử với người bạn thân của tôi. Nhà thằng bạn tôi có một cái phòng đầy những máy tính. Với tôi, nó rất khó cưỡng lại. Và điều kì diệu xảy ra, tôi dành rất nhiều giờ để khám phá rất nhiều trò chơi. Một ngày nọ tôi hỏi bạn tôi rằng: "Bằng cách nào chúng ta có thể tạo ra trò chơi được?"

Thằng bạn tôi nói không biết, vì vậy nó hỏi ba nó, ba nó với tay lên kệ kéo xuống cuốn sách của các trò chơi được lập trình một cách cơ bản nhất. Vì vậy, tôi đã bắt đầu con đường lập trình. Vào thời điểm trường công có dạy môn đại số, tôi đã rành về chủ đề này rồi, bởi vì lập trình cơ bản là đại số.

#### The Rise of Functional Programming (Sự tăng trưởng của FP)

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

![image](https://user-images.githubusercontent.com/69248909/213656630-0e64ab87-5a78-46cf-bc24-e193c3139b25.png)

Phép tính Lambda có ảnh hưởng lớn đến thiết kế phần mềm và trước khoảng năm 1980, rất nhiều biểu tượng có ảnh hưởng của khoa học máy tính đang xây dựng phần mềm bằng cách sử dụng function composition. Lisp là được tạo ra vào năm 1958 và chịu ảnh hưởng nặng nề của phép tính lambda. Ngày nay, Lisp là ứng dụng lâu đời thứ hai ngôn ngữ vẫn còn được sử dụng phổ biến.

Tôi đã được giới thiệu về nó thông qua AutoLISP: ngôn ngữ kịch bản được sử dụng trong Máy tính phổ biến nhất Phần mềm hỗ trợ thiết kế (CAD):AutoCAD. AutoCAD rất phổ biến, hầu như mọi CAD hỗ trợ AutoLISP để chúng có thể tương thích. Lisp cũng là một cách dạy phổ biến ngôn ngữ trong chương trình khoa học máy tính vì ba lý do:

1. Tính đơn giản của nó giúp bạn dễ dàng học Syntax và ngữ nghĩa cơ bản của Lisp trong khoảng một ngày.
2. Lisp là tất cả về function composition và function composition là một cách tao nhã để cấu trúc các ứng dụng.
3. Văn bản khoa học máy tính yêu thích của tôi sử dụng Lisp

#### The Fall of Functional Programming (Sự tuột dốc của FP)

Ở đâu đó giữa những năm 1970 và 1980, cách mà phần mềm đó được tạo ra đã rời xa sự đơn giản, toán đại số và trở thành một danh sách các hướng dẫn tuyến tính để máy tính tuân theo bằng các ngôn ngữ như K&R C (1978) và bộ biên dịch BASIC nhỏ bé được bán cùng với máy tính gia đình đầu tiên của Những năm 1970 và đầu những năm 1980.

Năm 1972, chương trình Smalltalk của Alan Kay được chính thức hóa và ý tưởng về các vật thể là đơn vị nguyên tử của composition đã được giữ vững. Ý tưởng tuyệt vời của Smalltalk về đóng gói Component và truyền Message đã bị biến dạng vào những năm 80 và 90 bởi C++ và Java thành một ý tưởng khủng khiếp về hệ thống phân cấp thừa kế và mối quan hệ is-a để sử dụng lại tính năng.

Mặc dù Smalltalk là một ngôn ngữ OOP, khi C++ và Java tiếp quản thị trường tư duy, Functional Progarmming đã bị loại bỏ bên lề và học viện: Nỗi ám ảnh hạnh phúc của những người đam mê lập trình nhất, các giáo sư trong tòa tháp của họ và một số sinh viên may mắn đã trốn thoát nỗi ám ảnh bức thực ở Java những năm 1990 - 2010.

Đối với hầu hết chúng ta, tạo ra phần mềm là một cơn ác mộng trong 30 năm. Thời kỳ đen tối.

Lưu ý: Tôi đã học viết mã bằng Basic, Pascal, C++ và Java. Tôi đã sử dụng AutoLisp để thao tác đồ họa 3D. Chỉ AutoLisp là hoạt động. Trong vài năm đầu sự nghiệp lập trình của tôi, tôi đã không nhận ra Functional Programming là một lựa chọn thiết thực bên ngoài lĩnh vực này lập trình đồ họa vector.

#### The Rise of Functional Programming (Sự tăng trưởng của FP)

Khoảng năm 2010, một điều tuyệt vời bắt đầu xảy ra: JavaScript bùng nổ. Trước khoảng năm 2006, JavaScript được nhiều người coi là ngôn ngữ đồ chơi được sử dụng để tạo ra các hoạt ảnh dễ thương trong trình duyệt web, nhưng nó có một số tính năng mạnh mẽ ẩn trong đó. Cụ thể, các tính năng quan trọng nhất của phép tính lambda. Mọi người bắt đầu truyền tai nhau về thứ hay ho này được gọi là “Functional Programming”.

Đến năm 2015, ý tưởng về Functional Programming lại phổ biến. Để làm cho nó đơn giản hơn, JavaScript Specification đã có bản nâng cấp lớn đầu tiên của thập kỷ và thêm Arrow Function, khiến nó dễ dàng hơn để tạo và đọc các hàm, biểu thức currying và lambda.

Arrow Function giống như nhiên liệu chất xúc tác cho Functional Programming trong JavaScript. Hôm nay hiếm khi thấy một ứng dụng lớn không sử dụng nhiều kỹ thuật Functional Programming.

Composition là một cách đơn giản, tao nhã và biểu cảm để mô hình hóa rõ ràng hành vi của phần mềm. Quá trình tổng hợp các hàm nhỏ, xác định để tạo các thành phần phần mềm lớn hơn và chức năng tạo ra phần mềm dễ tổ chức, dễ hiểu, gỡ lỗi, mở rộng, kiểm tra và duy trì.
