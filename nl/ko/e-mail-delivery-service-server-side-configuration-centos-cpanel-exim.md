---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud 이메일 전송 서비스(CentOS, cPanel 및 Exim)를 사용하도록 서버 구성

## 개요

{{site.data.keyword.cloud}} 이메일 서비스를 사용하도록 서버를 구성하려면 이 정보를 사용하십시오. 

## 전제조건

1.  스마트 호스트 설정을 추가하거나 업데이트하기 전에 디바이스에서 이메일을 발송할 수 있는지 확인하십시오. 진행하기 전에 발송/수신 프로세스에서 기존 문제점을 수정하십시오.
2. 다음 단계를 수행하여 Exim 구성 편집기에 액세스하십시오.
  * 고유 신임 정보를 사용하여 WHM에 액세스하십시오.
  * **서비스 구성 > Exim 구성 편집기**로 이동하십시오.
  * 화면 맨 아래의 **고급 편집기** 단추를 클릭하여 편집기를 여십시오.
  
**참고:**
- 고급 편집기 사용에 대한 특정 지시사항은 **Exim 구성 편집기** 화면에 있습니다.
- 이 프로시저로 인해 Exim이 실패할 수 있습니다.
- **Exim 구성 편집기** 화면에 _exim.conf_ 파일의 컨텐츠가 표시됩니다. Exim 구성 관리자를 사용하여 _exim.conf_를 편집할 수 있습니다.

## SendGrid 신임 정보를 사용한 인증

**인증자 시작** 섹션을 찾아 **Section: AUTH**라고 레이블 지정된 해당 텍스트 상자에 다음 명령을 입력하십시오.

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## 라우터 구성

**Section: PREROUTERS:** `send_via_sendgrid:`라고 레이블 지정된 섹션의
**라우터 구성**에 다음 명령을 추가하십시오.

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## 전송 구성

**Section: TRANSPORTSTART**라고 레이블 지정된 섹션의 **전송 구성**에 다음 명령을 추가하십시오.

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

페이지 맨 아래의 **저장**을 클릭하십시오.

<em>**참고:** 외부 주소로 전달된 root/nobody/cpanel 메일을 수신하려면 cPanel 서버의 호스트 이름이 /etc/localdomains 파일에 있어야 합니다.</em>

## 다음 작업

시스템은 업데이트된 구성 파일에 대한 일련의 검사를 실행하고 Exim을 다시 시작합니다. WebMail 페이지에 로그인한 경우 다시 시작이 완료된 후 로그아웃하고 다시 로그인하십시오. 테스트 이메일을 발송하여 [{{site.data.keyword.slportal_full}}![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}의 [이메일 전송 서비스![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/services/emaildelivery){: new_window} 화면에서 올바른 신용이 사용되는지 확인하십시오.
