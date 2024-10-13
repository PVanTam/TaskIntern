# Insecure direct object references (IDOR)
>Tên tài liệu: Insecure direct object references (IDOR)<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 13/10/2024
>
# Mục Lục
[1. Khái niệm ](#p1) <br>
[2. Cách thức tìm kiếm và khai thác](#p2) <br>
[3. Lab](#p3) <br>
# Nội dung
<a id="p1"></a>
## 1. Khái niệm
Insecure direct object references (IDOR) là chủng lỗi phổ biến của Access Control Vulnerabilities. <br>
**IDOR** là lỗi cho phép hacker truy cập trực tiếp tới các đối tượng thông qua untrusted data ( thường là mã định danh identifer) mà không hề kiểm tra quyền truy cập. <br>
***Note:***  Bug này nhận Utrusted Data vào là một mã định danh (identifer). <br>
IDOR có thể xảy ra ở bất cứ chức năng nào của trang web như: <br>
- Download
- Payment
- Video Platform
- User Pannel
- Social Media
- Delete/Close
<a id="p2"></a>
## 2. Cách thức tìm kiếm và khai thác
Tìm kiếm : <br>
Kiểm tra các điểm dễ bị IDOR như: <br>
- Các tham số trên url : id, user_id, order_id, document_id,...
- Các endpoint API có thể bao gồm các tham số trong request như :POST /api/orders/456
- Các yều cầu POST hay PUT : check nội dung các request, các tham số trong phần body.
Khai thác : <br>
- Thay đổi các untrusted data vào các mã định danh để test.
<a id="p3"></a>
## 3. Lab
### 3.1 Lab: Insecure direct object references
This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs. <br>
Solve the lab by finding the password for the user carlos, and logging into their account. <br>
![image](https://github.com/user-attachments/assets/ffd65b78-0dc0-4564-a5b6-b7dbdf088c43)
Lỗ hổng IDOR đang xuất hiện ở tính năng Live Chat <br>
![image](https://github.com/user-attachments/assets/dc605e49-d0b3-4288-98c0-7e53af62c019)
Ta thấy có tính năng send để gửi tin nhắn còn view transcript là để xem lại bản ghi chép , lúc bấm vào thì nó sẽ cho phép chúng ta tải về nội dung trò chuyện. <br>
![image](https://github.com/user-attachments/assets/9fee6fb9-8bb8-4413-b82f-0c310320fded)
Dùng burp bắt request ta thấy có 1 api call đến /download-transcript/3.txt
![image](https://github.com/user-attachments/assets/ba7efa88-1e6f-42d0-b985-dac557bd7770)
Ta thấy các bản ghi sẽ có số thứ tự tăng dần vậy sẽ ra sao nếu chúng ta thay đổi số 3.txt thành 1 số khác liệu có thể xem được bản ghi của người khác. <br>
![image](https://github.com/user-attachments/assets/07850dbb-02dd-419f-a36f-4f2b87a9fecf)
Và chúng ta đọc được bản ghi của user khác kèm password => Login và solve lab <br>
![image](https://github.com/user-attachments/assets/86e6a48f-9b1c-4684-ac93-710a07dcf601)
### 3.2 Invoices
![image](https://github.com/user-attachments/assets/1a85f8b6-43d3-42dc-9a4b-d23f0d008c83)
Trang web cho chúng ta xem hóa đơn của mình bấm view và xem thử <br>
Và chúng ta có hóa đơn của Sean Johnson kèm invoice_id=1 <br>
![image](https://github.com/user-attachments/assets/e2edf197-0e5f-44a1-a78a-f2971a542b13)
![image](https://github.com/user-attachments/assets/909febf8-9ae5-42c7-a415-affecde6ce8f)
Check source code và xem thử: <br>
![image](https://github.com/user-attachments/assets/5da5bde7-49f9-48db-a86d-90f2192f1d93)
Ta thấy tham số `invoice_id` được lấy từ trực tiếp Untrusted data $_GET['invoice_id'] mà không có bất kì lớp validate nào. <br>
Vậy sẽ ra sao chúng ta đổi giá trị của invoice_id này <br>
![image](https://github.com/user-attachments/assets/592bbd9a-8023-40a0-9b75-fd0bdf704b05)
Và chúng ta có thể xem được thông tin hóa đơn của user khác.
### 3.3 Ticket Sales
![image](https://github.com/user-attachments/assets/a6d464e5-a702-40a9-9891-7ea9aac95b17)
Đây là 1 trang web bán vé, tiến hành check source code : <br>
![image](https://github.com/user-attachments/assets/62abb35d-2d2c-4a49-983a-e3e80a09e315)
Untrusted data rơi vào $_POST['amount'] và $_POST['ticket_money'] cho phép lấy data input vào mà không hề có lớp validate nào. <br>
![image](https://github.com/user-attachments/assets/aa1b92c0-d1e0-44af-a969-db28edb908a8)
Chúng ta có thể mua vé với giá 0$ ở đây <br>
![image](https://github.com/user-attachments/assets/0af7a159-7475-45de-ab91-53a1cf202eed)
### 3.4 Changing Password
Để solve lab này chúng ta cần đổi password người khác mà mình không có quyền <br>
![image](https://github.com/user-attachments/assets/e0eaefe0-754f-4cdc-8ee1-9e66802aa80a)
Trang web cho phép chúng ta đổi password username hiện tại là Christopher <br>
Bắt requets burpsuite để xem: <br>
![image](https://github.com/user-attachments/assets/9c0ce7cd-d201-47e4-ab26-4d9501a6dbcf)
Password là pass chúng ta cần đổi còn user_id là id hiện tại của username : Christopher <br>
Check source code đễ xem rõ chức năng hơn: <br>
![image](https://github.com/user-attachments/assets/1ef4905b-9774-4af5-845c-60cd3c9cf0df)
Tham số user_id được lấy Untrusted data tại $_POST['user_id']  mà không hề kiểm tra hay validate nào. Cho phép chúng ta có thể đổi  với một user_id bất kì khác. <br>
Ban đầu : <br>
![image](https://github.com/user-attachments/assets/3a3dc308-f17e-4c14-96a1-ca698ebb2174)
Tiến hành thay đồi với user_id của user khác : <br>
![image](https://github.com/user-attachments/assets/72a87739-3f76-4b7a-b189-0754bb82ea84)
Và chúng ta có thể thay đổi password của user khác.
### 3.5 Money Transfer
Để solve lab này chúng ta cần chuyển tiền từ tài khoản người khác về tài khoản mình <br>
![image](https://github.com/user-attachments/assets/3a40fdca-1101-4f90-84e9-1722e89c82b7)
Trang web có chức năng chuyển tiền cho phép cho chúng ta chuyển tiền tới user khác kèm số tiền chuyển (Transfer amount) và ID người nhận (Receiver ID) <br>
Check qua source code :
![image](https://github.com/user-attachments/assets/88e036a8-b521-4577-b2b0-14097003f9de)
Các giá trị recipient_id và sender_id được lấy trực tiếp từ các Untrusted data $_POST['recipient_id'] , $_POST['sender_id'], $_POST['transfer_amount']  mà không có bất kỳ biện pháp xác thực nào để kiểm tra xem người dùng hiện tại có quyền thực hiện hành động đó hay không. <br>
Check request: <br>
![image](https://github.com/user-attachments/assets/1f6201ce-c68e-46b9-bcce-e893b07a5eca)
- transfer_amount: số tiền
- recipient_id : id người nhận
- sender_id: id người gửi
Ta sẽ thay đổi sender_id bằng user khác và chuyển tiền về cho chúng ta <br>
![image](https://github.com/user-attachments/assets/9417cb54-09fa-44b7-ab73-043077bd0e58)
![image](https://github.com/user-attachments/assets/fbae3d7d-c0ec-4f6d-b2e4-e6cf5667b2d9)
Thành công chuyển tiền từ user khác về tài khoản mình mặc dù mình không có quyền.
### 3.6 Address Entry
Để solve lab này chúng ta  xem thông tin địa chỉ của người dùng khác mà không có quyền  <br>
![image](https://github.com/user-attachments/assets/6dff59b1-2706-46c6-ae2c-9456009e09f8)
![image](https://github.com/user-attachments/assets/7f05c497-31ba-4e73-a5aa-5ce7b2ec1bd1)
Chọn Order và xem request ở burpsuite : <br>
![image](https://github.com/user-attachments/assets/44445193-ed90-4762-8c69-0f18f5d21e90)
Ta thấy có tham số addressID tiến hành check source : <br>
addressID được lấy từ Untrusted data $_POST['addressID'] nhưng không có biện pháp hay validate nào. <br>
Thay thế addressID và xem request: <br>
![image](https://github.com/user-attachments/assets/0029018d-7506-4bc4-a9f9-7f26fc972260)
Và chúng ta xem được địa chỉ oder của người khác.
### 3.7 About
Để solve lab này chúng ta thay đổi thông tin hồ sơ của người dùng khác  <br>
![image](https://github.com/user-attachments/assets/b6f2eaa5-9925-4b21-90ba-c1d2028d6d88)
![image](https://github.com/user-attachments/assets/056ee4ac-ece4-4ca5-b402-067057d5ed16)
Ta thấy có tham số userid check source code:
```
if (isset($_COOKIE['userid'])) {
    $userid = $_COOKIE['userid'];
    $control = 1;
    setcookie("userid", "", time() - 3600, "$cookiepath");
} else {
    $userid = 3;
    $control = 0;
}
```
Ta thấy gia trị userid được lấy từ Untrusted data $_COOKIE['userid'] mà không có bất kì kiểm tra hay xác thực nào.
Tiến hành thay đổi userid ở cookie và dẽ dàng sửa được profile người khác.
![image](https://github.com/user-attachments/assets/5b966624-da67-4e06-b204-f672be1583e6)
### 3.8: Shopping Cart
Để solve lab này chúng ta cần mua finish flag  <br>
![image](https://github.com/user-attachments/assets/c2dc14de-6e75-4beb-aca0-a394f33bb012)
Tiên hành check source code <br>
![image](https://github.com/user-attachments/assets/d9a69eb9-bcba-4f7b-89de-2391c697c910)
- Tham số $_GET['resetBalance'] có thể được giả mạo. Nếu người dùng gửi yêu cầu HTTP đến URL này mà không có xác thực, có thể dẫn đến việc khôi phục số dư mà không có quyền hợp lệ.
- Biến $balance['id'] không được kiểm tra xem có tồn tại và có phải là giá trị hợp lệ hay không.
Vì giá trị flag lớn hơn số tiền hiện tại của mình
Tiến hành add 1 sản phẩm bất kì : <br>
![image](https://github.com/user-attachments/assets/6f033fbf-5a20-4447-b75c-a216d0f867a3)
![image](https://github.com/user-attachments/assets/1d9682fd-abc7-4f2e-9e31-75a68e45d8ba)
Mỗi sản phẩm sẽ có một mã code: <br>
![image](https://github.com/user-attachments/assets/40e5110a-006f-4de5-b4a4-f265198b9ea3)
Lấy mã code và nhập vào và check request : <br>
![image](https://github.com/user-attachments/assets/45e1d51d-0aea-4e7e-a61d-a72d85cde9de)
![image](https://github.com/user-attachments/assets/8fc09b6c-e860-4d46-8496-5cd3cb2dcba6)
Mua thành công  <br>
Path : `http://192.168.106.131:1337/lab/idor/shopping-cart/3Dvalid.php?code=SSBoZWFyZCB0aGUgYWRtaW4gaXMgZm9yZ2V0ZnVs` <br>
Tiến hành mua flag:
![image](https://github.com/user-attachments/assets/f6e38b21-d824-4d66-87d9-d85fa9cb5c81)
Bấm mua nhưng lại có cảnh báo là không đủ tiền : 
![image](https://github.com/user-attachments/assets/b218552f-46ae-4d79-bf81-39fc04713f87)
Dùng lại đoạn path trên của sản phẩm khác để bypass việc lấy mã code gửi về <br>
`http://192.168.106.131:1337/lab/idor/shopping-cart/cart.php?mess=priceError` => `http://192.168.106.131:1337//lab/idor/shopping-cart/3Dvalid.php?code=SSBoZWFyZCB0aGUgYWRtaW4gaXMgZm9yZ2V0ZnVs` và lấy mã code <br>
![image](https://github.com/user-attachments/assets/dd4f482b-8188-4e6b-82b6-9c728b48f43b)
![image](https://github.com/user-attachments/assets/f64948d6-60f9-4234-9e6e-a32d302d7379)
Mua thành công 
![image](https://github.com/user-attachments/assets/c107f757-c365-4da2-827b-90cb9f59983c)













 




