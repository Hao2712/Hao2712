# Advance C

## Bài 1: Compiler - Macro

### Compiler
Là một chương trình phần mềm có chức năng chuyển đổi mã nguồn viết bằng ngôn ngữ lập trình bậc cao (C, C++...) thành mã máy hoặc ngôn ngữ trung gian mà có thể được thực thi bởi máy tính.<br>
Các bước trong quá trình biên dịch:
- __Preprocessing__: là quá trình tiền xử lý, các comment sẽ được xoá khỏi mã nguồn, trình biên dịch sẽ thay thế các macro được gọi trong mã nguồn thành đoạn mã đã được định nghĩa, các thư viện được gọi cũng sẽ được thêm vào mã nguồn. Sau quá trình này sẽ tạo ra các file có định dạng (.i, .ii).
- __Compilation__: là quá trình dịch các file (.i, .ii) thành file hợp ngữ (assembly code) có định dạng (.s).
- __Assemble__: là quá trình dịch file hợp ngữ (.s) thành file mã máy có định dạng (.o, .obj).
- __Linking__: là quá trình liên kết các file mã máy (.o, .obj) lại với nhau, các thư viện tĩnh (static library) có định dạng (.lib, .a) cũng sẽ được thêm vào chương trình. Kết hợp các thành phần tạo thành file Executable machine code (.exe), có thể gọi là chương trình máy tính. 
### Macro
Dùng để chỉ những thông tin được xử lý ở quá trình tiền xử lý. Các macro được nhận diện bằng dấu # trong mã nguồn, những chỉ thị này không phải mã lệnh, mà là hướng dẫn cho quá trình tiền xử lý.<br>
Các macro thường sử dụng:
- __#include__: để bao gồm nội dung của một file khác vào mã nguồn hiện tại. Sử dụng để thêm thư viện chuẩn hoặc file header.
- __#define__: định nghĩa hằng số, macro
- __#undef__: xoá định nghĩa trước đó
- __ifdef__, __ifndef__, __#endif__: kiểm tra xem đoạn mã đã được định nghĩa chưa, nếu có (__#ifdef__) hoặc không (__#ifndef__) thì sẽ định nghĩa đến khi gặp (__#endif__)
- __#if__, __#elif__, __#else__: kiểm tra các điều kiện biên dịch, tương tự như cấu trúc rẽ nhánh (__if_else__), sẽ dừng lại khi gặp (__#endif__)<br>
Toán tử trong macro:
- __#__: để chuyển đổi một tham số thành chuỗi ký tự
- __##__: là toán tử nối, cho phép liên kết hai biểu thức thành một tên duy nhất<br>
Variadic macro:
- Cho phép nhận một số lượng biến tham số có thể thay đổi
- Giúp địng nghĩa các macro có thể xử lý một lượng biến đầu vào khác nhau<br>
`#define MACRO_NAME(...) //Body macro`
- Cú pháp: Variadic macro được định nghĩa bằng cách sử dụng dấu ... để chỉ định rằng macro có thể nhận nhiều tham số. Có thể truy cập các tham số này bằng cách sử dụng `__VA_ARGS__`
## Bài 2: STDARG - ASSERT
### STDARG
Cung cấp các phương thức để làm việc với các hàm có số lượng tham số đầu vào (input parameter) không cố định.<br>
- __va_list__: là một kiểu dữ liệu để đại diện cho danh sách các đối số biến đổi
- __va_start__: bắt đầu một danh sách đối số biến đổi. Nó cần được gọi trước khi truy cập các đối số biến đổi đầu tiên
- __va_arg__: truy cập một đối số trong danh sách đối số biến đổi. Hàm này nhận một đối số của kiểu được xác định bởi tham số thứ hai
- __va_end__: kết thúc việc sử dụng danh sách đối số biến đổi. Nó cần được gọi trước khi kết thúc hàm<br>
Về bản chất, các câu lệnh trong thư viện __STDARG__ là các macro để xử lý các tham số biến, tương tự như Variadic macro.
### ASSERT
Cung cấp một macro để kiểm tra các điều kiện trong chương trình. Thường được sử dụng để xác nhận rằng một điều kiện nhất định là đúng trong quá trình thực thi. Nếu điều kiện không đúng, chương trình sẽ dừng lại và thông báo lỗi<br>
Cách hoạt động:
- Khai báo: `#include <assert.h>`
- Sử dụng macro: Có thể sử dụng macro __assert__ để kiểm tra một điều kiện. Nếu điều kiện sai, chương trình sẽ in ra thông báo lỗi và dừng lại
- Biên dịch: Trong môi trường phát triển, __assert__ giúp phát hiện lỗi sớm. Tuy nhiên, khi biên dịch với tuỳ chọn __#NDEBUG__ (vô hiệu hoá chế độ kiểm tra), tất cả câu lệnh __assert__ sẽ bị loại bỏ và không ảnh hưởng đến chương trình
## Bài 3: Pointer
Pointer trong ngôn ngữ C là một kiểu dữ liệu đặc biệt dùng để lưu trữ địa chỉ của một biến khác. Con trỏ cho phép thao tác trực tiếp với bộ nhớ, cung cấp sự linh hoạt và kiểm soát trong lập trình<br>
Các điểm chính về con trỏ:
- Khai báo con trỏ: Để khai báo một con trỏ, sử dụng dấu * trước tên biến. Kiểu dữ liệu của con trỏ phải tương ứng với kiểu dữ liệu của biến mà nó trỏ tới<br>
`int *ptr; // con trỏ kiểu int`<br>
`float *ptr; // con trỏ kiểu float`<br>
`char *ptr; // con trỏ kiểu char`
- Gán địa chỉ: Có thể gán địa chỉ của một biến cho con trỏ bằng toán tử &<br>
`int var = 10;`<br>
`int *ptr = &var; // ptr đang lưu địa chỉ của var`
- Truy cập giá trị: Để truy cập giá trị của biến mà con trỏ trỏ tới, sử dụng toán tử *<br>
`printf("%d", *ptr); // in ra màn hình giá trị của var`
- Thay đổi giá trị thông qua con trỏ: có thể thay đổi giá trị của biến thông qua con trỏ
- __NULL pointer__: con trỏ có thể được khởi tạo với giá trị _NULL_ để chỉ rằng nó không trỏ tới một địa chỉ hợp lệ
- __Void pointer__: là một con trỏ có thể trỏ tới biến có kiểu dữ liệu bất kỳ, việc sử dụng void pointer giúp ta có thể linh hoạt trong việc trỏ tới nhiều biến với nhiều kiểu dữ liệu khác nhau mà không cần khởi tạo nhiều con trỏ<br>
`void *ptr = NULL; // khởi tạo con trỏ void`<br>
`int var = 10;`<br>
`ptr = &var;`<br>
`printf("%d", *((int *)ptr)); // ép kiểu ptr về kiểu int`<br>
Để truy cập giá trị của con trỏ void, cần phải ép kiểu nó về giống với kiểu dữ liệu của biến mà nó trỏ vào
- __Function pointer__: con trỏ hàm cho phép lưu trữ địa chỉ của hàm và gọi hàm thông qua con trỏ. Cho phép truyền hàm như một tham số, xây dựng các bảng chức năng và thực hiện nhiều tác vụ khác<br>
`return_type (*ptr_name)(parameter_types); // khai báo con trỏ hàm`  
- __Pointer to constant__: con trỏ trỏ đến hằng số, là con trỏ có thể thay đổi địa chỉ biến mà nó trỏ vào (có thể trỏ đến biến khác), nhưng không thể thay đổi giá trị của đối tượng mà nó trỏ tới. Hữu ích trong việc bảo vệ dữ liệu khỏi bị thay đổi nhưng vẫn cần khả năng linh hoạt của con trỏ<br>
`const type *ptr_name;`
- __Constant pointer__: con trỏ hằng là một con trỏ mà không thể thay đổi địa chỉ mà nó trỏ đến sau khi khởi tạo. Có nghĩa là không thể gán lại giá trị của con trỏ, nhưng có thể thay đổi giá trị của đối tượng mà nó trỏ tới<br>
`type *const ptr_name;`
- __Pointer to pointer__: là một con trỏ trỏ đến địa chỉ của một con trỏ khác<br>
`int var = 10;`<br>
`int *ptr = &var; // ptr trỏ đến địa chỉ của var`<br>
`int **ptr1 = &ptr; // ptr1 trỏ đến địa chỉ của ptr`<br>
`printf("%d", **ptr1); // in ra giá trị của var thông qua ptr1`
## Bài 4: Memory layout
### Text segment
- Mã máy: chứa tập hợp các lệnh thực thi
- Quyền truy cập: chỉ có quyền đọc và thực thi, không có quyền ghi
- Lưu hằng số, con trỏ kiểu char
- Tất cả các biến lưu ở phân vùng text đều không thể thay đổi giá trị mà chỉ được đọc
### Data segment
- Dữ liệu đã khởi tạo
- Chứa các biến toàn cục đã được khởi tạo với giá trị khác 0
- Chứa các biến static được khởi tạo với giá trị khác 0
- Quyền truy cập là đọc và ghi, tức là có thể đọc và thay đổi giá trị của biến
- Tất cả các biến sẽ được thu hồi sau khi chương trình kết thúc
### Bss segment
- Dữ liệu chưa được khởi tạo
- Chứa các biến toàn cục khởi tạo với giá trị bằng 0 hoặc không gán giá trị
- Chứa các biến static với giá trị bằng 0 hoặc không gán giá trị
- Quyền truy cập là đọc và ghi, tức là có thể đọc và thay đổi giá trị của biến
- Tất cả các biến sẽ được thu hồi sau khi chương trình kết thúc
### Stack segment
- Chứa các biến cục bộ, tham số truyền vào
- Quyền truy cập: đọc và ghi, nghĩa là có thể đọc và thay đổi giá trị của biến trong suốt thời gian chương trình chạy
- Sau khi ra khỏi hàm, sẽ thu hồi vùng nhớ
### Heap segment
- Cấp phát động
- Heap được sử dụng để cấp phát bộ nhớ động trong quá trình thực thi chương trình
- Điều này cho phép chương trình tạo ra và giải phóng bộ nhớ theo nhu cầu, thích ứng với sự biến đổi trong quá trình chạy
- Các hàm malloc(), calloc(), realloc(), free() được sử dụng để cấp phát và giải phóng bộ nhớ trên heap
### Stack và heap
- Stack được dùng để lưu trữ các biến cục bộ trong hàm, tham số truyền vào... Truy cập vào bộ nhớ rất nhanh và được thực thi khi chương trình được biên dịch
- Heap được dùng để lưu trữ vùng nhớ cho những biến được cấp phát động
- Stack được quản lý bởi hệ điều hành, dữ liệu được lưu trong stack sẽ tự động giải phóng khi hàm thực hiện xong chương trình
- Heap được quản lý bởi lập trình viên, chỉ được giải phóng bằng free
## Bài 5:Extern - Static - Volatile - Register
### Extern
Được sử dụng để thông báo rằng một biến hoặc hàm được khai báo ở một nơi khác trong chương trình hoặc trong một file khác. Điều nàu giúp chương trình hiểu rằng biến hoặc hàm đã được định nghĩa và sẽ được sử dụng từ một vị trí khác giúp quản lý sự liên kết giữa các thành phần khác nhau của chương trình hoặc giữa các file nguồn.
### Static
Cục bộ: Khi static được sử dụng với biến cục bộ, nó giữu giá trị của biến qua các lần gọi hàm và giữ phạm vi biến chỉ trong hàm đó.<br>
Toàn cục:
- Khi static được sử dụng với biến toàn cục, nó hạn chế phạm vi của biến đó chỉ trong file nguồn hiện tại
- Ứng dụng: dùng để thiết kế các file thư viện
- Hàm stactic ngăn hàm không thể gọi từ file khác<br>
Trong class: Khi một thành viên của của class được khai báo là static, nó thuộc về class chứ không thuộc về các đối tượng cụ thể của class đó. Các đối tượng của class sẽ chia sẻ cùng một bản sao của thành viên static, và nó có thể được truy cập mà không cần tạo đối tượng. Nó thường được sử dụng để lưu trữ dữ liệu chung của tất cả đối tượng.
### Volatile
Được sử dụng để báo cho trình biên dịch rằng một biến có thể thay đổi ngẫu nhiên, ngoài sự kiểm soát của chương trình. Việc này ngăn chặn trình biên dịch tối ưu hoá hoặc xoá bỏ các thao tác trên biến đó, giữ cho các thao tác trên biến được thực hiện như đã được định nghĩa.
### Register
Được sử dụng để chỉ ra ý muốn của lập trình viên rằng một biến được sử dụng thường xuyên và có thể được lưu trữ trong một thanh ghi chứ không phải bộ nhớ RAM. Việc này giúp tăng tốc độ truy cập. Tuy nhiên, lưu ý rằng việc sử dụng register chỉ là một đề xuất cho trình biên dịch và không đảm bảo rằng biến sẽ được lưu trữ trong thanh ghi. Trong thực tế, trình biên dịch có thể quyết định không tuân thủ lời đề xuất này.
## Bài 6: Goto - Setjmp
### Goto
Là một từ khoá trong ngôn ngữ C, cho phép chương trình nhảy đến một label đã gán trước đó trong cùng một hàm. Mặc dù nó cung cấp khả năng kiểm soát flow của chương trình, nhưng việc sử dụng goto thường được xem là không tốt vì nó có thể làm cho mã nguồn trở nên khó đọc và khó bảo trì.
### Setjmp
Là một thư viện trong ngôn ngữ C, cung cấp hai hàm chính là setjmp và longjmp. Cả hai hàm này thường được sử dụng để thực hiện xử lý ngoại lệ trong C, mặc dù nó không phải là một cách tiêu biểu để xử lý ngoại lệ trong ngôn ngữ C
- __setjmp__: hàm này được sử dụng để lưu trạng thái của ngữ cảnh thực thi (bao gồm con trỏ ngăn xếp, biến, và địa chỉ lệnh tiếp theo) vào một biến __jmp_buf__
- __longjmp__: với cùng một jmp_buf, chương trình sẽ nhảy trở lại vị trí nơi __setjmp__ được gọi, và __setjmp__ sẽ trả về giá trị được truyền cho __longjmp__, thường là giá trị khác 0
### Bài 7: Bitmask
Bitmask là một kỹ thuật được sử dụng để thao tác với từng bit riêng lẻ trong số nguyên. Bitmask thường được sử dụng để tối ưu hóa bộ nhớ, thực hiện các phép toán logic trên một cụm bit, và quản lý các trạng thái, quyền truy cập, hoặc các thuộc tính khác của một đối tượng.<br>
Các toán tử thường sử dụng trong bitmask:
- __NOT__ (~): đảo giá trị của bit
- __AND__ (&): Khi 2 bit được AND với nhau có giá trị bằng 1 thì kết quả sẽ là 1, các trường hợp còn lại sẽ bằng 0 (giống phép nhân).
- __OR__ (|): Khi 2 bit được OR với nhau có giá trị bằng 0 thì kết quả sẽ là 0, các trường hợp còn lại sẽ bằng 1 (giống phép cộng).
- __XOR__ (^): Khi 2 bit được OR với nhau có giá trị bằng nhau thì kết quả sẽ là 0, khác nhau sẽ bằng 1.
- Dịch trái (<<): Di chuyển các bit của biến bên trái toán tử "<<" về bên trái với số lần là giá trị của biến bên phải toán tử "<<". Khi di chuyển, các bit tràn ra khỏi khung dữ liệu sẽ bị loại bỏ và các bit 0 sẽ điền vào các ô trống.
- Dịch phải (>>): Di chuyển các bit của biến bên trái toán tử ">>" về bên phải với số lần là giá trị của biến bên phải toán tử ">>". Khi di chuyển, các bit tràn ra khỏi khung dữ liệu sẽ bị loại bỏ và các bit 0 sẽ điền vào các ô trống (nếu số bị dịch là một số có dấu và có giá trị < 0 thì các bit 1 sẽ điền vào các ô trống).
## Bài 8: STRUCT - UNION
### Struct
Là một cấu trúc dữ liệu cho phép tự định nghĩa một kiểu dữ liệu mới bằng cách nhóm các biến có các kiểu dữ liệu khác nhau lại với nhau, __struct__ cho phép tạo ra một thực thể dữ liệu lớn hơn và có tổ chức hơn từ các member của nó. khi một __struct__ được khai báo, nó sẽ được cấp phát bộ nhớ liên tục cho tất cả các thành viên của nó. Bộ nhớ được cấp phát sẽ có kích thước bằng tổng kích thước của tất cả các thành phần cộng với bất kỳ khoảng trống (padding) nào cần thiết để đảm bảo căn chỉnh bộ nhớ.
### Union
Là một cấu trúc dữ liệu giúp lập trình viên kết hợp nhiều kiểu dữ liệu khác nhau vào cùng một vùng nhớ. Mục đích chính của __union__ là tiết kiệm bộ nhớ bằng cách chia sẻ cùng một vùng nhớ cho các thành viên của nó. Điều này có nghĩa, trong một thời điểm, chỉ một thành viên của __union__ có thể được sử dụng.
## Bài 9: JSON
JSON được thiết kế để dễ đọc và dễ viết cho con người, cũng như dễ dàng để phân tích và tạo ra cho máy tính. Nó sử dụng một cú pháp nhẹ dựa trên cặp key - value, tương tự như các đối tượng và mảng trong javascript. Mỗi đối tượng JSON bao gồm một tập hợp các cặp "key" và "value", trong khi mỗi mảng JSON là một tập hợp các giá trị.
## Bài 10: Linked list
Là một cấu trúc dữ liệu trong lập trình máy tính, được sử dụng để tổ chức và lưu trữ dữ liệu. Một __linked list__ bao gồm một chuỗi các node, mỗi node chứa một giá trị dữ liệu và một con trỏ đến nút tiếp theo trong chuỗi.<br>
Các đặc điểm chính:
- Có thể dễ dàng thay đổi kích thước, tức là có thể thêm hoặc xoá các node mà không cần phải cấp phát lại bộ nhớ cho toàn bộ danh sách
- Không cần cấp phát liên tục. Các node trong __linked list__ không cần phải được lưu trữ tại các địa chỉ bộ nhớ liên tục
## Bài 11: Stack - Queue
### Stack
Là một cấu trúc dữ liệu được xếp theo nguyên tắc LIFO (Last in Firt out), nghĩa là phần từ đầu tiên được đưa vào thì sẽ được lấy ra sau cùng và phần tử được đưa vào cuối cùng sẽ được lấy ra đầu tiên.<br>
Thao tác trên Stack:
- __PUSH__ : Đưa phần tử vào
- __POP__ : Lấy phần tử trên cùng ra
- __TOP__ : Lấy giá trị trên cùng
### Queue
Là một cấu trúc dữ liệu được xếp theo nguyên tắc FIFO (Fast in Firt out), nghĩa là phần từ đầu tiên được thêm vào sẽ được lấy ra đầu tiên.<br>
Thao tác trên Queue:
- __enqueue__: (thêm phần tử vào cuối hàng đợi) ( nếu đã full mà enqueue nữa thì sẽ bị Stack overflow )
- __dequeue__: (lấy phần tử từ đầu hàng đợi). ( nếu ko có phần tử nào trong mảng đó thì khi dequeue thì sẽ báo lỗi )
- __front__: để lấy giá trị của phần tử đứng đầu hàng đợi.
# C++
## Bài 1: Class
Là một cấu trúc dùng để định nghĩa một kiểu dữ liệu tuỳ chỉnh, cho phép nhóm các thuộc tính (data member) và phương thức (member function) lại với nhau. Đây là khái niệm cơ bản trong lập trình OOP, giúp tạo ra các đối tượng (object) với các đặc tính và hành vi riêng.<br>
Các thành phần chính:
- Thuộc tính (data member): các biến thuộc class, mô tả trạng thái của đối tượng
- Phương thức (member function): các hàm thuộc class, mô tả hành vi của đối tượng
- Phạm vi truy cập: quy địng mức độ truy cập vào các thành viên của class, bao gồm __public__, __protected__, __private__
- Constructor: sẽ tự động được khởi chạy khi khởi tạo object, set up các tham số ban đầu cho object đó. Khi khởi tạo một object trong 1 hàm, bản chất của nó sẽ tương tự như một biến trong C và lưu ở vùng nhớ trên bộ nhớ stack
- Destructor: trước khi vùng nhớ trên bộ nhớ stack được thu hồi sẽ tự khởi chạy __destructor__
## Bài 2: OOP
### Tính đóng gói (encapsulation)
Cho phép ẩn giấu dữ liệu bên trong một đối tượng và chỉ cho phép truy cập và thay đổi dữ liệu thông qua các phương thức công khai. Điều này không chỉ bảo vệ dữ liệu mà còn giúp kiểm soát cách thức mà dữ liệu đó được sử dụng.<br>
Lợi ích:
- Bảo mật: bằng cách ẩn giấu dữ liệu, giảm thiểu rủi ro từ việc sửa đổi không mong muốn từ bên ngoài. Các thuộc tính private không thể bị truy cập trực tiếp từ bên ngoài class
- Kiểm soát: có thể thêm logic vào các phương thức getter và setter để kiểm tra giá trị trước khi cho phép thay đổi
- Dễ bảo trì: khi thay đổi cách mà dữ liệu được lưu trữ bên trong lớp, không cần phải thay đổi mã nguồn ở phần khác trong chương trình, miễn là giao diện công khai không thay đổi
### Tính kế thừa (inheritance)
Cho phép một lớp con kế thừa thuộc tính và phương thức từ lớp cha.<br>
Các loại kế thừa:
- Kế thừa đơn: một lớp con kế thừa từ một lớp cha duy nhất. Đây là kiểu kế thừa đơn giản nhất
- Kế thừa đa cấp: lớp con có thể trở thành lớp cha cho lớp khác, tạo thành một chuỗi kế thừa
- Kế thừa đa hình: một lớp cso thể kế thừa từ nhiều lớp cha
- Kế thừa ảo: khi một lớp con kế thừa từ nhiều lớp cha, có thể xảy ra tình trạng các lớp cha có cùng thuộc tính, phương thức. Kế thừa ảo được sử dụng để giải quyết tình trạng này.
Ghi đè phương thức: khi lớp con có phương thức cùng tên với phương thức trong lớp cha, có thể ghi đè phương thức đó. Để cho phép ghi đè, phương thức trong lớp cha cần phải được khai báo virtual.
### Tính đa hình (polymorphism)
Là một trong những đặc điểm quan trọng của __OOP__. Cho phép các đối tượng khác nhau phản hồi theo những cách khác nhau đối với cùng một phương thức, dựa trên kiểu của đối tượng. Đa hình giúp tăng cường tính linh hoạt và mở rộng của mã nguồn.<br>
Các loại đa hình:
- Compiler: được gọi là đa hình biên dịch, xảy ra khi quyết định gọi phương thức được thực hiện tại thời điểm biên dịch. Hai kỹ thuật phổ biến cho compiler:
  - Method overloading: nhiều phương thức có cùng tên nhưng khác tham số (số lượng hoặc kiểu tham số)
  - Operator overloading: cho phép định nghĩa cách mà các toán tử hoạt động trên các đối tượng tuỳ chỉnh
- Run-time: xảy ra khi quyết định gọi phương thức được thực hiện tại thời điểm chạy chương trình. Thường được thực hiện thông qua kế thừa và __virtual method__. __Virtual method__: khi một phương thức trong lớp cha được khai báo là __virtual__, các lớp có thể ghi đè lên nó. Khi gọi phương thức này thông qua một con trỏ hoặc tham chiếu của lớp cha, phương thức của lớp con sẽ được thực hiện
### Tính trừu tượng (Abstract)
Cho phép làm việc với các khái niệm phức tạp bằng cách chỉ tập trung vào các thuộc tính và hành vi cần thiết, trong khi ẩn giấu các chi tiết không cần thiết. Tính trừu tượng giúp đơn giản hoá việc phát triển và quản lý phần mềm. Cho phép tạo ra các lớp mà chỉ định các phương thức mà không cần cung cấp cách thực hiện ngay lập tức.
## Bài 3: Standard template library C
__STL__ - Standard Template Library là một thư viện trong ngôn ngữ lập trình C++ cung cấp một số tập hợp các template classes và function để thực hiện các cấu trúc dữ liệu và một số thuật toán phổ biến. Một số thành phần chính của STL: Container Iterator Algorithms Funtors Container là một cấu trúc dữ liệu chứa nhiều phần tử theo một cách cụ thể.<br>
Một số container tiêu biểu:
- __Vector__
- __Map__
- __List__
- __Array__
- __Vector__
__Iterator__: là một khái niệm giúp truy cập các phần tử của một container, một cách tuần tự mà không cần phải biết cấu trúc nội bộ của container. Nó đóng vai trò như một con trỏ, nhưng mạnh mẽ và an toàn hơn. Iterator giúp dễ dàng duyệt qua và thao tác với các phần tử trong container một cách linh hoạt bằng cách dùng các method như __begin()__, __end()__ và các phép toán tử để duyệt qua
## Bài 4: Template - Lambda
### Template
Trong C++, __template__ là một tính năng cho phép bạn viết mã tổng quát, giúp tạo ra các hàm và lớp có thể hoạt động với nhiều kiểu dữ liệu khác nhau mà không cần phải viết mã riêng cho mỗi kiểu. Điều này rất hữu ích trong việc tối ưu hóa mã nguồn và tái sử dụng.
- __Function Templates__: Cho phép bạn định nghĩa một hàm tổng quát mà có thể nhận các kiểu dữ liệu khác nhau
- __Class Templates__: Cho phép bạn định nghĩa một lớp tổng quát
### Lambda
Là một cách để định nghĩa các hàm ẩn danh (anonymous functions) mà không cần phải khai báo tên hàm. __Lambda__ thường được sử dụng khi bạn cần một hàm tạm thời cho một tác vụ cụ thể, như trong các thuật toán __STL__ hoặc các callback.
## Bài 5: Smart pointer
Là một cơ chế quản lý bộ nhớ tự động, tự động giải phóng tài nguyên khi không còn sử dụng. Sử dụng đặc tính destructor trong class để tự động giải phóng khi không dùng nữa.<br>
Có 3 loại: __unique pointer__, __shared pointer__, __weak pointer__.
- __Unique pointer__: 1 vùng nhớ chỉ được phép có 1 con trỏ trỏ tới. Sẽ tự động thu hồi vùng nhớ khi pointer bị huỷ. Có thể chuyển quyền sở hữu vùng nhớ qua con trỏ khác
- __Shared pointer__: 1 vùng nhớ có thể có nhiều con trỏ trỏ tới. Sẽ có 1 biến count để theo dõi số pointer trỏ tới vùng nhớ đó. Nếu count = 0 thì vùng nhớ sẽ được thu hồi
- __Weak pointer__: sử dụng chung với __shared pointer__, chỉ có thể giám sát vùng nhớ mà nó trỏ vào. Không thể tác động lên vùng nhớ đó
## Bài 6: Design pattern
### Singleton
Đảm bảo rằng một class chỉ có một thể hiện duy nhất và cung cấp một điểm truy cập toàn cục dẫn đến thể hiện đó. VD: truy cập tới vùng địa chỉ của GPIO thì địa chỉ của GPIO là cố định Nếu khởi tạo nhiều đối tượng để truy cập GPIO, mỗi đối tượng sẽ chiếm một vùng nhớ khác nhau nhưng đều trỏ tới cùng địa chỉ GPIO, gây lãng phí bộ singleton khởi tạo 1 lần, những thằng khác chỉ là con trỏ trỏ tới địa chỉ của object, giúp tối ưu bộ nhớ, tránh khởi tạo nhiều object
### Observer
Cho phép một đối tượng (subject hay publisher) thông báo cho nhiều đối tượng khác (observer hay subcribers) về các thay đổi trạng thái của nó mà không cần biết rõ về chúng.
### Factory
Khởi tạo 1 object mà lớp con sẽ quyết định loại đối tượng nào.
### Decorator
Cho phép thêm các hành vi mới cho các đối tượng mà không cần thay đổi mã nguồn của lớp đó. Điều này giúp tăng cường khả năng mở rộng và linh hoạt cho các lớp đang làm việc.
## Bài 7: Thread
### Thread: 
là một đơn vị thực thi trong một quá trình (process). Mỗi process có không gian riêng cho stack, nhưng chúng chia sẻ bộ nhớ heap và các tài nguyên khác của quá trình.
### Process: 
là chương trình máy tính, được khởi chạy và nạp vào RAM. Process có thể có nhiều thread chạy song song với nhau.<br>
Trong môi trường đa luồng sẽ có các vấn đề về truy cập tài nguyên chung giữa các luồng thực thi (race condition). Do đó, việc sử dụng các phương pháp như __mutex__, __lock__, __condition_variable__, __atomic__ để giải quyết.<br>
#### Mutex
- Mutex đảm bảo rằng chỉ một luồng có thể truy cập vào tài nguyên chia sẻ tại một thời điểm. Điều này giúp tránh tình trạng race condition, nơi dữ liệu có thể bị thay đổi không đồng bộ giữa các luồng
- Khi một luồng muốn truy cập tài nguyên chia sẻ, nó sẽ lock mutex. Nếu __mutex__ đã bị khoá bởi một luồng khác, luồng đó sẽ phải đợi cho đến khi __mutex__ được giải phóng trước khi có thể tiếp tục<br>
#### Lock
- __Lock_guard__: được dùng để quản lý __mutex__, tự động quản lý việc khoá và mở khoá __mutex__, giảm thiểu nguy cơ phát sinh lỗi khi lập trình đa luồng
- __Unique_guard__: được dùng để quản lý __mutex__, nhưng cung cấp nhiều tính năng hơn. Có thể khoá và giải phóng linh hoạt, hỗ trợ time-lock<br>
#### Condition_variable
Cho phép một hoặc nhiều luồng chờ đợi cho một điều kiện cụ thể xảy ra. Điều này rất hữu ích khi bạn muốn quản lý sự đồng bộ giữa các luồng mà không cần khoá liên tục, điều này có thể gây ra lãng phí tài nguyên.<br>
Khái niệm:
- Condition variable: là một đối tượng cho phép luồng này đợi cho đến khi một điều kiện cụ thể được thoả mãn (thường được kiểm tra thông qua một biến chia sẻ)
- Synchronized waiting: luồng có thể "ngủ" cho đến khi điều kiện được đáp ứng, sau đó tiếp tục mà không lãng phí CPU
#### Atomic
Atomic trong C++ đề cập đến một loại biến hoặc phép toán mà có thể được thực hiện một cách an toàn trong môi trường đa luồng mà không cần sử dụng __mutex__. Điều này có nghĩa là các phép toán trên biến __atomic__ sẽ không bị gián đoạn bởi các luồng khác, giúp tránh được tình trạng race condition.<br>
## Bài 8: Bất đồng bộ
Khi __thread__ mất nhiều thời gian và chương trình không chờ đợi, thì bất đồng bộ sẽ dùng để lấy giá trị khi __thread__ xử lý xong dữ liệu.<br>
### Future
Cho phép quản lý và truy cập kết quả của một tác vụ bất đồng bộ. Nó cung cấp một cách an toàn để lấy giá trị từ một tác vụ trong luồng khác mà không cần quản lý luồng một cách thủ công.<br>
Các điểm quan trọng:
- Tạo future: có thể tạo một đối tượng future từ hàm bất đồng bộ, thường là thông qua `std::async`. Điều này cho phép thực hiện một tác vụ trong một luồng riêng biệt và lấy kết quả sau đó
- Trạng thái: một đối tượng __future__ có thể có các trạng thái khác nhau<br>
  Not ready: tác vụ vẫn đang chạy hoặc chưa bắt đầu
  Ready: tác vụ đã hoàn thành và có thể lấy kết quả
  Exception: tác vụ gặp lỗi và có thể lấy lỗi từ __future__
- Phương thức: __get()__, __wait()__, __valid()__
### Shared_future
Cho phép nhiều luồng chia sẻ cùng một kết quả từ một tác vụ bất đồng bộ. Điều này có nghĩa là có thể lấy giá trị từ __shared_future__ mà không cần lo lắng về việc kết quả đã được lấy hay chưa.<br>
Các điểm quan trọng:
- Chia sẻ kết quả: cho phép nhiều luồng truy cập cùng một kết quả mà không làm mất giá trị của nó. Có thể tạo một __shared_future__ từ một __future__ và sau đó nhiều luồng có thể gọi __get()__ để lấy kết quả
- Kết quả không bị tính toán lại
- __Shared_future__ có các phương thức tương tự như __future__

