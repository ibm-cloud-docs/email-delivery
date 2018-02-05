---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 이메일 전송 서비스 서버 측 구성: Sendmail 및 SendGrid

## 개요

이 프로시저를 사용하여 Sendmail로 {{site.data.keyword.cloud}} 이메일 전송 서비스를 사용하도록
서버를 구성하십시오. 다음 예제는 Centos 6.5 및 Ubuntu 14의 베어메탈 설치에서 수행되었습니다.

## 사전 구성

{{site.data.keyword.SendGrid}}를 스마트 호스트로 올바르게 사용하려면 Sendmail의 다음 패키지를 설치해야 합니다.

### RHEL/Centos
RHEL/Centos의 경우 다음 명령을 실행하십시오.
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Ubuntu/Debian의 경우 다음 명령을 실행하십시오.
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## 구성

1. 다음을 사용하여 {{site.data.keyword.SendGrid}} 사용자 이름 및 비밀번호를 /etc/mail/access 파일에 추가하십시오.
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. 다음 명령을 실행하여 /etc/mail/access.db 데이터베이스 맵을 생성하십시오.
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. /etc/mail/sendmail.mc 파일을 편집하여 {{site.data.keyword.SendGrid}}를 스마트 호스트로 사용하십시오.

### RHEL/Centos에서 sendmail.mc 구성
1. sendmail.mc 파일을 찾아 여십시오.
2. 다음 행을 주석 처리하십시오.
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. 또한 sendmail.mc 파일에 다음 코드가 포함된 새 행을 추가하십시오.
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Ubuntu/Debian에서 sendmail.mc 구성
1. sendmail.mc 파일을 찾아 여십시오.
2. 파일 맨 아래에서 'MAILER_DEFINITIONS'로 표시되는 행 위에 다음 코드를 배치하십시오.
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### sendmail.cf 재생성
sendmail.mc 파일은 실제(및 복잡한) sendmail.cf 구성 파일에 펼칠 수 있는 매크로의 콜렉션입니다. sendmail에서
변경사항에 액세스할 수 있도록 설정하려면 다음 m4 명령을 사용하여 sendmail.cf를 재생성하십시오.
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Sendmail 다시 시작
다음 명령을 사용하여 Sendmail을 다시 시작하십시오.
`service sendmail restart`

## 명령행 메일 유틸리티를 사용하여 테스트
다음 명령을 사용하여 변경사항을 테스트하십시오.
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
