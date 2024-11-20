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


