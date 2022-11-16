# SQL injection vulnerability allowing login bypass
--- 
### Ở ví dụ này chúng ta sẽ thực hành 1 trong những ứng dụng có sức ảnh hưởng lớn của SQLi đó chính là Login Bypass.

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_12.png)


* Và chúng ta có thể thấy được rằng tài chúng ta chưa kết nối với tài khoản của chúng ta khi ở trang web này. Click vào ‘ My Account’ ta sẽ thấy 1 cửa sổ đăng nhập hiện lên. 

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_13.png)

* Trang web yêu cầu chúng ta đăng nhập và sau khi thử 1 tên tài khoản bất kì và 1 password bất kì và kiểm tra trong Burp Suite ta được kết quả trả về như sau:

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_14.png)

* Kết quả trả về trong Burp Suite:

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_15.png)

* Vậy thì để kiểm tra xem trang form đăng nhập này có vấn đề gì không thì ta có thể thử cách giống như ví dụ trước, đó chính là thêm 1 dấu “  ‘  ” ở phía cuối xem có lỗi gì xảy ra không. 

* Và tất nhiên trang web sẽ báo lỗi vì thế khả năng cao chúng ta có thể khai thác lỗ hổng ở phần này.

* Vậy tại sao lại xuất hiện lỗi ở đây ? Lí do bởi đoạn SQL query bị sửa lại thành sai.

```SQL
SELECT * From users where username = 'Huy' and password = 'haha' 

// Đoạn code sau khi chúng ta sửa sẽ thành như thế này. 

SELECT * From users where username = 'Huy'' and password = 'haha'
```
* Ta dễ dàng nhận thấy ở đoạn code bị sửa ta có username bị thừa ra dấu “ ‘ ” vì chúng ta đã cố ý đặt nó ở vị trí như vậy nên khi dòng code chạy nó sẽ không nhận ra và trả về lỗi.

* Giờ làm thế nào để chúng ta có thể khai thác lỗ hổng này ?
Như ví dụ trước, ta để ý “ - - ” có vai trò như là 1 comment vậy nên ở đây ta hoàn toàn có thể thao tác tương tự để có thể comment đi phần mật khẩu và chúng ta có thể bypass login form

* **Ý tưởng của nó được thực hiện như sau**

```SQL
SELECT * From users where username = 'administrator'-- and password = 'haha'
```
* Ta biết được rằng username của lab là **administrator** nên ta sẽ sử dụng tên đăng nhập này để bypass.

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_22.png)

* Và ta có kết quả như sau: 

![PIC](https://github.com/thewantedx/SQLi-PortSwigger-WriteUp/blob/main/Bin/SQLi_23.png)
