---
title: Apache를 사용하여 Linux에서 ASP.NET Core 호스트
description: CentOS에서 Apache를 역방향 프록시 서버로 설정하여 Kestrel에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 리디렉션하는 방법을 알아봅니다.
author: spboyer
ms.author: spboyer
ms.custom: mvc
ms.date: 09/08/2018
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 534e0415b2d278a518aea0ecb8042aeab4a0aa0e
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523209"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a>Apache를 사용하여 Linux에서 ASP.NET Core 호스트

작성자: [Shayne Boyer](https://github.com/spboyer)

이 가이드를 사용하여 [CentOS 7](https://www.centos.org/)에서 [Apache](https://httpd.apache.org/)를 역방향 프록시 서버로 설정하여 [Kestrel](xref:fundamentals/servers/kestrel)에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 리디렉션하는 방법을 알아봅니다. [mod_proxy 확장](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 및 관련 모듈은 서버의 역방향 프록시를 만듭니다.

## <a name="prerequisites"></a>전제 조건

1. sudo 권한을 가진 표준 사용자 계정으로 CentOS 7을 실행하는 서버가 필요합니다.
1. 서버에서 .NET Core 런타임을 설치합니다.
   1. [.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)로 이동합니다.
   1. **런타임** 아래의 목록에서 최신 미리 보기 상태가 아닌 런타임을 선택합니다.
   1. CentOS/Oracle에 대한 지침을 선택하고 따릅니다.
1. 기존 ASP.NET Core 앱입니다.

## <a name="publish-and-copy-over-the-app"></a>앱 게시 및 복사

[프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우 앱을 구성합니다.

서버에서 실행할 수 있는 디렉터리(예: *bin/Release/&lt;target_framework_moniker&gt;/publish*)로 앱을 패키징하기 위해 개발 환경에서 [dotnet publish](/dotnet/core/tools/dotnet-publish)를 실행합니다.

```console
dotnet publish --configuration Release
```

.NET Core 런타임을 서버에서 유지 관리하지 않으려는 경우 앱은 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)로 게시될 수도 있습니다.

조직의 워크플로에 통합된 도구(예: SCP, SFTP)를 사용하여 ASP.NET Core 앱을 서버에 복사합니다. *var* 디렉터리(예: *var/aspnetcore/hellomvc*)에서 웹앱을 찾는 것이 일반적입니다.

> [!NOTE]
> 프로덕션 배포 시나리오에서 지속적인 통합 워크플로는 앱을 게시하고 자산을 서버로 복사하는 워크플로를 수행합니다.

## <a name="configure-a-proxy-server"></a>프록시 서버 구성

역방향 프록시는 동적 웹앱을 지원하기 위한 일반적인 설정입니다. 역방향 프록시는 HTTP 요청을 종료하고 이 요청을 ASP.NET 앱에 전달합니다.

프록시 서버는 클라이언트 요청을 자체 수행하는 대신 다른 서버에 전달하는 서버입니다. 역방향 프록시는 일반적으로 임의의 클라이언트 대신 고정 대상에 전달됩니다. 이 가이드에서 Apache는 Kestrel이 ASP.NET Core 앱을 제공하는 동일한 서버에서 실행되는 역방향 프록시로 구성됩니다.

요청이 역방향 프록시를 통해 전달되므로 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 [전달된 헤더 미들웨어](xref:host-and-deploy/proxy-load-balancer)를 사용합니다. 이 미들웨어는 `X-Forwarded-Proto` 헤더를 사용하여 `Request.Scheme`을 업데이트하므로 리디렉션 URI 및 기타 보안 정책이 제대로 작동합니다.

전달된 헤더 미들웨어를 호출한 후에 인증, 링크 생성, 리디렉션 및 지리적 위치 등 체계에 따라 달라지는 구성 요소를 배치해야 합니다. 일반 규칙으로 전달된 헤더 미들웨어는 진단 및 오류 처리 미들웨어를 제외한 다른 미들웨어 전에 실행해야 합니다. 이 순서를 지정하면 전달된 헤더 정보에 따라 달라지는 미들웨어는 처리하기 위해 헤더 값을 사용할 수 있습니다.

::: moniker range=">= aspnetcore-2.0"

> [!NOTE]
> &mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

::: moniker-end

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다. `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity)와 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다. `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.

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

미들웨어에 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 지정되지 않은 경우 전달할 기본 헤더는 `None`입니다.

localhost(127.0.0.1, [::1])에서 실행되는 프록시만 기본적으로 신뢰됩니다. 조직 내의 다른 신뢰할 수 있는 프록시 또는 네트워크가 인터넷과 웹 서버 간의 요청을 처리하는 경우 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>를 사용하여 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> 또는 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> 목록에 추가합니다. 다음 예제는 IP 주소 10.0.0.100의 신뢰할 수 있는 프록시 서버를 `Startup.ConfigureServices`의 전달된 헤더 미들웨어 `KnownProxies`에 추가합니다.

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.

### <a name="install-apache"></a>Apache 설치

CentOS 패키지를 안정적인 최신 버전으로 업데이트합니다.

```bash
sudo yum update -y
```

단일 `yum` 명령을 사용하여 CentOS에 Apache 웹 서버를 설치합니다.

```bash
sudo yum -y install httpd mod_ssl
```

명령을 실행한 후 샘플 출력은 다음과 같습니다.

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
> 이 예제에서 CentOS 7 버전은 64비트이므로 출력에는 httpd.86_64가 반영됩니다. Apache를 설치한 위치를 확인하려면 명령 프롬프트에서 `whereis httpd`를 실행합니다.

### <a name="configure-apache"></a>Apache 구성

Apache의 구성 파일은 `/etc/httpd/conf.d/` 디렉터리 내에 위치합니다. `/etc/httpd/conf.modules.d/`의 모듈 구성 파일 외에도 *.conf* 확장을 포함한 모든 파일은 알파벳순으로 처리됩니다. 여기에는 모듈을 로드하는 데 필요한 구성 파일도 포함됩니다.

앱에 대해 *hellomvc.conf*라는 구성 파일을 만듭니다.

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

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

`VirtualHost` 블록은 서버에 있는 하나 이상의 파일에 여러 번 나타날 수 있습니다. 이전 구성 파일에서 Apache는 포트 80에서 공용 트래픽을 허용합니다. 도메인 `www.example.com`을 제공하고 있고 `*.example.com` 별칭이 동일한 웹 사이트로 확인됩니다. 자세한 내용은 [Name-based virtual host support](https://httpd.apache.org/docs/current/vhosts/name-based.html)(이름 기반 가상 호스트 지원)를 참조하세요. 요청은 127.0.0.1에 있는 서버의 포트 5000에 대한 루트에서 프록시 처리됩니다. 양방향 통신의 경우 `ProxyPass` 및 `ProxyPassReverse`가 필요합니다. Kestrel의 IP/포트를 변경 하려면 [Kestrel: 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조합니다.

> [!WARNING]
> **VirtualHost** 블록에서 적절한 [ServerName 지시문](https://httpd.apache.org/docs/current/mod/core.html#servername)을 지정하지 않으면 앱이 보안 취약성에 노출됩니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.example.com`)에는 이러한 보안 위험이 발생하지 않습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

로깅은 `ErrorLog` 및 `CustomLog` 지시문을 사용하여 `VirtualHost`별로 구성할 수 있습니다. `ErrorLog`는 서버가 오류를 기록하는 위치이고 `CustomLog`는 로그 파일의 파일 이름과 형식을 설정합니다. 이 경우에는 요청 정보가 기록되는 위치입니다. 각 요청이 한 줄에 기록됩니다.

파일을 저장하고 구성을 테스트합니다. 모든 항목이 통과하는 경우 응답은 `Syntax [OK]`이어야 합니다.

```bash
sudo service httpd configtest
```

Apache를 다시 시작합니다.

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a>앱 모니터링

이제 Apache는 `http://localhost:80`에 대해 실행된 요청을 `http://127.0.0.1:5000`의 Kestrel에서 실행되는 ASP.NET Core 앱에 전달하도록 설정됩니다.  그러나 Apache는 Kestrel 프로세스를 관리하도록 설정되지 않습니다. *systemd*를 사용하고 서비스 파일을 만들어 기본 웹앱을 시작하고 모니터링합니다. *systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다. 

### <a name="create-the-service-file"></a>서비스 파일 만들기

서비스 정의 파일을 만듭니다.

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

앱의 예제 서비스 파일:

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

사용자 *apache*가 구성에서 사용되지 않을 경우 사용자를 먼저 만들고 적절한 파일 소유권을 부여해야 합니다.

`TimeoutStopSec`를 사용하여 초기 인터럽트 신호를 받은 후 앱이 종료되기를 기다리는 기간을 구성합니다. 이 기간 내에 앱이 종료되지 않으면 앱을 종료하기 위해 SIGKILL이 실행됩니다. 단위 없는 초로 된 값(예: `150`) 또는 시간 범위 값(예: `2min 30s`)으로 값을 입력하거나, 시간 제한을 사용하지 않으려면 `infinity`를 입력합니다. `TimeoutStopSec`의 기본값은 관리자 구성 파일(*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*)의 `DefaultTimeoutStopSec` 값입니다. 대부분의 배포에서 기본 시간 제한은 90초입니다.

```
# The default value is 90 seconds for most distributions.
TimeoutStopSec=90
```

일부 값(예: SQL 연결 문자열)은 환경 변수를 읽기 위해 구성 공급자에 대해 이스케이프되어야 합니다. 다음 명령을 사용하여 구성 파일에서 사용할 제대로 이스케이프된 값을 생성합니다.

```console
systemd-escape "<value-to-escape>"
```

파일을 저장하고 서비스를 사용하도록 설정합니다.

```bash
sudo systemctl enable kestrel-hellomvc.service
```

서비스를 시작하고 실행 중인지 확인합니다.

```bash
sudo systemctl start kestrel-hellomvc.service
sudo systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

역방향 프록시를 구성하고 *systemd*를 통해 Kestrel을 관리하면 웹앱이 완전히 구성되고 로컬 컴퓨터(`http://localhost`)의 브라우저에서 웹앱에 액세스할 수 있습니다. 응답 헤더를 검사하는 **Server** 헤더는 ASP.NET Core 앱이 Kestrel에서 제공됨을 나타냅니다.

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>로그 보기

Kestrel을 사용하는 웹앱은 *systemd*를 사용하여 관리되므로 이벤트 및 프로세스가 중앙형 저널에 기록됩니다. 그러나 이 저널에는 *systemd*에서 관리하는 모든 서비스 및 프로세스에 대한 항목이 포함됩니다. `kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

시간 필터링의 경우 명령을 사용하여 시간 옵션을 지정합니다. 예를 들어 `--since today`를 사용하여 현재 날짜를 기준으로 필터링하거나 `--until 1 hour ago`를 사용하여 이전 시간의 항목을 확인합니다. 자세한 내용은 [journalctl에 대한 기본 페이지](https://www.unix.com/man-page/centos/1/journalctl/)를 참조하세요.

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a>데이터 보호

[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/index)은 인증 미들웨어(예: 쿠키 미들웨어) 및 CSRF(교차 사이트 요청 위조) 보호를 비롯한 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에 사용됩니다. 사용자 코드에서 데이터 보호 API가 호출되지 않더라도 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다. 데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.

키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.

* 모든 쿠키 기반 인증 토큰이 무효화됩니다.
* 사용자는 다음 요청에서 다시 로그인해야 합니다.
* 키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다. 여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.

키 링을 유지하고 암호화하도록 데이터 보호를 구성하려면 다음을 참조하십시오.

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="securing-the-app"></a>앱 보안

### <a name="configure-firewall"></a>방화벽 구성

*Firewalld*는 네트워크 영역에 대한 지원을 통해 방화벽을 관리하는 동적 디먼입니다. 포트 및 패킷 필터링은 iptables로 계속 관리할 수 있습니다. *Firewalld*는 기본적으로 설치해야 합니다. `yum`을 사용하여 패키지를 설치하거나 설치되었는지 확인할 수 있습니다.

```bash
sudo yum install firewalld -y
```

`firewalld`를 사용하여 앱에 필요한 포트만 엽니다. 이 경우에는 포트 80 및 443을 사용합니다. 다음 명령은 포트 80 및 443이 영구적으로 열리도록 설정합니다.

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

방화벽 설정을 다시 로드합니다. 기본 영역의 사용 가능한 서비스 및 포트를 확인합니다. `firewall-cmd -h`를 검사하여 옵션을 사용할 수 있습니다.

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

SSL에 Apache를 구성하려면 *mod_ssl* 모듈을 사용합니다. *httpd* 모듈이 설치될 때 *mod_ssl* 모듈도 설치되었습니다. 설치되지 않은 경우 `yum`을 사용하여 구성에 추가합니다.

```bash
sudo yum install mod_ssl
```

SSL을 적용하려면 URL 재작성을 사용할 수 있도록 `mod_rewrite` 모듈을 설치합니다.

```bash
sudo yum install mod_rewrite
```

포트 443에서 URL 재작성 및 보안 통신을 사용할 수 있도록 *hellomvc.conf* 파일을 수정합니다.

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
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
> 이 예제에서는 로컬로 생성된 인증서를 사용합니다. **SSLCertificateFile**은 도메인 이름에 대한 기본 인증서 파일이어야 합니다. **SSLCertificateKeyFile**은 CSR을 만들 때 생성된 키 파일이어야 합니다. **SSLCertificateChainFile**은 인증 기관에서 제공된 중간 인증서 파일(있는 경우)이어야 합니다.

파일을 저장하고 구성을 테스트합니다.

```bash
sudo service httpd configtest
```

Apache를 다시 시작합니다.

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a>추가 Apache 제안

### <a name="additional-headers"></a>추가 헤더

악의적인 공격으로부터 보호하기 위해 몇 가지 헤더를 수정하거나 추가해야 합니다. `mod_headers` 모듈이 설치되었는지 확인합니다.

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a>클릭재킹(clickjacking) 공격으로부터 Apache 보호

또한 ‘UI 교정 공격’이라고도 하는[클릭재킹(Clickjacking)](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)은 웹 사이트 방문자를 속여서 현재 방문 중인 것과 다른 페이지에서 링크 또는 단추를 클릭하게 하는 악의적인 공격입니다. `X-FRAME-OPTIONS`를 사용하여 사이트를 보호합니다.

*httpd.conf* 파일을 편집합니다.

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

`Header append X-FRAME-OPTIONS "SAMEORIGIN"` 줄을 추가합니다. 파일을 저장합니다. Apache를 다시 시작합니다.

#### <a name="mime-type-sniffing"></a>MIME 형식 검색

`X-Content-Type-Options` 헤더는 Internet Explorer에서 ‘MIME 스니핑’을 방지합니다(파일 콘텐츠에서 파일의 `Content-Type` 확인). 서버에서 `nosniff` 옵션 집합을 사용하여 `Content-Type` 헤더를 `text/html`로 설정하는 경우 Internet Explorer는 파일 콘텐츠에 관계없이 콘텐츠를 `text/html`로 렌더링합니다.

*httpd.conf* 파일을 편집합니다.

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

`Header set X-Content-Type-Options "nosniff"` 줄을 추가합니다. 파일을 저장합니다. Apache를 다시 시작합니다.

### <a name="load-balancing"></a>부하 분산

이 예제에서는 동일한 인스턴스 컴퓨터에서 CentOS 7와 Kestrel의 Apache를 설정하고 구성하는 방법을 보여줍니다. 단일 실패 지점이 없도록 하기 위해 *mod_proxy_balancer*를 사용하고 **VirtualHost**를 수정하면 Apache 프록시 서버 뒤에 있는 웹앱의 여러 인스턴스를 관리할 수 있습니다.

```bash
sudo yum install mod_proxy_balancer
```

아래 표시된 구성 파일에서 `hellomvc` 앱의 추가 인스턴스는 포트 5001에서 실행되도록 설정됩니다. *Proxy* 섹션은 *byrequests*의 부하를 분산하는 두 개의 멤버가 있는 분산 장치 구성을 사용하여 설정됩니다.

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
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

*httpd* 모듈에 포함된 *mod_ratelimit*을 사용하여 클라이언트의 대역폭을 제한할 수 있습니다.

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
예제 파일에서는 루트 위치 아래에서 대역폭을 600KB/초로 제한합니다.

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```

## <a name="additional-resources"></a>추가 자료

* [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)
