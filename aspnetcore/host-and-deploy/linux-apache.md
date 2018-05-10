---
title: Apache를 사용하여 Linux에서 ASP.NET Core 호스트
description: Kestrel에서 실행 되는 ASP.NET Core 웹 앱에 HTTP 트래픽을 리디렉션하기 위해 Apache CentOS에 역방향 프록시 서버로 설정 하는 방법에 알아봅니다.
author: spboyer
manager: wpickett
ms.author: spboyer
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 473585f1be180645395c14a154c9c017ca50edab
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="host-aspnet-core-on-linux-with-apache"></a>Apache를 사용하여 Linux에서 ASP.NET Core 호스트

작성자: [Shayne Boyer](https://github.com/spboyer)

설정 하는 방법은이 가이드를 사용 하 여 [Apache](https://httpd.apache.org/) 에 역방향 프록시 서버로 [CentOS 7](https://www.centos.org/) 에서 실행 되는 ASP.NET Core 웹 앱에 HTTP 트래픽을 리디렉션하기 위해 [Kestrel](xref:fundamentals/servers/kestrel)합니다. [mod_proxy 확장](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 관련된 모듈 역방향 프록시 서버를 만듭니다.

## <a name="prerequisites"></a>전제 조건

1. Sudo 권한으로 표준 사용자 계정을 사용 하 여 CentOS 7을 실행 하는 서버
2. ASP.NET Core 응용 프로그램

## <a name="publish-the-app"></a>앱 게시

해당 응용 프로그램을 게시 한 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd) CentOS 7 런타임에 대 한 릴리스 구성에서 (`centos.7-x64`). 내용을 복사 하는 *bin/Release/netcoreapp2.0/centos.7-x64/publish* SCP, FTP 또는 기타 파일 전송 방법을 사용 하 여 서버에는 폴더입니다.

> [!NOTE]
> 프로덕션 배포 시나리오에서 연속 통합 워크플로 응용 프로그램을 게시 및 자산에서 서버로 복사 작업을 수행 합니다. 

## <a name="configure-a-proxy-server"></a>프록시 서버 구성

역방향 프록시는 동적 웹 앱을 처리 하기 위한 일반적인 설치. 역방향 프록시는 HTTP 요청을 종료 하 고 ASP.NET 응용 프로그램에 전달 합니다.

프록시 서버는 하나 자체 요청을 수행 하는 대신 다른 서버에 대 한 클라이언트 요청을 전달 합니다. 역방향 프록시는 일반적으로 임의의 클라이언트 대신 고정 대상에 전달됩니다. 이 가이드에서는 Apache Kestrel ASP.NET Core 응용 프로그램을 처리는 동일한 서버에서 실행 하는 역방향 프록시도 구성 됩니다.

전달 헤더 미들웨어를 사용 하 여 요청 역방향 프록시를 전달 하기 때문에 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지 합니다. 미들웨어 업데이트는 `Request.Scheme`를 사용 하 여는 `X-Forwarded-Proto` 헤더로, 해당 리디렉션 Uri 및 기타 보안 정책을 올바르게 작동 하도록 합니다.

모든 종류의 인증 미들웨어를 사용 하 여 전달 헤더 미들웨어 첫 번째 실행 해야 합니다. 이 순서 지정 하면 인증 미들웨어 헤더 값을 사용 하 고 올바른 리디렉션 Uri를 생성할 수 있습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어입니다. 미들웨어 전달 하도록 구성 된 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더:

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 및 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어입니다. 미들웨어 전달 하도록 구성 된 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더:

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

없는 경우 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 하도록 기본 헤더는 미들웨어를 지정 된 `None`합니다.

프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

### <a name="install-apache"></a>Apache 설치

CentOS 패키지를 안정적인 최신 버전으로 업데이트 합니다.

```bash
sudo yum update -y
```

단일 CentOS에 Apache 웹 서버를 설치 `yum` 명령:

```bash
sudo yum -y install httpd mod_ssl
```

명령을 실행 한 후 출력 샘플:

```bash
Downloading packages:
httpd-2.4.6-40.el7.centos.4.x86_64.rpm               | 2.7 MB  00:00:01
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 
Verifying  : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 

Installed:
httpd.x86_64 0:2.4.6-40.el7.centos.4

Complete!
```

> [!NOTE]
> 이 예제에서는 출력 CentOS 7 버전은 64 비트 이후 httpd.86_64을 반영 합니다. Apache를 설치한 위치를 확인하려면 명령 프롬프트에서 `whereis httpd`를 실행합니다.

### <a name="configure-apache-for-reverse-proxy"></a>역방향 프록시에 Apache 구성

Apache의 구성 파일은 `/etc/httpd/conf.d/` 디렉터리 내에 위치합니다. 모든 파일이 *.conf* 확장은 모듈 구성 파일 뿐 아니라 알파벳 순서로 처리 `/etc/httpd/conf.modules.d/`, 구성이 포함 된 모듈을 로드 하는 데 필요한 파일입니다.

명명 된 구성 파일을 만드는 *hellomvc.conf*, 응용 프로그램:

```
<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}hellomvc-error.log
    CustomLog ${APACHE_LOG_DIR}hellomvc-access.log common
</VirtualHost>
```

`VirtualHost` 블록은 서버에서 하나 이상의 파일에 여러 번 나타날 수 있습니다. 이전 구성 파일에서 Apache 포트 80에서 공용 트래픽을 허용합니다. 도메인 `www.example.com` 제공 하는 고 `*.example.com` 별칭 동일한 웹 사이트를 확인 합니다. 참조 [가상 호스트 이름 기반 지원](https://httpd.apache.org/docs/current/vhosts/name-based.html) 자세한 정보에 대 한 합니다. 요청은 127.0.0.1 서버 5000 포트로 루트에 프록시입니다. 양방향 통신을 위해 `ProxyPass` 및 `ProxyPassReverse` 필요 합니다.

> [!WARNING]
> 적절 한 입력 하지 않으면 [ServerName 지시문](https://httpd.apache.org/docs/current/mod/core.html#servername) 에 **VirtualHost** 블록 보안 취약성이 있는 응용 프로그램을 노출 합니다. 와일드 카드 바인딩 하위 도메인 (예를 들어 `*.example.com`) 전체 부모 도메인을 제어 하는 경우이 보안 위험을 노출 하지 않습니다 (반대인 `*.com`, 취약 한 변수인). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

당 로깅을 구성할 수 있습니다 `VirtualHost` 를 사용 하 여 `ErrorLog` 및 `CustomLog` 지시문입니다. `ErrorLog` 서버에서 오류를 기록 하는 위치는 위치 및 `CustomLog` 파일 이름 및 로그 파일의 형식을 설정 합니다. 이 경우 요청 정보를 기록 하는 위치입니다. 각 요청에 대 한 줄이 있습니다.

파일을 저장 하 고 구성을 테스트 합니다. 모든 항목이 통과하는 경우 응답은 `Syntax [OK]`이어야 합니다.

```bash
sudo service httpd configtest
```

Apache 다시 시작 합니다.

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a>응용 프로그램 모니터링

Apache에 대 한 요청을 전달 하도록 설정 되어 이제 `http://localhost:80` 에 Kestrel에서 실행 중인 ASP.NET Core 응용 프로그램에 `http://127.0.0.1:5000`합니다.  그러나 Apache Kestrel 프로세스를 관리할 수를 설정 되지 않습니다. 사용 하 여 *systemd* 을 시작 하 고 기본 웹 응용 프로그램 모니터링 서비스 파일을 만듭니다. *systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다. 


### <a name="create-the-service-file"></a>서비스 파일 만들기

서비스 정의 파일을 만듭니다.

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

응용 프로그램에 대 한 예제 서비스 파일:

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if dotnet service crashes
RestartSec=10
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

> [!NOTE]
> **사용자** &mdash; 경우 사용자 *apache* 는 사용 하지 않으며, 구성에서 사용자를 만든 다음 먼저 파일에 대 한 적절 한 소유권을 부여 합니다.

> [!NOTE]
> 환경 변수를 읽을 수는 구성 공급자에 대 한 일부 값 (예를 들어 SQL 연결 문자열)를 이스케이프 해야 합니다. 다음 명령을 사용 하 여 구성 파일에서 사용 하기 위해 올바르게 이스케이프 된 값을 생성 합니다.
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

파일을 저장 하 고 서비스를 활성화 합니다.

```bash
systemctl enable kestrel-hellomvc.service
```

서비스를 시작 하 고 실행 중인지 확인 합니다.

```bash
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

역방향 프록시 구성 및 통해 관리 되는 Kestrel *systemd*, 웹 응용 프로그램 구성 완벽 하 게 되 고 브라우저에서 로컬 컴퓨터에서 액세스할 수 `http://localhost`합니다. 응답 헤더를 검사 하는 **서버** 헤더 ASP.NET Core 응용 프로그램 Kestrel에 의해 제공 되는 나타냅니다.

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>로그 보기

웹 앱 이후 Kestrel를 사용 하 여 관리를 사용 하 여 *systemd*, 이벤트 및 프로세스 중앙 집중식된 저널에 기록 됩니다. 이 저널 모든 서비스 및 관리 하는 프로세스에 대 한 항목을 포함 하는 반면 *systemd*합니다. `kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

시간 필터링에 대 한 명령을 사용 하 여 시간 옵션을 지정 합니다. 사용 예를 들어 `--since today` 은 현재 날짜에 대 한 필터링 또는 `--until 1 hour ago` 이전 시간 항목을 볼 수 있습니다. 자세한 내용은 참조는 [journalctl 매뉴얼 페이지](https://www.unix.com/man-page/centos/1/journalctl/)합니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a>응용 프로그램 보안 설정

### <a name="configure-firewall"></a>방화벽 구성

*Firewalld* 네트워크 영역에 대 한 지원과 함께 방화벽을 관리 하는 동적 디먼은 합니다. 포트 및 패킷 필터링 여전히 iptables 하 여 관리할 수 있습니다. *Firewalld* 기본적으로 설치 해야 합니다. `yum` 패키지를 설치 하거나 설치 되었는지 확인 데 사용할 수 있습니다.

```bash
sudo yum install firewalld -y
```

사용 하 여 `firewalld` 를 응용 프로그램에 필요한 포트만 엽니다. 이 경우에는 포트 80 및 443을 사용합니다. 다음 명령 포트 80 및 443이 열을 영구적으로 설정:

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

방화벽 설정을 다시 로드 합니다. 사용 가능한 서비스 및 기본 영역에는 포트를 확인 합니다. 검사 하 여 옵션을 사용할 수 `firewall-cmd -h`합니다.

```bash 
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

```bash
public (default, active)
interfaces: eth0
sources: 
services: dhcpv6-client
ports: 443/tcp 80/tcp
masquerade: no
forward-ports: 
icmp-blocks: 
rich rules: 
```

### <a name="ssl-configuration"></a>SSL 구성

Apache ssl을 구성 하는 *mod_ssl* 모듈은 사용 됩니다. 경우는 *httpd* 모듈을 설치 하 되는 *mod_ssl* 모듈도 설치 되었습니다. 사용 하 여 설치 되지 않은 경우 `yum` 구성에 추가 합니다.

```bash
sudo yum install mod_ssl
```
SSL을 적용 하려면 설치는 `mod_rewrite` 모듈 URL 다시 쓰기를 사용 하도록 설정 하려면:

```bash
sudo yum install mod_rewrite
```

수정 된 *hellomvc.conf* URL 다시 쓰기를 사용 하도록 설정 하 고 포트 443에서 통신을 보호 하려면 파일:

```
<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/ [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> 이 예에서는 로컬로 생성 된 인증서를 사용 하는 합니다. **SSLCertificateFile** 도메인 이름에 대 한 기본 인증서 파일 이어야 합니다. **SSLCertificateKeyFile** 키 파일이 생성 되어야 CSR 만들어집니다. **SSLCertificateChainFile** (있는 경우) 중간 인증서 파일이 있어야 인증 기관에서 제공 된 이름입니다.

파일을 저장 하 고 구성을 테스트 합니다.

```bash
sudo service httpd configtest
```

Apache 다시 시작 합니다.

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a>추가 Apache 제안

### <a name="additional-headers"></a>추가 헤더

를 악의적인 공격 으로부터 보호 하기 위해 해야 수정 하거나 추가 헤더는 몇 가지가 있습니다. 확인 된 `mod_headers` 모듈은 설치:

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a>Apache clickjacking 공격 으로부터 보호

[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)라고도 하는 *UI redress 공격*, 여기서 웹 사이트 방문자는 스크립트가 속아 서 현재 방문 하는 것 보다 링크 또는 다른 페이지에 단추를 클릭 하는 악의적인 공격에는 합니다. 사용 하 여 `X-FRAME-OPTIONS` 사이트 보호를 합니다.

편집 된 *httpd.conf* 파일:

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

줄 추가 `Header append X-FRAME-OPTIONS "SAMEORIGIN"`합니다. 파일을 저장합니다. Apache를 다시 시작합니다.

#### <a name="mime-type-sniffing"></a>MIME 형식 검색

`X-Content-Type-Options` 헤더에서 Internet Explorer를 방지 *MIME 스니핑* (파일의 결정 `Content-Type` 파일의 내용을 사용). 서버를 설정 하는 경우는 `Content-Type` 헤더를 `text/html` 와 `nosniff` 으로 콘텐츠를 렌더링 하는 옵션 집합, Internet Explorer `text/html` 파일의 내용에 관계 없이 합니다.

편집 된 *httpd.conf* 파일:

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

줄 추가 `Header set X-Content-Type-Options "nosniff"`합니다. 파일을 저장합니다. Apache를 다시 시작합니다.

### <a name="load-balancing"></a>부하 분산 

이 예제에서는 동일한 인스턴스 컴퓨터에서 CentOS 7와 Kestrel의 Apache를 설정하고 구성하는 방법을 보여줍니다. 단일 실패 지점이 없는. 사용 하 여 *mod_proxy_balancer* 및 수정 된 **VirtualHost** Apache 프록시 서버 뒤에 있는 웹 응용 프로그램의 여러 인스턴스를 관리 하기 위한 허용 합니다.

```bash
sudo yum install mod_proxy_balancer
```

다른 인스턴스를 아래 표시 된 구성 파일에는 `hellomvc` 앱 5001이 고 포트에서 수행 되도록 설정 되어 있습니다. *프록시* 섹션은 부하 분산을 위해 두 멤버가 포함 된 분산 장치 구성으로 설정 된 *byrequests*합니다.

```
<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/ [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPass / balancer://mycluster/ 

    ProxyPassReverse / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5001/

    <Proxy balancer://mycluster>
        BalancerMember http://127.0.0.1:5000
        BalancerMember http://127.0.0.1:5001 
        ProxySet lbmethod=byrequests
    </Proxy>

    <Location />
        SetHandler balancer
    </Location>
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a>속도 제한
사용 하 여 *mod_ratelimit*에 포함 되어 있는 *httpd* 모듈의 클라이언트는 대역폭 제한 될 수 있습니다.

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
예제 파일은 루트 위치 아래의 600 KB/sec로 대역폭을 제한합니다.

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```
