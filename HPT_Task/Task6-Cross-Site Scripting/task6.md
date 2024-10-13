![image](https://github.com/user-attachments/assets/1b11a4c3-88f2-4332-a658-fb919fed6693)# Cross-Site Scripting
>Tên tài liệu: Cross-Site Scripting<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 11/10/2024
>
# Mục Lục
[1. Khái niệm ](#p1) <br>
[2. Cách thức tìm kiếm và khai thác ](#p2) <br>
[3. Lab ](#p3) <br>
[4. Recommendations](#p4)

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
Untrusted data từ tham số name có thể chứa các ký tự đặc biệt hoặc mã độc hại, và nếu hàm encodeB() không thực hiện mã hóa đúng cách, dữ liệu đó có thể được đưa vào HTML mà không được escaping. Điều này cho phép kẻ tấn công đưa mã JavaScript hoặc HTML vào tham số name để thực thi mã độc. <br>
Input của chúng ta ta được đưa vào attribute href của tag <a>. <br>
Payload:
```
"onmouseover="alert("xss")"
```
### 3.5 Welcome to Our Exhibition
![image](https://github.com/user-attachments/assets/f219aa61-9485-49e0-aa71-3911255c54e4)
Là trang web triển lãm ảnh khi chọn 1 tấm ảnh thì url sẽ là :`http://192.168.106.131:1337/lab/xss/our-gallery/?img=1#` <br>
Check source code <br>
![image](https://github.com/user-attachments/assets/3be6eae7-f2c4-4c00-85d4-a7636a7b36d5)
Untrusted data ($_GET['img']) được đưa trực tiếp vào thuộc tính src của thẻ <img> mà không qua bước xử lý phù hợp. Mặc dù hàm encodeB() có thay thế các ký tự < và > bằng giá trị được mã hóa URL (%3C và %3E), nhưng hàm này không đủ để ngăn chặn các cuộc tấn công XSS khác nếu kẻ tấn công chèn nội dung JavaScript độc hại. <br>
Payload:
```
1" onerror="alert('XSS')
```
![image](https://github.com/user-attachments/assets/ac20426a-50b3-4e4b-a180-d40bace4df46)
### 3.6 User Agent
Tiến hành login với user và password đã được cung cấp
![image](https://github.com/user-attachments/assets/299ea369-3ab3-49e9-bffc-19bc40f4d000)
![image](https://github.com/user-attachments/assets/1a7b339f-f5b4-4ec5-9eb1-7e1ba7c842ff)
Có thể thấy đây là trang web để admin có thể xem user agent của người dùng. <br>
![image](https://github.com/user-attachments/assets/75b5733c-a107-4d00-b923-17269f2c4dc3)
Check source code thì thấy Untrusted data đến từ cơ sở dữ liệu, cụ thể là giá trị useragent được lấy từ bảng user_agent. Khi dữ liệu này được đưa vào HTML mà không được mã hóa, có khả năng xảy ra lỗ hổng XSS.
```
echo '<td>' . $cikti['useragent'] . '</td>';
```
Dùng burpsuite để bắt request <br> 
Và chèn payload vào trường User-Agent: <br>
Payload: `<script>alert("xss")</script>
![image](https://github.com/user-attachments/assets/b1a78287-9f45-4079-9f68-3c67db4d4d07)
![image](https://github.com/user-attachments/assets/f546cb33-536a-4f42-8a7e-19682aa769b3)
### 3.7 New
Trang web thêm tin tức <br>
![image](https://github.com/user-attachments/assets/174b7dcb-6650-46c4-80d8-55cf004d77f7)
Check source code  thì thấy Untrusted data đến từ cơ sở dữ liệu, cụ thể là giá trị title và link trong bảng links. Dữ liệu này được lấy từ cơ sở dữ liệu và hiển thị lên trang web trong các thẻ HTML <a> mà không qua bước mã hóa hay kiểm tra kỹ. <br>
![image](https://github.com/user-attachments/assets/37c212cd-dcee-4ada-84ab-32af6e4a9cad) <br>
Payload:
```
javascript:alert("xss")
```
![image](https://github.com/user-attachments/assets/11a96f78-7a8c-4d07-b27a-070c8b689500)
### 3.8 File Upload
![image](https://github.com/user-attachments/assets/6939cc8d-ecee-443b-9535-7aa21d8758ca)
Là trang web cho phép chúng ta upload ảnh để thay đổi ảnh profile. <br>
Check qua source code : <br>
![image](https://github.com/user-attachments/assets/5553f68c-9abb-4305-b041-16fba7c9e49a)
Biến $_FILES["image"]["name"] có thể bị thao túng nếu không kiểm soát chặt chẽ tên của file được upload lên. <br>
Vậy câu hỏi đặt ra là: Nếu chúng ta đặt tên của file là một đoạn javascript thì chuyện gì sẽ xảy ra ??? <br>
Ví dụ tam.png => "><script>alert("xss")</script>.png <br>
Ta sẽ encode nó như này : `%22%3e%3c%73%63%72%69%70%74%3e%61%6c%65%72%74%28%31%29%3c%2f%73%63%72%69%70%74%3e.png` và up lên <br>
![image](https://github.com/user-attachments/assets/2bb86d73-76ad-4b2f-91a6-62fdbc96d976)
### 3.9 DOM XSS in document.write sink using source location.search
Lab này chứa lỗ hổng  [DOM-based cross-site scripting](https://portswigger.net/web-security/cross-site-scripting/dom-based)  trong chức năng search . Nó sử dụng hàm `document.write` của JavaScript để ghi dữ liệu ra trang. <br>
Mục tiêu của bài lab này là thực hiện tấn công Cross-site scripting và gọi hàm `alert`
`document.write` có chức năng call data từ `location.search` cái mà bạn có thể kiểm soát bằng cách sử dụng URL website <br>
![image](https://github.com/user-attachments/assets/77d42020-993c-4843-b78e-f13ae066a38c)
Check bằng dev-tools thì thấy chuỗi nhập vào được set bên trong attribute img src <br>
Payload: <br>
```
"><svg onload=alert(1)>
```
![image](https://github.com/user-attachments/assets/ee28ff3a-34e2-4e04-9aa1-a80f175872e8)
### 3.10 DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded
Lab liên quan đến một lỗ hổng **DOM-based XSS** trong ứng dụng web sử dụng **`AngularJS`**, một framework JavaScript phổ biến <br>
- **`AngularJS`** là một framework JavaScript giúp phát triển các ứng dụng web tương tác. Nó sử dụng một cơ chế gọi là **`directive`** (chỉ thị), với cú pháp trong dấu ngoặc kép đôi (`{{}}`), cho phép chèn và xử lý các biểu thức JavaScript bên trong HTML.
- **`ng-app`** là một chỉ thị của AngularJS, cho phép AngularJS quản lý và xử lý các phần tử bên trong một ứng dụng.
Mục tiêu là khai thác lỗ hổng để thực thi một biểu thức AngularJS và gọi hàm `alert()` trong trình duyệt của người dùng. <br>
Payload : <br>
```
{{$watch.constructor('alert(1)')()}}
```
![image](https://github.com/user-attachments/assets/2dd4f8fe-82d6-4e67-9a77-bce03b23c8a6)
![image](https://github.com/user-attachments/assets/1af8ff73-3277-4dae-be7b-0889a3b6dfb7)
<a id="p4"></a>
## 4. Recommendations
1. Sử dụng các biện pháp mã hóa đầu vào người dùng để ngăn chặn mã độc từ XSS.
2. Áp dụng cơ chế lọc và kiểm tra đầu vào của người dùng, đảm bảo rằng các ký tự đặc biệt được xử lý đúng cách.
3. Sử dụng Content Security Policy (CSP) để hạn chế các nguồn tài nguyên mà trình duyệt có thể tải và thực thi.
4. Triển khai cơ chế xác thực mạnh mẽ, chẳng hạn như xác thực hai yếu tố (2FA), để bảo vệ tài khoản admin.
5. Thực hiện kiểm tra bảo mật định kỳ để phát hiện và khắc phục các lỗ hổng bảo mật sớm nhất có thể.









