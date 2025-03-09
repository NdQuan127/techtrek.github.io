---
{"dg-publish":true,"permalink":"/atlas/notes/progressive-web-application-tao-ung-dung-web-nhu-zalo-tele-discord/","tags":["on/firefox"]}
---

Câu nói quen thuộc của người dùng khi sử dụng lợn Zalo, bản PC thì chậm, ngốn tài nguyên, ngốn ổ đĩa, khởi động cùng hệ thống một cách vô lý... Bản web cũng chả kém cạnh gây chậm trình duyệt do lưu trữ một lượng IndexDB lớn. Cơ mà ở Việt Nam mà không dùng Zalo thì khỏi nghĩ tới:  

- Tán gái, gái Việt dùng Zalo, không có khỏi tán gái
- Nhiều công ty ép nhân viên dùng Zalo, không có khỏi làm việc
- Xã hội dùng Zalo, không có khỏi giao tiếp

Vậy nên mấy hôm trước mình lặn lội thân cò tìm đường cứu nước, và giải pháp ở đây là biến thằng Zalo này thành ứng dụng web (PWA/Progressive Web Application), để nó tách biệt với trình duyệt và hoạt động như một ứng dụng web kiểu Electron có hẳn một biểu tượng riêng để mở ở Desktop, và đặc biệt khác với Zalo thường, thằng PWA này biến Zalo thành Portable, nghĩa là bê đi đâu cũng được mở phát lên dùng như khi ở nhà. Sau vài hôm sử dụng và nghiên cứu để có thể viết hướng dẫn mà ai cũng có thể làm được dù lấy não đặt sang một bên. ![:D](https://statics.voz.tech/styles/next/xenforo/smilies/popo/biggrin.png?v=01 "Big grin    :D")  
  
Addon này nhìn chung giống với PWA của Chrome, cơ mà ngon hơn nhiều về tính năng.  
  
Vậy thì vào việc thôi.  
  
Vậy đầu tiên đối tượng nào phù hợp để biến thành PWA ? Vào Settings -> Manage Cookies and SIte Data, thấy thằng nào dùng tầm 1-2GB thì nghĩa là phù hợp, ví dụ:
![Pasted image 20230901152906.png](/img/user/Atlas/Utilities/Images/Pasted%20image%2020230901152906.png)

**Hướng dẫn:**
- Cài đặt [**Progressive Web Application**](https://addons.mozilla.org/en-US/firefox/addon/pwas-for-firefox/) vào Firefox.
- Vào trang này tìm file kiểu [firefoxpwa_2.5.0_online.paf.exe](https://github.com/filips123/PWAsForFirefox/releases/download/v2.5.0/firefoxpwa_2.5.0_online.paf.exe) rồi cài vào: [https://github.com/filips123/PWAsForFirefox/releases](https://github.com/filips123/PWAsForFirefox/releases)
- Chạy PWAsForFirefoxPortable.exe
- Chuột phải vào file PWAsForFirefoxPortable.exe rồi Copy
- Win + R, mở `%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup`
- Paste Shortcut vào để nó khởi động cùng hệ thống
- Quay lại Firefox, mở [https://chat.zalo.me/](https://chat.zalo.me/) lên, đăng nhập các kiểu rồi ấn vào biểu tượng PWA đỏ đỏ bên trên -> Install current site -> Install Web App là xong thôi. Nếu muốn sửa lại tên ứng dụng thì cứ sửa.
- Chọn Launch Web App hoặc cứ mở [https://chat.zalo.me/](https://chat.zalo.me/) là nó mở thẳng qua PWA như một ứng dụng Zalo điện thoại, kết quả:
![2dXsrKZ.png](/img/user/Atlas/Utilities/Images/2dXsrKZ.png)

## Pin PWA vào Taskbar
Lấy command line từ cái process `firefox.exe` sau đó New shortcut -> Paste vào (cố gắng để folder PWA càng ngắn càng tốt vì shortcut có giới hạn 256 ký tự thôi), thế là xong ez, làm tương tự với Linux/Mac:
![1691331024652.png](/img/user/Atlas/Utilities/Images/1691331024652.png)

![Pasted image 20230901153441.png](/img/user/Atlas/Utilities/Images/Pasted%20image%2020230901153441.png)
  
Nếu muốn Pin vào Taskbar thì chuột phải vào cái Shortcut mới tạo, chọn Pin to Taskbar là xong nhé.

## -~~Ép cho PWA tiết kiệm RAM bằng cách tắt Fission~~-
- Tạo một folder rỗng ở đâu thì tùy, ví dụ `pwat`
- Tạo một file `user.js` trong thư mục trên, copy toàn bộ đoạn dưới vào:

Code:

```javaScript
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
```

- Save lại
- Từ cửa sổ Firefox/Floorp, ấn vào biểu tượng PWA
- Ấn vào cái bánh răng
- Dán đường dẫn tới thư mục `pwat` vừa tạo ban nãy:
![Pasted image 20230901153816.png](/img/user/Atlas/Utilities/Images/Pasted%20image%2020230901153816.png)

Và thế là xong, từ nay mỗi khi bạn tạo một ứng dụng PWA mới, nó sẽ thừa hưởng file `user.js` và tắt Fission đi tiết kiệm rất nhiều RAM

Ở phần **Tối ưu Firefox** mình có để rất nhiều tối ưu, hoàn toàn có thể áp dụng một số tối ưu để tăng tốc PWA lên được như nglayout, tắt chạy nền, ví dụ đây là một file `user.js` hịn tắt Fission, tối ưu nglayout, tắt chạy nền: *(bạn chỉ cần xoá đoạn code trên và thay đoạn code sau là được)*
```javaScript
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
// Enable Multi-Account Container
user_pref("privacy.userContext.enabled", true); //enable Multi-Account Container
user_pref("privacy.userContext.ui.enabled", true); //enable Multi-Account Container

/*** [SECTION 0200]: GEOLOCATION / LANGUAGE / LOCALE ***/
user_pref("_user.js.parrot", "0200 syntax error: the parrot's definitely deceased!");
/* 0201: use Mozilla geolocation service instead of Google if permission is granted [FF74+]
 * Optionally enable logging to the console (defaults to false) ***/
user_pref("geo.provider.network.url", "https://location.services.mozilla.com/v1/geolocate?key=%MOZILLA_API_KEY%");
   // user_pref("geo.provider.network.logging.enabled", true); // [HIDDEN PREF]
/* 0202: disable using the OS's geolocation service ***/
user_pref("geo.provider.ms-windows-location", false); // [WINDOWS]
user_pref("geo.provider.use_corelocation", false); // [MAC]
user_pref("geo.provider.use_gpsd", false); // [LINUX]
user_pref("geo.provider.use_geoclue", false); // [FF102+] [LINUX]

/*** [SECTION 0300]: QUIETER FOX ***/
user_pref("_user.js.parrot", "0300 syntax error: the parrot's not pinin' for the fjords!");
/** RECOMMENDATIONS ***/
/* 0320: disable recommendation pane in about:addons (uses Google Analytics) ***/
user_pref("extensions.getAddons.showPane", false); // [HIDDEN PREF]
/* 0321: disable recommendations in about:addons' Extensions and Themes panes [FF68+] ***/
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
/* 0322: disable personalized Extension Recommendations in about:addons and AMO [FF65+]
 * [NOTE] This pref has no effect when Health Reports (0331) are disabled
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to make personalized extension recommendations
 * [1] https://support.mozilla.org/kb/personalized-extension-recommendations ***/
user_pref("browser.discovery.enabled", false);

/** TELEMETRY ***/
/* 0330: disable new data submission [FF41+]
 * If disabled, no policy is shown or upload takes place, ever
 * [1] https://bugzilla.mozilla.org/1195552 ***/
user_pref("datareporting.policy.dataSubmissionEnabled", false);
/* 0331: disable Health Reports
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send technical... data ***/
user_pref("datareporting.healthreport.uploadEnabled", false);
/* 0332: disable telemetry
 * The "unified" pref affects the behavior of the "enabled" pref
 * - If "unified" is false then "enabled" controls the telemetry module
 * - If "unified" is true then "enabled" only controls whether to record extended data
 * [NOTE] "toolkit.telemetry.enabled" is now LOCKED to reflect prerelease (true) or release builds (false) [2]
 * [1] https://firefox-source-docs.mozilla.org/toolkit/components/telemetry/telemetry/internals/preferences.html
 * [2] https://medium.com/georg-fritzsche/data-preference-changes-in-firefox-58-2d5df9c428b5 ***/
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false); // see [NOTE]
user_pref("toolkit.telemetry.server", "data:,");
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.newProfilePing.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.shutdownPingSender.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.updatePing.enabled", false); // [FF56+]
user_pref("toolkit.telemetry.bhrPing.enabled", false); // [FF57+] Background Hang Reporter
user_pref("toolkit.telemetry.firstShutdownPing.enabled", false); // [FF57+]
/* 0333: disable Telemetry Coverage
 * [1] https://blog.mozilla.org/data/2018/08/20/effectively-measuring-search-in-firefox/ ***/
user_pref("toolkit.telemetry.coverage.opt-out", true); // [HIDDEN PREF]
user_pref("toolkit.coverage.opt-out", true); // [FF64+] [HIDDEN PREF]
user_pref("toolkit.coverage.endpoint.base", "");
/* 0334: disable PingCentre telemetry (used in several System Add-ons) [FF57+]
 * Defense-in-depth: currently covered by 0331 ***/
user_pref("browser.ping-centre.telemetry", false);
/* 0335: disable Firefox Home (Activity Stream) telemetry ***/
user_pref("browser.newtabpage.activity-stream.feeds.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry", false);

/** STUDIES ***/
/* 0340: disable Studies
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to install and run studies ***/
user_pref("app.shield.optoutstudies.enabled", false);
/* 0341: disable Normandy/Shield [FF60+]
 * Shield is a telemetry system that can push and test "recipes"
 * [1] https://mozilla.github.io/normandy/ ***/
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");

/** CRASH REPORTS ***/
/* 0350: disable Crash Reports ***/
user_pref("breakpad.reportURL", "");
user_pref("browser.tabs.crashReporting.sendReport", false); // [FF44+]
   // user_pref("browser.crashReports.unsubmittedCheck.enabled", false); // [FF51+] [DEFAULT: false]
/* 0351: enforce no submission of backlogged Crash Reports [FF58+]
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send backlogged crash reports  ***/
user_pref("browser.crashReports.unsubmittedCheck.autoSubmit2", false); // [DEFAULT: false]

/** OTHER ***/
/* 0360: disable Captive Portal detection
 * [1] https://www.eff.org/deeplinks/2017/08/how-captive-portals-interfere-wireless-security-and-privacy ***/
user_pref("captivedetect.canonicalURL", "");
user_pref("network.captive-portal-service.enabled", false); // [FF52+]
/* 0361: disable Network Connectivity checks [FF65+]
 * [1] https://bugzilla.mozilla.org/1460537 ***/
user_pref("network.connectivity-service.enabled", false);

/*** [SECTION 0400]: SAFE BROWSING (SB)
   SB has taken many steps to preserve privacy. If required, a full url is never sent
   to Google, only a part-hash of the prefix, hidden with noise of other real part-hashes.
   Firefox takes measures such as stripping out identifying parameters and since SBv4 (FF57+)
   doesn't even use cookies. (#Turn on browser.safebrowsing.debug to monitor this activity)

   [1] https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/
   [2] https://wiki.mozilla.org/Security/Safe_Browsing
   [3] https://support.mozilla.org/kb/how-does-phishing-and-malware-protection-work
   [4] https://educatedguesswork.org/posts/safe-browsing-privacy/
***/
user_pref("_user.js.parrot", "0400 syntax error: the parrot's passed on!");
/* 0401: disable SB (Safe Browsing)
 * [WARNING] Do this at your own risk! These are the master switches
 * [SETTING] Privacy & Security>Security>... Block dangerous and deceptive content ***/
   // user_pref("browser.safebrowsing.malware.enabled", false);
   // user_pref("browser.safebrowsing.phishing.enabled", false);
/* 0402: disable SB checks for downloads (both local lookups + remote)
 * This is the master switch for the safebrowsing.downloads* prefs (0403, 0404)
 * [SETTING] Privacy & Security>Security>... "Block dangerous downloads" ***/
   // user_pref("browser.safebrowsing.downloads.enabled", false);
/* 0403: disable SB checks for downloads (remote)
 * To verify the safety of certain executable files, Firefox may submit some information about the
 * file, including the name, origin, size and a cryptographic hash of the contents, to the Google
 * Safe Browsing service which helps Firefox determine whether or not the file should be blocked
 * [SETUP-SECURITY] If you do not understand this, or you want this protection, then override this ***/
user_pref("browser.safebrowsing.downloads.remote.enabled", false);
   // user_pref("browser.safebrowsing.downloads.remote.url", ""); // Defense-in-depth
/* 0404: disable SB checks for unwanted software
 * [SETTING] Privacy & Security>Security>... "Warn you about unwanted and uncommon software" ***/
   // user_pref("browser.safebrowsing.downloads.remote.block_potentially_unwanted", false);
   // user_pref("browser.safebrowsing.downloads.remote.block_uncommon", false);
/* 0405: disable "ignore this warning" on SB warnings [FF45+]
 * If clicked, it bypasses the block for that session. This is a means for admins to enforce SB
 * [TEST] see https://github.com/arkenfox/user.js/wiki/Appendix-A-Test-Sites#-mozilla
 * [1] https://bugzilla.mozilla.org/1226490 ***/
   // user_pref("browser.safebrowsing.allowOverride", false);
```
## Ép PWA tiết kiệm RAM ver 2.0
*Đây là tối ưu giảm RAM cực đoan và có lẽ là hết cỡ luôn rồi ![: D]( https://statics.voz.tech/styles/next/xenforo/smilies/popo/biggrin.png?v=01 "Big grin    : D")*
**Chú ý một điều là cái file `user.js` trên chỉ dành cho PWA vì tính bảo mật nó thấp hơn**, không dùng cho trình duyệt chính mà có dùng phải bỏ tất những thứ liên quan tới tắt Fission đi.  
> *Phần dưới đây chỉ nhằm giải thích chi tiết cách tối ưu còn anh em chỉ cần update lại file user.js bằng đoạn code ở cuối là được😁

Cập nhập giảm tiếp đọc ghi ổ đĩa, CPU bằng cách tăng sessionstore delay:  

|   |   |   |
|---|---|---|
|browser.sessionstore.idleDelay|3600000||

|   |   |
|---|---|
|browser.sessionstore.interval|3600000|

|   |   |
|---|---|
|browser.sessionstore.collect_zoom|false|

|   |   |
|---|---|
|browser.sessionstore.privacy_level|2|

|   |   |
|---|---|
|browser.sessionstore.restore_pinned_tabs_on_demand|true|

  
Giảm RAM bằng cách tắt Fast Back cache mà PWA không bao giờ dùng đến nên tự dưng ôm đồm nó phí RAM:  

|   |   |
|---|---|
|browser.sessionhistory.max_total_viewers|0|

**File `user.js` cuối, có vẻ lần này là hết cỡ thật trừ khi trong tương lai mình nhào nặn ra cái gì khác:**
```javaScript
user_pref("browser.sessionstore.idleDelay", 3600000);
user_pref("browser.sessionstore.interval", 3600000);
user_pref("browser.sessionstore.collect_zoom", false);
user_pref("browser.sessionstore.privacy_level", 2);
user_pref("browser.sessionstore.restore_pinned_tabs_on_demand", true);
user_pref("browser.sessionhistory.max_total_viewers", 0);

user_pref("dom.ipc.processCount.webIsolated", 1);
user_pref("fission.webContentIsolationStrategy", 0);
user_pref("identity.fxaccounts.enabled", false);
user_pref("extensions.pocket.enabled", false);
user_pref("accessibility.force_disabled", 1);
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
// Enable Multi-Account Container
user_pref("privacy.userContext.enabled", true); //enable Multi-Account Container
user_pref("privacy.userContext.ui.enabled", true); //enable Multi-Account Container

/*** [SECTION 0200]: GEOLOCATION / LANGUAGE / LOCALE ***/
user_pref("_user.js.parrot", "0200 syntax error: the parrot's definitely deceased!");
/* 0201: use Mozilla geolocation service instead of Google if permission is granted [FF74+]
 * Optionally enable logging to the console (defaults to false) ***/
user_pref("geo.provider.network.url", "https://location.services.mozilla.com/v1/geolocate?key=%MOZILLA_API_KEY%");
   // user_pref("geo.provider.network.logging.enabled", true); // [HIDDEN PREF]
/* 0202: disable using the OS's geolocation service ***/
user_pref("geo.provider.ms-windows-location", false); // [WINDOWS]
user_pref("geo.provider.use_corelocation", false); // [MAC]
user_pref("geo.provider.use_gpsd", false); // [LINUX]
user_pref("geo.provider.use_geoclue", false); // [FF102+] [LINUX]

/*** [SECTION 0300]: QUIETER FOX ***/
user_pref("_user.js.parrot", "0300 syntax error: the parrot's not pinin' for the fjords!");
/** RECOMMENDATIONS ***/
/* 0320: disable recommendation pane in about:addons (uses Google Analytics) ***/
user_pref("extensions.getAddons.showPane", false); // [HIDDEN PREF]
/* 0321: disable recommendations in about:addons' Extensions and Themes panes [FF68+] ***/
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
/* 0322: disable personalized Extension Recommendations in about:addons and AMO [FF65+]
 * [NOTE] This pref has no effect when Health Reports (0331) are disabled
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to make personalized extension recommendations
 * [1] https://support.mozilla.org/kb/personalized-extension-recommendations ***/
user_pref("browser.discovery.enabled", false);

/** TELEMETRY ***/
/* 0330: disable new data submission [FF41+]
 * If disabled, no policy is shown or upload takes place, ever
 * [1] https://bugzilla.mozilla.org/1195552 ***/
user_pref("datareporting.policy.dataSubmissionEnabled", false);
/* 0331: disable Health Reports
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send technical... data ***/
user_pref("datareporting.healthreport.uploadEnabled", false);
/* 0332: disable telemetry
 * The "unified" pref affects the behavior of the "enabled" pref
 * - If "unified" is false then "enabled" controls the telemetry module
 * - If "unified" is true then "enabled" only controls whether to record extended data
 * [NOTE] "toolkit.telemetry.enabled" is now LOCKED to reflect prerelease (true) or release builds (false) [2]
 * [1] https://firefox-source-docs.mozilla.org/toolkit/components/telemetry/telemetry/internals/preferences.html
 * [2] https://medium.com/georg-fritzsche/data-preference-changes-in-firefox-58-2d5df9c428b5 ***/
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false); // see [NOTE]
user_pref("toolkit.telemetry.server", "data:,");
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.newProfilePing.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.shutdownPingSender.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.updatePing.enabled", false); // [FF56+]
user_pref("toolkit.telemetry.bhrPing.enabled", false); // [FF57+] Background Hang Reporter
user_pref("toolkit.telemetry.firstShutdownPing.enabled", false); // [FF57+]
/* 0333: disable Telemetry Coverage
 * [1] https://blog.mozilla.org/data/2018/08/20/effectively-measuring-search-in-firefox/ ***/
user_pref("toolkit.telemetry.coverage.opt-out", true); // [HIDDEN PREF]
user_pref("toolkit.coverage.opt-out", true); // [FF64+] [HIDDEN PREF]
user_pref("toolkit.coverage.endpoint.base", "");
/* 0334: disable PingCentre telemetry (used in several System Add-ons) [FF57+]
 * Defense-in-depth: currently covered by 0331 ***/
user_pref("browser.ping-centre.telemetry", false);
/* 0335: disable Firefox Home (Activity Stream) telemetry ***/
user_pref("browser.newtabpage.activity-stream.feeds.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry", false);

/** STUDIES ***/
/* 0340: disable Studies
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to install and run studies ***/
user_pref("app.shield.optoutstudies.enabled", false);
/* 0341: disable Normandy/Shield [FF60+]
 * Shield is a telemetry system that can push and test "recipes"
 * [1] https://mozilla.github.io/normandy/ ***/
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");

/** CRASH REPORTS ***/
/* 0350: disable Crash Reports ***/
user_pref("breakpad.reportURL", "");
user_pref("browser.tabs.crashReporting.sendReport", false); // [FF44+]
   // user_pref("browser.crashReports.unsubmittedCheck.enabled", false); // [FF51+] [DEFAULT: false]
/* 0351: enforce no submission of backlogged Crash Reports [FF58+]
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send backlogged crash reports  ***/
user_pref("browser.crashReports.unsubmittedCheck.autoSubmit2", false); // [DEFAULT: false]

/** OTHER ***/
/* 0360: disable Captive Portal detection
 * [1] https://www.eff.org/deeplinks/2017/08/how-captive-portals-interfere-wireless-security-and-privacy ***/
user_pref("captivedetect.canonicalURL", "");
user_pref("network.captive-portal-service.enabled", false); // [FF52+]
/* 0361: disable Network Connectivity checks [FF65+]
 * [1] https://bugzilla.mozilla.org/1460537 ***/
user_pref("network.connectivity-service.enabled", false);

/*** [SECTION 0400]: SAFE BROWSING (SB)
   SB has taken many steps to preserve privacy. If required, a full url is never sent
   to Google, only a part-hash of the prefix, hidden with noise of other real part-hashes.
   Firefox takes measures such as stripping out identifying parameters and since SBv4 (FF57+)
   doesn't even use cookies. (#Turn on browser.safebrowsing.debug to monitor this activity)

   [1] https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/
   [2] https://wiki.mozilla.org/Security/Safe_Browsing
   [3] https://support.mozilla.org/kb/how-does-phishing-and-malware-protection-work
   [4] https://educatedguesswork.org/posts/safe-browsing-privacy/
***/
user_pref("_user.js.parrot", "0400 syntax error: the parrot's passed on!");
/* 0401: disable SB (Safe Browsing)
 * [WARNING] Do this at your own risk! These are the master switches
 * [SETTING] Privacy & Security>Security>... Block dangerous and deceptive content ***/
   // user_pref("browser.safebrowsing.malware.enabled", false);
   // user_pref("browser.safebrowsing.phishing.enabled", false);
/* 0402: disable SB checks for downloads (both local lookups + remote)
 * This is the master switch for the safebrowsing.downloads* prefs (0403, 0404)
 * [SETTING] Privacy & Security>Security>... "Block dangerous downloads" ***/
   // user_pref("browser.safebrowsing.downloads.enabled", false);
/* 0403: disable SB checks for downloads (remote)
 * To verify the safety of certain executable files, Firefox may submit some information about the
 * file, including the name, origin, size and a cryptographic hash of the contents, to the Google
 * Safe Browsing service which helps Firefox determine whether or not the file should be blocked
 * [SETUP-SECURITY] If you do not understand this, or you want this protection, then override this ***/
user_pref("browser.safebrowsing.downloads.remote.enabled", false);
   // user_pref("browser.safebrowsing.downloads.remote.url", ""); // Defense-in-depth
/* 0404: disable SB checks for unwanted software
 * [SETTING] Privacy & Security>Security>... "Warn you about unwanted and uncommon software" ***/
   // user_pref("browser.safebrowsing.downloads.remote.block_potentially_unwanted", false);
   // user_pref("browser.safebrowsing.downloads.remote.block_uncommon", false);
/* 0405: disable "ignore this warning" on SB warnings [FF45+]
 * If clicked, it bypasses the block for that session. This is a means for admins to enforce SB
 * [TEST] see https://github.com/arkenfox/user.js/wiki/Appendix-A-Test-Sites#-mozilla
 * [1] https://bugzilla.mozilla.org/1226490 ***/
   // user_pref("browser.safebrowsing.allowOverride", false);
```