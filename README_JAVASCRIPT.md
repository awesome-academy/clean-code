Original Repository: [ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

# Clean Code JavaScript

## Mục lục
1. [Giới thiệu](#giới-thiệu)
2. [Biến](#biến)
3. [Hàm](#hàm)
4. [Đối tượng và cấu trúc dữ liệu](#đối-tượng-và-cấu-trúc-dữ-liệu)
5. [Lớp](#lớp)
6. [SOLID](#solid)
7. [Testing](#testing)
8. [Xử lý đồng thời](#xử-lý-đồng-thời)
9. [Xử lý lỗi](#xử-lý-lỗi)
10. [Định dạng](#định-dạng)
11. [Viết chú thích](#viết-chú-thích)

## Giới thiệu
![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Những nguyên tắc kỹ thuật phần mềm, từ cuốn sách [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) của Robert C. Martin's, được áp dụng cho ngôn ngữ JavaScript.
Đây không phải là một hướng dẫn về cách viết code Javascript mà là hướng dẫn về cách viết các đoạn code dễ đọc hiểu, tái sử dụng và tái cấu trúc được trong Javascript.

Không phải mọi nguyên tắc ở đây phải được tuân thủ một cách nghiêm ngặt, và thậm chí chỉ có một ít trong số đó được sử dụng phổ biến. Ở đây, nó chỉ là một hướng dẫn - không hơn không kém, nhưng chúng được hệ thống hóa thông qua kinh nghiệm thu thập được qua nhiều năm của các tác giả của cuốn sách *Clean Code*

Ngành kỹ thuật phần mềm chỉ phát triển được hơn 50 năm, và chúng ta vẫn
đang học rất nhiều. Một khi kiến trúc phần mềm trở thành phổ biến, có lẽ sau đó
chúng ta sẽ có thêm nhiều luật lệ khó hơn phải tuân theo. Còn giờ đây,
hãy để những hướng dẫn này như là một tiêu chuẩn để đánh giá chất lượng các đoạn
code Javascript mà bạn và team của bạn tạo ra.

Biết những hướng dẫn này thôi sẽ không thể ngay lập tức làm bạn trở thành một
lập trình viên phần mềm tốt hơn được, và làm việc với chúng trong nhiều năm
cũng không có nghĩa bạn sẽ không gặp bất cứ sai lầm nào. Mỗi đoạn code bắt đầu
như một bản thảo đầu tiên, giống như đất sét được nặn nhào và cho tới cuối cùng
thì nó sẽ lộ diện hình hài. Cuối cùng, chúng ta gọt tỉa những khuyết điểm khi
chúng ta xem xét lại nó cùng với các đồng nghiệp.
Đừng để bản thân bạn bị đánh bại bởi những bản thảo đầu tiên,
thứ mà vẫn cần phải được chỉnh sửa. Thay vào đó hãy đánh bại những dòng code.
