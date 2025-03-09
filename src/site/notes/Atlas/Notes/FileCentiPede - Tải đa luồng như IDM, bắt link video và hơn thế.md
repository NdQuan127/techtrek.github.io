---
{"dg-publish":true,"permalink":"/atlas/notes/file-centi-pede-tai-da-luong-nhu-idm-bat-link-video-va-hon-the/","tags":["on/firefox"]}
---

Hướng dẫn cách cài con vịt pede xòe ra hai cái cánh để bắt link và tải đa luồng như IDM:  
- Tải tại đây: [https://github.com/filecxx/FileCentipede/releases](https://github.com/filecxx/FileCentipede/releases)

Nếu các bạn xài Firefox Portable hay Floorp thì vào trang addon cài **[https://addons.mozilla.org/vi/firefox/addon/filecxx/](https://addons.mozilla.org/vi/firefox/addon/filecxx/)** hoặc tải file `firefox.xpi` [**tại đây**](https://github.com/filecxx/FileCentipede/releases) rồi kéo thả nó vào để cài đặt là xong nếu nó không tự cài đặt, thường thì khi xài Firefox cài đặt là nó tự cài.  
  
Tính năng thì:  
- Y như IDM (đa luồng, thời gian biểu (schedule), bắt link video, hàng loạt...)
- Hơn IDM (kéo Torrent, ED2K)
- KHÔNG GHÉP FILE mà tạo ra một file ảo sau đó ghi liên tiếp vào file ảo trên, không nghẽn ổ đĩa  *(đây chính là tính năng ưu việt hơn hẳn IDM khi mà IDM tách ra từng phần tải rồi ghép vào nên dẫn đến bị full disk và tốn thời gian)*

## Hướng dẫn cách để con vịt hết pede
Đầu tiên anh em tạo 1 file .bat bằng notepad để tiện việc tắt hẳn app.  

Code:

```
taskkill /im fileu.exe /f
net stop filec
taskkill /im filec.exe /f
```

Chạy file .bat để kill con vịt  

Sau đó tải app này: https://portableapps.com/apps/development/sqlite_database_browser_portable

Tải về giải nén các kiểu cài ra được app portabe, chạy nó.  
Vào File > open database chọn file `filecxx_2.71_win_x64\lib\data_windows.db`  

Thấy cái table Local chuột phải -> *delete table*  

![1666550072889.png](https://voz.vn/attachments/1666550072889-png.1456757/ "1666550072889.png")

  
Ấn Ctrl + S để save lại  

Sau đó bật lại con vịt vào *Help > Activation code* coi số ngày nó reset lại 3 ngày sử dụng chưa.  

Rồi chạy file .bat tiếp để kill con vịt  

Mở lại cửa sổ SQL Lite ấn F5 nó sẽ hiển thị lại table local  
Tới đây bấm tab Browser data chọn Local  

![1666550198563.png](https://voz.vn/attachments/1666550198563-png.1456758/ "1666550198563.png")

Dòng số 1,2 là 2 dãy chữ số giống nhau. Ấn đè kéo cái 2 dòng đó để edit được. *Đổi chữ cái gần cuối cùng thành chữ a*. 
VD: FdyQ764Gih**k**Y thành FdyQ764Gih**a**Y  

![1666550471799.png](https://voz.vn/attachments/1666550471799-png.1456764/ "1666550471799.png")

  
Sau đó ấn Ctrl + S để save lại  
Rồi mở con vịt lên và thấy số ngày tăng ![:sexy_girl:](https://statics.voz.tech/styles/next/xenforo/smilies/popopo/sexy_girl.png?v=01 "sexy_girl    :sexy_girl:")  

![1666550349246.png](https://voz.vn/attachments/1666550349246-png.1456763/ "1666550349246.png")