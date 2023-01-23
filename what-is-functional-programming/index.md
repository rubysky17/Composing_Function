### What is Functional Programming?

Functional Programming đã trở thành một chủ đề thực sự nóng trong thế giới JavaScript. Chỉ vài năm trước, rất ít lập trình viên JavaScript biết Functional Programming là gì, nhưng mọi cơ sở mã ứng dụng lớn mà tôi thấy trong 3 năm qua đều sử dụng rất nhiều ý tưởng Functional Programming.

_Functional Programming_ (thường được viết tắt là FP) là một mô hình lập trình trong đó các ứng dụng được tạo bằng cách sử dụng các pure functions, tránh shared mutable state và các side-effects. Functional Programming thường mang tính khai báo hơn là mệnh lệnh, nghĩa là chúng ta diễn đạt những việc cần làm hơn là cách thực hiện.

Các ví dụ khác về mô hình lập trình bao gồm lập trình hướng đối tượng, trong đó dữ liệu và hành vi được đặt cùng một nơi, và lập trình thủ tục, là một kiểu bắt buộc nhóm các thuật toán thành các thủ tục có xu hướng dựa vào trạng thái có thể thay đổi được chia sẻ.

Mã chức năng có xu hướng ngắn gọn hơn, dễ dự đoán hơn và dễ kiểm tra hơn mã mệnh lệnh hoặc mã hướng đối tượng — nhưng nếu bạn không quen với nó và các mẫu phổ biến liên quan đến nó, thì mã chức năng cũng có vẻ dày đặc hơn rất nhiều, và tài liệu liên quan có thể không thể tiếp cận được đối với những người mới đến.

Nếu bạn bắt đầu tra cứu trên Google các thuật ngữ Functional Programming, bạn sẽ nhanh chóng va vào bức tường gạch của biệt ngữ học thuật có thể rất đáng sợ. Nói rằng nó có một đường cong học tập là một cách nói quá nghiêm túc. Nhưng nếu bạn đã lập trình JavaScript được một thời gian, rất có thể bạn đã sử dụng rất nhiều khái niệm và tiện ích Functional Programming trong phần mềm thực của mình.

Đừng để tất cả những từ mới làm bạn sợ hãi. Nó dễ dàng hơn nhiều so với bạn nghe được.

Phần khó nhất là xoay quanh tất cả các định nghĩa không quen thuộc. Có rất nhiều ý tưởng trong định nghĩa có vẻ ngây thơ ở trên mà tất cả cần phải được hiểu trước khi bạn có thể bắt đầu nắm bắt ý nghĩa của Functional Programming:

- Pure functions
- Function composition
- Avoid shared state
- Avoid mutating state
- Avoid side effects
- Declarative vs imperative

Nói cách khác, nếu bạn muốn biết lập trình hàm có nghĩa là gì trong thực tế, bạn phải bắt đầu với sự hiểu biết về các khái niệm cốt lõi đó.

#### Pure Functions

Một hàm thuần túy là một hàm:

- Given the same inputs, always returns the same output, and
- Has no side-effects

Các hàm thuần túy có nhiều thuộc tính quan trọng trong lập trình hàm, bao gồm tính minh bạch tham chiếu (bạn có thể thay thế lệnh gọi hàm bằng giá trị kết quả của nó mà không làm thay đổi ý nghĩa của chương trình).

#### Function Composition

Function composition là quá trình kết hợp hai hoặc nhiều chức năng để tạo ra một chức năng mới hoặc thực hiện một số tính toán. Ví dụ, thành phần f . g (dấu chấm có nghĩa là “được tạo bằng”) tương đương với f(g(x)) trong JavaScript. Hiểu Function composition là một bước quan trọng để hiểu cách phần mềm được xây dựng bằng cách sử dụng lập trình chức năng. Xem thên “Function composition là gì?” để biết thêm.

#### Shared State

Trạng thái được chia sẻ (Shared State) là bất kỳ biến, đối tượng hoặc không gian bộ nhớ nào tồn tại trong một phạm vi được chia sẻ hoặc dưới dạng thuộc tính của một đối tượng được chuyển giữa các phạm vi. Phạm vi chia sẻ có thể bao gồm global scope hoặc closure scopes. Thông thường, trong lập trình hướng đối tượng, các đối tượng được chia sẻ giữa các phạm vi bằng cách thêm thuộc tính vào các đối tượng khác.

Ví dụ: một trò chơi trên máy tính có thể có một đối tượng trò chơi chính, với các nhân vật và vật phẩm trò chơi được lưu trữ dưới dạng các thuộc tính thuộc sở hữu của đối tượng đó. Functional Programming tránh Shared State — thay vào đó dựa vào cấu trúc dữ liệu bất biến và tính toán thuần túy để lấy dữ liệu mới từ dữ liệu hiện có.

Vấn đề với Shared State là để hiểu tác dụng của một hàm, bạn phải biết toàn bộ lịch sử của mọi biến được chia sẻ mà hàm đó sử dụng hoặc ảnh hưởng.

Hãy tưởng tượng bạn có một đối tượng người dùng cần lưu. Hàm _saveUser()_ của bạn đưa ra yêu cầu đối với API trên máy chủ. Trong khi điều đó đang xảy ra, người dùng thay đổi ảnh hồ sơ của họ bằng _updateAvatar()_ và kích hoạt một yêu cầu _saveUser()_ khác. Khi lưu, máy chủ sẽ gửi lại một đối tượng người dùng chính tắc sẽ thay thế bất kỳ thứ gì có trong bộ nhớ để đồng bộ hóa với các thay đổi xảy ra trên máy chủ hoặc để đáp ứng các lệnh gọi API khác.

Thật không may, phản hồi thứ hai được nhận trước phản hồi đầu tiên, vì vậy khi phản hồi đầu tiên (hiện đã lỗi thời) được trả về, ảnh hồ sơ mới sẽ bị xóa trong bộ nhớ và được thay thế bằng ảnh cũ. Đây là một ví dụ về race condition — một lỗi rất phổ biến liên quan đến Shared State.

Một vấn đề phổ biến khác liên quan đến Shared State là việc thay đổi thứ tự các chức năng được gọi có thể gây ra một loạt lỗi vì các chức năng hoạt động trên Shared State phụ thuộc vào thời gian. Với Shared State, thứ tự thực hiện các lời gọi hàm sẽ thay đổi kết quả của các lời gọi hàm:

```js
// Shared state
const x = {
  val: 2,
};

// Mutates shared state
const x1 = () => (x.val += 1);

// Mutates shared state
const x2 = () => (x.val *= 2);

x1();
x2();

console.log(x.val); // 6

// This example is exactly equivalent to the above, except...
const y = {
  val: 2,
};
const y1 = () => (y.val += 1);

const y2 = () => (y.val *= 2);
// ...the order of the function calls is reversed...
y2();
y1();

// ... which changes the resulting value:
console.log(y.val); // 5
```

Khi bạn tránh Shared State, thời gian và thứ tự của các lời gọi hàm không thay đổi kết quả của việc gọi hàm. Với các hàm thuần túy, với cùng một đầu vào, bạn sẽ luôn nhận được cùng một đầu ra. Điều này làm cho các lời gọi hàm hoàn toàn độc lập với các lời gọi hàm khác, điều này có thể đơn giản hóa triệt để các thay đổi và tái cấu trúc. Thay đổi trong một chức năng hoặc thời gian của lệnh gọi chức năng sẽ không bị ảnh hưởng và phá vỡ các phần khác của chương trình.

```js
const x = {
  val: 2,
};

const inc = (x) => ({ ...x, val: x.val + 1 });
const double = (x) => ({ ...x, val: x.val * 2 });

console.log(inc(double(x)).val); // 5

/**
 * Because the functions don't mutate, you can call
 * these functions as many times as you want, in any order,
 * without changing the result of other function calls.
 * **/

const y = {
  val: 2,
};

// These calls do nothing:
inc(y);
double(y);
console.log(inc(double(y)).val); // 5
```

Trong ví dụ trên, chúng tôi sử dụng object spread ({...x, val: x.val + 1}) để sao chép các thuộc tính của x thay vì thay đổi nó tại chỗ.

Nếu bạn xem xét kỹ các câu lệnh _console.log()_ trong ví dụ này, bạn sẽ nhận thấy một điều mà tôi đã đề cập rồi: function composition. Nhớ lại từ trước đó, function composition trông như thế này: f(g(x)). Trong trường hợp này, chúng tôi thay f() và g() bằng inc() và double() cho thành phần: x1. x2.

Tất nhiên, nếu bạn thay đổi thứ tự của thành phần, đầu ra sẽ thay đổi. Thứ tự của các hoạt động vẫn còn quan trọng. f(g(x)) không phải lúc nào cũng bằng g(f(x)), nhưng điều không còn quan trọng nữa là điều gì xảy ra với các biến bên ngoài hàm — và đó là một vấn đề lớn. Với các hàm không tinh khiết, bạn không thể hiểu đầy đủ chức năng của nó trừ khi bạn biết toàn bộ lịch sử của mọi biến mà hàm đó sử dụng hoặc ảnh hưởng.

Loại bỏ sự phụ thuộc vào thời gian gọi hàm và bạn loại bỏ toàn bộ lớp bugs.

#### Immutability

Một đối tượng bất biến là một đối tượng không thể sửa đổi sau khi nó được tạo. Ngược lại, một đối tượng có thể thay đổi là bất kỳ đối tượng nào có thể được sửa đổi sau khi nó được tạo.

Tính bất biến là một khái niệm trung tâm của lập trình chức năng bởi vì không có nó, luồng dữ liệu trong chương trình của bạn sẽ bị mất. Lịch sử trạng thái bị bỏ rơi và các bug có thể xâm nhập vào phần mềm của bạn.

Trong JavaScript, điều quan trọng là không nhầm lẫn giữa _const_ với tính bất biến. _const_ tạo một liên kết tên biến không thể gán lại sau khi tạo, _const_ không tạo các đối tượng bất biến. Bạn không thể thay đổi đối tượng mà ràng buộc đề cập đến, nhưng bạn vẫn có thể thay đổi các thuộc tính của đối tượng, điều đó có nghĩa là các ràng buộc được tạo bằng _const_ là có thể thay đổi, không phải là bất biến.

Các đối tượng bất biến hoàn toàn không thể thay đổi. Bạn có thể làm cho một giá trị thực sự bất biến bằng cách freezing sâu đối tượng. JavaScript có một phương thức freezing đối tượng sâu một cấp:

```js
const a = Object.freeze({
  foo: "Hello",
  bar: "world",
  baz: "!",
});

a.foo = "Goodbye";

// Error: Cannot assign to read only property 'foo' of object Object
```

Nhưng các đối tượng bị đóng băng chỉ là bất biến bề ngoài. Ví dụ: đối tượng sau có thể thay đổi:

```js
const a = Object.freeze({
  foo: { greeting: "Hello" },
  bar: "world",
  baz: "!",
});

a.foo.greeting = "Goodbye";
console.log(`${a.foo.greeting}, ${a.bar}${a.baz}`); // 'Goodbye, world!'
```

Như bạn có thể thấy, các thuộc tính nguyên thủy cấp cao nhất của một đối tượng bị đóng băng không thể thay đổi, nhưng bất kỳ thuộc tính nào cũng là một đối tượng (bao gồm cả mảng, v.v.) vẫn có thể bị thay đổi — vì vậy ngay cả các đối tượng bị đóng băng cũng không phải là bất biến trừ khi bạn đi toàn bộ cây đối tượng và đóng băng mọi thuộc tính đối tượng.

Trong nhiều ngôn ngữ Functional Programming, có các cấu trúc dữ liệu bất biến đặc biệt được gọi là cấu trúc dữ liệu trie (phát âm là "cây") được đóng băng sâu một cách hiệu quả — có nghĩa là không thuộc tính nào có thể thay đổi, bất kể cấp độ của thuộc tính trong hệ thống phân cấp đối tượng.

Các lần thử sử dụng tính năng chia sẻ cấu trúc để chia sẻ các vị trí bộ nhớ tham chiếu cho tất cả các phần của đối tượng không thay đổi sau một "đột biến", sử dụng ít bộ nhớ hơn và cho phép cải thiện hiệu suất đáng kể cho một số loại thao tác.

Ví dụ: bạn có thể sử dụng phép so sánh nhận dạng ở gốc của cây đối tượng để so sánh. Nếu danh tính giống nhau, bạn không cần phải đi trên toàn bộ cây để kiểm tra sự khác biệt.

Có một số thư viện trong JavaScript tận dụng các lần thử, bao gồm Immutable.js²⁴ và Mori²⁵.

#### Side Effects

Hiệu ứng phụ là bất kỳ thay đổi trạng thái ứng dụng nào có thể quan sát được bên ngoài hàm được gọi ngoài giá trị trả về của nó. Tác dụng phụ bao gồm:

- Modifying any external variable or object property (e.g., a global variable, or a variable in the parent function scope chain)
- Logging to the console
- Writing to the screen
- Writing to a file
- Writing to the network
- Triggering any external process
- Calling any other functions with side-effects

Các tác dụng phụ hầu như được tránh trong lập trình chức năng, điều này làm cho các hiệu ứng của chương trình dễ dàng mở rộng, tái cấu trúc, debug, kiểm tra và bảo trì. Đây là lý do mà hầu hết các khung khuyến khích người dùng quản lý kết xuất trạng thái và thành phần trong các mô-đun riêng biệt, được kết hợp lỏng lẻo.

#### Reusability Through Higher Order Functions

Hàm bậc cao hơn là bất kỳ hàm nào lấy một hàm làm đối số, trả về một hàm hoặc cả hai. Các hàm bậc cao hơn thường được sử dụng để:

- Abstract or isolate actions, effects, or async flow control using callback functions, promises, monads, etc.
- Create utilities which can act on a wide variety of data types
- Partially apply a function to its arguments or create a curried function for the purpose of reuse or function composition
- Take a list of functions and return some composition of those input functions

Lập trình chức năng có xu hướng sử dụng lại một tập hợp các tiện ích chức năng chung để xử lý dữ liệu. Lập trình hướng đối tượng có xu hướng sắp xếp các phương thức và dữ liệu trong các đối tượng. Trong hầu hết các phần mềm hướng đối tượng, các phương thức được đặt cùng vị trí đó chỉ có thể hoạt động trên loại dữ liệu mà chúng được thiết kế để hoạt động và thường chỉ dữ liệu chứa trong thể hiện đối tượng cụ thể đó.

Trong lập trình chức năng, bất kỳ loại dữ liệu nào cũng là trò chơi công bằng. Tiện ích _map()_ tương tự có thể ánh xạ qua các đối tượng, chuỗi, số hoặc bất kỳ loại dữ liệu nào khác vì tiện ích này nhận một hàm làm đối số xử lý thích hợp loại dữ liệu đã cho. FP loại bỏ mánh khóe tiện ích chung của nó bằng cách sử dụng các hàm bậc cao hơn và thay thế tham số.

JavaScript có các hàm hạng nhất, cho phép chúng ta coi các hàm là dữ liệu — gán chúng cho các biến, chuyển chúng cho các hàm khác, trả về chúng từ các hàm, v.v.

#### Containers, Functors, Lists, and Streams

Cấu trúc dữ liệu functor là cấu trúc dữ liệu có thể được ánh xạ qua (ví dụ: [1,2,3].map(x => x \* 2)). Nói cách khác, đó là một vùng chứa có giao diện có thể được sử dụng để áp dụng một hàm cho các giá trị bên trong nó. Khi bạn nhìn thấy từ functor, bạn nên nghĩ đến "mappable".

Trước đó, chúng ta đã biết rằng cùng một tiện ích map() có thể hoạt động trên nhiều loại dữ liệu. Nó thực hiện điều đó bằng cách nâng hoạt động ánh xạ để hoạt động với API functor. Các hoạt động kiểm soát luồng quan trọng được sử dụng bởi _map()_ tận dụng giao diện đó.

Trong trường hợp của _Array.prototype.map()_, vùng chứa là một mảng, nhưng các cấu trúc dữ liệu khác cũng có thể là functor — miễn là chúng cung cấp API ánh xạ.

Hãy xem cách _Array.prototype.map()_ cho phép bạn trừu tượng hóa loại dữ liệu từ tiện ích ánh xạ để làm cho _map()_ có thể sử dụng được với bất kỳ loại dữ liệu nào. Chúng ta sẽ tạo một ánh xạ _double()_ đơn giản mà chỉ cần nhân bất kỳ giá trị nào được truyền vào với 2:

```js
const double = (n) => n * 2;
const doubleMap = (numbers) => numbers.map(double);
console.log(doubleMap([2, 3, 4])); // [ 4, 6, 8 ]
```

Điều gì sẽ xảy ra nếu chúng ta muốn thao tác trên các mục tiêu trong trò chơi để nhân đôi số điểm mà chúng cho? Tất cả những gì chúng ta phải làm là thực hiện một thay đổi nhỏ đối với hàm double() mà chúng ta chuyển vào map() và mọi thứ vẫn hoạt động:

```js
const double = (n) => n.points * 2;
const doubleMap = (numbers) => numbers.map(double);

console.log(
  doubleMap([
    { name: "ball", points: 2 },
    { name: "coin", points: 3 },
    { name: "candy", points: 4 },
  ])
); // [ 4, 6, 8 ]
```

Khái niệm sử dụng các khái niệm trừu tượng như hàm functor và các hàm bậc cao hơn để sử dụng các hàm tiện ích chung để thao tác với bất kỳ số loại dữ liệu khác nhau nào là quan trọng trong lập trình hàm. Bạn sẽ thấy một khái niệm tương tự được áp dụng theo nhiều cách khác nhau.

> “A list expressed over time is a stream.”

Mảng và functor không phải là cách duy nhất áp dụng khái niệm vùng chứa và giá trị trong vùng chứa này. Ví dụ, một mảng chỉ là một danh sách các thứ. Một danh sách được thể hiện theo thời gian là một luồng — vì vậy bạn có thể áp dụng các loại tiện ích tương tự để xử lý các luồng sự kiện đến — điều mà bạn sẽ thấy rất nhiều khi bắt đầu xây dựng phần mềm thực với FP.

#### Declarative vs Imperative

Functional programming là một mô hình khai báo, nghĩa là logic chương trình được thể hiện mà không mô tả rõ ràng điều khiển luồng.

- _Imperative_ các chương trình sử dụng các dòng mã mô tả các bước cụ thể được sử dụng để đạt được kết quả mong muốn — kiểm soát luồng: Cách thực hiện mọi việc.
- _Declarative_ các chương trình trừu tượng hóa quy trình kiểm soát luồng (cách thức được trừu tượng hóa) và thay vào đó sử dụng các dòng mã mô tả luồng dữ liệu: Phải làm gì?

Ví dụ: mapping bắt buộc này lấy một mảng số và trả về một mảng mới với mỗi số nhân với 2:

```js
const doubleMap = (numbers) => {
  const doubled = [];
  for (let i = 0; i < numbers.length; i++) {
    doubled.push(numbers[i] * 2);
  }
  return doubled;
};

console.log(doubleMap([2, 3, 4])); // [4, 6, 8]
```

Mapping khai báo này thực hiện tương tự, nhưng trừu tượng hóa điều khiển luồng bằng cách sử dụng tiện ích Array.prototype.map() chức năng, cho phép bạn thể hiện luồng dữ liệu rõ ràng hơn:

```js
const doubleMap = (numbers) => numbers.map((n) => n * 2);
console.log(doubleMap([2, 3, 4])); // [4, 6, 8]
```

Mã mệnh lệnh thường sử dụng các câu lệnh. Một tuyên bố là một đoạn mã thực hiện một số hành động. Ví dụ về các câu lệnh thường được sử dụng bao gồm for, if, switch, throw, v.v.

Mã khai báo dựa nhiều hơn vào các biểu thức. Một biểu thức là một đoạn mã đánh giá một số giá trị. Biểu thức thường là sự kết hợp của các lời gọi hàm, giá trị và toán tử được đánh giá để tạo ra giá trị kết quả.

Đây là tất cả các ví dụ về biểu thức:

- 2 \* 2
- doubleMap([2, 3, 4])
- Math.max(4, 3, 2)
- 'a' + 'b' + 'c'
- {...a, ...b, ...c}

Thông thường trong mã, bạn sẽ thấy các biểu thức được gán cho một mã định danh (tên biến), được trả về từ các hàm hoặc được chuyển vào một hàm. Trước khi được chỉ định, trả lại hoặc chuyển, biểu thức được ước tính trước và giá trị kết quả được sử dụng.

#### Conclusion

Lập trình chức năng ủng hộ:

- Pure functions over shared state and side effects
- Immutability over mutable data
- Function composition over imperative flow control
- Generic utilities that act on many data types over object methods that only operate on their
  colocated data
- Declarative over imperative code (what to do, rather than how to do it)
- Expressions over statements
