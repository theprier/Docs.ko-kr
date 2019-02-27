---
title: ASP.NET Core 프로젝트 문제 해결
author: Rick-Anderson
description: ASP.NET Core 프로젝트를 사용하여 경고 및 오류를 이해하고 문제를 해결합니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: test/troubleshoot
ms.openlocfilehash: c8b34f51fd329eb9a7c34f7be93bd7f2aa054283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56899293"
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="340e2-103">ASP.NET Core 프로젝트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="340e2-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="340e2-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="340e2-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="340e2-105">다음 링크를 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-105">The following links provide troubleshooting guidance:</span></span>

* <xref:host-and-deploy/azure-apps/troubleshoot>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-iis-errors-reference>
* [<span data-ttu-id="340e2-106">NDC 회의 (런던, 2018): ASP.NET Core 응용 프로그램에서 문제 진단</span><span class="sxs-lookup"><span data-stu-id="340e2-106">NDC Conference (London, 2018): Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [<span data-ttu-id="340e2-107">ASP.NET 블로그: ASP.NET Core 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="340e2-107">ASP.NET Blog: Troubleshooting ASP.NET Core Performance Problems</span></span>](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a><span data-ttu-id="340e2-108">.NET core SDK 경고</span><span class="sxs-lookup"><span data-stu-id="340e2-108">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="340e2-109">32 비트와 64 비트 버전의.NET Core SDK가 설치 된</span><span class="sxs-lookup"><span data-stu-id="340e2-109">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>

<span data-ttu-id="340e2-110">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-110">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="340e2-111">모두 32 비트 및 64 비트 버전의.NET Core SDK 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-111">Both 32 and 64 bit versions of the .NET Core SDK are installed.</span></span> <span data-ttu-id="340e2-112">에 설치 된 64 비트 버전의 템플릿만 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-112">Only templates from the 64 bit version(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="340e2-114">이 경고를 표시 하는 경우 32 비트 (x86)와 버전의 64 비트 (x64) 합니다 [.NET Core SDK](https://www.microsoft.com/net/download/all) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="340e2-115">두 버전을 설치할 수 있습니다 하는 일반적인 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-115">Common reasons both versions may be installed include:</span></span>

* <span data-ttu-id="340e2-116">원래 32 비트 컴퓨터를 사용 하 여.NET Core SDK 설치 관리자를 다운로드 하지만 다음 복사 하는 것을 64 비트 컴퓨터에 설치.</span><span class="sxs-lookup"><span data-stu-id="340e2-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine but then copied it across and installed it on a 64-bit machine.</span></span>
* <span data-ttu-id="340e2-117">32 비트.NET Core SDK가 다른 응용 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="340e2-118">잘못 된 버전 다운로드 되어 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="340e2-119">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="340e2-120">제거할 **Control Panel** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="340e2-121">경고가 발생 하는 이유 및 그 의미를 이해 하면 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="340e2-122">여러 위치에서.NET Core SDK가 설치</span><span class="sxs-lookup"><span data-stu-id="340e2-122">The .NET Core SDK is installed in multiple locations</span></span>

<span data-ttu-id="340e2-123">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-123">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="340e2-124">.NET Core SDK는 여러 위치에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="340e2-125">Sdk의 템플릿만에 설치 된 템플릿 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-125">Only templates from the SDK(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="340e2-127">하나 이상의.NET Core SDK 설치 디렉터리 외부에 있는 경우에이 메시지를 참조 하세요 *c:\\Program Files\\dotnet\\sdk\\* 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-127">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\\Program Files\\dotnet\\sdk\\*.</span></span> <span data-ttu-id="340e2-128">일반적으로.NET Core SDK MSI 설치 관리자 대신 복사/붙여넣기를 사용 하는 컴퓨터에 배포 된 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-128">Usually this happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="340e2-129">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="340e2-130">제거할 **Control Panel** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="340e2-131">경고가 발생 하는 이유 및 그 의미를 이해 하면 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="340e2-132">.NET Core Sdk 발견</span><span class="sxs-lookup"><span data-stu-id="340e2-132">No .NET Core SDKs were detected</span></span>

<span data-ttu-id="340e2-133">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-133">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="340e2-134">.NET Core Sdk 발견, 'PATH' 환경 변수에 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-134">No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="340e2-136">이 경고를 표시 하는 경우 환경 변수 `PATH` 컴퓨터에서 모든.NET Core Sdk를 가리키지 않습니다. (예를 들어 `C:\Program Files\dotnet\` 고 `C:\Program Files (x86)\dotnet\`).</span><span class="sxs-lookup"><span data-stu-id="340e2-136">This warning appears when the environment variable `PATH` doesn't point to any .NET Core SDKs on the machine (for example, `C:\Program Files\dotnet\` and `C:\Program Files (x86)\dotnet\`).</span></span> <span data-ttu-id="340e2-137">이 문제를 해결 하려면</span><span class="sxs-lookup"><span data-stu-id="340e2-137">To resolve this problem:</span></span>

* <span data-ttu-id="340e2-138">설치 또는.NET Core SDK 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-138">Install or verify the .NET Core SDK is installed.</span></span> <span data-ttu-id="340e2-139">최신 설치 관리자를 가져옵니다 [.NET 다운로드](https://dotnet.microsoft.com/download)합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-139">Obtain the latest installer from [.NET Downloads](https://dotnet.microsoft.com/download).</span></span> 
* <span data-ttu-id="340e2-140">확인을 `PATH` 환경 변수는 SDK를 설치할 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-140">Verify that the `PATH` environment variable points to the location where the SDK is installed.</span></span> <span data-ttu-id="340e2-141">설치 관리자가 일반적으로 설정 된 `PATH`합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-141">The installer normally sets the `PATH`.</span></span>

## <a name="obtain-data-from-an-app"></a><span data-ttu-id="340e2-142">앱에서 데이터 얻기</span><span class="sxs-lookup"><span data-stu-id="340e2-142">Obtain data from an app</span></span>

<span data-ttu-id="340e2-143">앱 요청에 응답할 수 인 경우에 미들웨어를 사용 하 여 앱에서 다음 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-143">If an app is capable of responding to requests, you can obtain the following data from the app using middleware:</span></span>

* <span data-ttu-id="340e2-144">요청 &ndash; 메서드를 체계, 호스트, pathbase, 경로, 쿼리 문자열, 헤더</span><span class="sxs-lookup"><span data-stu-id="340e2-144">Request &ndash; Method, scheme, host, pathbase, path, query string, headers</span></span>
* <span data-ttu-id="340e2-145">연결 &ndash; 원격 IP 주소, 포트를 원격, 로컬 IP 주소, 로컬 포트, 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="340e2-145">Connection &ndash; Remote IP address, remote port, local IP address, local port, client certificate</span></span>
* <span data-ttu-id="340e2-146">Identity &ndash; 이름, 표시 이름</span><span class="sxs-lookup"><span data-stu-id="340e2-146">Identity &ndash; Name, display name</span></span>
* <span data-ttu-id="340e2-147">구성 설정</span><span class="sxs-lookup"><span data-stu-id="340e2-147">Configuration settings</span></span>
* <span data-ttu-id="340e2-148">환경 변수</span><span class="sxs-lookup"><span data-stu-id="340e2-148">Environment variables</span></span>

<span data-ttu-id="340e2-149">다음 배치 [미들웨어](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder) 맨 앞에 코드를 `Startup.Configure` 메서드 요청 처리 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="340e2-149">Place the following [middleware](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder) code at the beginning of the `Startup.Configure` method's request processing pipeline.</span></span> <span data-ttu-id="340e2-150">미들웨어는 코드를 개발 환경에만 실행 되도록 실행 되기 전에 환경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-150">The environment is checked before the middleware is run to ensure that the code is only executed in the Development environment.</span></span>

<span data-ttu-id="340e2-151">환경을 얻으려면 다음 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-151">To obtain the environment, use either of the following approaches:</span></span>

* <span data-ttu-id="340e2-152">삽입 합니다 `IHostingEnvironment` 에 `Startup.Configure` 메서드 및 지역 변수를 사용 하 여 환경 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-152">Inject the `IHostingEnvironment` into the `Startup.Configure` method and check the environment with the local variable.</span></span> <span data-ttu-id="340e2-153">다음 샘플 코드에는이 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-153">The following sample code demonstrates this approach.</span></span>

* <span data-ttu-id="340e2-154">환경 속성에 할당 된 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="340e2-154">Assign the environment to a property in the `Startup` class.</span></span> <span data-ttu-id="340e2-155">확인 속성을 사용 하 여 환경 (예를 들어 `if (Environment.IsDevelopment())`).</span><span class="sxs-lookup"><span data-stu-id="340e2-155">Check the environment using the property (for example, `if (Environment.IsDevelopment())`).</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, 
    IConfiguration config)
{
    if (env.IsDevelopment())
    {
        app.Run(async (context) =>
        {
            var sb = new StringBuilder();
            var nl = System.Environment.NewLine;
            var rule = string.Concat(nl, new string('-', 40), nl);
            var authSchemeProvider = app.ApplicationServices
                .GetRequiredService<IAuthenticationSchemeProvider>();

            sb.Append($"Request{rule}");
            sb.Append($"{DateTimeOffset.Now}{nl}");
            sb.Append($"{context.Request.Method} {context.Request.Path}{nl}");
            sb.Append($"Scheme: {context.Request.Scheme}{nl}");
            sb.Append($"Host: {context.Request.Headers["Host"]}{nl}");
            sb.Append($"PathBase: {context.Request.PathBase.Value}{nl}");
            sb.Append($"Path: {context.Request.Path.Value}{nl}");
            sb.Append($"Query: {context.Request.QueryString.Value}{nl}{nl}");

            sb.Append($"Connection{rule}");
            sb.Append($"RemoteIp: {context.Connection.RemoteIpAddress}{nl}");
            sb.Append($"RemotePort: {context.Connection.RemotePort}{nl}");
            sb.Append($"LocalIp: {context.Connection.LocalIpAddress}{nl}");
            sb.Append($"LocalPort: {context.Connection.LocalPort}{nl}");
            sb.Append($"ClientCert: {context.Connection.ClientCertificate}{nl}{nl}");

            sb.Append($"Identity{rule}");
            sb.Append($"User: {context.User.Identity.Name}{nl}");
            var scheme = await authSchemeProvider
                .GetSchemeAsync(IISDefaults.AuthenticationScheme);
            sb.Append($"DisplayName: {scheme?.DisplayName}{nl}{nl}");

            sb.Append($"Headers{rule}");
            foreach (var header in context.Request.Headers)
            {
                sb.Append($"{header.Key}: {header.Value}{nl}");
            }
            sb.Append(nl);

            sb.Append($"Websockets{rule}");
            if (context.Features.Get<IHttpUpgradeFeature>() != null)
            {
                sb.Append($"Status: Enabled{nl}{nl}");
            }
            else
            {
                sb.Append($"Status: Disabled{nl}{nl}");
            }

            sb.Append($"Configuration{rule}");
            foreach (var pair in config.AsEnumerable())
            {
                sb.Append($"{pair.Path}: {pair.Value}{nl}");
            }
            sb.Append(nl);

            sb.Append($"Environment Variables{rule}");
            var vars = System.Environment.GetEnvironmentVariables();
            foreach (var key in vars.Keys.Cast<string>().OrderBy(key => key, 
                StringComparer.OrdinalIgnoreCase))
            {
                var value = vars[key];
                sb.Append($"{key}: {value}{nl}");
            }

            context.Response.ContentType = "text/plain";
            await context.Response.WriteAsync(sb.ToString());
        });
    }
}
```
