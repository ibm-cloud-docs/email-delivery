---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 配置伺服器以使用 IBM Cloud 電子郵件遞送服務：CentOS、cPanel 及 Exim

## 概觀

請使用此資訊以配置伺服器來使用 {{site.data.keyword.cloud}} 電子郵件服務。 

## 準備

1.  確認您可以從裝置傳送電子郵件，然後才新增或更新智慧型主機設定。請先修正傳送/接收程序中的任何現有問題，然後才繼續。
2. 執行下列步驟以存取 Exim Configuration Editor：
  * 使用您的唯一認證存取 WHM。
  * 導覽至 **Service Configuration > Exim Configuration Editor**。
  * 按一下畫面底端的 **Advanced Editor** 按鈕以開啟編輯器。
  
**附註：**
- 使用 Advanced Editor 的特定指示位於 **Exim Configuration Editor** 畫面。
- 此程序可能導致 Exim 失敗。
- **Exim Configuration Editor** 畫面會顯示 _exim.conf_ 檔案的內容。您可以使用 Exim Configuration Manager 編輯 _exim.conf_。

## 使用 SendGrid 認證進行鑑別

找到 **Begin Authenticators** 區段，並在標籤為 **Section: AUTH** 的對應文字框中輸入下列指令：

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## 配置 Routers

將下列指令新增至標籤為 **Section: PREROUTERS** 中的 **Routers Configuration**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## 配置 Transports

將下列指令新增至標籤為 **Section: TRANSPORTSTART** 中的 **Transports Configuration**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

按一下頁面底端的 **Save**。

<em>**附註：**為了收到轉遞給外部位址的 root/nobody/cpanel 郵件，cPanel 伺服器的主機名稱需要在 /etc/localdomains 檔案中。</em>

## 後續情形

系統會針對更新過的配置檔執行一系列的檢查，並重新啟動 Exim。如果您登入任何 WebMail 頁面，請登出並在重新啟動完成之後重新登入。從 [{{site.data.keyword.slportal_full}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window} 中的 [E-mail Delivery 服務 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/services/emaildelivery){: new_window} 畫面，傳送測試電子郵件以確定使用了適當的認證。
