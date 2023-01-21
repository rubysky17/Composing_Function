### Why Learn Functional Programming in JavaScript?

Quên hết điều gì bạn nghĩ rằng bạn biết về JavaScript đi và tiếp cận tài liệu này với người mới bắt đầu. Để giúp bạn làm điều đó, chúng tôi sẽ xem lại những điều cơ bản về JavaScript từ đầu, như thể bạn chưa từng thấy JavaScript trước đây. Nếu bạn là người mới bắt đầu, bạn thật may mắn. Cuối cùng một cái gì đó khám phá ES6 và FP từ đầu! Hy vọng rằng tất cả các khái niệm mới được giải thích theo cách - nhưng đừng tin vào quá nhiều sự nuông chiều bản thân.

Nếu bạn là nhà phát triển dày dạn kinh nghiệm đã quen thuộc với JavaScript hoặc FP thuần túy, có thể bạn đang nghĩ rằng JavaScript là một lựa chọn thú vị để khám phá lập trình chức năng. Bỏ gạt đi những suy nghĩ đó sang một bên và cố gắng tiếp cận tài liệu với tinh thần cởi mở. Bạn có thể thấy rằng ở đó là một cấp độ khác để lập trình JavaScript. Một trong những bạn không bao giờ biết tồn tại.

Vì sách này được gọi là "Composing Software", và FP là cách hiển nhiên để soạn thảo phần mềm (sử dụng function composition, higher order functions, v.v…), bạn có thể tự hỏi tại sao tôi không nói về Haskell, ClojureScript hoặc Elm, thay vì JavaScript.

JavaScript có các tính năng quan trọng nhất cần thiết cho FP:

1. First class functions: Khả năng sử dụng hàm làm giá trị dữ liệu: truyền hàm làm đối số, return về các hàm và gán các hàm cho các biến và thuộc tính đối tượng. Thuộc tính này cho phép cho các higher order functions, cho phép ứng dụng một phần, currying và composition.
2. Anonymous functions và cú pháp lambda ngắn gọn: _x => x \* 2_ là một biểu thức hàm hợp lệ trong JavaScript. Lambda ngắn gọn giúp làm việc với higher-order functions dễ dàng hơn.
3. Closures (tính bao đóng): A closure là gói một chức năng với môi trường của nó, Closure được tạo tại thời điểm tạo Function. Khi một hàm được định nghĩa bên trong một hàm khác, nó có quyền truy cập vào các liên kết biến trong function bên ngoài, ngay cả sau Function bên ngoài exit. Closure là cách các ứng dụng từng phần nhận được các đối số cố định của chúng. Một đối số cố định là một đối số bị ràng buộc trong phạm vi Closure của hàm được trả về. Trong _add2(1)(2)_, _1_ là cố định đối số trong function được return về bởi _add2(1)_.

#### What JavaScript is Missing

JavaScript là một ngôn ngữ đa mô hình, có nghĩa là nó hỗ trợ lập trình ở nhiều dạng khác nhau. Các kiểu khác được JavaScript hỗ trợ bao gồm lập trình thủ tục (bắt buộc) (như C), trong đó các Function đại diện cho một chương trình con của các hướng dẫn có thể được gọi nhiều lần để reusable và organization, hướng đối tượng, trong đó các Object - không phải function - là chính khối xây dựng. Nhược điểm của ngôn ngữ đa mô hình là lập trình hướng đối tượng và bắt buộc có xu hướng ngụ ý rằng hầu hết mọi thứ cần phải được thay đổi.

Mutation là một thay đổi đối với cấu trúc dữ liệu xảy ra tại đó. Ví dụ:

```js
const foo = {
  bar: 'bar';
}

foo.bar = 'qux'; // mutation
```

Các Object thường cần phải có thể thay đổi để các thuộc tính của chúng có thể được cập nhật bằng các phương thức, bắt buộc
lập trình, hầu hết các cấu trúc dữ liệu có thể thay đổi để cho phép thao tác hiệu quả trực tiếp trên các đối tượng và mảng.

Dưới đây là một số tính năng mà một số ngôn ngữ Functional có, mà JavaScript không có:

1. Purity (Độ thuần khiết): Trong một số ngôn ngữ FP, độ thuần khiết được thực thi bởi ngôn ngữ. Biểu hiện với side-effect không được cho phép.
2. Immutation (Tính bất biến): Một số ngôn ngữ FP vô hiệu hóa các đột biến. Thay vì thay đổi một dữ liệu hiện có trên cấu trúc dữ liệu, chẳng hạn như một mảng hoặc đối tượng, các biểu thức đánh giá các cấu trúc dữ liệu mới, điều này có thể nghe có vẻ không hiệu quả, nhưng hầu hết các ngôn ngữ chức năng đều sử dụng cấu trúc dữ liệu dưới hood, điều này chia sẻ cấu trúc tính năng: có nghĩa là đối tượng cũ và đối tượng mới chia sẻ tham chiếu đến dữ liệu giống nhau.
3. Recursion (Đệ quy): Đệ quy là khả năng một hàm tự tham chiếu cho mục đích lặp lại. Trong nhiều ngôn ngữ FP đệ quy là cách duy nhất để lặp lại. Không có báo cáo vòng lặp như vòng lặp for, while hoặc do.

Purity (Độ tinh khiết): Trong JavaScript, độ tinh khiết phải đạt được theo quy ước. Nếu bạn không xây dựng hầu hết ứng dụng bằng cách composing các hàm thuần túy, bạn không lập trình bằng cách sử dụng Functional. hật không may, JavaScript rất dễ đi chệch hướng do vô tình tạo và sử dụng các hàm không thuần túy.

Immutability (Tính bất biến): Trong các ngôn ngữ pure functional tính bất biến thường được thực thi. JavaScript thiếu cấu trúc dữ liệu dựa trên trie hiệu quả, không thay đổi được sử dụng bởi hầu hết các ngôn ngữ Functional, nhưng có các thư viện trợ, bao gồm Immutable.js và Mori. Tôi hy vọng rằng các phiên bản tương lai của Thông số kỹ thuật ECMAScript sẽ bao gồm các cấu trúc dữ liệu bất biến. Có những dấu hiệu mang lại hy vọng, như bổ sung từ khóa const trong ES6. Không thể gán lại ràng buộc tên được xác định bằng const tham chiếu đến một giá trị khác. Điều quan trọng là phải hiểu rằng const không đại diện cho một giá trị bất biến.

Một đối tượng _const_ không thể được chỉ định lại để tham chiếu đến một đối tượng hoàn toàn khác, nhưng đối tượng mà nó tham chiếu để có thể có các thuộc tính của nó bị đột biến. JavaScript cũng có khả năng freeze() các object, nhưng những đối tượng đó các đối tượng chỉ bị freeze ở cấp gốc, nghĩa là một đối tượng lồng nhau vẫn có thể có các thuộc tính của nó bị thay đổi. Nói cách khác, vẫn còn một chặng đường dài phía trước trước khi chúng ta nhìn thấy composite thực sự, Immutables trong đặc tả JavaScript.

Recursion (Đệ quy): Về mặt kỹ thuật, JavaScript hỗ trợ đệ quy, nhưng hầu hết các ngôn ngữ chức năng đều có một tính năng được gọi là proper tail calls. Proper tail calls là một tính năng ngôn ngữ cho phép các hàm đệ quy sử dụng lại các Stack Frames cho các lần gọi đệ quy.

Nếu không có Proper tail calls, 1 stack được gọi có thể phát triển tràn ra Stack. JavaScript các Proper tail calls phù hợp về mặt kỹ thuật trong đặc tả ES6. Thật không may, chỉ có một trong những trình duyệt chính công cụ kích hoạt nó như một tính năng mặc định và tối ưu hóa đã được thực hiện một phần và sau đó sau đó bị xóa khỏi Babel (trình biên dịch JavaScript chuẩn phổ biến nhất, được sử dụng để biên dịch ES6 đến ES5 để sử dụng trong các trình duyệt cũ hơn).

Điểm mấu chốt: Sử dụng đệ quy cho các lần lặp lớn vẫn không an toàn — ngay cả khi bạn cẩn thận gọi hàm ở vị trí đuôi.

#### What JavaScript Has that Pure Functional Languages Lack

Một người theo chủ nghĩa thuần túy sẽ nói với bạn rằng khả năng biến đổi của JavaScript là nhược điểm chính của nó, điều này đôi khi đúng.
Tuy nhiên, tác dụng phụ và đột biến đôi khi có lợi. Trên thực tế, không thể tạo ra hầu hết các ứng dụng hiện đại hữu ích mà không có hiệu ứng. Các ngôn ngữ chức năng thuần túy như Haskell sử dụng các hiệu ứng, nhưng ngụy trang chúng khỏi các chức năng thuần túy bằng cách sử dụng các hộp được gọi là monads, cho phép chương trình duy trì purity mặc dù các hiệu ứng được đại diện bởi các đơn tử là không purity.

Rắc rối với các monads là, mặc dù việc sử dụng chúng khá đơn giản, nhưng việc giải thích thế nào là một monads đối với ai đó không quen thuộc với nhiều ví dụ thì hơi giống như giải thích màu “xanh dương” trông như thế nào như một người mù. Ở dạng cơ bản nhất, một monads chỉ đơn giản là một kiểu dữ liệu ánh xạ và làm phẳng trong một thao tác (sẽ được đề cập sâu hơn sau này). Nhưng để có trực giác về cách chúng được sử dụng và tính linh hoạt mà chúng mang lại cho chúng tôi, bạn thực sự chỉ cần nhảy vào và bắt đầu sử dụng chúng. Nếu bạn đang sử dụng promises hoặc phương thức Array.prototype.flatMap() mới, bạn đã sẵn sàng.

Nhưng học chúng lần đầu tiên có thể rất đáng sợ, và tài liệu thành ngữ về chủ đề không giúp được gì:

> “A monad is a monoid in the category of endofunctors, what’s the problem?” ∼ James Iry, fictionally quoting Philip Wadler, paraphrasing a real quote by Saunders Mac Lane. “A Brief, Incomplete, and Mostly Wrong History of Programming Languages”¹⁵

Thông thường, tác phẩm nhái phóng đại mọi thứ để làm cho điểm hài hước trở nên hài hước hơn. Trong đoạn trích dẫn trên, giải thích về các monads thực sự được đơn giản hóa từ trích dẫn ban đầu, như sau:

> “Một đơn nguyên trong X chỉ là một đơn nguyên trong loại nguyên hàm của X, với tích Ã— được thay thế bằng thành phần của endofunctor và đơn vị được thiết lập bởi endofunctor nhận dạng.” ∼ Saunders Mac. “Danh mục dành cho nhà toán học đang làm việc”¹⁶

Mặc dù vậy, theo tôi, sợ hãi các Monad là lý do yếu. Cách tốt nhất để học các monad không phải là để đọc một loạt sách và bài đăng trên blog về chủ đề này, nhưng để nhảy vào và bắt đầu sử dụng chúng. Như với hầu hết mọi thứ trong Functional Programming, từ vựng học thuật khó hiểu hơn nhiều để hiểu hơn các khái niệm. Tin tôi đi, bạn không cần phải hiểu Saunders Mac Lane để hiểu lập trình chức năng.

Mặc dù nó có thể không hoàn toàn lý tưởng cho mọi phong cách lập trình, nhưng JavaScript là một ngôn ngữ có mục đích chung là được thiết kế để nhiều người có thể sử dụng được với các biến thể style programming và backgrounds.

Theo Brendan Eich¹⁷, điều này đã được cố ý ngay từ đầu. Netscape đã phải hỗ trợ hai các loại lập trình viên:

> “…các tác giả thành phần, những người đã viết bằng C++ hoặc (chúng tôi hy vọng) Java và 'người viết kịch bản', nghiệp dư hoặc chuyên nghiệp, những người sẽ viết mã được nhúng trực tiếp vào HTML.”.

Ban đầu, ý định là Netscape sẽ hỗ trợ hai ngôn ngữ khác nhau và kịch bản ngôn ngữ có thể giống với Scheme (một phương ngữ của Lisp).Như Brendan Eich:

> “Tôi được tuyển dụng vào Netscape với lời hứa sẽ ‘làm Scheme’ trên trình duyệt.”

JavaScript phải là một ngôn ngữ mới:

> “Diktat từ ban quản lý kỹ thuật cấp cao là ngôn ngữ phải 'trông giống như Java’. Điều đó đã loại trừ Perl, Python và Tcl, cùng với Scheme.”

Vì vậy, những ý tưởng trong đầu Brendan Eich ngay từ đầu là:

1. Scheme trong trình duyệt
2. Trông giống như Java.

Nó thậm chí còn giống như một mớ hỗn độn hơn:

“Tôi không tự hào, nhưng tôi rất vui vì tôi đã chọn các first-class function của Scheme-ish và các nguyên mẫu Selfish (mặc dù là số ít) làm thành phần chính. Ảnh hưởng của Java, đặc biệt là y2k Các lỗi ngày mà cả sự phân biệt the primitive vs. object distinction (ví dụ: chuỗi so với Chuỗi), là thật không may."

Tôi muốn thêm vào danh sách các tính năng giống như Java “unfortunate” cuối cùng đã được đưa vào JavaScript:

- Constructor functions và từ khóa mới, với cách gọi và ngữ nghĩa sử dụng khác với các hàm gốc.
- Từ khóa _class_ có tổ tiên _extend_ làm cơ chế as the primary inheritance mechanism.
- Người dùng có xu hướng nghĩ về một _class_ như thể đó là a static type (không phải vậy).

Lời khuyên của tôi: Tránh những thứ đó bất cứ khi nào viết trong mã của riêng bạn. Khi bạn đang đóng góp cho mã không thuộc về mình, hãy áp dụng câu thần chú “khi ở Rome”. Làm như người Rô-ma làm.

Chúng ta thật may mắn khi cuối cùng JavaScript lại trở thành một ngôn ngữ có khả năng như vậy, bởi vì hóa ra cách tiếp cận “scripting” đã chiến thắng cách tiếp cận “component” (ngày nay, các tiện ích mở rộng Java, Flash và ActiveX không được hỗ trợ trong một số lượng lớn trình duyệt đã cài đặt).

Cuối cùng chúng tôi đã có được một ngôn ngữ được trình duyệt hỗ trợ trực tiếp: JavaScript.

Điều đó có nghĩa là các trình duyệt ít cồng kềnh hơn và ít lỗi hơn, bởi vì chúng chỉ cần hỗ trợ một bộ ràng buộc ngôn ngữ duy nhất: JavaScript. Bạn có thể nghĩ rằng WebAssugging là một ngoại lệ, nhưng một trong những mục tiêu thiết kế của WebAssugging là chia sẻ các ràng buộc ngôn ngữ của JavaScript bằng cách sử dụng Abstract Syntax Tree (AST). Trên thực tế, các bản trình diễn đầu tiên đã biên dịch WebAssembly thành một tập con JavaScript được gọi là ASM.js.

Vị trí là ngôn ngữ lập trình mục đích chung tiêu chuẩn duy nhất cho nền tảng web đã cho phép JavaScript vượt qua làn sóng phổ biến ngôn ngữ lớn nhất trong lịch sử phần mềm:

Ứng dụng nuốt chửng thế giới, web nuốt chửng ứng dụng và JavaScript nuốt chửng web.

Theo multiple¹⁸ measures¹⁹, JavaScript²⁰ hiện là ngôn ngữ lập trình phổ biến nhất trên thế giới.

JavaScript không phải là công cụ lý tưởng để FP, nhưng nó là một công cụ tuyệt vời để xây dựng các ứng dụng lớn trên các team độc lập, nơi các team khác nhau có thể có những ý tưởng khác nhau về cách xây dựng ứng dụng.

Một số nhóm có thể tập trung vào việc viết script, nơi lập trình mệnh lệnh đặc biệt hữu ích. Những người khác có thể tập trung vào việc xây dựng các khái niệm abstractions về kiến trúc, trong đó một chút suy nghĩ OO (kiềm chế, cẩn thận) có thể không phải là một ý tưởng tồi. Vẫn còn những người khác có thể nắm lấy FP, giảm các hành động của người dùng bằng cách sử dụng các Pure Function để quản lý ứng dụng có thể kiểm tra, application
state. Các thành viên trong các nhóm này đều sử dụng cùng một ngôn ngữ, nghĩa là họ có thể dễ dàng trao đổi ý kiến, học hỏi lẫn nhau và phát triển dựa trên công việc của nhau.

Trong JavaScript, tất cả những ý tưởng này có thể cùng tồn tại, điều này cho phép nhiều người nắm bắt JavaScript hơn, điều này đã dẫn đến open-source package lớn nhất trên thế giới (tính đến tháng 2 năm 2017), npm

![image](https://user-images.githubusercontent.com/69248909/213859122-0943dcfa-ce0a-4818-9267-88bb6f5cd289.png)

