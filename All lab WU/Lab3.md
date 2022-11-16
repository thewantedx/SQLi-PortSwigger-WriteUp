# SQL injection UNION attack, determining the number of columns returned by the query.
---

* Ta truy cập vào trang web, click vào ‘Clothing, shoes and accessories’ (Sử dụng burp suite) và ta được như sau:

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_30.png)

* Ta chèn vào câu lệnh: 
```SQL
UNION SELECT NULL -- // Dùng để kiểm tra xem có tất cả bao nhiêu cột trong table
```

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_31.png)

* Ta có kết quả trả về lỗi và khi ta tăng dần số NULL lên ta thấy được rằng kết quả trả về 200OK khi ta sử dụng đến NULL thứ 3. 

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_32.png)

* Sau khi chúng ta tìm được số cột và send request đi chúng ta đã solve được lab.

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_33.png)

