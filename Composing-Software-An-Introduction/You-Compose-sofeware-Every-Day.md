## Composing Software: An Introduction

Cấu tạo thành phần: “Hành động kết hợp các bộ phận hoặc yếu tố để tạo thành một tổng thể.”

Trong lớp lập trình đầu tiên ở trường trung học, tôi được hướng dẫn rằng phát triển phần mềm là “hành động của chia một vấn đề phức tạp thành các vấn đề nhỏ hơn và lập trình giải pháp đơn giản để hình thành một giải pháp toàn diện cho vấn đề phức tạp.”.
Một trong những hối tiếc lớn nhất trong cuộc đời tôi là tôi đã không hiểu sớm ý nghĩa của bài học trên. Tôi đã học được bản chất của thiết kế phần mềm quá muộn trong cuộc đời.
Tôi đã phỏng vấn hàng trăm nhà phát triển. Điều tôi học được từ những buổi đó là tôi không cô đơn. Rất ít nhà phát triển phần mềm đang làm việc nắm bắt tốt bản chất của phần mềm phát triển. Họ không nhận thức được những công cụ quan trọng nhất mà chúng ta có hoặc cách đặt chúng để sử dụng tốt. 100% đã phải vật lộn để trả lời một hoặc cả hai câu hỏi quan trọng nhất trong Lĩnh vực phát triển phần mềm:

- Thế nào là Function Composition ?
- Thế nào là Object Composition ?

Vấn đề mà bạn không thể tránh Composition là bạn không biết gì về nó. Bạn vẫn làm nó nhưng làm điều đó rất tệ, bạn viết code nhiều bugs, và làm nó khó để cho những Developer khác hiểu được. Đó chính là vấn đề lớn. Hậu quá rất nghiêm trọng. Chúng tôi mất rất nhiều thời gian để bảo trì phần mềm hơn là bạn tạo nó từ Scratch (Sơ khai), và Bug của họ tác động đến hàng tỉ người trên thế giới.

Toàn bộ thế giới đều sử dụng phần mềm. Mỗi chiếc xe mới là một siêu máy tính mini trên vô lăng, và vấn đề với thiết kế phần mềm gây ra những tai nạn và kinh phí cho người khác.

### Bạn Composing Software mỗi ngày

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

Nếu bạn một thử viế code này mà không cần _Import_ thứ gì hết, thì bạn có thể khai báo lại hàm _pipe_ như sau:

```js
// pipe(...fns: [...Function]) => x => y
const pipe =
  (...fns) =>
  (x) =>
    fns.reduce((y, f) => f(y), x);
```

Đừng lo lắng nếu bạn chưa biết được cách hoạt động của nó ngay bây giờ. Sau đây chúng ta sẽ khám phá Function Composing trong nhiều chi tiết hơn. Sự thật là, nó rất essential (thiết yếu, cần thiết), bạn sẽ thấy nó được chứng minh và xác minh (demonstrated) nhiều lần khắp bài viết. Điểm đáng chú ý này sẽ giúp bạn trở nên quen thuộc với cách khai báo và cách sử dụng nó một cách tự động. Hãy hoà làm 1 với Composition.

_pipe()_ tạo một pipelines cho Hàm 1, passing kết quả qua Hàm 2 với tham số là kết quả trước đó của Hàm 1. Khi bạn sử dụng _pipe()_ (và nó có thể là twin, _compose()_) Bạn không cần định nghĩa biến. Viết hàm mà không cần đề cập hay quan tâm tới tham số được gọi là _"point-free style"_. Để làm được điều đó, bạn sẽ gọi 1 hàm return về 1 hàm mới, còn hơn là khai báo hàm đó tường minh ra. Điều đó có nghĩa bạn không cần sử dụng từ khoá _function_ hoặc Arrow Syntax (=>).

_point-free style_
