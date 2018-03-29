---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 埠 25 上的出埠電子郵件

自 2015 年 10 月 28 日起，{{site.data.keyword.BluSoftlayer_notm}} 已不再允許新帳戶透過 TCP 埠 25 (SMTP) 建立出埠連線。

## 為何封鎖標準電子郵件埠？

依預設，會封鎖標準的 SMTP TCP 埠 25，因為有大量的濫用情形以此埠為目標。{{site.data.keyword.BluSoftlayer_notm}} 提供來自 SendGrid 的具公信力第三者電子郵件中繼服務，如果您需要從他們的網域或應用程式傳送出埠電子郵件的話。  

## 想要從我的伺服器或應用程式傳送電子郵件時，有什麼選項？

如果您需要從您的伺服器傳送電子郵件，您需要使用 {{site.data.keyword.BluSoftlayer_notm}} 之外的智慧型主機。智慧型主機會中繼來自 SMTP 伺服器、郵件用戶端或任何能夠處理 SMTP 之其他服務或程式設計語言的 SMTP 資料流量。伺服器通常會使用郵件提交 TCP 埠 465 或 587 來傳送這類型的資料流量。您可以與那些埠或非 TCP 埠 25 的任何自訂埠進行通訊。如果您想要在自訂埠上使用自己的電子郵件伺服器，請使用您的電子郵件服務特有的文件，以配置自訂電子郵件埠。

## IBM Cloud 有提供智慧型主機服務嗎？

{{site.data.keyword.BluSoftlayer_notm}} 現在提供由 SendGrid 提供的電子郵件遞送服務，它允許用戶端使用智慧型主機來中繼您的出埠郵件服務。此服務有許多其他的功能，例如產生度量值、追蹤電子郵件清單、追蹤電子郵件活動、協助新聞信件，以及鑑別。
