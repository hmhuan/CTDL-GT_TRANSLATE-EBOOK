# Phần III - Cấu trúc dữ liệu

## Giới thiệu

Tập hợp là những thứ cơ bản trong cả khoa học máy tính lẫn toán học. Trong khi tập hợp toán học là bất biến, thì tập hợp trong giải thuật có thể bị tinh chỉnh như tăng lên, giảm xuống hay nói cách khác tập hợp. Ta gọi đó là các tập hợp động. Năm chương tiếp theo trình bày các kỹ thuật cơ bản để thể hiện các tập hợp động hữu hạn và thao tác với chúng trên máy tính.

Những giải thuật có thể đòi hỏi một vài loại thao tác khác nhau được thực hiện trên các tập hợp tương ứng. Thỉ dụ, nhiều giải thuật chỉ cần có khả năng chèn các phần tử vào, xóa các phần tử và kiểm tra tính liên quan giữa các phần tử trong tập hợp. Ta gọi một tập hợp động hỗ trợ các thao tác như vậy là một từ điển (dictionary). Những giải thuật khác đòi hỏi các thao tác phức tạp hơn. Ví dụ như cấu trúc hàng đợi ưu tiên cực tiểu (min-priority queues) sẽ được giới thiệu trong chương 6 trong nội dung của mục cấu trúc dữ liệu đống (heap), hỗ trợ các thao tác như chèn một phần tử và trích ra phần tử nhỏ nhất từ tập hợp. Cách tốt nhất để cài đặt một tập hợp động phụ thuộc vào các thao tác mà tập hợp đó sẽ được sử dụng.

## Các phần tử trong một tập hợp

Trong một triển khai điển hình của một tập động, mỗi phần tử được thể hiện bởi một đối tượng có các thuộc tính được kiểm tra và tinh chỉnh nếu ta có con trỏ đến đối tượng đó, (Mục 10.3 sẽ thảo luận thêm về cách triển khai những đối tượng và con trỏ trong môi trường lập trình mà không chứa chúng như là các kiểu dữ liệu cơ bản). Một vài loại tập hợp động giả sử rằng một trong các thuộc tính của đối tượng là một khóa định danh. Nếu tất cả các khóa đều phân biệt, ta có thể nghĩ rằng tập hợp động như là một tập hợp khóa giá trị. Đối tượng có thể chứa dữ liệu “vệ tinh” (satellite data), mang lại những thuộc tính đối tượng khác mà không được sử dụng trong triển khai tập hợp. Nó cũng có thể chứa các thuộc tính được điều khiển bởi các thao tác trên tập hợp; Các thuộc tính đó có thể chứa dữ liệu hay con trỏ đến đối tượng khác trong tập hợp.

Một vài loại tập hợp động mà có các khóa được rút ra từ tập hợp có thứ tự hoàn toàn, như là các số thực, hay tập các từ theo thứ tự từ điển trong bảng chữ cái thông thường. Ví dụ như một thứ tự đầy đủ cho phép ta xác định được phần tử nhỏ nhất trong tập hợp, hay chọn được phần tử tiếp theo lớn hơn một phần tử cho trước trong tập hợp.

## Các thao tác trên các tập động

Các thao tác trên tập động có thể được nhóm thành 2 loại: truy vấn, trả về các thông tin về tập hợp, và thao tác chỉnh sửa, thay đổi trên tập hợp. Dưới đây là danh sách các thao tác điển hình. Bất cứ ứng dụng cụ thể nào đều thường sẽ cần cài đặt một vài thao tác dưới đây.

### SEARCH(S, k)

    Một truy vấn, cho một tập S và một khóa giá trị là k, trả về con trỏ x đối với phần tử tương ứng trong tập S sao cho x.key = k, hoặc NIL nếu không tồn tại phần tử như vậy trong S.

### INSERT(S, x)

    Một phép chỉnh sửa làm tăng kích thước tập S lên với phần tử trỏ tới x. Ta luôn giả sử rằng các thuộc tính của phần tử x đều đã được khởi tạo.

### DELETE(S, x)

    Một phép chỉnh sửa mà, với một con trỏ x đến một phần tử trong tập S, xóa x trong S. (Lưu ý rằng thao tác này nhận đối số là một con trỏ đến phần tử x, không phải một giá trị khóa.)

### MINIMUM(S)

    Một truy vấn trên toàn bộ tập có thứ tự S để trả về một phần tử trong S có khóa là lớn nhất

### MAXIMUM(S)

    Một truy vấn trên toàn bộ tập có thứ tự S để trả về một phần tử trong S có khóa là lớn nhất.

### SUCCESSOR(S, x)

    Một truy vấn mà, cho trước một phần tử x có khóa từ một tập hợp có thứ tự S, trả về một con trỏ đến phần tử lớn hơn kế tiếp trong S hay là NIL nếu x là phần tử cực đại. 

### PREDECESSOR(S, x)

    Một truy vấn mà, cho trước một phần tử x có khóa từ một tập hợp có thứ tự S, trả về một con trỏ đến phần tử nhỏ hơn kế tiếp trong S hay là NIL nếu x là phần tử cực tiểu.

Trong nhiều trường hợp, ta có thể mở rộng các câu truy vấn SUCCESSOR và PREDECESSOR sao cho chúng áp dụng được trên các tập có khóa không phân biệt. Trong một tập có n khóa, thông thường giả định là một lệnh gọi đến MINIMUM theo sau là n - 1 lệnh gọi tới SUCCESSOR liệt kê các phần tử trong tập hợp theo thứ tự được sắp xếp.

Ta thường đo thời gian thực thi của một thao tác trên tập hợp dựa trên kích thước của tập hợp. Thí dụ, như chương 13 mô tả một cấu trúc dữ liệu mà có thể hỗ trợ bất kỳ thao tác nào được liệt kê ở trên với một tập có kích thước n trong thời gian O(lg n).

## Tổng quan phần III

Các chương từ **10 - 14** mô tả các cấu trúc dữ liệu ta có thể sử dụng để cài đặt tập hợp động; ta sẽ sử dụng nhiều trong số chúng sau này để xây dựng các giải thuật hiệu quả với nhiều bài toán. Ta đã thấy được một cấu trúc dữ liệu quan trọng khác - cấu trúc đống (heap) - trong chương 6.

**Chương 10** trình bày những điều cơ bản khi làm việc với các cấu trúc dữ liệu đơn giản như hàng đợi, ngăn xếp, danh sách liên kết và cây có gốc. Chương này cũng sẽ trình bày cách cài đặt các đối tượng và con trỏ trong môi trường lập trình mà không hỗ trợ chúng ở mức mặc định. Nếu bạn đã từng tham gia một khóa giới thiệu về lập trình, thì nhiều truy vấn trên toàn bộ tập có thứ tự S để trả về một phần tử trong S có khóa là nhỏ nhất.

**Chương 11** giới thiệu về bảng băm (hash table), cấu trúc dữ liệu hỗ trợ các thao tác từ điển (dictionary operations) INSERT, DELETE và SEARCH. Trong trường hợp tệ nhất, truy vấn băm tốn O(n) thời gian với mỗi thao tác SEARCH, nhưng 

Cây nhị phân tìm kiếm, được gói gọn trong **chương 12**, hỗ trợ tất cả các thao tác trên tập động đã được liệt kê ở bên trên. Trong trường hợp tệ nhất, mỗi thao tác tốn O(n) time với cây có n phần tử, nhưng đối với một cây nhị phân tìm kiếm được xây dựng ngẫu nhiên, thời gian mong đợi với mỗi thao tác là O(lg n). Cây tìm kiếm nhị phân làm cơ sở cho nhiều cấu trúc dữ liệu khác.

**Chương 13** giới thiệu về cây đỏ-đen là một biến thể của cây tìm kiếm nhị phân. Không giống như cây tìm kiếm nhị phân thông thường, cây đỏ-đen đảm bảo thực thi tốt các tác vụ với thời gian O(lg n) trong cả trường hợp tệ nhất. Một cây đỏ-đen là một cây tìm kiếm cân bằng; chương 18 trong phần V sẽ trình bày một loại cây tìm kiếm cân bằng khác, được gọi là B-cây. Mặc dù cơ chế của cây đỏ-đen có phần hơi phức tạp, bạn có thể thu thập các tính chất từ chúng ở chương này mà không cần nghiên cứu chi tiết về cơ chế của nó.  

Trong **chương 14**, chúng tôi đưa ra cách tăng cường cây đỏ-đen để hỗ trợ các thao tác khác ngoài các thao tác đã liệt kê bên trên. Trước tiên, Chúng tôi tăng cường chúng sao cho ta có thể duy trì linh động các thống kê có thứ tự với một tập hợp khóa. Sau đó, chúng tôi tăng cường chúng theo một cách khác để duy trì các khoảng số thực.
