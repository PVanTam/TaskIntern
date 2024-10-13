# Information Gathering
>Tên tài liệu: Information Gathering<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 14/10/2024
>
# Mục Lục
[1.Target ](#p1) <br>

# Nội dung
<a id="p1"></a>
## 1. Target
Mục tiêu của chúng ta là trang web : `www.coolblue.be`
## 2 Conduct Search Engine Discovery Reconnaissance for Information Leakage
Tìm kiếm cơ bản với Google
Nhập vào thanh tìm kiếm `site:www.coolblue.be` để liệt kê tất cả các trang nào đang hiển thị công khai <br>
![image](https://github.com/user-attachments/assets/8068f5d4-3035-4289-961c-e802cc37b530) <br>
Check thử qua thì không thấy gì đáng ngờ hết <br>
`filetype:pdf, filetype:doc, filetype:xls` : check các file chưa thông tin nhạy cảm <br>
![image](https://github.com/user-attachments/assets/328137c5-04f3-4862-9de2-add9aa91804f)
`cache:www.coolblue.be` để kiểm tra lưu trữ bộ nhớ đệm <br>
![image](https://github.com/user-attachments/assets/000291bc-0238-47d0-b860-4b9badd53978)
Check login pages or admin panels: <br>
`site:www.coolblue.nl inurl:login, site:www.coolblue.nl inurl:admin`
![image](https://github.com/user-attachments/assets/38c1495d-8602-4581-be34-3bd84aa3bd82)
![image](https://github.com/user-attachments/assets/8e244dcc-5435-4b44-addf-a0008e3c5543)
![image](https://github.com/user-attachments/assets/8b5fc216-12bf-4b1d-89f9-3c5896570426) <br>
Có tính năng điều hướng tới 1 URL => open redirect <br>
`site:www.coolblue.nl intitle:"index of"` check thư mục <br>
![image](https://github.com/user-attachments/assets/15a72add-2521-4655-a7f7-62ad9608e043)
`site:www.coolblue.nl "Internal Server Error", site:www.coolblue.nl "Fatal Error"` check các thông báo lỗi của web <br>
![image](https://github.com/user-attachments/assets/4591e6e1-307e-4cc8-8062-f33dc28e21a8)
![image](https://github.com/user-attachments/assets/c5d81428-cb0a-4bc0-8249-e27df911cea5)
Check sơ qua thì không thây gì <br>
`site:www.coolblue.nl inurl:.git` : check git
![image](https://github.com/user-attachments/assets/871a8e54-c263-4a3e-95f4-a813269505fb)




