## Composing Software: An Introduction

Cấu tạo thành phần: “Hành động kết hợp các bộ phận hoặc yếu tố để tạo thành một tổng thể.”

Trong lớp lập trình đầu tiên ở trường trung học, tôi được hướng dẫn rằng phát triển phần mềm là “hành động của chia một vấn đề phức tạp thành các vấn đề nhỏ hơn và lập trình giải pháp đơn giản để hình thành một giải pháp toàn diện cho vấn đề phức tạp.”.
Một trong những hối tiếc lớn nhất trong cuộc đời tôi là tôi đã không hiểu sớm ý nghĩa của bài học trên. Tôi đã học được bản chất của thiết kế phần mềm quá muộn trong cuộc đời.
Tôi đã phỏng vấn hàng trăm nhà phát triển. Điều tôi học được từ những buổi đó là tôi không cô đơn. Rất ít nhà phát triển phần mềm đang làm việc nắm bắt tốt bản chất của phần mềm phát triển. Họ không nhận thức được những công cụ quan trọng nhất mà chúng ta có hoặc cách đặt chúng để sử dụng tốt. 100% đã phải vật lộn để trả lời một hoặc cả hai câu hỏi quan trọng nhất trong Lĩnh vực phát triển phần mềm:

- Thế nào là Function Composition ?
- Thế nào là Object Composition ?

Vấn đề mà bạn không thể tránh Composition là bạn không biết gì về nó. Bạn vẫn làm nó nhưng làm điều đó rất tệ, bạn viết code nhiều bugs, và làm nó khó để cho những Developer khác hiểu được. Đó chính là vấn đề lớn. Hậu quá rất nghiêm trọng. Chúng tôi mất rất nhiều thời gian để bảo trì phần mềm hơn là bạn tạo nó từ Scratch (Sơ khai), và Bug của họ tác đ65ng đến hà tỉ người trên thế giới.

Toàn bộ thế giới đều sử dụng phần mềm. Mỗi chiếc xe mới là một siêu máy tính mini trên vô lăng, và vấn đề với thiết kế phần mềm gây ra những tai nọ và kinh phí cho người khác.

### Bạn Composing Software mỗi ngày

Nếu bạn đang là một LTV, Bạn soạn thảo Functions và Cấu trúc dữ liệu mỗi ngày, liệu bạn biết nó hay chưa? Bạn có thể làm nó 1 cách có ý thức (consciously) (và tốt hơn), hoặc bạn có thể làm nó 1 cách vô tình với một cách vô thức.
Vấn đề của quá trình phát triển phần mềm là chia nhỏ các vấn đề lớn thành nhiều vấn đề nhỏ hơn, xây dựng các components giải quyết các vấn đề nhỏ hơn đ1, sau đó kết hợp những thành phần đó lại với nhau để tạo thành 1 ứng dụng hoàn chỉnh.

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
```
