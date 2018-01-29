---
title: "Apache를 사용하여 Linux에서 ASP.NET Core 호스트"
description: "Kestrel에서 실행 되는 ASP.NET Core 웹 앱에 HTTP 트래픽을 리디렉션하기 위해 Apache CentOS에 역방향 프록시 서버로 설정 하는 방법에 알아봅니다."
author: spboyer
ms.author: spboyer
manager: wpickett
ms.custom: mvc
ms.date: 10/19/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/linux-apache
ms.openlocfilehash: caa8cce53b3982815f1eab75792a10ec390f3257
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="host-aspnet-core-on-linux-with-apache"></a><span data-ttu-id="bdf06-103">Apache를 사용하여 Linux에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="bdf06-103">Host ASP.NET Core on Linux with Apache</span></span>

<span data-ttu-id="bdf06-104">작성자: [Shayne Boyer](https://github.com/spboyer)</span><span class="sxs-lookup"><span data-stu-id="bdf06-104">By [Shayne Boyer](https://github.com/spboyer)</span></span>

<span data-ttu-id="bdf06-105">설정 하는 방법은이 가이드를 사용 하 여 [Apache](https://httpd.apache.org/) 에 역방향 프록시 서버로 [CentOS 7](https://www.centos.org/) 에서 실행 되는 ASP.NET Core 웹 앱에 HTTP 트래픽을 리디렉션하기 위해 [Kestrel](xref:fundamentals/servers/kestrel)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-105">Using this guide, learn how to set up [Apache](https://httpd.apache.org/) as a reverse proxy server on [CentOS 7](https://www.centos.org/) to redirect HTTP traffic to an ASP.NET Core web app running on [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="bdf06-106">[mod_proxy 확장](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 관련된 모듈 역방향 프록시 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-106">The [mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) and related modules create the server's reverse proxy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdf06-107">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="bdf06-107">Prerequisites</span></span>

1. <span data-ttu-id="bdf06-108">Sudo 권한으로 표준 사용자 계정을 사용 하 여 CentOS 7을 실행 하는 서버</span><span class="sxs-lookup"><span data-stu-id="bdf06-108">Server running CentOS 7 with a standard user account with sudo privilege</span></span>
2. <span data-ttu-id="bdf06-109">ASP.NET Core 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bdf06-109">ASP.NET Core app</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="bdf06-110">앱 게시</span><span class="sxs-lookup"><span data-stu-id="bdf06-110">Publish the app</span></span>

<span data-ttu-id="bdf06-111">해당 응용 프로그램을 게시 한 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd) CentOS 7 런타임에 대 한 릴리스 구성에서 (`centos.7-x64`).</span><span class="sxs-lookup"><span data-stu-id="bdf06-111">Publish the app as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) in Release configuration for the CentOS 7 runtime (`centos.7-x64`).</span></span> <span data-ttu-id="bdf06-112">내용을 복사 하는 *bin/Release/netcoreapp2.0/centos.7-x64/publish* SCP, FTP 또는 기타 파일 전송 방법을 사용 하 여 서버에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-112">Copy the contents of the *bin/Release/netcoreapp2.0/centos.7-x64/publish* folder to the server using SCP, FTP, or other file transfer method.</span></span>

> [!NOTE]
> <span data-ttu-id="bdf06-113">프로덕션 배포 시나리오에서 연속 통합 워크플로 응용 프로그램을 게시 및 자산에서 서버로 복사 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-113">Under a production deployment scenario, a continuous integration workflow does the work of publishing the app and copying the assets to the server.</span></span> 

## <a name="configure-a-proxy-server"></a><span data-ttu-id="bdf06-114">프록시 서버 구성</span><span class="sxs-lookup"><span data-stu-id="bdf06-114">Configure a proxy server</span></span>

<span data-ttu-id="bdf06-115">역방향 프록시는 동적 웹 앱을 처리 하기 위한 일반적인 설치.</span><span class="sxs-lookup"><span data-stu-id="bdf06-115">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="bdf06-116">역방향 프록시는 HTTP 요청을 종료 하 고 ASP.NET 응용 프로그램에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-116">The reverse proxy terminates the HTTP request and forwards it to the ASP.NET app.</span></span>

<span data-ttu-id="bdf06-117">프록시 서버는 클라이언트 요청을 자체 수행하는 대신 다른 서버에 전달하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-117">A proxy server is one which forwards client requests to another server instead of fulfilling them itself.</span></span> <span data-ttu-id="bdf06-118">역방향 프록시는 일반적으로 임의의 클라이언트 대신 고정 대상에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-118">A reverse proxy forwards to a fixed destination, typically on behalf of arbitrary clients.</span></span> <span data-ttu-id="bdf06-119">이 가이드에서는 Apache Kestrel ASP.NET Core 응용 프로그램을 처리는 동일한 서버에서 실행 하는 역방향 프록시도 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-119">In this guide, Apache is configured as the reverse proxy running on the same server that Kestrel is serving the ASP.NET Core app.</span></span>

### <a name="install-apache"></a><span data-ttu-id="bdf06-120">Apache 설치</span><span class="sxs-lookup"><span data-stu-id="bdf06-120">Install Apache</span></span>

<span data-ttu-id="bdf06-121">CentOS 패키지를 안정적인 최신 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-121">Update CentOS packages to their latest stable versions:</span></span>

```bash
sudo yum update -y
```

<span data-ttu-id="bdf06-122">단일 CentOS에 Apache 웹 서버를 설치 `yum` 명령:</span><span class="sxs-lookup"><span data-stu-id="bdf06-122">Install the Apache web server on CentOS with a single `yum` command:</span></span>

```bash
sudo yum -y install httpd mod_ssl
```

<span data-ttu-id="bdf06-123">명령을 실행 한 후 출력 샘플:</span><span class="sxs-lookup"><span data-stu-id="bdf06-123">Sample output after running the command:</span></span>

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
> <span data-ttu-id="bdf06-124">이 예제에서는 출력 CentOS 7 버전은 64 비트 이후 httpd.86_64을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-124">In this example, the output reflects httpd.86_64 since the CentOS 7 version is 64 bit.</span></span> <span data-ttu-id="bdf06-125">Apache를 설치한 위치를 확인하려면 명령 프롬프트에서 `whereis httpd`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-125">To verify where Apache is installed, run `whereis httpd` from a command prompt.</span></span> 

### <a name="configure-apache-for-reverse-proxy"></a><span data-ttu-id="bdf06-126">역방향 프록시에 Apache 구성</span><span class="sxs-lookup"><span data-stu-id="bdf06-126">Configure Apache for reverse proxy</span></span>

<span data-ttu-id="bdf06-127">Apache의 구성 파일은 `/etc/httpd/conf.d/` 디렉터리 내에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-127">Configuration files for Apache are located within the `/etc/httpd/conf.d/` directory.</span></span> <span data-ttu-id="bdf06-128">모든 파일이 *.conf* 확장은 모듈 구성 파일 뿐 아니라 알파벳 순서로 처리 `/etc/httpd/conf.modules.d/`, 구성이 포함 된 모듈을 로드 하는 데 필요한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-128">Any file with the *.conf* extension is processed in alphabetical order in addition to the module configuration files in `/etc/httpd/conf.modules.d/`, which contains any configuration files necessary to load modules.</span></span>

<span data-ttu-id="bdf06-129">명명 된 앱에 대 한 구성 파일을 만드는 `hellomvc.conf`:</span><span class="sxs-lookup"><span data-stu-id="bdf06-129">Create a configuration file for the app named `hellomvc.conf`:</span></span>

```
<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
</VirtualHost>
```

<span data-ttu-id="bdf06-130">**VirtualHost** 노드는 서버에서 하나 이상의 파일에 여러 번 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-130">The **VirtualHost** node can appear multiple times in one or more files on a server.</span></span> <span data-ttu-id="bdf06-131">**VirtualHost** 포트 80을 사용 하 여 모든 IP 주소에서 수신 하도록 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-131">**VirtualHost** is set to listen on any IP address using port 80.</span></span> <span data-ttu-id="bdf06-132">다음 두 줄은 포트 5000에서 루트에 있는 서버에 127.0.0.1에 프록시 요청으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-132">The next two lines are set to proxy requests at the root to the server at 127.0.0.1 on port 5000.</span></span> <span data-ttu-id="bdf06-133">양방향 통신을 위해 *ProxyPass* 및 *ProxyPassReverse* 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-133">For bi-directional communication, *ProxyPass* and *ProxyPassReverse* are required.</span></span>

<span data-ttu-id="bdf06-134">당 로깅을 구성할 수 있습니다 **VirtualHost** 를 사용 하 여 **ErrorLog** 및 **CustomLog** 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-134">Logging can be configured per **VirtualHost** using **ErrorLog** and **CustomLog** directives.</span></span> <span data-ttu-id="bdf06-135">**ErrorLog** 서버가 오류를 기록 하는 위치 및 **CustomLog** 파일 이름 및 로그 파일의 형식을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-135">**ErrorLog** is the location where the server logs errors, and **CustomLog** sets the filename and format of log file.</span></span> <span data-ttu-id="bdf06-136">이 경우 요청 정보를 기록 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-136">In this case, this is where request information is logged.</span></span> <span data-ttu-id="bdf06-137">각 요청에 대 한 줄이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-137">There's one line for each request.</span></span>

<span data-ttu-id="bdf06-138">파일을 저장 하 고 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-138">Save the file and test the configuration.</span></span> <span data-ttu-id="bdf06-139">모든 항목이 통과하는 경우 응답은 `Syntax [OK]`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-139">If everything passes, the response should be `Syntax [OK]`.</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="bdf06-140">Apache 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-140">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a><span data-ttu-id="bdf06-141">응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="bdf06-141">Monitoring the app</span></span>

<span data-ttu-id="bdf06-142">Apache에 대 한 요청을 전달 하도록 설정 되어 이제 `http://localhost:80` 에 Kestrel에서 실행 중인 ASP.NET Core 응용 프로그램에 `http://127.0.0.1:5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-142">Apache is now setup to forward requests made to `http://localhost:80` to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span>  <span data-ttu-id="bdf06-143">그러나 Apache Kestrel 프로세스를 관리할 수를 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-143">However, Apache isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="bdf06-144">사용 하 여 *systemd* 을 시작 하 고 기본 웹 응용 프로그램 모니터링 서비스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-144">Use *systemd* and create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="bdf06-145">*systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-145">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 


### <a name="create-the-service-file"></a><span data-ttu-id="bdf06-146">서비스 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="bdf06-146">Create the service file</span></span>

<span data-ttu-id="bdf06-147">서비스 정의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-147">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="bdf06-148">응용 프로그램에 대 한 예제 서비스 파일:</span><span class="sxs-lookup"><span data-stu-id="bdf06-148">An example service file for the app:</span></span>

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
> <span data-ttu-id="bdf06-149">**사용자** &mdash; 경우 사용자 *apache* 는 사용 하지 않으며, 구성에서 사용자를 만든 다음 먼저 파일에 대 한 적절 한 소유권을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-149">**User** &mdash; If the user *apache* isn't used by the configuration, the user must be created first and given proper ownership for files.</span></span>

<span data-ttu-id="bdf06-150">파일을 저장 하 고 서비스를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-150">Save the file and enable the service:</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="bdf06-151">서비스를 시작 하 고 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-151">Start the service and verify that it's running:</span></span>

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

<span data-ttu-id="bdf06-152">역방향 프록시 구성 및 통해 관리 되는 Kestrel *systemd*, 웹 응용 프로그램 구성 완벽 하 게 되 고 브라우저에서 로컬 컴퓨터에서 액세스할 수 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-152">With the reverse proxy configured and Kestrel managed through *systemd*, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="bdf06-153">응답 헤더를 검사 하는 **서버** 헤더 ASP.NET Core 응용 프로그램 Kestrel에 의해 제공 되는 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-153">Inspecting the response headers, the **Server** header indicates that the ASP.NET Core app is served by Kestrel:</span></span>

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="bdf06-154">로그 보기</span><span class="sxs-lookup"><span data-stu-id="bdf06-154">Viewing logs</span></span>

<span data-ttu-id="bdf06-155">웹 앱 이후 Kestrel를 사용 하 여 관리를 사용 하 여 *systemd*, 이벤트 및 프로세스 중앙 집중식된 저널에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-155">Since the web app using Kestrel is managed using *systemd*, events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="bdf06-156">이 저널 모든 서비스 및 관리 하는 프로세스에 대 한 항목을 포함 하는 반면 *systemd*합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-156">However, this journal includes entries for all of the services and processes managed by *systemd*.</span></span> <span data-ttu-id="bdf06-157">`kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-157">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="bdf06-158">시간 필터링에 대 한 명령을 사용 하 여 시간 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-158">For time filtering, specify time options with the command.</span></span> <span data-ttu-id="bdf06-159">사용 예를 들어 `--since today` 은 현재 날짜에 대 한 필터링 또는 `--until 1 hour ago` 이전 시간 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-159">For example, use `--since today` to filter for the current day or `--until 1 hour ago` to see the previous hour's entries.</span></span> <span data-ttu-id="bdf06-160">자세한 내용은 참조는 [journalctl 매뉴얼 페이지](https://www.unix.com/man-page/centos/1/journalctl/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-160">For more information, see the [man page for journalctl](https://www.unix.com/man-page/centos/1/journalctl/).</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a><span data-ttu-id="bdf06-161">응용 프로그램 보안 설정</span><span class="sxs-lookup"><span data-stu-id="bdf06-161">Securing the app</span></span>

### <a name="configure-firewall"></a><span data-ttu-id="bdf06-162">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="bdf06-162">Configure firewall</span></span>

<span data-ttu-id="bdf06-163">*Firewalld* 네트워크 영역에 대 한 지원과 함께 방화벽을 관리 하는 동적 디먼은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-163">*Firewalld* is a dynamic daemon to manage the firewall with support for network zones.</span></span> <span data-ttu-id="bdf06-164">포트 및 패킷 필터링 여전히 iptables 하 여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-164">Ports and packet filtering can still be managed by iptables.</span></span> <span data-ttu-id="bdf06-165">*Firewalld* 기본적으로 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-165">*Firewalld* should be installed by default.</span></span> <span data-ttu-id="bdf06-166">`yum`패키지를 설치 하거나 설치 되었는지 확인 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-166">`yum` can be used to install the package or verify it's installed.</span></span>

```bash
sudo yum install firewalld -y
```

<span data-ttu-id="bdf06-167">사용 하 여 `firewalld` 를 응용 프로그램에 필요한 포트만 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-167">Use `firewalld` to open only the ports needed for the app.</span></span> <span data-ttu-id="bdf06-168">이 경우에는 포트 80 및 443을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-168">In this case, port 80 and 443 are used.</span></span> <span data-ttu-id="bdf06-169">다음 명령 포트 80 및 443이 열을 영구적으로 설정:</span><span class="sxs-lookup"><span data-stu-id="bdf06-169">The following commands permanently set ports 80 and 443 to open:</span></span>

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

<span data-ttu-id="bdf06-170">방화벽 설정을 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-170">Reload the firewall settings.</span></span> <span data-ttu-id="bdf06-171">사용 가능한 서비스 및 기본 영역에는 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-171">Check the available services and ports in the default zone.</span></span> <span data-ttu-id="bdf06-172">검사 하 여 옵션을 사용할 수 `firewall-cmd -h`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-172">Options are available by inspecting `firewall-cmd -h`.</span></span>

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

### <a name="ssl-configuration"></a><span data-ttu-id="bdf06-173">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="bdf06-173">SSL configuration</span></span>

<span data-ttu-id="bdf06-174">Apache ssl을 구성 하는 *mod_ssl* 모듈은 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-174">To configure Apache for SSL, the *mod_ssl* module is used.</span></span> <span data-ttu-id="bdf06-175">경우는 *httpd* 모듈을 설치 하 되는 *mod_ssl* 모듈도 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-175">When the *httpd* module was installed, the *mod_ssl* module was also installed.</span></span> <span data-ttu-id="bdf06-176">사용 하 여 설치 되지 않은 경우 `yum` 구성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-176">If it wasn't installed, use `yum` to add it to the configuration.</span></span>

```bash
sudo yum install mod_ssl
```
<span data-ttu-id="bdf06-177">SSL을 적용 하려면 설치는 `mod_rewrite` 모듈 URL 다시 쓰기를 사용 하도록 설정 하려면:</span><span class="sxs-lookup"><span data-stu-id="bdf06-177">To enforce SSL, install the `mod_rewrite` module to enable URL rewriting:</span></span>

```bash
sudo yum install mod_rewrite
```

<span data-ttu-id="bdf06-178">수정 된 *hellomvc.conf* URL 다시 쓰기를 사용 하도록 설정 하 고 포트 443에서 통신을 보호 하려면 파일:</span><span class="sxs-lookup"><span data-stu-id="bdf06-178">Modify the *hellomvc.conf* file to enable URL rewriting and secure communication on port 443:</span></span>

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
> <span data-ttu-id="bdf06-179">이 예에서는 로컬로 생성 된 인증서를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-179">This example is using a locally-generated certificate.</span></span> <span data-ttu-id="bdf06-180">**SSLCertificateFile** 도메인 이름에 대 한 기본 인증서 파일 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-180">**SSLCertificateFile** should be the primary certificate file for the domain name.</span></span> <span data-ttu-id="bdf06-181">**SSLCertificateKeyFile** 키 파일이 생성 되어야 CSR 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-181">**SSLCertificateKeyFile** should be the key file generated when CSR is created.</span></span> <span data-ttu-id="bdf06-182">**SSLCertificateChainFile** (있는 경우) 중간 인증서 파일이 있어야 인증 기관에서 제공 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-182">**SSLCertificateChainFile** should be the intermediate certificate file (if any) that was supplied by the certificate authority.</span></span>

<span data-ttu-id="bdf06-183">파일을 저장 하 고 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-183">Save the file and test the configuration:</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="bdf06-184">Apache 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-184">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a><span data-ttu-id="bdf06-185">추가 Apache 제안</span><span class="sxs-lookup"><span data-stu-id="bdf06-185">Additional Apache suggestions</span></span>

### <a name="additional-headers"></a><span data-ttu-id="bdf06-186">추가 헤더</span><span class="sxs-lookup"><span data-stu-id="bdf06-186">Additional headers</span></span>

<span data-ttu-id="bdf06-187">를 악의적인 공격 으로부터 보호 하기 위해 해야 수정 하거나 추가 헤더는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-187">In order to secure against malicious attacks, there are a few headers that should either be modified or added.</span></span> <span data-ttu-id="bdf06-188">확인 된 `mod_headers` 모듈은 설치:</span><span class="sxs-lookup"><span data-stu-id="bdf06-188">Ensure that the `mod_headers` module is installed:</span></span>

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a><span data-ttu-id="bdf06-189">Apache clickjacking 공격 으로부터 보호</span><span class="sxs-lookup"><span data-stu-id="bdf06-189">Secure Apache from clickjacking attacks</span></span>

<span data-ttu-id="bdf06-190">[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)라고도 하는 *UI redress 공격*, 여기서 웹 사이트 방문자는 스크립트가 속아 서 현재 방문 하는 것 보다 링크 또는 다른 페이지에 단추를 클릭 하는 악의적인 공격에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-190">[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger), also known as a *UI redress attack*, is a malicious attack where a website visitor is tricked into clicking a link or button on a different page than they're currently visiting.</span></span> <span data-ttu-id="bdf06-191">사용 하 여 `X-FRAME-OPTIONS` 사이트 보호를 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-191">Use `X-FRAME-OPTIONS` to secure the site.</span></span>

<span data-ttu-id="bdf06-192">편집 된 *httpd.conf* 파일:</span><span class="sxs-lookup"><span data-stu-id="bdf06-192">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="bdf06-193">줄 추가 `Header append X-FRAME-OPTIONS "SAMEORIGIN"`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-193">Add the line `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.</span></span> <span data-ttu-id="bdf06-194">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-194">Save the file.</span></span> <span data-ttu-id="bdf06-195">Apache를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-195">Restart Apache.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="bdf06-196">MIME 형식 검색</span><span class="sxs-lookup"><span data-stu-id="bdf06-196">MIME-type sniffing</span></span>

<span data-ttu-id="bdf06-197">`X-Content-Type-Options` 헤더에서 Internet Explorer 방지 *MIME 스니핑* (파일의 확인 `Content-Type` 파일의 내용을 사용).</span><span class="sxs-lookup"><span data-stu-id="bdf06-197">The `X-Content-Type-Options` header prevents Internet Explorer from *MIME-sniffing* (determing a file's `Content-Type` from the file's content).</span></span> <span data-ttu-id="bdf06-198">서버를 설정 하는 경우는 `Content-Type` 헤더를 `text/html` 와 `nosniff` 으로 콘텐츠를 렌더링 하는 옵션 집합, Internet Explorer `text/html` 파일의 내용에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-198">If the server sets the `Content-Type` header to `text/html` with the `nosniff` option set, Internet Explorer renders the content as `text/html` regardless of the file's content.</span></span>

<span data-ttu-id="bdf06-199">편집 된 *httpd.conf* 파일:</span><span class="sxs-lookup"><span data-stu-id="bdf06-199">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="bdf06-200">줄 추가 `Header set X-Content-Type-Options "nosniff"`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-200">Add the line `Header set X-Content-Type-Options "nosniff"`.</span></span> <span data-ttu-id="bdf06-201">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-201">Save the file.</span></span> <span data-ttu-id="bdf06-202">Apache를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-202">Restart Apache.</span></span>

### <a name="load-balancing"></a><span data-ttu-id="bdf06-203">부하 분산</span><span class="sxs-lookup"><span data-stu-id="bdf06-203">Load Balancing</span></span> 

<span data-ttu-id="bdf06-204">이 예제에서는 동일한 인스턴스 컴퓨터에서 CentOS 7와 Kestrel의 Apache를 설정하고 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-204">This example shows how to setup and configure Apache on CentOS 7 and Kestrel on the same instance machine.</span></span> <span data-ttu-id="bdf06-205">단일 실패 지점이 없는. 사용 하 여 *mod_proxy_balancer* 및 수정 된 **VirtualHost** Apache 프록시 서버 뒤에서 웹 앱의 여러 인스턴스를 관리 하기 위한 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-205">In order to not have a single point of failure; using *mod_proxy_balancer* and modifying the **VirtualHost** would allow for managing mutliple instances of the web apps behind the Apache proxy server.</span></span>

```bash
sudo yum install mod_proxy_balancer
```

<span data-ttu-id="bdf06-206">다른 인스턴스를 아래 표시 된 구성 파일에는 `hellomvc` 앱 5001이 고 포트에서 수행 되도록 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-206">In the configuration file shown below, an additional instance of the `hellomvc` app is setup to run on port 5001.</span></span> <span data-ttu-id="bdf06-207">*프록시* 섹션은 부하 분산을 위해 두 멤버가 포함 된 분산 장치 구성으로 설정 된 *byrequests*합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-207">The *Proxy* section is set with a balancer configuration with two members to load balance *byrequests*.</span></span>

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

### <a name="rate-limits"></a><span data-ttu-id="bdf06-208">속도 제한</span><span class="sxs-lookup"><span data-stu-id="bdf06-208">Rate Limits</span></span>
<span data-ttu-id="bdf06-209">사용 하 여 *mod_ratelimit*에 포함 되어 있는 *httpd* 모듈의 클라이언트는 대역폭 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-209">Using *mod_ratelimit*, which is included in the *httpd* module, the bandwidth of clients can be limited:</span></span>

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
<span data-ttu-id="bdf06-210">예제 파일은 루트 위치 아래의 600 KB/sec로 대역폭을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf06-210">The example file limits bandwidth as 600 KB/sec under the root location:</span></span>

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```
