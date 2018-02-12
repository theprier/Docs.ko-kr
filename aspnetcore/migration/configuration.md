---
title: "구성 마이그레이션"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/configuration
ms.openlocfilehash: f258e12a95770909bff24fd5dd3611324179596f
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="migrating-configuration"></a><span data-ttu-id="5d9ad-102">구성 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5d9ad-102">Migrating Configuration</span></span>

<span data-ttu-id="5d9ad-103">작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="5d9ad-103">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="5d9ad-104">이전 문서에서는 하기 시작 [ASP.NET Core mvc ASP.NET MVC 프로젝트 마이그레이션](mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-104">In the previous article, we began [migrating an ASP.NET MVC project to ASP.NET Core MVC](mvc.md).</span></span> <span data-ttu-id="5d9ad-105">이 문서에서는 구성을 마이그레이션 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-105">In this article, we migrate configuration.</span></span>

<span data-ttu-id="5d9ad-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5d9ad-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="setup-configuration"></a><span data-ttu-id="5d9ad-107">설치 구성</span><span class="sxs-lookup"><span data-stu-id="5d9ad-107">Setup Configuration</span></span>

<span data-ttu-id="5d9ad-108">ASP.NET Core 더 이상 사용 하지는 *Global.asax* 및 *web.config* 이전 버전의 ASP.NET 사용 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-108">ASP.NET Core no longer uses the *Global.asax* and *web.config* files that previous versions of ASP.NET utilized.</span></span> <span data-ttu-id="5d9ad-109">이전 버전의 ASP.NET 응용 프로그램 시작 논리에 배치 된는 `Application_StartUp` 메서드 내에서 *Global.asax*합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-109">In earlier versions of ASP.NET, application startup logic was placed in an `Application_StartUp` method within *Global.asax*.</span></span> <span data-ttu-id="5d9ad-110">ASP.NET MVC의 뒷부분에 나오는 *Startup.cs* 고 파일; 프로젝트의 루트에 포함 된 응용 프로그램이 시작 될 때 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-110">Later, in ASP.NET MVC, a *Startup.cs* file was included in the root of the project; and, it was called when the application started.</span></span> <span data-ttu-id="5d9ad-111">ASP.NET Core가이 접근 방법을 채택 완전히 모든 시작 논리에 배치 하 여는 *Startup.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-111">ASP.NET Core has adopted this approach completely by placing all startup logic in the *Startup.cs* file.</span></span>

<span data-ttu-id="5d9ad-112">*web.config* 파일 에서도 ASP.NET Core 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-112">The *web.config* file has also been replaced in ASP.NET Core.</span></span> <span data-ttu-id="5d9ad-113">자체 구성 이제을 구성할 수 있으며 응용 프로그램 시작에서 설명한 절차의 일부로 *Startup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-113">Configuration itself can now be configured, as part of the application startup procedure described in *Startup.cs*.</span></span> <span data-ttu-id="5d9ad-114">구성 XML 파일을 사용할 수 있지만 일반적으로 ASP.NET Core 프로젝트에에서 배치 됩니다 구성 값을 JSON 형식 파일을 같은 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-114">Configuration can still utilize XML files, but typically ASP.NET Core projects will place configuration values in a JSON-formatted file, such as *appsettings.json*.</span></span> <span data-ttu-id="5d9ad-115">ASP.NET Core 구성 시스템 환경 변수를 제공할 수 있는도 쉽게 액세스할 수는 [더 안전 하 고 강력한 위치](xref:security/app-secrets) 환경 관련 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-115">ASP.NET Core's configuration system can also easily access environment variables, which can provide a [more secure and robust location](xref:security/app-secrets) for environment-specific values.</span></span> <span data-ttu-id="5d9ad-116">연결 문자열 및 소스 제어에 체크 인할 수 하지 않아야 하는 API 키와 같은 기밀 정보에 대 한 경우 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-116">This is especially true for secrets like connection strings and API keys that shouldn't be checked into source control.</span></span> <span data-ttu-id="5d9ad-117">참조 [구성](xref:fundamentals/configuration/index) ASP.NET Core에서 구성에 대 한 자세한 내용을 보려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-117">See [Configuration](xref:fundamentals/configuration/index) to learn more about configuration in ASP.NET Core.</span></span>

<span data-ttu-id="5d9ad-118">ASP.NET Core 일부만 마이그레이션된 프로젝트와 시작 되며이 문서에 대 한 [이전 문서](mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-118">For this article, we are starting with the partially-migrated ASP.NET Core project from [the previous article](mvc.md).</span></span> <span data-ttu-id="5d9ad-119">구성 설정, 다음 생성자 및 속성을 추가 하는 *Startup.cs* 프로젝트의 루트에 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="5d9ad-119">To setup configuration, add the following constructor and property to the *Startup.cs* file located in the root of the project:</span></span>

[!code-csharp[Main](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]

<span data-ttu-id="5d9ad-120">이 시점에서 즉 참고는 *Startup.cs* 파일에 다음 추가 해야 하는 대로 컴파일되지 않습니다 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="5d9ad-120">Note that at this point, the *Startup.cs* file won't compile, as we still need to add the following `using` statement:</span></span>

```csharp
using Microsoft.Extensions.Configuration;
```

<span data-ttu-id="5d9ad-121">추가 *appsettings.json* 적절 한 항목 템플릿을 사용 하 여 프로젝트의 루트에 파일:</span><span class="sxs-lookup"><span data-stu-id="5d9ad-121">Add an *appsettings.json* file to the root of the project using the appropriate item template:</span></span>

![AppSettings JSON 추가](configuration/_static/add-appsettings-json.png)

## <a name="migrate-configuration-settings-from-webconfig"></a><span data-ttu-id="5d9ad-123">Web.config에서 구성 설정을 마이그레이션하십시오</span><span class="sxs-lookup"><span data-stu-id="5d9ad-123">Migrate Configuration Settings from web.config</span></span>

<span data-ttu-id="5d9ad-124">ASP.NET MVC 프로젝트 진행에 필요한 데이터베이스 연결 문자열을 포함 *web.config*에 `<connectionStrings>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-124">Our ASP.NET MVC project included the required database connection string in *web.config*, in the `<connectionStrings>` element.</span></span> <span data-ttu-id="5d9ad-125">ASP.NET Core 프로젝트 진행에 하겠습니다에이 정보를 저장 하는 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-125">In our ASP.NET Core project, we are going to store this information in the *appsettings.json* file.</span></span> <span data-ttu-id="5d9ad-126">열기 *appsettings.json*, 다음을 이미 포함 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-126">Open *appsettings.json*, and note that it already includes the following:</span></span>

[!code-json[Main](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]


<span data-ttu-id="5d9ad-127">위에 표시 하는 강조 표시 된 줄에서 데이터베이스의 이름을 변경 **_CHANGE_ME** 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-127">In the highlighted line depicted above, change the name of the database from **_CHANGE_ME** to the name of your database.</span></span>

## <a name="summary"></a><span data-ttu-id="5d9ad-128">요약</span><span class="sxs-lookup"><span data-stu-id="5d9ad-128">Summary</span></span>

<span data-ttu-id="5d9ad-129">ASP.NET Core 응용 프로그램에 대 한 모든 시작 논리는 필요한 서비스 및 종속성 수 정의 되어 있으며 구성 된 단일 파일을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-129">ASP.NET Core places all startup logic for the application in a single file, in which the necessary services and dependencies can be defined and configured.</span></span> <span data-ttu-id="5d9ad-130">대체는 *web.config* 다양 한 환경 변수 뿐만 아니라 JSON와 같은 파일 형식의 활용할 수 있는 유연한 구성 기능으로는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d9ad-130">It replaces the *web.config* file with a flexible configuration feature that can leverage a variety of file formats, such as JSON, as well as environment variables.</span></span>
