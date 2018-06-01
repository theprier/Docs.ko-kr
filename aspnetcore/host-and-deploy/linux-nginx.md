---
title: Nginx를 사용하여 Linux에서 ASP.NET Core 호스트
author: rick-anderson
description: Ubuntu 16.04에서 Nginx를 역방향 프록시로 설정하여 Kestrel에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 전달하는 방법을 설명합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: d37aa25c712d715aa4134587a84e5923f9cb5b79
ms.sourcegitcommit: 50d40c83fa641d283c097f986dde5341ebe1b44c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34452557"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a>Nginx를 사용하여 Linux에서 ASP.NET Core 호스트

작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다.

> [!NOTE]
> Ubuntu 14.04의 경우 Kestrel 프로세스를 모니터링하기 위한 솔루션으로 *supervisord*를 사용하는 것이 좋습니다. *systemd*는 Ubuntu 14.04에서 사용할 수 없습니다. [이 문서의 이전 버전을 참조하세요](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).

이 가이드의 내용:

* 기존 ASP.NET Core 앱을 역방향 프록시 서버 뒤에 배치합니다.
* 역방향 프록시 서버를 설정하여 Kestrel 웹 서버에 요청을 전달합니다.
* 웹앱이 시작 시 디먼으로 실행되는지 확인합니다.
* 웹앱 다시 시작을 지원하도록 프로세스 관리 도구를 구성합니다.

## <a name="prerequisites"></a>전제 조건

1. sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스
1. 기존 ASP.NET Core 앱

## <a name="copy-over-the-app"></a>앱을 통해 복사

개발 환경에서 [dotnet publish](/dotnet/core/tools/dotnet-publish)를 실행하여 앱을 서버에서 실행될 수 있는 자체 포함된 디렉터리로 패키지합니다.

무엇이든 조직의 워크플로에 통합된 도구(예: SCP, FTP)를 사용하여 ASP.NET Core 앱을 서버에 복사합니다. 다음과 같이 앱을 테스트합니다.

* 명령줄에서 `dotnet <app_assembly>.dll`을 실행합니다.
* 브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 작동하는지 확인합니다. 
 
## <a name="configure-a-reverse-proxy-server"></a>역방향 프록시 서버 구성

역방향 프록시는 동적 웹앱을 지원하기 위한 일반적인 설정입니다. 역방향 프록시는 HTTP 요청을 종료하고 이 요청을 ASP.NET Core 앱에 전달합니다.

### <a name="why-use-a-reverse-proxy-server"></a>역방향 프록시 서버를 사용하는 이유는 무엇인가요?

Kestrel은 ASP.NET Core에서 동적 콘텐츠를 제공하는 데 유용합니다. 그러나 웹 지원 기능은 IIS, Apache 또는 Nginx와 같은 서버만큼 기능이 다양하지 않습니다. 역방향 프록시 서버는 정적 콘텐츠 지원, 요청 캐시, 요청 압축 및 HTTP 서버에서 SSL 종료 같은 작업을 오프로드할 수 있습니다. 역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.

이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다. 이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다. 요구 사항에 따라 다른 설정을 선택할 수 있습니다.

요청이 역방향 프록시를 통해 전달되므로 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 전달된 헤더 미들웨어를 사용합니다. 이 미들웨어는 `X-Forwarded-Proto` 헤더를 사용하여 `Request.Scheme`을 업데이트하므로 리디렉션 URI 및 기타 보안 정책이 제대로 작동합니다.

인증 미들웨어 유형을 사용하는 경우에는 전달된 헤더 미들웨어를 먼저 실행해야 합니다. 이렇게 순서를 지정하면 인증 미들웨어가 헤더 값을 사용하고 올바른 리디렉션 URI를 생성할 수 있습니다.

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

프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

### <a name="install-nginx"></a>Nginx 설치

```bash
sudo apt-get install nginx
```

> [!NOTE]
> 선택적 Nginx 모듈이 설치될 경우 소스에서 Nginx를 빌드해야 할 수 있습니다.

`apt-get`을 사용하여 Nginx를 설치합니다. 설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 System V init 스크립트를 만듭니다. Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.

```bash
sudo service nginx start
```

브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다.

### <a name="configure-nginx"></a>Nginx 구성

Nginx를 역방향 프록시로 구성하여 요청을 ASP.NET Core 앱에 프로그램에 전달하려면 */etc/nginx/sites-available/default*를 수정합니다. 텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $http_host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

`server_name`이 일치하지 않으면 Nginx는 기본 서버를 사용합니다. 기본 서버가 정의되지 않은 경우 구성 파일의 첫 번째 서버는 기본 서버입니다. 구성 파일에 있는 444 상태 코드를 반환하는 특정 기본 서버를 추가하는 것이 좋습니다. 기본 서버 구성 예제는 다음과 같습니다.

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

이전 구성 파일과 기본 서버를 사용하여 Nginx는 포트 80에서 호스트 헤더 `example.com` 또는 `*.example.com`가 포함된 공용 트래픽을 허용합니다. 이러한 호스트와 일치하지 않는 요청은 Kestrel로 전달되지 않습니다. Nginx는 일치하는 요청을 `http://localhost:5000`의 Kestrel에 전달합니다. 자세한 내용은 [How nginx processes a request](https://nginx.org/docs/http/request_processing.html)(nginx가 요청을 처리하는 방법)를 참조하세요.

> [!WARNING]
> 적절한 [server_name 지시문](https://nginx.org/docs/http/server_names.html)을 지정하지 않으면 앱이 보안 취약성에 노출됩니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.example.com`)에는 이러한 보안 위험이 발생하지 않습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

Nginx 구성이 설정되면 `sudo nginx -t`를 실행하여 구성 파일의 구문을 확인합니다. 구성 파일 테스트에 성공하면 `sudo nginx -s reload`를 실행하여 Nginx가 변경 내용을 선택하도록 합니다.

## <a name="monitoring-the-app"></a>앱 모니터링

서버는 `http://<serveraddress>:80`에 대해 실행된 요청을 `http://127.0.0.1:5000`의 Kestrel에서 실행되는 ASP.NET Core 앱에 전달하도록 설정됩니다. 그러나 Nginx는 Kestrel 프로세스를 관리하도록 설정되지 않습니다. *systemd*를 사용하여 기본 웹앱을 시작 및 모니터링하기 위한 서비스 파일을 만들 수 있습니다. *systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다. 

### <a name="create-the-service-file"></a>서비스 파일 만들기

서비스 정의 파일을 만듭니다.

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

앱에 대한 예제 서비스 파일은 다음과 같습니다.

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

사용자 *www-data*가 구성에서 사용되지 않을 경우 여기서 정의된 사용자를 먼저 만들고 파일에 대한 적절한 소유권을 제공해야 합니다.

Linux에는 대/소문자를 구분하는 파일 시스템이 있습니다. ASPNETCORE_ENVIRONMENT를 “프로덕션”으로 설정하면 *appsettings.production.json* 대신 구성 파일 *appsettings.Production.json*을 검색합니다.

> [!NOTE]
> 일부 값(예: SQL 연결 문자열)은 환경 변수를 읽기 위해 구성 공급자에 대해 이스케이프되어야 합니다. 다음 명령을 사용하여 구성 파일에서 사용할 제대로 이스케이프된 값을 생성합니다.
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

파일을 저장하고 서비스를 사용하도록 설정합니다.

```bash
systemctl enable kestrel-hellomvc.service
```

서비스를 시작하고 실행 중인지 확인합니다.

```
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

역방향 프록시를 구성하고 systemd를 통해 Kestrel을 관리하면 웹앱이 완전히 구성되고 로컬 컴퓨터(`http://localhost`)의 브라우저에서 웹앱에 액세스할 수 있습니다. 차단 중인 방화벽이 없다면 원격 컴퓨터에서 액세스할 수도 있습니다. 응답 헤더를 검사하는 `Server` 헤더는 Kestrel에서 지원하는 ASP.NET Core 앱을 보여줍니다.

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>로그 보기

Kestrel을 사용하는 웹앱은 `systemd`를 사용하여 관리되므로 모든 이벤트 및 프로세스가 중앙형 저널에 기록됩니다. 그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다. `kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a>앱 보안

### <a name="enable-apparmor"></a>AppArmor 사용

LSM(Linux Security Modules)은 Linux 2.6 이후 Linux 커널에 포함된 프레임워크입니다. LSM은 보안 모듈의 다양한 구현을 지원합니다. [AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다. AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.

### <a name="configuring-the-firewall"></a>방화벽 구성

사용되지 않는 모든 외부 포트를 닫습니다. 복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다. `ufw`가 필요한 모든 포트에서 트래픽을 허용하도록 구성되어 있는지 확인합니다.

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a>Nginx 보안

Nginx의 기본 배포 시에는 SSL이 사용하도록 설정되지 않습니다. 추가 보안 기능을 사용하도록 설정하려면 소스에서 빌드합니다.

#### <a name="download-the-source-and-install-the-build-dependencies"></a>소스 다운로드 및 빌드 종속성 설치

```bash
# Install the build dependencies
sudo apt-get update
sudo apt-get install build-essential zlib1g-dev libpcre3-dev libssl-dev libxslt1-dev libxml2-dev libgd2-xpm-dev libgeoip-dev libgoogle-perftools-dev libperl-dev

# Download Nginx 1.10.0 or latest
wget http://www.nginx.org/download/nginx-1.10.0.tar.gz
tar zxf nginx-1.10.0.tar.gz
```

#### <a name="change-the-nginx-response-name"></a>Nginx 응답 이름 변경

*src/http/ngx_http_header_filter_module.c*를 편집합니다.

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-the-options-and-build"></a>옵션 구성 및 빌드

정규식의 경우 PCRE 라이브러리가 필요합니다. 정규식은 ngx_http_rewrite_module에 대한 위치 지시문에서 사용됩니다. http_ssl_module은 HTTPS 프로토콜 지원을 추가합니다.

*ModSecurity* 같은 웹앱 방화벽을 사용하여 앱을 강화해 보세요.

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a>SSL 구성

* 신뢰할 수 있는 CA(인증 기관)에서 발급된 유효한 인증서를 지정하여 포트 `443`에서 HTTPS 트래픽을 수신 대기하도록 서버를 구성합니다.

* 다음 */etc/nginx/nginx.conf* 파일에 설명된 일부 사례를 채택하여 보안을 강화합니다. 예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.

* HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청에 HTTPS만 사용됩니다.

* Strict-Transport-Security 헤더를 추가하지 않거나, 나중에 SSL을 사용하지 않도록 설정할 경우 적절한 `max-age`를 선택합니다.

*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.

[!code-nginx[](linux-nginx/proxy.conf)]

*/etc/nginx/nginx.conf* 구성 파일을 편집합니다. 예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a>클릭재킹(clickjacking)으로부터 Nginx 보호
클릭재킹은 감염된 사용자의 클릭을 수집하는 악의적인 기술입니다. 클릭재킹은 희생자(방문자)를 속여서 감염된 사이트를 클릭하게 합니다. X-FRAME-OPTIONS를 사용하여 사이트를 보호합니다.

*nginx.conf* 파일을 편집합니다.

```bash
sudo nano /etc/nginx/nginx.conf
```

줄 `add_header X-Frame-Options "SAMEORIGIN";`을 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.

#### <a name="mime-type-sniffing"></a>MIME 형식 검색

이 헤더는 응답 콘텐츠 형식을 재정의하지 않도록 브라우저에 지시하므로 대부분의 브라우저에서 선언된 콘텐츠 형식이 아닌 응답에 대한 MIME 검색을 차단합니다. `nosniff` 옵션을 사용하면 서버에 콘텐츠가 “text/html”이라고 표시될 경우 브라우저는 콘텐츠를 “text/html”으로 렌더링합니다.

*nginx.conf* 파일을 편집합니다.

```bash
sudo nano /etc/nginx/nginx.conf
```

줄 `add_header X-Content-Type-Options "nosniff";`를 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.
