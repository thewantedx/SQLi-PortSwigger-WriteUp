# SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
---
Ảnh page khi ta mới đăng nhập

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_1.png)

Khi để ý kĩ và click vào các mục ở trong page như ‘Clothing’, ‘Gift’, ‘Lifestyle’, … ta có với ví dụ đường link **LifeStyle** xuất hiện như sau:

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_2.png)

Ta nhận thấy cả 2 đường link đều có điểm chung là đi vào ‘category’ và thay đổi ở **Lifestyle** và **Gift**

Điều này cho chúng ta thấy website thực hiện SQL querry để truy suất chi tiết các sản phẩm có liên quan từ cơ sở dữ liệu trong trường hợp này chính là **Lifestyle** và **Gift**

```SQL
    SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1 
```

Câu hỏi đặt ra là: Nếu chúng ta sửa đổi 1 chút vào đường link thì chúng ta sẽ ra được kết quả như thế nào ? 

Ta có thể ví dụ trong đường link trên ta bỏ đi Lifestyle và giữ nguyên phần còn lại của link trên thì ta có kết quả như dưới đây:

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_4.png)

Và đây là kết quả: 

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_5.png)

Ta thấy kết quả trả về không hề báo lỗi tức là ta có thể khai thác lỗ hổng SQLi ở đây.
Để có thể chắc chắn hơn trong việc có lỗ hổng SQLi ở trang web trên ta có thể sử dụng 1 kĩ thuật điển hình đó chính là thêm 1 dấu “  ‘  ” vào đằng sau SQLi để kiểm tra:

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_6.png)

Ta có thể thấy được website báo lỗi ngay lập tức.

Đoạn code khi chúng ta sửa lại có thể được hiểu là: 

```SQL
    SELECT * FROM products WHERE category = ''' AND released = 1
```
Chính vì lí do đó mà trang web của chúng ta mới xuất hiện ra lỗi. 

**Thế thì chúng ta có thể làm gì để có thể khai thác lỗ hổng SQLi ở đây ?**

Ta sẽ thực hiện 1 câu lệnh rất hay dùng với SQLi đó chính là “ +OR+1=1 – “ ý nghĩa của nó là 1 điều kiện mới mà chúng ta đưa ra vào thời điểm này là luôn luôn đúng.

Link sẽ trở thành như thế này:

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_9.png)

Ta có thể hiểu code nó sẽ như sau

```SQL
    SELECT * FROM products WHERE category = '' OR 1=1--' AND released = 1
```
Hai dấu  ‘- - ’ ở cuối dòng lệnh nghĩa là tất cả những gì ở đằng sau nó có thể hiểu như là 1 comment. Và thế là chúng ta có thể xem được tất cả các hidden data(Ở đây là các sản phẩm bị ẩn đi.

![Pic](https://github.com/thewantedx/Picture-Security/blob/main/SQLi_11.png)