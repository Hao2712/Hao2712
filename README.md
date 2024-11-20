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
