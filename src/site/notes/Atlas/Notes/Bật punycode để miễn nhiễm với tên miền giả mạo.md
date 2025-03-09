---
{"dg-publish":true,"permalink":"/atlas/notes/bat-punycode-de-mien-nhiem-voi-ten-mien-gia-mao/"}
---

up:: [[Atlas/Maps/Firefox MOC\|Firefox MOC]]
tags:: #on/bt_chiase 

# Bật punycode để miễn nhiễm với tên miền giả mạo
Bảo mật và riêng tư luôn đi liền với bất tiện, nhìn chung nên xác định điều này và Firefox mặc định nó đủ bảo mật và riêng tư rồi, chỉ cái:  

|   |   |
|---|---|
|network.IDN_show_punycode|true|
  
Là ai cũng nên bật vì nó sẽ phá mấy trang web dùng unicode thành dạng `xn--abcxyz` giúp mấy trang lừa đảo giả tên miền kiểu `google.com` không còn linh nữa.  
  
Ví dụ `フラワーナイトガール.攻略wiki.com` khi bật punycode sẽ bị buộc thành `xn--eckq7fg8cygsa1a1je.xn--wiki-4i9hs14f.com`  
  
Hoặc ngoạn mục là `GOOGᒪE.com` được sửa thành `xn--googe-bkz.com`, `𝐠𝐨𝐨𝐠ʟ𝐞.𝐜𝐨𝐦` thành `xn--googe-hxc.com`  
  
Đó là sự đáng sợ của tên miền giả mạo, và tụi hacker tụi nó không nhân từ như mình mà nó y hệt `google.com` luôn.