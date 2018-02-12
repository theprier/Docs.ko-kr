---
title: "Nginx를 사용하여 Linux에서 ASP.NET Core 호스트"
author: rick-anderson
description: "Ubuntu 16.04 Kestrel에서 실행 되는 ASP.NET Core 웹 앱에 대 한 HTTP 트래픽을 전달 하도록에 역방향 프록시로 Nginx를 설정 하는 방법을 설명 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 08/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: 1044a87a4dcc7636413078b0fc09ade206c97d0a
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a>Nginx를 사용하여 Linux에서 ASP.NET Core 호스트

작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다.

**참고:** Ubuntu 14.04에 대 한 *supervisord* Kestrel 프로세스를 모니터링 하기 위한 솔루션으로 것이 좋습니다. *systemd* Ubuntu 14.04에서 사용할 수 없습니다. [이 문서의 이전 버전을 참조하세요](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).

이 가이드의 내용:

* 역방향 프록시 서버로 보호 하는 기존 ASP.NET Core 응용 프로그램을 배치합니다.
* Kestrel 웹 서버에 요청 전달 하는 역방향 프록시 서버를 설정 합니다.
* 디먼 시작 시에 실행 하는 웹 응용 프로그램을 확인 합니다.
* 웹 앱을 다시 시작 하려면 프로세스 관리 도구를 구성 합니다.

## <a name="prerequisites"></a>필수 구성 요소

1. sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스
1. 기존 ASP.NET Core 응용 프로그램

## <a name="copy-over-the-app"></a>응용 프로그램을 통해 복사

개발 환경에서 `dotnet publish`를 실행하여 앱을 서버에서 실행될 수 있는 자체 포함된 디렉터리로 패키지합니다.

ASP.NET Core 응용 프로그램 (예: SCP, FTP) 조직의 워크플로로 통합 하는 어떤 도구를 사용 하 여 서버에 복사 합니다. 다음과 같이 앱을 테스트합니다.

* 명령줄에서 실행 `dotnet <app_assembly>.dll`합니다.
* 브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 작동하는지 확인합니다. 
 
## <a name="configure-a-reverse-proxy-server"></a>역방향 프록시 서버 구성

역방향 프록시는 동적 웹 앱을 처리 하기 위한 일반적인 설치. 역방향 프록시는 HTTP 요청을 종료 하 고 ASP.NET Core 응용 프로그램에 전달 합니다.

### <a name="why-use-a-reverse-proxy-server"></a>역방향 프록시 서버를 사용하는 이유는 무엇인가요?

Kestrel은 ASP.NET Core에서 동적 콘텐츠를 처리 하기 위한 훌륭한입니다. 그러나 웹 서비스 기능으로 IIS, Apache 또는 Nginx 등의 서버 기능 풍부한으로 되지 않습니다. 역방향 프록시 서버는 정적 콘텐츠를 처리, 요청을 캐시 하 고, 요청, 및 HTTP 서버에서 SSL 종료를 압축 하는 등의 작업을 줄일 수 있습니다. 역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.

이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다. 이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다. 다른 설치 요구 사항에 따라 선택한을 수 있습니다.

전달 헤더 미들웨어를 사용 하 여 요청 역방향 프록시를 전달 하기 때문에 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지 합니다. 미들웨어 업데이트는 `Request.Scheme`를 사용 하 여는 `X-Forwarded-Proto` 헤더로, 해당 리디렉션 Uri 및 기타 보안 정책을 올바르게 작동 하도록 합니다.

모든 종류의 인증 미들웨어를 사용 하 여 전달 헤더 미들웨어 첫 번째 실행 해야 합니다. 이 순서 지정 하면 인증 미들웨어 헤더 값을 사용 하 고 올바른 리디렉션 Uri를 생성할 수 있습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어:

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 및 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어:

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

### <a name="install-nginx"></a>Nginx 설치

```bash
sudo apt-get install nginx
```

> [!NOTE]
> 선택적 Nginx 모듈 설치 되는 경우에 원본에서 Nginx 구축 필요할 수 있습니다.

`apt-get`을 사용하여 Nginx를 설치합니다. 설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 System V init 스크립트를 만듭니다. Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.

```bash
sudo service nginx start
```

브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다.

### <a name="configure-nginx"></a>Nginx 구성

요청을 전달 우리의 ASP.NET Core 응용 프로그램에 역방향 프록시로 Nginx을 구성 하려면 수정 `/etc/nginx/sites-available/default`합니다. 텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.

```
server {
    listen 80;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $http_host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

이 Nginx 구성 파일은 들어오는 공용 트래픽을 포트 `80`에서 포트 `5000`으로 전달합니다.

Nginx 구성, 설정 되 면 실행 `sudo nginx -t` 구성 파일의 구문을 확인 합니다. 구성 파일 테스트에 성공한 경우 강제로 실행 하 여 변경 내용을 적용 하려면 Nginx `sudo nginx -s reload`합니다.

## <a name="monitoring-the-app"></a>응용 프로그램 모니터링

서버에 대 한 요청을 전달 하도록 설치가 `http://<serveraddress>:80` 에 Kestrel에서 실행 중인 ASP.NET Core 응용 프로그램에 로그온 `http://127.0.0.1:5000`합니다. 그러나 Nginx Kestrel 프로세스를 관리할 수를 설정 되지 않습니다. *systemd* 시작 하 고 기본 웹 응용 프로그램 모니터링 서비스 파일을 만드는 데 사용할 수 있습니다. *systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다. 

### <a name="create-the-service-file"></a>서비스 파일 만들기

서비스 정의 파일을 만듭니다.

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

다음은 응용 프로그램에 대 한 서비스 파일의 예입니다.

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

**참고:** 경우 사용자 *www 데이터* 사용 되지 않는 구성, 여기에 정의 된 사용자를 만든 다음 먼저 파일에 대 한 적절 한 소유권을 부여 합니다.
**참고:** Linux는 대/소문자 구분 파일 시스템이 있습니다. 구성 파일에 대 한 검색에 "Production"을로 ASPNETCORE_ENVIRONMENT 설정 *appsettings 합니다. Production.json*이 아니라 *appsettings.production.json*합니다.

파일을 저장하고 서비스를 사용하도록 설정합니다.

```bash
systemctl enable kestrel-hellomvc.service
```

서비스를 시작 하 고 실행 중인지 확인 합니다.

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

된 역방향 프록시 구성 및 Kestrel systemd 통해 관리 되는 웹 응용 프로그램이 완전히 구성 된 하 고 브라우저에서 로컬 컴퓨터에서 액세스할 수 `http://localhost`합니다. 막을 수 있는 모든 방화벽을 제한 하 여 원격 컴퓨터에서 액세스할 수 이기도 합니다. 응답 헤더를 검사 하 여 `Server` 헤더 Kestrel에서 제공 하는 ASP.NET Core 응용 프로그램을 표시 합니다.

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>로그 보기

웹 앱 이후 Kestrel를 사용 하 여 관리를 사용 하 여 `systemd`, 모든 이벤트 및 프로세스 중앙 집중식된 저널에 기록 됩니다. 그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다. `kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a>응용 프로그램 보안 설정

### <a name="enable-apparmor"></a>AppArmor 사용

Linux 보안 모듈 (LSM)는 Linux 2.6 이후 Linux 커널의 일부인 프레임 워크. LSM은 보안 모듈의 다양한 구현을 지원합니다. [AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다. AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.

### <a name="configuring-the-firewall"></a>방화벽 구성

사용되지 않는 모든 외부 포트를 닫습니다. 복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다. 확인 `ufw` 필요한 모든 포트에서 트래픽을 허용 하도록 구성 됩니다.

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

와 같은 웹 응용 프로그램 방화벽을 사용 하는 것이 좋습니다. *ModSecurity* 강화 응용 프로그램 보안을 강화 합니다.

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a>SSL 구성

* HTTPS 트래픽에 포트에서 수신 하도록 서버 구성 `443` 신뢰할 수 있는 인증 기관 (CA)에서 발급 한 올바른 인증서를 지정 하 여 합니다.

* 다음에서에 사용 된 사례 중 일부를 사용 하 여 보안을 강화 */etc/nginx/nginx.conf* 파일입니다. 예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.

* HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청에 HTTPS만 사용됩니다.

* 적절 한 선택한 또는 Strict-전송-보안 헤더를 추가 하지 `max-age` 경우 SSL을 나중에 사용할 수 없게 됩니다.

*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.

[!code-nginx[Main](linux-nginx/proxy.conf)]

*/etc/nginx/nginx.conf* 구성 파일을 편집합니다. 예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.

[!code-nginx[Main](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a>클릭재킹(clickjacking)으로부터 Nginx 보호
클릭재킹은 감염된 사용자의 클릭을 수집하는 악의적인 기술입니다. 클릭재킹은 희생자(방문자)를 속여서 감염된 사이트를 클릭하게 합니다. X-프레임-옵션을 사용 사이트를 보호 합니다.

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
