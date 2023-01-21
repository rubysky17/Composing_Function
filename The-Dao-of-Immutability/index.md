#### The Dao of Immutability (The Way of the Functional Programmer)

Functional Programming là nền tảng của Javascript và tính bất biến cũng là nền tảng trụ cột của FP. Bạn không thể hiểu đầy đủ về FP nếu không hiểu tính bất biến. Chương này có thể có ích cho bạn.

#### Forward

Tôi dạo lại các kho lưu trữ của những thư viện cũ, và tìm thấy được một hầm tối tăm của tính toán trong đó. Ở đó, tôi đã scroll xuống tìm thấy một cuộn giấy bị lãng quên trên sàn nhà. Cuộc giấy đó được bao bọc trong một ống thép bụi bặm và có nhãn là: "Từ kho lưu trữ của nhà thờ Lambda."

Một Master Lập trình và một người học việc của anh ta ngồi thiền Turing, chiêm ngưỡng Lambda. Người học việc nhìn thầy và hỏi: _"Thầy ơi, thầy bảo con đơn giản hoá, những các chương trình lại phức tạp. Frameworks giảm bớt công việc sáng tạo vằng bỏ những gì khó khăn. Cái nào tốt hơn, một class hay một framework?"_ Sư phụ lập trình nhìn người học việc và hỏi: _"Con không đọc lời dạy của bậc thầy Carmack?"_ - trích dẫn

> “Đôi khi, việc triển khai đơn thuần chỉ là một chức năng. Không phải là một phương pháp. Không phải là một Class. Cũng không phải là một Framework. Chỉ là một Function thôi.”

Nhưng thầy à, _"người học việc bắt đầu"_, nhưng thầy ngắn lời, hỏi:
_Có phải từ "not functional" là "dysfunctional" không ?_

Và rồi người học việc hiểu ra.

---

Ở mặt sau của tờ giấy có ghi là mục lục dường như đề cập đến nhiều cuốn sách trong phòng tính toán. Tôi lén nhìn vào bên trong những cuốn sách, nhưng chúng chứa đầy những từ to tá mà tôi đã không hiểu, vì vậy ôi đặt nó xuống và tiếp tục đọc cuộn giấy. Tôi nhận ra rằng klo75i nhậun của chỉ mục được điền vào những bình luận ngắn, mà tôi sẽ sao chép ở đây, một cách trung thực, cùng với bài viết từ cuộn giấy.

**_Immutability:_** là hằng số thực sự bị thay đổi. Biến đổi che giấu sự thay đổi. Ẩn trốn thay đổi thể hiện sự hỗn loạn. Do đó, người khôn ngoan sẽ nằm bắt được lịch sự thay đổi của nó.

Nếu bạn có 1 dollar, và tôi đưa cho bạn 1 dollar khác, điều đó không thay đổi sự thật trước đó là bạn chỉ có 1 dollar thôi, và bây giờ bạn có 2 dollar. Mutation cố gắng xoá lịch sự thay đổi, nhưng lịch sử không thể xoá bỏ được. Khi quá khứ không được giữ lại, nó sẽ quay lại ám ảnh bạn, biểu hiện là những con bug trong Code của bạn.

**_Separation:_** Logic là suy nghĩ. Hiệu ứng là hành động.. Vì vậy, người khôn ngoan nghĩ trước khi hành động và hành động đó chỉ thực hiện khi suy nghĩ xong.

Nếu bạn cố gắng biểu diễn hiệu ứng và logic cùng 1 l1c, bạn có lẽ ẩn đi các tác dụng phụ chúng có thể gây ra bug trong loc. Giữ function nhỏ. Làm 1 thứ trong 1 thời gian và làm nó thật sự tốt.

**_Composition:_** Tất cả mọi thứ trong tự nhiên hoạt động một cách hài hoà. Cây không thể lớn nếu không có nước. Chim không thể bay nếu không có bầu trời. Vì thế, người thông minh sẽ pha trộn các thành phần 1 cách khôn khéo để làm nó có vị ngon hơn.

Plan cho Composition. Viết các function mà đầu ra của nó sẽ làm việc 1 cách tự nhiên bởi đầu vào của nhiều function khác. Giữ cho function càng đơn giản càng tốt. Tiết kiệm: thời gian là quý giá, và nổ lực thì tốn hời gian. Vì thế, người thông minh sẽ tái sử dụng các công cụ nhiều nhất mà họ có thể làm. Người ngu ngốc tạo các công cụ đặc biệt cho mỗi sự sáng tạo mới.

Không thể sử dụng lại các function dành riêng cho loại cho data type khác. Lập trình viên khôn ngoan nâng function của họ có thể làm việc trên nhiều loại dữ liệu hoặc wrap data để làm nó trở nên là một function đáng mong đợi. Danh sách và items làm trừu tượng hoá vũ trụ rất tốt.

**_Flow:_** nước tĩnh lặng không an toàn để uống. Thức ăn để lâu sẽ bị ôi thiu. Người khôn phát triển là họ làm mọi thứ trở nên trôi chảy.

[Ghi chú của biên tập viên: Hình minh họa duy nhất trên cuộn giấy là một hàng vịt trông khác nhau trôi xuống một dòng suối ngay phía trên câu này. Tôi chưa sao chép hình minh họa vì tôi không tin rằng mình có thể làm điều đó công bằng. Thật kỳ lạ, nó được chú thích:]

> Một danh sách được thể hiện theo thời gian là một luồng.

[Ghi chú tương ứng đọc:]

Các Shared Object và dữ liệu cơ sỡ có thể khiến các function can thiệp lẫn nhau. Chủ đề này đối với có thể cạnh tranh với các tài nguyên giống nhau khác có thể vấp ngã lẫn nhau. Một chương trình có thể được lập luận và kết quả chỉ được dự đoán khi data flows chảy tự do qua cách pure function.

[Ghi chú của biên tập viên: Cuộn sách kết thúc với câu thơ cuối cùng này, không có lời bình luận nào:]

**_Wisdom:_** : Lập trình viên khôn ngoan hiểu đường đi trước khi đi con đường. Vì vậy lập trình viên khôn ngoan có functional, trong khi người không khôn ngoan bị lạc trong rừng.
