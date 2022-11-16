# SQL injection UNION attack, finding a column containing text
---

* Sau khi vào lab ta có thể chọn bất kì thư mục nào như ‘Accessories’ và sử dụng Burp Suite để xem rằng có những gì đang diễn ra 
Và để ý kĩ thì ta thấy đề bài đang yêu cầu chúng ta tìm cụm : “nNVp9e”

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_40.png)

Sau đó ta có thể chỉnh như lab trước và thu được kết quả báo lỗi:

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_42.png)

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_43.png)

* Sau đó đề bài yêu cầu tim string bên trên nên ta có thể thêm vào string đó để kiểm tra.

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_44.png)

* Mặc dù thêm vào cột đầu kết quả vẫn trả về lỗi nhưng sau khi thử đến cột thứ 2 thì kết quả đã đúng.

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_46.png)

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_47.png)

* Send request và ta đã hoàn thành lab.

![PIC](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_48.png)


## Tổng kết

* Ta nhận thấy rằng cột mà chúng ta thêm vào string “nNVp9e” sẽ là cột phù hợp để truy xuất dữ liệu chuỗi. Từ đó xác định được rằng nó nằm ở cột số 2. và ta có thể sử dụng nó để có thể biết được kiểu dạng thông tin chứa trong cột đó 


