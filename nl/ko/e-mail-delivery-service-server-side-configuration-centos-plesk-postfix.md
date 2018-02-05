---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 이메일 전송 서비스 서버 측 구성: CentOS, Plesk 및 Postfix

## 개요

다음은 {{site.data.keyword.SendGrid}}, 즉 {{site.data.keyword.cloud}} 이메일 전송 서비스를 스마트 호스트로 사용하도록 서버를 구성하는 단계입니다. 다음 예제는 Plesk 12 및 Postfix가 포함된 CentOS 6.5의 표준 {{site.data.keyword.cloud}} OS 재로드에서 수행되었습니다.

## 구성

1.  Postfix 구성 파일을 찾으십시오. 보통 /etc/postfix/main.cf에 있습니다.
2.  텍스트 편집기를 사용하여 main.cf 파일을 열고 구성에 다음을 추가하십시오.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  /etc/postfix/main.cf 파일을 저장하고 닫으십시오.
4.  다음 명령을 사용하여 postfix를 다시 시작하십시오.

  `/etc/init.d/postfix restart`

## 문제점 해결

1.  "사용 가능한 메커니즘이 없음" 오류가 발생한 경우 인증/암호화에 필요한 모든 라이브러리가 있는지 확인하십시오. 다음 명령을 사용하여 이러한 라이브러리를 설치할 수 있습니다.

  Debian/Ubuntu의 경우:  `apt-get install libsasl2-modules`

  Redhat/CentOS의 경우: `yum install cyrus-sasl-plain`

  이러한 라이브러리를 설치한 후 동일한 다시 시작 명령을 실행하십시오.

    /etc/init.d/postfix restart

2.  포트 587이 작동되지 않는 경우 postfix 구성에서 포트 2525를 사용하십시오. 또한 구성 파일 /etc/postfix/main.cf를 열고 다음 행을 주석 해제해야 합니다.

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
