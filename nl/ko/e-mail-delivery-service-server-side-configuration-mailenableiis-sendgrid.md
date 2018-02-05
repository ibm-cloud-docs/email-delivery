---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 이메일 전송 서비스 서버 측 구성: MailEnable/IIS 및 SendGrid

## 개요

이 프로시저를 사용하여 {{site.data.keyword.cloud}} 이메일 전송 서비스를 스마트 호스트로 사용하도록 서버를 구성하십시오. 다음 예제는 SMTP 서비스로 구성된, MailEnable 또는 IIS가 포함된 표준 Windows 2008 또는 2012 서버에 대한 예제입니다.

## IIS 구성

1.  Windows에서 IIS 관리자를 여십시오.
2.  사이트를 클릭하십시오. 기본 구성 옵션 페이지가 오른쪽에 표시됩니다.
3.  SMTP 이메일 아이콘을 두 번 클릭하십시오.
4.  이메일 주소 필드에 발신인이 될 이메일 주소를 입력하십시오.
5.  SMTP 서버로 이메일 전송 단일 선택 단추를 클릭하십시오.
6.  SMTP 서버 필드에 smtp.sendgrid.net을 입력하십시오.
7.  포트 필드에 587을 입력하십시오.
8.  인증 설정에서 신임 정보 지정을 선택하고 설정을 클릭하십시오.
9.  {{site.data.keyword.SendGrid}} 사용자 이름 및 비밀번호를 추가하고 저장을 클릭하십시오.

## MailEnable

1.  MailEnableAdmin 애플리케이션을 여십시오.
2.  왼쪽 탐색 분할창에서 서버 탭을 펼치십시오.
3.  로컬 호스트 > 시스템 > SMTP에서 마우스 오른쪽 클릭을 클릭하십시오.
4.  SMTP 특성 상자에서 스마트 호스트 탭을 클릭하십시오.
5.  스마트 호스트 사용 옆에 있는 상자를 사용으로 설정하십시오.
6.  IP/도메인에 smtp.sendgrid.net을 입력하십시오. 
7.  포트 필드에 587을 입력하십시오.
8.  '원격 서버에 인증이 필요함'이라고 표시된 상자를 선택하십시오.
9.  {{site.data.keyword.SendGrid}} 사용자 이름 및 비밀번호를 입력하고 적용을 클릭하십시오.
10.  Windows 서비스로 이동하고 MailEnable을 다시 시작하십시오.
