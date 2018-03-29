---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 電子郵件遞送服務伺服器端配置：MailEnable/IIS 及 SendGrid

請完成下列步驟，配置您的伺服器以使用 {{site.data.keyword.cloud}} 電子郵件遞送服務作為智慧型主機。下列範例適用於標準 Windows 2008 或 2012 伺服器，並已配置 MailEnable 或 IIS 作為您的 SMTP 服務。

## IIS 配置

1.  在 Windows 中開啟 IIS Manager。
2.  按一下您的網站。主要配置選項頁面會顯示在右邊。
3.  按兩下 **SMTP 電子郵件**圖示。
4.  在「電子郵件位址」欄位中，鍵入將為寄件者的電子郵件位址。
5.  按一下**將電子郵件傳遞到 SMTP 伺服器**圓鈕。
6.  在 **SMTP 伺服器**欄位中，鍵入 smtp.sendgrid.net。
7.  在**連接埠**欄位中，鍵入 587。
8.  在**驗證設定**下，選擇**指定認證**然後按一下**設定**。
9.  新增您的 {{site.data.keyword.SendGrid}} 使用者名稱及密碼，然後按一下**儲存**。

## MailEnable

1.  開啟 MailEnableAdmin 應用程式。
2.  展開左手邊導覽窗格中的 **Servers** 標籤。
3.  按一下 localhost > System > 在 SMTP 上按一下滑鼠右鍵。
4.  在 **SMTP Properties** 方框，按一下 **Smart Host**。
5.  啟用 **Smart Host Enabled** 旁邊的方框。
6.  在 **IP/Domain** 下，鍵入 smtp.sendgrid.net。 
7.  在 **Port** 欄位中，鍵入 587。
8.  勾選 The remote server requires authentication 方框。
9.  輸入您的 {{site.data.keyword.SendGrid}} 使用者名稱及密碼，然後按一下 **Apply**。
10.  移至 **Windows 服務**，重新啟動 MailEnable。
