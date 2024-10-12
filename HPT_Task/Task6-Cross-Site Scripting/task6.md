![image](https://github.com/user-attachments/assets/1b11a4c3-88f2-4332-a658-fb919fed6693)# Cross-Site Scripting
>Tên tài liệu: Cross-Site Scripting<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 11/10/2024
>
# Mục Lục
[1. Khái niệm ](#p1) <br>
[2. Cách thức tìm kiếm và khai thác ](#p2) <br>
[3. Lab ](#p3) <br>

# Nội dung
<a id="p1"></a>
## 1. Khái niệm và các kiểu lỗi XSS
**XSS** là một lỗ hổng bảo mật cho phép kẻ tấn công thực hiện các đoạn mã Javascript độc hại. Thường thì kẻ tấn công sẽ đánh cắp cookie qua lỗ hổng này và truy cập, xâm phạm dữ liệu của người dùng hoặc tổ chức. Nguy hiểm hơn kẻ tấn công sẽ deface toàn bộ trang web nạn nhân, chỉnh sửa các chức năng, đưa mã độc vào. <br>
**XSS** hoạt động khi kẻ tấn công thao túng một trang web yếu, dễ bị tấn công bằng đoạn mã Javascript độc hại.
Có ba loại **XSS** chính:
- Reflected XSS: xảy ra trên yêu cầu HTTP. Ví dụ: các tham số trên url, ...
- Stored XSS: xảy ra khi ta truy cập, click vào. Ví dụ: click vào chức năng, load lại trang, ...
- DOM-based XSS: lỗ hổng tồn tại phía máy khách. Ví dụ: thay đổi DOM trong trình duyệt để thực thi lệnh.
<a id="p2"></a>
## 2. Cách thức tìm kiếm và khai thác
**Stored XSS** <br>
Tìm kiếm các điểm nhập liệu cho phép người dùng gửi và lưu trữ dữ liệu trên server, như form đăng ký, bình luận, phần mô tả sản phẩm, hoặc hồ sơ người dùng. <br>
**Reflected XSS** <br>
Tìm kiếm các tham số URL hoặc các trường nhập liệu mà khi gửi dữ liệu, kết quả được phản chiếu lại trên giao diện trang mà không xử lý đúng cách. <br>
**DOM-based XSS** <br>
- Phân tích mã JavaScript của trang web để xác định các đoạn mã xử lý dữ liệu từ URL, cookie, hoặc các input khác mà không kiểm tra đúng cách.
- Kiểm tra các phương thức như document.write(), innerHTML, eval(), và các phương thức có khả năng thay đổi DOM.
Test XSS bằng cách dùng các payload `<script>alert('XSS')</script>`
Một số Tool:
XSSTrike, https://github.com/s0md3v/XSStrike
- Dalfox, https://github.com/hahwul/dalfox
- XSS Hunter, https://github.com/mandatoryprogrammer/xsshunter
- https://github.com/mandatoryprogrammer/xsshunter-express
- https://xsshunter.trufflesecurity.com/
<a id="p3"></a>
## 3. Lab
### 3.1 Basic Reflected
![image](https://github.com/user-attachments/assets/336340e0-68da-4597-8857-054d57b67f1c) <br>
Trang web có chức năng search tiến hành thử search <br>
![image](https://github.com/user-attachments/assets/65dabbbf-acee-4e03-9753-66574ec7f82c) <br>
Check source code để hiểu hơn về chức năng này <br>
![image](https://github.com/user-attachments/assets/d5355ca5-09eb-4a7b-98e3-d3b51560d25f) <br>
Untrusted data nằm ở `$_GET['q']` và khi giá trị từ tham số q trong URL được lấy từ người dùng và hiển thị lại trên trang web mà không qua kiểm tra hoặc mã hóa.
Payload:
```
<script>alert('XSS')</script>
```
![image](https://github.com/user-attachments/assets/2150824c-9306-4db8-81af-da4ce5dc57f7)
### 3.2 Stored Message
Tiến hành login với user pass đã được cho <br>
![image](https://github.com/user-attachments/assets/ed20ed48-d75c-45df-bc91-a39ac1cf7087) <br>
Trang web có chức năng send Message :
![image](https://github.com/user-attachments/assets/ef9f0cd7-a664-4137-8ef3-347081c884ee) <br>
Check source code để xem:
![image](https://github.com/user-attachments/assets/06506d4a-3c2f-46ec-9354-905eec9f7a41)
Untrusted data ($_POST['mes']) được chèn vào cơ sở dữ liệu mà không qua bất kỳ kiểm tra hoặc mã hóa nào, sau đó được hiển thị trực tiếp trên trang mà không qua mã hóa đầu ra (output encoding). Điều này cho phép người dùng chèn mã JavaScript độc hại vào nội dung tin nhắn và mã này sẽ được thực thi khi nội dung được hiển thị.
Payload:
```
<script>alert('XSS')</script>
```
![image](https://github.com/user-attachments/assets/dc407d91-e56b-4d56-83c6-db9f339426ae) 
### 3.3 Basic Dom-Based
Trang web có chức năng tìm diện tích của 1 hình tam giác bằng cách nhập vào Height và Base <br>
![image](https://github.com/user-attachments/assets/3e46366e-d1ef-4ceb-bd40-5dc7e687087b)
Check source code
![image](https://github.com/user-attachments/assets/dcd7be78-84e4-4374-b985-03642f95e9d3)
Untrusted data trong đoạn mã này là các giá trị từ $_GET['base'] và $_GET['height'], chúng được sử dụng trực tiếp trong mã JavaScript mà không qua escaping: <br>
```
echo 'var height = '.$_GET['height'].';';
echo 'var base = '.$_GET['base'].';';
```
Có thể thấy thuộc tính innerHTML rất dễ bị XSS nếu không xử lý đúng cách, ở đây chúng ta có thể control được `$strings['alert']` và trigger XSS.

Final payload: 
```
;alert("xss")
```
![image](https://github.com/user-attachments/assets/f451c5bc-1c7c-4ff6-8b85-1904aea96048)
![image](https://github.com/user-attachments/assets/f35a654a-e7ee-4340-be02-405c4682c6cc)
### 3.4 HTML Attribute Manipulation
Tổng quan trang web là nơi bán ve phim Mandalorian bằng cách nhập tên vào và get the ticker
![image](https://github.com/user-attachments/assets/5a3b542b-3ad3-45ad-bba4-c12d0d816c80)
![image](https://github.com/user-attachments/assets/be43c6b1-9182-44b3-89a6-e302cb8a0600)
Check source code:
![image](https://github.com/user-attachments/assets/af26d98f-1e8e-4111-b727-a5a198e27307)
Untrusted data từ tham số name có thể chứa các ký tự đặc biệt hoặc mã độc hại, và nếu hàm encodeB() không thực hiện mã hóa đúng cách, dữ liệu đó có thể được đưa vào HTML mà không được escaping. Điều này cho phép kẻ tấn công đưa mã JavaScript hoặc HTML vào tham số name để thực thi mã độc.
Payload:
```
"onmouseover="alert(document.domain)"
```






