# clean-code-dart
## Mục lục:
  1. [Giới thiệu](#giới-thiệu)
  2. [Biến](#biến)
  3. [Hàm](#hàm)
  4. [Đối tượng và Cấu trúc dữ liệu](#đối-tượng-và-cấu-trúc-dữ-liệu)
  5. [Lớp](#lớp)
  6. [SOLID](#solid)
  7. [Testing](#testing)
  8. [Xử lí đồng thời](#xử-lí-đồng-thời)
  9. [Xử lí lỗi](#xử-lí-lỗi)
  10. [Định dạng](#định-dạng)
  11. [Viết chú thích](#viết-chú-thích)
  12. [Các ngôn ngữ khác](#các-ngôn-ngữ-khác)


## Giới thiệu
![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Những nguyên tắc kỹ thuật phần mềm, từ cuốn sách
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
áp dụng cho ngôn ngữ Dart. Đây không phải là một hướng dẫn về cách viết code Dart mà là hướng dẫn về cách viết các đoạn code dễ đọc hiểu, tái sử dụng và tái cấu trúc được trong Dart.
Không phải mọi nguyên tắc ở đây phải được tuân thủ một cách nghiêm ngặt,
và thậm chí chỉ có một ít trong số đó được sử dụng phổ biến. Ở đây, nó chỉ là một
hướng dẫn - không hơn không kém, nhưng chúng được hệ thống hóa thông qua kinh
nghiệm thu thập được qua nhiều năm của các tác giả của cuốn sách [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

Ngành kỹ thuật phần mềm chỉ phát triển được hơn 50 năm, và chúng ta vẫn
đang học rất nhiều. Một khi kiến trúc phần mềm trở thành phổ biến, có lẽ sau đó
chúng ta sẽ có thêm nhiều luật lệ khó hơn phải tuân theo. Còn giờ đây,
hãy để những hướng dẫn này như là một tiêu chuẩn để đánh giá chất lượng các đoạn
code Dart mà bạn và team của bạn tạo ra.
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
```dart
final formatter = DateFormat('yyyy/MM/dd');
final yyyymmddStr = formatter.format(DateTime.now());

```
**Tốt:**
```dart
final formatter = DateFormat('yyyy/MM/dd');
final currentDate = formatter.format(DateTime.now());
```

**[⬆ về đầu trang](#mục-lục)**

### Sử dụng cùng từ vựng cho cùng loại biến

**Không tốt:**
```dart
getUserInfo();
getClientData();
getCustomerRecord();
```
**Tốt:**
```dart
getUser();
```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng các tên có thể tìm kiếm được
Chúng ta sẽ đọc code nhiều hơn là viết chúng. Điều quan trọng là code chúng ta
viết có thể đọc được và tìm kiếm được. Việc đặt tên các biến *không* có ngữ
nghĩa so với chương trình, chúng ta có thể sẽ làm người đọc code bị tổn thương
tinh thần.
Hãy làm cho các tên biến của bạn có thể tìm kiếm được.

**Không tốt:**
```dart
// 86400000 là cái gì thế?
setTimeout(blastOff, 86400000);
```
**Tốt:**
```dart
// Khai báo chúng như một biến hằng.
const millisecondsInADay = 86400000;
setTimeout(blastOff, millisecondsInADay);
```
**[⬆ Về đầu trang](#mục-lục)**

### Sử dụng những biến có thể giải thích được

**Không tốt:**
```dart
final address = "One Infinite Loop, Cupertino 95014";
saveCityZipCode(address.split(',')[0].trim(), address.split(',')[1].trim());
```
**Tốt:**
```dart
final address = "One Infinite Loop, Cupertino 95014";
final city = address.split(',')[0].trim();
final zipCode = address.split(',')[1].trim();
saveCityZipCode(city, zipCode);
```
**[⬆ Về đầu trang](#mục-lục)**

### Tránh hại não người khác
Tường minh thì tốt hơn là ẩn.

**Không tốt:**
```dart
final l = ["Austin", "New York", "San Francisco"];
  
l.forEach((city) {
  doStuff(city);
  doSomeOtherStuff(city);
  //...
  //...
});
```
**Tốt:**
```dart
final locations = ["Austin", "New York", "San Francisco"];
  
locations.forEach((city) {
  doStuff(city);
  doSomeOtherStuff(city);
  //...
  //...
});
```
**[⬆ Về đầu trang](#mục-lục)**

### Đừng thêm những ngữ cảnh không cần thiết
Nếu tên của lớp hay đối tượng của bạn đã nói lên điều gì đó rồi, đừng lặp lại điều đó trong tên biến nữa.

**Không tốt:**
```dart
class Car {
  var carMake = "Honda";
  var carModel = "Accord";
  var carColor = "Blue";
}

void paintCar(Car car) {
  car.carColor = "Red";
}
```
**Tốt:**
```dart
class Car {
  var make = "Honda"
  var model = "Accord"
  var color = "Blue"
}

void paintCar(Car car) {
  car.color = "Red"
}
```
**[⬆ Về đầu trang](#mục-lục)**

## Hàm
### Đối số của hàm (lý tưởng là ít hơn hoặc bằng 2)
Giới hạn số lượng param của hàm là một điều cực kì quan trọng bởi vì nó làm cho
hàm của bạn trở nên dễ test hơn. Trường hợp có nhiều hơn 3 params có thể dẫn
đến việc bạn phải test hàng tấn test case khác nhau với những đối số riêng biệt.

1 hoặc 2 đối số là trường hợp lý tưởng, còn trường hợp 3 đối số thì nên tránh
nếu có thể. Những trường hợp khác (từ 3 params trở lên) thì nên được gộp lại.
Thông thường nếu có nhiều hơn 2 đối số thì hàm của bạn đang cố thực hiện quá
nhiều việc rồi đấy. Trong trường hợp ngược lại, phần lớn thời gian một đối
tượng cấp cao sẽ là đủ để làm đối số.

**[⬆ Về đầu trang](#mục-lục)**

### Hàm chỉ nên giải quyết một vấn đề
Đây là quy định quan trọng nhất của kỹ thuật phần mềm. Khi một hàm thực hiện
nhiều hơn 1 việc, chúng sẽ trở nên khó khăn hơn để viết code, test, và suy luận.
Khi bạn có thể tách biệt một hàm để chỉ thực hiện một hành động, thì sẽ dễ dàng
hơn để tái cấu trúc và code của bạn sẽ dễ đọc hơn nhiều. Nếu bạn chỉ cần làm theo
hướng dẫn này thôi mà không cần làm gì khác thì bạn cũng đã giỏi hơn nhiều
developer khác rồi.

**Không tốt:**
```dart
void emailClients(List<Client> clients) {
  clients.forEach((client) {
    var clientRecord = repository.findOne(client.getId());
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**Tốt:**
```dart
void emailClients(List<Client> clients) {
  clients.forEach((client) {
    if (isActiveClient(client)) {
      email(client);
    }
  });
}

bool isActiveClient(Client client) {
  return repository.findOne(client.getId()).isActive();
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Tên hàm phải nói ra được những gì chúng làm

**Không tốt:**
```dart
void addToDate(DateTime date, int month) {
  //..
}
var date = DateTime.now();
// Khó để biết được hàm này thêm gì thông qua tên hàm.
addToDate(date, 1);
```
**Tốt:**
```dart
void addMonthToDate(DateTime date, int month) {
  //..
}
var date = DateTime.now();
// Khó để biết được hàm này thêm gì thông qua tên hàm.
addMonthToDate(date, 1);
```

**[⬆ Về đầu trang](#mục-lục)**

### Xóa code trùng lặp
Tuyệt đối tránh những dòng code trùng lặp. Code trùng lặp thì không tốt bởi vì
nếu bạn cần thay đổi cùng một logic, bạn phải sửa ở nhiều hơn một nơi.

Hãy tưởng tượng nếu bạn điều hành một nhà hàng và bạn theo dõi hàng tồn kho:
bao gồm cà chua, hành tây, tỏi, gia vị, vv.... Nếu bạn có nhiều danh sách
quản lý, thì tất cả chúng phải được thay đổi khi bạn phục vụ một món ăn có
chứa cà chua. Nếu bạn chỉ có 1 danh sách, thì việc cập nhật ở một nơi thôi.

Thông thường, bạn có những dòng code lặp lại bởi vì bạn có 2 hay nhiều hơn
những thứ chỉ khác nhau chút ít, mà chia sẻ nhiều thứ chung, nhưng sự khác
nhau của chúng buộc bạn phải có 2 hay nhiều hàm riêng biệt để làm nhiều điều
tương tự nhau. Xóa đi những dòng code trùng có nghĩa là tạo ra một abstraction
có thể xử lý tập những điểm khác biệt này chỉ với một hàm/module hay class.

Có được một abstraction đúng thì rất quan trọng, đó là lý do tại sao bạn nên
tuân thủ các nguyên tắc SOLID được đặt ra trong phần *Lớp*. Những abstraction
không tốt có thể còn tệ hơn cả những dòng code bị trùng lặp, vì thế hãy cẩn
thận! Nếu bạn có thể tạo ra một abstraction tốt, hãy làm nó! Đừng lặp lại chính
mình, nếu bạn không muốn đi cập nhật nhiều nơi bất cứ khi nào bạn muốn thay đổi
một thứ gì đó.

**[⬆ Về đầu trang](#mục-lục)**

### Tránh những ảnh hưởng phụ (Side Effect)
Một hàm tạo ra ảnh hưởng phụ nếu nó làm bất kì điều gì khác hơn là nhận một giá
trị đầu vào và trả về một hoặc nhiều giá trị. Ảnh hưởng phụ có thể là ghi một
file, thay đổi vài biến toàn cục, hoặc vô tình đưa tất cả tiền của bạn cho một
người lạ.

Bây giờ, cũng có khi bạn cần ảnh hưởng phụ trong một chương trình. Giống như ví dụ
trước, bạn cần ghi một file. Những gì bạn cần làm là tập trung vào nơi bạn sẽ làm
nó. Đừng viết hàm và lớp riêng biệt để tạo ra một file cụ thể. Hãy có một service
để viết nó. Một và chỉ một.

Điểm chính là để tránh những lỗi chung như chia sẻ trạng thái giữa những đối tượng
mà không có bất kì cấu trúc nào, sử dụng các kiểu dữ liệu có thể thay đổi được mà
có thể được ghi bởi bất cứ thứ gì, và không tập trung nơi có thể xảy ra các ảnh hưởng
phụ. Nếu bạn có thể làm điều đó, bạn sẽ hạnh phúc hơn so với phần lớn các lập trình
viên khác đấy.

**Không tốt:**
```dart
// Biến toàn cục được tham chiếu bởi hàm dưới đây.
// Nếu chúng ta có một hàm khác sử dụng name, nó sẽ trả về kết quả sai
void splitIntoFirstAndLastName(String name) {
  var names = name.split(' ');
  if (names.length > 0) {
    name = names[0];
  }
}
var name = "Ryan McDermott";
splitIntoFirstAndLastName(name);
print('Name: $name'); // Name: Ryan
```

**Tốt:**
```dart
String splitIntoFirstAndLastName(String name) {
  // Assuming that the name is in the "First Last" format
  var names = name.split(' ');
  if (names.length > 0) {
    return names[0];
  } else {
    return name;
  }
}
var name = "Ryan McDermott";
var newName = splitIntoFirstAndLastName(name);
print('Name: $name'); // Name: Ryan McDermott
print('New Name: $newName'); // Name: Ryan
```

**[⬆ Về đầu trang](#mục-lục)**

### Đóng gói các điều kiện

**Không tốt:**
```dart
if ("fetching" == fsmState && listNode.isEmpty) {
  // ...
}
```

**Tốt:**
```dart
bool isShowProgressBar(dynamic fsm, String listNode) {
  return "fetching" == fsm.getState() && listNode.isEmpty;
}
if (isShowProgressBar(fsmInstance, listNodeInstance)) {
  // ...
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Tránh những điều kiện phủ định

**Không tốt:**
```dart
bool isDOMNodeNotPresent(dynamic node) {
  // ...
}
if (!isDOMNodeNotPresent(nodeInstance)) {
  // ...
}
```

**Tốt:**
```dart
bool isDOMNodePresent(dynamic node) {
  // ...
}
if (isDOMNodePresent(nodeInstance)) {
  // ...
}
```
**[⬆ Về đầu trang](#mục-lục)**

### Tránh điều kiện
Đây dường như là một việc bất khả thi. Khi nghe điều này đầu tiên, hầu hết mọi
người đều nói, "Làm sao tôi cần phải làm gì mà không có mệnh đề `if`?"
Câu trả lời là bạn có thể sử dụng tính đa hình để đạt được công việc tương tự
trong rất nhiều trường hợp. Câu hỏi thứ hai thường là "Đó là điều tốt nhưng tại
sao tôi lại muốn làm điều đó?" Câu trả lời là khái niệm mà ta đã học ở phần
trước: một hàm chỉ nên thực hiện một việc. Khi bạn có nhiều lớp và hàm mà có
nhiều mệnh đề `if`, bạn đang cho người dùng của bạn biết rằng hàm của bạn đang
làm nhiều hơn một việc. Hãy nhớ, chỉ làm một công việc thôi.

**Không tốt:**
```dart
class Airplane {
  // ...
  double getCruisingAltitude(Airplane airplane) {
    switch (type) {
      case "777":
        return airplane.getMaxAltitude() - airplane.getPassengerCount();
      case "Air Force One":
        return airplane.getMaxAltitude();
      case "Cessna":
        return airplane.getMaxAltitude() - airplane.getFuelExpenditure();
      default:
        return 0.0; // Hoặc giá trị mặc định khác tùy thuộc vào logic của bạn
    }
  }
}
```

**Tốt:**
```dart
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  @override
  double getCruisingAltitude() {
    return getMaxAltitude() - getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  @override
  double getCruisingAltitude() {
    return getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  @override
  double getCruisingAltitude() {
    return getMaxAltitude() - getFuelExpenditure();
  }
}

```
**[⬆ Về đầu trang](#mục-lục)**

### Xóa code chết (dead code)
Dead code cũng tệ như code trùng lặp. Không có lý do gì để giữ chúng lại trong
codebase của bạn. Nếu nó không được gọi nữa, hãy bỏ nó đi! Nó vẫn sẽ nằm trong
lịch sử phiên bản của bạn nếu bạn vẫn cần nó.

**[⬆ Về đầu trang](#mục-lục)**

## Đối tượng và cấu trúc dữ liệu
### Sử dụng getter và setter
Đây là một danh sách các lí do tại sao:

* Khi bạn muốn thực hiện nhiều hơn việc lấy một thuộc tính của đối tượng, bạn không
cần phải tìm kiếm và thay đổi mỗi accessor trong codebase của bạn.
* Làm cho việc thêm các validation đơn giản khi thực hiện trên một `tập hợp`.
* Đóng gói các biểu diễn nội bộ.
* Dễ dàng thêm log và xử lí lỗi khi getting và setting.
* Kế thừa lớp này, bạn có thể override những hàm mặc định.
* Bạn có thể lazy load các thuộc tính của một đối tượng, lấy nó từ server.

**[⬆ Về đầu trang](#mục-lục)**

## Lớp
### Sử dụng hàm khởi tạo (constructor) quá nhiều biến hoặc gọi nhiều hàm set liên tiếp nhau
- Tránh sử dụng hàm constructor với nhiều hơn 3 đối số truyền vào thay vì vậy hãy áp dụng _Builder Pattern_

### Ưu tiên thành phần hơn là kế thừa
- Như đã được nhấn mạnh nhiều trong [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns)
của Gang of Four, bạn nên sử dụng cấu trúc thành phần hơn là thừa kế nếu có thể.
Có rất nhiều lý do tốt để sử dụng kế thừa cũng như sử dụng thành phần.
Điểm nhấn cho phương châm này đó là nếu tâm trí của bạn đi theo bản năng thừa kế,
thử nghĩ nếu thành phần có thể mô hình vấn đề của bạn tốt hơn. Trong một số trường
hợp nó có thể.

Bạn có thể tự hỏi, "khi nào tôi nên sử dụng thừa kế?" Nó phụ thuộc vào
vấn đề trong tầm tay của bạn, nhưng đây là một danh sách manh nha khi kế thừa
có ý nghĩa hơn thành phần:

1. Kế thừa của bạn đại diện cho mỗi quan hệ "is-a" và không có mỗi quan hệ "has-a"
(Human->Animal vs. User->UserDetails).
2. Bạn có thể sử dụng lại code từ lớp cơ bản (Humans có thể di chuyển giống tất cả Animals).
3. Bạn muốn làm thay đổi toàn cục đến các lớp dẫn xuất bằng cách thay đổi lớp cơ bản.

**[⬆ Về đầu trang](#mục-lục)**

## **SOLID**
### Nguyên lí đơn trách nhiệm (Single Responsibility Principle)
Như đã được nói đến trong cuốn Clean Code, "Chỉ có thể thay đổi một lớp vì một lí
do duy nhất". Thật là hấp dẫn để nhồi nhét nhiều chức năng vào cho một lớp, giống
như là khi bạn chỉ có thể lấy một chiếc vali cho chuyến bay vậy. Vấn đề là lớp của
bạn sẽ không được hiểu gắn kết về mặt khái niệm của nó và sẽ có rất nhiều lí do
để thay đổi. Việc làm giảm thiểu số lần bạn cần phải thay đổi một lớp là một việc
quan trọng. Nó quan trọng bởi vì nếu có quá nhiều chức năng trong một lớp và bạn
chỉ muốn thay đổi một chút xíu của lớp đó, thì có thể sẽ rất khó để hiểu được việc
thay đổi đó sẽ ảnh hưởng đến những module khác trong codebase như thế nào.

**Không tốt:**
```dart
class UserSettings {
  User _user;
  // ...

  bool _verifyCredentials() {
    //...
  }

  void changeSettings(UserSettings settings) {
    if (_verifyCredentials()) {
      // ...
    }
  }
}

class User {
  // Define properties and methods for the User class
  // ...
}
```

**Tốt:**
```dart
class UserAuth {
  User _user;

  UserAuth(User user) {
    _user = user;
  }

  bool verifyCredentials() {
    //...
  }
}

class UserSettings {
  User _user;
  UserAuth _auth;

  UserSettings(User user) {
    _user = user;
    _auth = UserAuth(user);
  }

  void changeSettings(UserSettings settings) {
    if (_auth.verifyCredentials()) {
      //...
    }
  }
}

class User {
  // Define properties and methods for the User class
  // ...
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Nguyên lí đóng mở (Open/Closed Principle)
Betrand Meyer đã nói "có thể thoải mái mở rộng một module, nhưng hạn chế sửa
đổi bên trong module đó". Điều đó nghĩa là gì? Nguyên tắc này cơ bản nhấn mạnh
rằng bạn phải cho phép người dùng thêm các chức năng mới mà không làm thay
đổi các code đang có.

**Không tốt:**
```dart
abstract class Adapter {
  String name;

  Adapter(this.name);
}

class AjaxAdapter extends Adapter {
  AjaxAdapter() : super("ajaxAdapter");
}

class NodeAdapter extends Adapter {
  NodeAdapter() : super("nodeAdapter");
}

class HttpRequester {
  Adapter adapter;

  HttpRequester(Adapter adapter) {
    this.adapter = adapter;
  }

  void fetch(String url) {
    switch (adapter.name) {
      case "ajaxAdapter":
        makeAjaxCall(url);
        break;
      case "nodeAdapter":
        makeHttpCall(url);
        break;
      default:
        break;
    }
  }

  Future<Response> makeAjaxCall(String url) {
    // request and return Future<Response>
  }

  Future<Response> makeHttpCall(String url) {
    // request and return Future<Response>
  }
}

class Response {
  // Define properties and methods for the Response class
  // ...
}
```

**Tốt:**
```dart
abstract class Adapter {
  String name;

  Adapter(this.name);

  Future<Response> request(String url);
}

class AjaxAdapter extends Adapter {
  AjaxAdapter() : super("ajaxAdapter");

  @override
  Future<Response> request(String url) async {
    // request and return Future<Response>
    // For example, you can use the http package for making HTTP requests.
  }
}

class NodeAdapter extends Adapter {
  NodeAdapter() : super("nodeAdapter");

  @override
  Future<Response> request(String url) async {
    // request and return Future<Response>
    // For example, you can use the http package for making HTTP requests.
  }
}

class HttpRequester {
  Adapter adapter;

  HttpRequester(Adapter adapter) {
    this.adapter = adapter;
  }

  Future<void> fetch(String url) async {
    await adapter.request(url);
  }
}

class Response {
  // Define properties and methods for the Response class
  // ...
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Nguyên lí thay thế Liskov (Liskov Substitution Principle)
Đây là một thuật ngữ đáng sợ cho một khái niệm rất đơn giản. Nó được định nghĩa
một cách chính thức là: "Nếu S là một kiểu con của T, thì các đối tượng của kiểu
T có thể được thay thế bằng các đối tượng của kiểu S (ví dụ các đối tượng của
kiểu S có thể thay thế các đối tượng của kiểu T) mà không làm thay đổi bất kì thuộc tính mong muốn nào của chương trình đó (tính chính xác, thực hiện tác vụ, ..).
Đó thậm chí còn là một định nghĩa đáng sợ hơn.

Sự giải thích tốt nhất cho nguyên lí này là, nếu bạn có một lớp cha và một lớp con,
thì lớp cơ sở và lớp con có thể được sử dụng thay thế cho nhau mà không làm thay
đổi tính đúng đắn của chương trình. Có thể vẫn còn hơi rối ở đây, vậy hãy xem
cái ví dụ cổ điển hình vuông-hình chữ nhật (Square-Rectangle) dưới đây. Về mặt
toán học, một hình vuông là một hình chữ nhật, tuy nhiên nếu bạn mô hình hoá điều
này sử dụng quan hệ "is a" thông qua việc kế thừa, bạn sẽ nhanh chóng gặp phải
rắc rối đấy.

**Không tốt:**
```dart
class Rectangle {
  int width;
  int height;

  Rectangle(this.width, this.height);

  void setColor(int color) {
    // ...
  }

  void render(int area) {
    print(area);
  }

  void setWidth(int width) {
    this.width = width;
  }

  void setHeight(int height) {
    this.height = height;
  }

  int getArea() {
    return width * height;
  }
}

class Square extends Rectangle {
  Square(int side) : super(side, side);

  @override
  void setWidth(int width) {
    super.setWidth(width);
    super.setHeight(width);
  }

  @override
  void setHeight(int height) {
    super.setHeight(height);
    super.setWidth(height);
  }
}

void renderLargeRectangles(List<Rectangle> rectangles) {
  rectangles.forEach((rectangle) {
    rectangle.setWidth(4);
    rectangle.setHeight(5);
    var area = rectangle.getArea();
    rectangle.render(area);
  });
}


var rectangles = [Rectangle(width: 0, height: 0), Square(width: 0, height: 0)]
renderLargeRectangles(rectangles: rectangles)
```

**Tốt:**
```dart
class Shape {
  void setColor(int color) {
    // ...
  }

  void render(int area) {
    // ...
  }

  int getArea() {
    // ...
    return 0; // Placeholder, thay thế với logic thực tế của bạn
  }
}

class Rectangle extends Shape {
  int recWidth;
  int recHeight;

  Rectangle(int width, int height) {
    recWidth = width;
    recHeight = height;
  }

  @override
  int getArea() {
    return recWidth * recHeight;
  }
}

class Square extends Shape {
  int squareLength;

  Square(int length) {
    squareLength = length;
  }

  @override
  int getArea() {
    return squareLength * squareLength;
  }
}

void renderLargeShapes(List<Shape> shapes) {
  shapes.forEach((shape) {
    var area = shape.getArea();
    shape.render(area);
  });
}

void main() {
  var shapes = [Rectangle(4, 5), Square(5)];
  renderLargeShapes(shapes);
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Nguyên lí phân tách interface (Interface Segregation Principle)
Nguyên lí phân tách interface nhấn mạnh rằng "Người dùng không nên bị bắt
buộc phải phụ thuộc vào các interfaces mà họ không sử dụng."

Một ví dụ tốt để minh hoạ cho nguyên lí này trong Dart là các lớp mà yêu
cầu cài đặt các đối tượng lớn. Việc không yêu cầu người dùng thiết lập một số
lượng lớn các phương thức là một điều tốt, bởi vì đa số họ không cần tất
cả các cài đặt. Làm cho chúng trở thành tuỳ chọn giúp tránh được việc có một
"fat interface".


**[⬆ Về đầu trang](#mục-lục)**

### Nguyên lí đảo ngược dependency (Dependency Inversion Principle)
Với cách code thông thường, các module cấp cao sẽ gọi các module cấp thấp.
Module cấp cao sẽ phụ thuộc và module cấp thấp, điều đó tạo ra các dependency.
Khi module cấp thấp thay đổi, module cấp cao phải thay đổi theo.
Một thay đổi sẽ kéo theo hàng loạt thay đổi, giảm khả năng bảo trì của code.

Nguyên lí này khẳng định hai điều cần thiết sau:
1. Nhưng module cấp cao không nên phụ thuộc vào những module cấp thấp. Cả
hai nên phụ thuộc vào abstraction.
2. Abstraction (interface) không nên phụ thuộc vào chi tiết, mà ngược lại.

Điều này có thể khó hiểu lúc ban đầu, nhưng nếu bạn đã từng làm việc với Angular.js,
bạn đã thấy một sự hiện thực của nguyên lí này trong dạng của Dependency Injection
(DI). Khi chúng không phải là các khái niệm giống nhau, DIP giữ cho module cấp
cao không biết chi tiết các module cấp thấp của nó và thiết lập chúng. Có thể đạt
được điều này thông qua DI. Một lợi ích to lớn của DIP là nó làm giảm sự phụ thuộc
lẫn nhau giữa các module. Sự phụ thuộc lẫn nhau là một kiểu mẫu không tốt, vì nó
làm cho việc tái cấu trúc code trở nên khó khăn.

**Không tốt:**
```dart
// SavingHandler là module cấp cao
class SavingHandler {
  void save(String path) {
    LocalFileHandler().save(path);
  }
}

// LocalFileHandler là module thấp
class LocalFileHandler {
  static final LocalFileHandler _shared = LocalFileHandler._internal();

  factory LocalFileHandler() {
    return _shared;
  }

  LocalFileHandler._internal();

  void save(String path) {
    // Thực hiện lưu dữ liệu cục bộ
  }
}
```

**Tốt:**
```dart
// Protocol
abstract class Storage {
  void save(String path);
}

// Module làm nhiệm vụ quản lý việc lưu trữ
class SavingManager {
  static final SavingManager _shared = SavingManager._internal();

  factory SavingManager() {
    return _shared;
  }

  SavingManager._internal();

  void save(String path, Storage storage) {
    storage.save(path);
  }
}

// Các Module implement các protocol
class FileSystemSaving implements Storage {
  @override
  void save(String path) {
    // saving...
  }
}

// Giờ muốn lưu gì thì chỉ cần gọi manage thôi
void saveLocalData(String path) {
  var fileSystemSaving = FileSystemSaving();
  SavingManager().save(path, fileSystemSaving);
}
```

Trong thực tế, người ta thường áp dụng pattern DI (Dependency Injection) để đảm bảo nguyên lý DIP (Dependency Inversion Principle) trong code.

**[⬆ Về đầu trang](#mục-lục)**

## Testing
Testing thì quan trọng hơn shipping. Nếu bạn không có test hoặc không đủ,
thì mỗi lần ship code bạn sẽ không chắc là mình có làm hư hại thứ gì không.
Việc quyết định những gì để tạo thành số lượng test đủ là do team của bạn,
nhưng việc có 100% độ bao phủ (tất cả các câu lệnh và rẽ nhánh) là cách để
bạn đạt được sự tự tin cao. Điều này có nghĩa ngoài việc có được một framework
để test tốt, bạn cũng cần sử dụng một công cụ tính độ bao phủ tốt

Không có lí do gì để không viết test. Có rất nhiều framework test Dart tốt,
vì thế hãy tìm một framework mà team bạn thích. Khi đã tìm được một cái thích
hợp với team của mình, hãy đặt mục tiêu để luôn luôn viết test cho mỗi tính
năng hoặc module mới của bạn. Nếu phương pháp test ưa thích của bạn là Test
Driven Development (TDD), điều đó thật tuyệt, nhưng điểm quan trọng là phải
chắc chắn bạn đạt được mục tiêu về độ bao phủ trước khi launch một tính năng
hoặc refactor một tính năng cũ nào đó.

**[⬆ Về đầu trang](#mục-lục)**

## Xử lí đồng thời
### Hãy dùng higher-order function, đừng dùng callback tránh callback hell
Tham khảo thư viện [ReactiveX/RxDart](https://pub.dev/packages/rxdart)

**[⬆ Về đầu trang](#mục-lục)**

## Xử lí lỗi
Thông báo lỗi là một điều tốt! Nghĩa là chương trình của bạn nhận dạng
được khi có một cái gì đó chạy không đúng và nó sẽ cho bạn biết bằng việc
dừng chức năng mà nó đang thực thi và thông
báo cho bạn trong console với một log để theo dấu.

### Đừng bỏ qua những lỗi đã bắt được
Nếu không làm gì với lỗi đã bắt được, bạn sẽ không thể sửa hoặc phản ứng
lại được với lỗi đó. Ghi lỗi ra console (`debugPrint`) cũng không tốt hơn
bao nhiêu vì đa số nó có thể bị trôi mất trong một đống những thứ được hiển
thị ra ở console. Nếu bạn đặt bất cứ đoạn code nào trong một block `try/catch`,
tức là bạn nghĩ một lỗi có thể xảy ra ở đây, do đó bạn nên có một giải pháp
hoặc tạo một luồng code để xử lí lỗi khi nó xảy ra.

**Không tốt:**
```dart
try {
  functionThatMightThrow();
} catch (error) {
  print(error);
}
```

**Tốt:**
```dart
try {
  functionThatMightThrow();
} catch (error) {
  // Một lựa chọn (nhiều tiếng ồn hơn so với console.log):
  throw Exception('error');
  // Một lựa chọn khác:
  notifyUserOfError(error);
  // Lựa chọn khác:
  reportErrorToService(error);
  // HOẶC thực hiện cả ba!
}

```

**[⬆ Về đầu trang](#mục-lục)**

## Định dạng
Việc định dạng code mang tính chủ quan. Giống như nhiều quy tắc được trình
bày trong tài liệu này, không có quy tắc nào cứng nhắc và nhanh chóng mà bạn
bắt buộc phải tuân theo. Điểm chính của phần này là ĐỪNG BAO GIỜ TRANH CÃI
về việc định dạng code như thế nào. Thật tốn thời gian và
tiền bạc chỉ để tranh cãi về vấn đề định dạng code.

Đối với những thứ không thuộc phạm vi của việc tự động định dạng code (thụt đầu
dòng, tab và space, nháy đơn và nháy kép,..) hãy xem một số hướng dẫn ở [đây](https://dart.dev/effective-dart/style).

### Các hàm gọi và hàm được gọi nên nằm gần nhau
Nếu một hàm gọi một hàm  khác, hãy giữ những hàm này nằm gần theo chiều dọc trong
file. Lí tưởng là, hãy giữ cho hàm gọi ở trên hàm được gọi. Chúng ta có xu hướng
đọc code từ trên xuống, giống như đọc báo vậy. Do đó, hãy làm cho code của chúng
ta cũng được đọc theo cách đó.

**[⬆ Về đầu trang](#mục-lục)**

## Viết chú thích
### Chỉ nên viết chú thích cho những thứ có logic phức tạp.
Các chú thích thường là lời xin lỗi, chứ không phải là yêu cầu.
Những đoạn code tốt thì *đa số* tự nó đã là tài liệu rồi.

**Không tốt:**
```dart
void hashIt(String data) {
  // Khai báo hash
  var hash = 0;
  // Lấy chiều dài của chuỗi
  final length = data.length;
  // Lặp qua mỗi kí tự
  for (var char in data.runes) {
    // Chuyển kí tự qua số trong bảng Ascii
    hash = char;
    // Chuyển số qua dạng binary
    print(hash.toRadixString(2));
  }
}
```

**Tốt:**
```dart
void hashIt(String data) {
  var hash = 0;
  final length = data.length;
  data.runes.forEach((int rune) {
    // Chuyển số qua dạng binary
    print(rune.toRadixString(2));
  });
}
```

**[⬆ Về đầu trang](#mục-lục)**

### Đừng giữ lại những đoạn code bị chú thích
Những công cụ quản lí phiên bản sinh ra để làm nhiệm vụ của chúng.
Hãy để code cũ của bạn nằm lại trong dĩ vãng đi.

**Không tốt:**
```dart
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Tốt:**
```dart
doStuff();
```
**[⬆ Về đầu trang](#mục-lục)**

### Đừng viết các chú thích nhật ký.
Hãy nhớ, sử dụng công cụ quản lí phiên bản như Git! Chúng ta không cần những đoạn code
vô dụng, bị chú thích và đặc biệt là những chú thích dạng nhật ký...
Sử dụng `git log` để xem lịch sử được mà!

**Không tốt:**
```dart
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
int combine(int a, int b) {
  return a + b;
}
```

**Tốt:**
```dart
int combine(int a, int b) {
  return a + b;
}
```
**[⬆ Về đầu trang](#mục-lục)**

### Tránh những đánh dấu vị trí
Chúng thường xuyên làm nhiễu code. Hãy để những tên hàm, biến cùng với các
định dạng thích hợp tự tạo thành cấu trúc trực quan cho code của bạn.

**Không tốt:**
```dart
// MARK: ReloadData

void reloadData() {
  // ...
}

// MARK: Const setup

const leftPadding =  ...

```

**Tốt:**
```dart
void reloadData() {
  // ...
}

const leftPadding =  ...
```
**[⬆ Về đầu trang](#mục-lục)**
