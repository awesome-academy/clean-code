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

## Biến
### Sử dụng tên biến có nghĩa và dễ phát âm

**Không tốt:**
```javascript
const yyyymmdstr = moment().format('YYYY/MM/DD');
```

**Tốt:**
```javascript
const currentDate = moment().format('YYYY/MM/DD');
```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng cùng từ vựng cho cùng loại biến

**Không tốt:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Tốt:**
```javascript
getUser();
```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng các tên có thể tìm kiếm được
Chúng ta sẽ đọc code nhiều hơn là viết chúng. Điều quan trọng là code chúng ta viết có thể đọc được và tìm kiếm được. Việc đặt tên các biến *không* có ngữ nghĩa so với chương trình, chúng ta có thể sẽ làm người đọc code bị tổn thương tinh thần.
Hãy làm cho các tên biến của bạn có thể tìm kiếm được. Các công cụ như [buddy.js](https://github.com/danielstjules/buddy.js) và [ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md) có thể giúp nhận ra các hằng chưa được đặt tên.

**Không tốt:**
```javascript
// 86400000 là cái quái gì thế?
setTimeout(blastOff, 86400000);

```

**Tốt:**
```javascript
// Khai báo chúng như một biến global.
const MILLISECONDS_IN_A_DAY = 86400000;

setTimeout(blastOff, MILLISECONDS_IN_A_DAY);

```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng những biến có thể giải thích được
**Không tốt:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
);
```

**Tốt:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```
**[⬆ Về đầu trang](#mục-lục)**

### Tránh hại não người khác
Tường minh thì tốt hơn là viết tắt.

**Không tốt:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Khoan, `l` là cái gì vậy?
  dispatch(l);
});
```

**Tốt:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```
**[⬆ Về đầu trang](#mục-lục)**

### Đừng thêm những ngữ cảnh không cần thiết
Nếu tên của lớp hay đối tượng của bạn đã nói lên điều gì đó rồi, đừng lặp lại điều đó trong tên biến nữa.

**Không tốt:**
```javascript
const Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

**Tốt:**
```javascript
const Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng những tham số mặc định thay vì kiểm tra các điều kiện lòng vòng

**Không tốt:**
```javascript
function createMicrobrewery(name) {
  const breweryName = name || 'Hipster Brew Co.';
  // ...
}

```

**Tốt:**
```javascript
function createMicrobrewery(breweryName = 'Hipster Brew Co.') {
  // ...
}

```
**[⬆ Về đầu trang](#mục-lục)**
