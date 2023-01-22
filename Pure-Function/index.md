### Pure Functions

Pure Functions rất cần thiết cho nhiều mục đích khác nhau, bao gồm functional programming, concurrency, các thành phần UX đáng tin cậy. Nhưng "chức năng thuần túy" nghĩa là gì?

Trước khi chúng ta có thể giải quyết Pure Function là gì, có lẽ nên xem xét kỹ hơn về các hàm. Có thể có một cách khác để xem xét chúng giúp lập trình hàm dễ hiểu hơn.

#### What is a Function ?

Hàm là một quá trình lấy một số input đầu vào, được gọi là đối số và tạo ra một số output đầu ra được gọi là giá trị trả về. Các chức năng có thể phục vụ các mục đích sau:

- _Mapping_: Tạo ra một số đầu ra dựa trên các đầu vào đã cho. Một hàm maps các giá trị đầu vào thành đầu ra các giá trị.
- _Procedures_ (Các thủ tục): Một hàm có thể được gọi để thực hiện một chuỗi các bước. trình tự đã biết như một thủ tục, và lập trình theo phong cách này được gọi là lập trình thủ tục.
- _I/O_: Một số chức năng tồn tại để giao tiếp với các phần khác của hệ thống, chẳng hạn như màn hình, lưu trữ, nhật ký hệ thống hoặc mạng.

#### Mapping

Pure Functions là tất cả về Mapping. Các hàm Mapping các đối số đầu vào thành các giá trị trả về, nghĩa là đối với mỗi bộ đầu vào sẽ tồn tại một đầu ra. Một hàm sẽ nhận đầu vào và trả về đầu ra tương ứng.

_Math.max()_ lấy number làm đối số và trả về số lớn nhất:

```js
Math.max(2, 8, 5); // 8
```

Trong ví dụ này, 2, 8, & 5 là các đối số. Chúng là các giá trị được truyền vào hàm.

_Math.max()_ là một hàm nhận bất kỳ số lượng đối số nào và trả về giá trị đối số lớn nhất. Trong trường hợp này, số lớn nhất mà chúng tôi chuyển vào là 8 và đó là số đã được trả về.

Các hàm thực sự quan trọng trong điện toán và toán học. Chúng giúp chúng tôi xử lý dữ liệu theo những cách hữu ích. Các lập trình viên giỏi đặt tên mô tả cho hàm để khi chúng ta xem mã, chúng ta có thể nhìn thấy tên hàm và hiểu chức năng đó làm gì.

Math chúng hoạt động rất giống các hàm trong JavaScript. Bạn có thể đã thấy các chức năng trong đại số. Họ trông giống như thế này:

> f(x) = 2x

Điều đó có nghĩa là chúng ta đang khai báo một hàm có tên là f và nó nhận một đối số có tên là x và nhân x với 2.

Để sử dụng chức năng này, chúng tôi chỉ cần cung cấp một giá trị cho x:

> f(2)

Trong đại số, điều này có nghĩa chính xác như viết 4, vì vậy bất kỳ chỗ nào bạn thấy f(2) bạn có thể thay thế 4. Tính chất này được gọi là độ trong suốt tham chiếu. Bây giờ, hãy chuyển đổi chức năng đó thành JavaScript:

```js
const double = (x) => x * 2;
```

Bạn có thể kiểm tra đầu ra của hàm bằng console.log():

```js
console.log(double(5)); // 10
```

Bạn có nhớ khi tôi nói rằng trong các hàm toán học, bạn có thể thay _f(2)_ bằng _4_ không? Trong trường hợp này, công cụ JavaScript thay thế _double(5)_ bằng câu trả lời là _10_.

Vì vậy, _console.log( double(5) );_ giống như _console.log(10);_

Điều này đúng bởi vì _double()_ là một hàm thuần túy, nhưng nếu _double()_ có side-effect, chẳng hạn như lưu giá trị vào đĩa hoặc ghi nhật ký vào bảng điều khiển, bạn không thể thay thế _double(5)_ bằng _10_ mà không thay đổi ý nghĩa .

Nếu bạn muốn minh bạch tham chiếu, bạn cần sử dụng Pure Functions.

#### Pure Functions

Một hàm thuần túy là một hàm:

1. Với cùng một đầu vào, sẽ luôn trả về cùng một đầu ra.
2. Sản xuất không có Side-effects.

Một điều chắc chắn rằng một hàm impure là nếu việc gọi nó mà không sử dụng giá trị trả về của nó là hợp lý. Đối với các Pure Functions, đó là một noop.

Tôi khuyên bạn nên ưu tiên Pure Functions. Có nghĩa là, nếu việc thực hiện một yêu cầu chương trình bằng cách sử dụng Pure Functions là hữu ích, thì bạn nên sử dụng chúng thay vì các tùy chọn khác. Pure Functions nhận một số đầu vào và trả về một số đầu ra dựa trên đầu vào đó. Chúng là các khối mã xây dựng có thể tái sử dụng đơn giản nhất trong một chương trình. Có lẽ nguyên tắc thiết kế quan trọng nhất trong khoa học máy tính là KISS (Keep It Simple, Stupid). Tôi thích "Keep It Stupid Simple" hơn. Các chức năng thuần túy là ngu ngốc đơn giản theo cách tốt nhất có thể.

Pure Functions cũng cực kỳ độc lập — dễ dàng di chuyển, tái cấu trúc và tổ chức lại mã của bạn, giúp chương trình của bạn linh hoạt hơn và dễ thích ứng với những thay đổi trong tương lai.

Pure Functions có nhiều thuộc tính có lợi và tạo thành nền tảng của FP. Pure Functions hoàn toàn độc lập với state bên ngoài và do đó, chúng miễn nhiễm với toàn bộ các loại lỗi liên quan đến shared mutable state. Bản chất độc lập của chúng cũng khiến chúng trở thành những ứng cử viên tuyệt vời để xử lý song song trên nhiều CPU và trên toàn bộ cụm máy tính phân tán, điều này khiến chúng trở nên cần thiết cho nhiều loại tác vụ điện toán khoa học và sử dụng nhiều tài nguyên.

Pure functions cũng cực kỳ độc lập — dễ dàng di chuyển, tái cấu trúc và tổ chức lại mã của bạn, giúp chương trình của bạn linh hoạt hơn và dễ thích ứng với những thay đổi trong tương lai.

#### The Trouble with Shared State

Cách đây vài năm, tôi đang làm một ứng dụng cho phép người dùng tìm kiếm cơ sở dữ liệu về các nghệ sĩ âm nhạc và tải playlist của nghệ sĩ đó vào một trình phát trên web. Đây là khoảng thời gian Google tự động hoàn tất ra mắt. Tính năng tự động hoàn thành do AJAX hỗ trợ đột nhiên trở nên thịnh hành.

Vấn đề duy nhất là người dùng thường nhập nhanh hơn so với phản hồi tìm kiếm tự động hoàn thành của API có thể được trả về, điều này gây ra một số lỗi lạ. Nó sẽ kích hoạt các điều kiện, trong đó các đề xuất mới hơn sẽ được thay thế bằng các đề xuất lỗi thời.

Tại sao điều đó lại xảy ra? Bởi vì mỗi trình xử lý thành công AJAX được cấp quyền truy cập để cập nhật trực tiếp danh sách đề xuất được hiển thị cho người dùng. Yêu cầu AJAX chậm nhất sẽ luôn thu hút sự chú ý của người dùng bằng cách thay thế các kết quả một cách mù quáng, ngay cả khi những kết quả được thay thế đó có thể mới hơn.

Để khắc phục sự cố, tôi đã tạo một trình quản lý đề xuất — một nguồn thông tin xác thực duy nhất để quản lý trạng thái của các đề xuất truy vấn. Nó đã biết về một yêu cầu AJAX hiện đang chờ xử lý và khi người dùng nhập nội dung nào đó mới, yêu cầu AJAX đang chờ xử lý sẽ bị hủy trước khi một yêu cầu mới được đưa ra, vì vậy chỉ một trình xử lý phản hồi duy nhất tại một thời điểm mới có thể kích hoạt UI state cập nhật.

Bất kỳ loại hoạt động không đồng bộ hoặc đồng bộ nào cũng có thể gây ra các điều kiện tương tự. Điều kiện cạnh tranh xảy ra nếu đầu ra phụ thuộc vào chuỗi sự kiện không thể kiểm soát (chẳng hạn như mạng, độ trễ của thiết bị, đầu vào của người dùng, tính ngẫu nhiên, v.v.). Trên thực tế, nếu bạn đang sử dụng state được chia sẻ và state đó phụ thuộc vào các trình tự khác nhau tùy thuộc vào các yếu tố không xác định, đối với mọi ý định và mục đích, thì không thể dự đoán đầu ra và điều đó có nghĩa là không thể kiểm tra chính xác hoặc hiểu đầy đủ. Như Martin Odersky (người tạo ra Scala) đã nói:

> “Non-determinism = parallel processing + mutable state” - “Không xác định = xử lý song song + trạng thái có thể thay đổi”

Tính xác định của chương trình thường là một thuộc tính mong muốn trong điện toán. Có thể bạn nghĩ rằng mình ổn vì JS chạy trong một luồng đơn và do đó, không bị ảnh hưởng bởi các mối lo ngại về xử lý song song, nhưng như ví dụ AJAX đã chứng minh, một công cụ JS luồng đơn không có nghĩa là không có đồng thời.

Ngược lại, có nhiều nguồn tương tranh trong JavaScript. API I/O, event listenter, web workers, iframe và timeouts đều có thể đưa tính không xác định vào chương trình của bạn. Kết hợp điều đó với shared state và bạn đã có một công thức cho các lỗi.

Pure Functions có thể giúp bạn tránh được các loại lỗi đó.

#### Same Input, Same Output

Với hàm _double()_, bạn có thể thay thế function call bằng kết quả, và chương trình sẽ có nghĩa giống như vậy — *double(5)* sẽ luôn có nghĩa giống như _10_ trong chương trình của bạn, bất kể ngữ cảnh, bất kể có bao nhiêu lần bạn gọi nó hoặc khi nào.

Nhưng bạn không thể nói điều tương tự về tất cả functions. Một số hàm dựa vào thông tin khác với các đối số mà bạn truyền vào để tạo ra kết quả.

Bạn có thể xem xét qua ví dụ:

```js
Math.random(); // => 0.4011148700956255
Math.random(); // => 0.8533405303023756
Math.random(); // => 0.3550692005082965
```

Mặc dù chúng ta không chuyển bất kỳ đối số nào vào bất kỳ lệnh gọi hàm nào, nhưng tất cả chúng đều tạo ra đầu ra khác nhau, nghĩa là _Math.random()_ không thuần túy.

_Math.random()_ tạo ra một số ngẫu nhiên mới trong khoảng từ 0 đến 1 mỗi khi bạn chạy nó, vì vậy rõ ràng là bạn không thể thay thế nó bằng _0.4011148700956255_ mà không làm thay đổi ý nghĩa của chương trình.

Điều đó sẽ tạo ra kết quả tương tự mỗi lần. Khi chúng tôi yêu cầu máy tính cung cấp một số ngẫu nhiên, điều đó thường có nghĩa là chúng tôi muốn một kết quả khác với lần trước. Điểm của một cặp xúc xắc có cùng số được in trên mọi mặt là gì?

Đôi khi chúng ta phải hỏi máy tính về thời gian hiện tại:

```js
const time = () => new Date().toLocaleTimeString();
time(); // => "5:15:45 PM"
```

Điều gì sẽ xảy ra nếu bạn thay thế lệnh gọi hàm _time()_ bằng thời gian hiện tại?

Nó sẽ luôn nói rằng đó là cùng một lúc: thời gian mà lệnh gọi hàm được thay thế. Nói cách khác, nếu bạn chạy nó mỗi mili giây, thì nó chỉ có thể tạo ra kết quả chính xác một lần mỗi ngày.

Vì vậy, rõ ràng, _time()_ không giống hàm _double()_ của chúng ta.

Một chức năng chỉ thuần túy nếu được cung cấp cùng một đầu vào, nó sẽ luôn tạo ra cùng một đầu ra. Bạn có thể nhớ quy tắc này từ lớp đại số: các giá trị đầu vào giống nhau sẽ luôn ánh xạ tới cùng một giá trị đầu ra. Tuy nhiên, nhiều giá trị đầu vào có thể ánh xạ tới cùng một giá trị đầu ra. Ví dụ, chức năng sau đây là thuần túy:

```js
const highpass = (cutoff, value) => value >= cutoff;
```

Các giá trị đầu vào giống nhau sẽ luôn ánh xạ tới cùng một giá trị đầu ra:

```js
highpass(5, 5); // => true
highpass(5, 5); // => true
highpass(5, 5); // => true
```

Nhiều giá trị đầu vào có thể ánh xạ tới cùng một giá trị đầu ra:

```js
highpass(5, 123); // true
highpass(5, 6); // true
highpass(5, 18); // true

highpass(5, 1); // false
highpass(5, 3); // false
highpass(5, 4); // false
```

A pure function không được dựa vào bất kỳ trạng thái có thể thay đổi bên ngoài nào, bởi vì nó sẽ không còn mang tính xác định hoặc minh bạch về mặt tham chiếu.

#### No Side Effects

A pure function không tạo ra tác dụng phụ, có nghĩa là nó không thể thay đổi bất kỳ trạng thái bên ngoài nào.

#### Immutability

Các đối số đối tượng của JavaScript là các tham chiếu, có nghĩa là nếu một hàm thay đổi một thuộc tính trên một đối tượng hoặc tham số mảng, thì điều đó sẽ thay đổi trạng thái có thể truy cập được bên ngoài hàm. Các chức năng thuần túy không được thay đổi trạng thái bên ngoài.

```js
const addToCart = (cart, item, quantity) => {
  cart.items.push({
    item,
    quantity,
  });

  return card;
};

const originalCart = { items: [] };

const newCart = addToCart(
  originalCart,
  {
    name: "Digital SLR Camera",
    price: "1495",
  },
  1
);

console.log(
  // pretty print originalCart to the console
  JSON.stringify(originalCart, undefined, 2)
);
```

Logs:

```js
{
 "items": [
 {
 "item": {
 "name": "Digital SLR Camera",
 "price": "1495"
 },
 "quantity": 1
 }
 ]
};
```

Nó hoạt động bằng cách chuyển vào một giỏ hàng và mặt hàng để thêm vào giỏ hàng đó và số lượng mặt hàng. Sau đó, hàm trả về cùng một giỏ hàng, với mặt hàng được thêm vào đó.

Vấn đề với điều này là chúng ta vừa thay đổi một số Shared State. Các hàm khác có thể dựa vào trạng thái đối tượng giỏ hàng đó như trước khi hàm được gọi và bây giờ chúng ta đã thay đổi trạng thái được chia sẻ đó, chúng ta phải lo lắng về tác động của nó đối với logic chương trình nếu chúng ta thay đổi trạng thái được chia sẻ. thứ tự mà các chức năng đã được gọi. Tái cấu trúc mã có thể dẫn đến lỗi xuất hiện, điều này có thể làm hỏng đơn đặt hàng và khiến khách hàng không hài lòng.

Nếu phần mềm của bạn dựa vào các bản state updates của bạn là thuần túy, thì điều này có thể gây ra lỗi. Ví dụ: nếu chế độ xem của bạn so sánh trạng thái tiếp theo với trạng thái trước đó trước khi kết xuất để nó có thể bỏ qua kết xuất khi trạng thái không thay đổi, thì phiên bản đột biến này sẽ không bao giờ cập nhật chế độ xem, mặc dù trạng thái đã thực sự thay đổi.

Bây giờ hãy xem xét phiên bản này:

```js
// Pure addToCart() returns a new cart
// It does not mutate the original.
const addToCart = (cart, item, quantity) => {
  return {
    ...cart,
    items: cart.items.concat([
      {
        item,
        quantity,
      },
    ]),
  };
};

const originalCart = {
  items: [],
};

const newCart = addToCart(
  originalCart,
  {
    name: "Digital SLR Camera",
    price: "1495",
  },
  1
);

console.log(
  // pretty print originalCart to the console
  JSON.stringify(originalCart, undefined, 2)
);
```

Logs:

```js
{
"items": []
}
```

Và _newCart_ chứa mục mới:

```js
{
 "items": [
 {
 "item": {
 "name": "Digital SLR Camera",
 "price": "1495"
 },
 "quantity": 1
 }
 ]
}
```

#### Conclusion

Một hàm thuần túy là một hàm, với cùng một trạng thái, luôn trả về cùng một đầu ra và không có tác dụng phụ.

Hàm thuần túy là loại hàm đơn giản nhất. Bạn nên ưu tiên chúng bất cứ khi nào practical. Chúng mang tính quyết định, giúp họ dễ hiểu, gỡ lỗi và kiểm tra. Chủ nghĩa quyết định cũng khiến họ miễn nhiễm với toàn bộ các loại lỗi liên quan đến trạng thái có thể shared mutable state, side-effects, race conditions, v.v.

Một biểu thức là trong suốt về mặt tham chiếu nếu bạn có thể thay thế biểu thức bằng giá trị tương ứng của nó mà không làm thay đổi ý nghĩa của chương trình.

Các chức năng thuần túy có thể được sử dụng để tối ưu hóa hiệu suất phần mềm. Ví dụ: hiển thị chế độ xem thường là một hoạt động tốn kém, có thể bỏ qua nếu dữ liệu bên dưới chế độ xem không thay đổi. Khi các hàm thuần túy được sử dụng để cập nhật trạng thái chế độ xem, bạn có thể kiểm tra xem có nên hiển thị lại chế độ xem hay không bằng cách so sánh trạng thái trước đó với trạng thái mới.
