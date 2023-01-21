### Composing Software: An Introduction

Cấu tạo thành phần: “Hành động kết hợp các bộ phận hoặc yếu tố để tạo thành một tổng thể.”

Trong lớp lập trình đầu tiên ở trường trung học, tôi được hướng dẫn rằng phát triển phần mềm là “hành động của chia một vấn đề phức tạp thành các vấn đề nhỏ hơn và lập trình giải pháp đơn giản để hình thành một giải pháp toàn diện cho vấn đề phức tạp.”.
Một trong những hối tiếc lớn nhất trong cuộc đời tôi là tôi đã không hiểu sớm ý nghĩa của bài học trên. Tôi đã học được bản chất của thiết kế phần mềm quá muộn trong cuộc đời.
Tôi đã phỏng vấn hàng trăm nhà phát triển. Điều tôi học được từ những buổi đó là tôi không cô đơn. Rất ít nhà phát triển phần mềm đang làm việc nắm bắt tốt bản chất của phần mềm phát triển. Họ không nhận thức được những công cụ quan trọng nhất mà chúng ta có hoặc cách đặt chúng để sử dụng tốt. 100% đã phải vật lộn để trả lời một hoặc cả hai câu hỏi quan trọng nhất trong Lĩnh vực phát triển phần mềm:

- Thế nào là Function Composition ?
- Thế nào là Object Composition ?

Vấn đề mà bạn không thể tránh Composition là bạn không biết gì về nó. Bạn vẫn làm nó nhưng làm điều đó rất tệ, bạn viết code nhiều bugs, và làm nó khó để cho những Developer khác hiểu được. Đó chính là vấn đề lớn. Hậu quá rất nghiêm trọng. Chúng tôi mất rất nhiều thời gian để bảo trì phần mềm hơn là bạn tạo nó từ Scratch (Sơ khai), và Bug của họ tác động đến hàng tỉ người trên thế giới.

Toàn bộ thế giới đều sử dụng phần mềm. Mỗi chiếc xe mới là một siêu máy tính mini trên vô lăng, và vấn đề với thiết kế phần mềm gây ra những tai nạn và kinh phí cho người khác.

#### Bạn Composing Software mỗi ngày

Nếu bạn đang là một LTV, Bạn soạn thảo Functions và Cấu trúc dữ liệu mỗi ngày, liệu bạn biết nó hay chưa? Bạn có thể làm nó 1 cách có ý thức (consciously) (và tốt hơn), hoặc bạn có thể làm nó 1 cách vô tình với một cách vô thức.
Vấn đề của quá trình phát triển phần mềm là chia nhỏ các vấn đề lớn thành nhiều vấn đề nhỏ hơn, xây dựng các components giải quyết các vấn đề nhỏ hơn đó, sau đó kết hợp những thành phần đó lại với nhau để tạo thành 1 ứng dụng hoàn chỉnh.

Mỗi lần bạn biết code như thế này, bạn đang Composing Functions:

```js
const g = (n) => n + 1;
const f = (n) => n * 2;

const doStuff = (x) => {
  const afterG = g(x);
  const afterF = f(afterG);
  return afterF;
};

doStuff(20); // 42
// Mỗi lần bạn viết a promise chain, Bạn đang composing functions:
const g = (n) => n + 1;
const f = (n) => n * 2;

const wait = (time) =>
  new Promise((resolve, reject) => setTimeout(resolve, time));

wait(300)
  .then(() => 20)
  .then(g)
  .then(f)
  .then((value) => console.log(value)); //42
```

Tương tự như vậy, mỗi lần bạn chain array phương thức calls, lodash, observables (RxJS, etc...) là bạn đang Composing Functions đó. Nếu bạn chaining, là bạn đang composing. Nếu bạn passing return values vào 1 hàm, bạn cũng đang composing. Nếu bạn gọi 2 phường thức song song, bạn cũng đang composing và sử dụng _this_ với input data.

> Nếu bạn đang chaining thì bạn đang composing.

Khi bạn compose 1 Function cách có chủ ý thì bạn sẽ làm nó một cách tốt hơn.
Composing functions một cách chủ ý (intentionally), Chúng ta có thể cải thiện hàm _doStuff()_ đơn giản thành 1 dòng như sau

```js
const g = (n) => n + 1;
const f = (n) => n * 2;

const doStuffBetter = (x) => f(g(x));

doStuffBetter(20); // 42
```

Một Objection chung cho mẫu này là khó khăn để Debug hơn. Lấy 1 ví dụ, bằng cách nào chúng ta có thể viết điều đó bằng cách sử dụng Function Composing?

```js
const doStuff = (x) => {
  const afterG = g(x);
  console.log(`after g: ${afterG}`);
  const afterF = f(g(x));
  console.log(`after f: ${afterF}`);

  return afterF;
};

doStuff(20); // =>
/*
  "afterG: 21"
  "afterF: 42"
*/
```

Đầu tiên, hãy kế thừa (abstract) cái "after f", "after g" logging vào 1 cái utility có tên là _trace()_;

```js
const trace = (label) => (value) => {
  console.log(`${label}: ${value}`);
  return value;
};
```

và bây giờ chúng ta sử dụng nó nè:

```js
const doStuff = (x) => {
  const afterG = g(x);
  trace("after g")(afterG);
  const afterF = f(afterG);
  trace("after f")(afterF);
  return afterF;
};

doStuff(20); // =>
/*
  "afterG: 21"
  "afterF: 42"
*/
```

Những Thư viện phổ biến như Lodash hoặc Ramda bao gồm những utilities để tạo composing một cách dễ dàng hơn. Bạn có thể viết lại (rewrite) chức năng trên như sau:

```js
import pipe from "lodash/fp/flow";

const doStuffBetter = pipe(g, trace("after g"), trace("after f"));

doStuffBetter(20); // =>
/*
  "afterG: 21"
  "afterF: 42"
*/
```

Nếu bạn một thử viết code này mà không cần _Import_ thứ gì hết, thì bạn có thể khai báo lại hàm _pipe_ như sau:

```js
// pipe(...fns: [...Function]) => x => y
const pipe =
  (...fns) =>
  (x) =>
    fns.reduce((y, f) => f(y), x);
```

Đừng lo lắng nếu bạn chưa biết được cách hoạt động của nó ngay bây giờ. Sau đây chúng ta sẽ khám phá Function Composing trong nhiều chi tiết hơn. Sự thật là, nó rất essential (thiết yếu, cần thiết), bạn sẽ thấy nó được chứng minh và xác minh (demonstrated) nhiều lần khắp bài viết. Điểm đáng chú ý này sẽ giúp bạn trở nên quen thuộc với cách khai báo và cách sử dụng nó một cách tự động. Hãy hoà làm 1 với Composition.

_pipe()_ tạo một pipelines cho Hàm 1, passing kết quả qua Hàm 2 với tham số là kết quả trước đó của Hàm 1. Khi bạn sử dụng _pipe()_ (và nó có thể là twin, _compose()_) Bạn không cần định nghĩa biến. Viết hàm mà không cần đề cập hay quan tâm tới tham số được gọi là _"point-free style"_. Để làm được điều đó, bạn sẽ gọi 1 hàm return về 1 hàm mới, còn hơn là khai báo hàm đó tường minh ra. Điều đó có nghĩa bạn không cần sử dụng từ khoá _function_ hoặc Arrow Syntax (=>).

_point-free style_ có thể đi sâu hơn nữa nhưng 1 ít ở đây cũng đủ tuyệt vời rồi bởi vì những điều đó phải thêm 1 số biến phức tạp không cần thiết cho function của bạn.

Có một vài lợi ích để giảm độ phức tạp:

#### Working Memory (Bộ nhớ làm việc)

Con người trung bình chỉ có một vài tài nguyên được chia sẻ cho lượng tử riêng biệt trong bộ nhớ làm việc⁴ và mỗi biến có khả năng tiêu thụ một trong những lượng tử đó. Khi bạn thêm nhiều biến hơn, khả năng của chúng tôi nhớ lại chính xác ý nghĩa của từng biến bị giảm đi. Các mô hình bộ nhớ làm việc điển hình liên quan đến 4-7 lượng tử rời rạc. Trên những con số đó, tỷ lệ lỗi tăng lên đáng kể.
Sử dụng _pipe()_, chúng tôi đã loại bỏ 3 biến – giải phóng gần một nửa công việc hiện có của bộ nhớ cho những thứ khác. Điều đó làm giảm tải memory một cách đáng kể. Các nhà phát triển phần mềm có xu hướng giỏi hơn trong việc sắp xếp dữ liệu vào bộ nhớ làm việc so với người bình thường, nhưng không nhiều bằng để làm suy yếu tầm quan trọng của bảo tồn.

#### Signal to Noise Ratio

Mã ngắn gọn giúp cải thiện Signal to Noise Ratio của bạn. Nó giống như nghe radio – khi radio không được điều chỉnh đúng với đài, bạn sẽ bị nhiễu nhiều và khó nghe hơn. Khi bạn chỉnh đúng đài, tiếng ồn sẽ biến mất và tìn hiệu rõ hơn nghe hay hơn.

Code cũng tương tự như vậy. Càng ngắn gọn code thì code càng nâng cao khả năng hiểu. Một số code cung cấp thông tin hữu ích nhưng chỉ chiếm 1 ít dung lượng. Nếu bạn giảm số lượng code sử dụng đi mà vẫn không giảm thông tin muốn truyền tải thì bạn sẽ làm cho đoạn code dễ phân tích cú pháp hơn và dễ hiểu hơn cho người khác cần đọc nó.

#### Surface Area for Bugs

Hãy xem các chức năng trước và sau. Có vẻ như chức năng này đã gọn hơn và một đi 1 tấn tải trọng. Điều đó rất quan trọng bởi vì bổ sung đoạn code dễ gây khu vực bề mặt bug ẩn sâu bên trong, điều này có nghĩa bugs sẽ tiềm ẩn trong đó.

> Less code = less surface area for bugs = fewer bugs

## Composing Objects

> "Favor object composition over class inheritance" the Gang of Four, “Design Patterns: Elements of Reusable Object Oriented Software”⁵

> "Trong khoa học máy tính, kiểu dữ liệu tổng hợp hoặc kiểu dữ liệu phức tạp có thể được xây dựng từ Kiểu dữ liệu nguyên thuỷ của Lập trình ngôn ngữ và các hỗn hợp khác. Hành động này là xây dựng một loại Composite type (hỗn hợp) được biết đến như 1 Composition. ~ Wikipedia"

Đây là kiểu dữ liệu nguyên thuỷ:

```js
const firstName = "Claude";
const lastName = "Debussy";
```

và đây là hỗn hợp lại:

```js
const fullName = {
  firstName,
  lastName,
};
```

Tương tự như thể, tất cả Arrays, Sets, Maps, WeakMaps, TypedArrays, v.v tất cả đều là composite datatypes. Mỗi lần bạn xây dựng bất kì non-primitive cấu trúc dữ liệu, _Bạn đang biểu diễn một số loại điển hình cho Object Composition_.

Chú ý rằng _the Gane if Four_ định nghĩa 1 pattern được gọi là **composite pattern** đó là loại cụ thể của đệ quy Object cho phép bạn xử lý riêng lẻ Components và tổng hợp những composites giống nhau. Một số nhà phá triển bối rối, nghĩ rằng **composite pattern** là một **biểu mẫu của Object Composition**. Đừng bối rối. Rất nhiều loại khác nhau của **Object Composition**.

_the Gang of Four_ tiếp tục thêm, "Bạn sẽ thấy Object Composirion áp dụng lần nữa và lần nữa trong design pattern". và sau đó họ liệu kê ra 3 loại relationship (quan hệ) với **Object Composition**, bao gồm **delegation** (Khi một Object cho phép truy cập thuộc tính của 1 object khác, như được sử dụng trong state, strategy, visitor pattern), **acquaintance** (Khi một Object biết một Object khác bằng cách tham chiếu tới, thường được passing dưới dạng tham số như: relationship, ví dụ như trình xử lý yêu cầu network của Amazon: [link](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612/ref=as_li_ss_tl?ie=UTF8&qid=1494993475&sr=8-1&keywords=design+patterns&linkCode=ll1&tag=eejs-20&linkId=6c553f16325f3939e5abadd4ee04e8b4) Composing Software: Giới thiệu 8 tham chiếu tới logger để yêu cầu log request --- gọi là trình xử lý logger). Và cuối cùng là **aggregation** (Khi một Object con tạo thành 1 phần của Object cha có một Relationship ví dụ như: DOM children là những component elements trong DOM node -- A DOM node có children).

Class Inheritance (Kế thừa) có thể được sử dụng để khởi tạo composite objects, nhưng điều đó là 1 cách hạn chế và dễ vỡ để làm. Khi _the Gang of Four_ nói rằng "Ưu tiên Object composition hơn là Class Inheritance", họ đang tư vấn bạn tiếp cận linh hoạt hơn Object building, thay vì tiếp cận cứng nhắc, liên kết chặc chẽ class inheritance. Họ đang khuyến khích bạn ủng hộ mối quan hệ has-a và used-a hơn là quan hệ is-a.

Thay vì đề cập đến các Design Pattern cụ thể, chúng tôi sẽ sử dụng định nghĩa tổng quát hơn về Composition Object từ “Categorical Methods in Computer Science: With Aspects from Topology”⁶ (1989):

> Các Composite objects được hình thành bằng cách đặt các object lại với nhau sao cho mỗi object sau 'một phần' của cái trước.

Lớp kế thừa là một loại cấu trúc Composite Object. Tất cả các Class tạo ra Composite Object, nhưng không phải tất cả Composite Object được tạo bởi các lớp hoặc lớp kế thừa. "Ưu tiên object composition hơn class inheritance" có nghĩa là bạn nên tạo composite objects từ từng phần nhỏ của Components, thay vì kế thừa tất cả thuộc tính từ ancestor (cha) trong class hierarchy. Sau này có thể gây ra nhiều vấn đề nổi tiếng trong thiết kế hướng đối tượng:

- **The tight coupling problem (Vấn đề liên kết chặc chẽ)** Bởi vì những lớp con đều phụ thuộc và sự biểu diễn của lớp cha, lớp kế thừa là khớp nối chặt chẽ nhất có sẵn trong hướng đối tượng.
- **The fragile base class problem (Vấn đề lớp cơ sở bị mỏng manh)** Do liên kết chặc chẽ, những thay đổi mới đối với lớp cơ sở có thể phá vỡ một số lượng lớn những lớp sau - có khả năng trong code của bên thứ 3 quản lý. Các tác giả có thể phá vỡ code mà họ không hề hay biết.
- **The inflexible hierarchy problem (Vấn đề phân cấp không linh hoạt)** Nguyên tắc phân loại ancestor duy nhất, nếu có đủ thời gian và tiến hoá, tất cả các class cuối cùng phân loại đều sai đối với trường hợp use-cases mới.
- **The duplication by necessity problem (Sự trùng lặp các vấn đề không cần thiết)** Do hệ thống phân cấp không linh hoạt, các trường hợp sử dụng mới được thường được thực hiện bằng cách duplicate, thay vì mở rộng, dẫn đến các lớp tương tự khác nhau một cách bất ngờ. Sau khi duplicate bắt đầu, không rõ lớp nào lớp mới nên đi từ đâu, hoặc tại sao.
- **The gorilla/banana problem** vấn đề với các ngôn ngữ hướng đối tượng là chúng có tất cả môi trường tiềm ẩn này mà nó mang theo. "Bạn muốn một quả chuối nhưng những gì bạn có một con khỉ đột ôm chuối và toàn bộ khu rừng." ∼Joe Armstrong.

Hình thức phổ biến nhất của Objec Composition trong JavaScript được gọi là nối đối tượng **concatenation** (hay còn được gọi là kết thừa nối tiếp (concatenative inheritance): Một cách không chính thức, "Thành phần mixins"). Nó giống như cây kem. bạn bắt đầu với Object (ví dụ: Kem vani), và sau đó trộn với những tín năng mà bạn muốn. Thêm 1 số loại hạt, caramels, chocolate, và kết thúc với món kem trộn cholalate hấp dẫn.

Xây dựng Composites với lớp kế thừa (Class Inheritance):

```js
class Foo {
  constructor() {
    this.a = "a";
  }
}

class Bar extends Foo {
  constructor(options) {
    super(options);
    this.b = "b";
  }
}

const myBar = new Bar(); // {a: 'a', b: 'b'}
```

Xây dựng composites với mixin composition:

```js
  const a = {
    a: 'a';
  };

  const b = {
    b: 'b';
  }

  const c = {...a, ...b} // {a: 'a', b: 'b'}
```

Chúng ta sẽ khám phá kiểu khác nhau của Object Composition sâu hơn sau. Và vây giờ, bạn đã hiểu nên làm:

1. Nhiều hơn 1 cách để làm điều đó
2. Một số cách tốt hơn những cách khác.
3. Bạn muốn chọn giải pháp đơn giản nhất và linh hoạt nhất cho task hiện tại.
