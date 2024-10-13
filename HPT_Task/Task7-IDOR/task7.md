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






