---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 2 ASP.NET MVC 1.0 응용 프로그램 업그레이드 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 모두 수동으로 하 고 마법사를 사용 하 여 ASP.NET MVC 2를 ASP.NET MVC 1.0 응용 프로그램을 업그레이드 하는 방법입니다. 이 문서는 d에 대 한도 중...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 3de69df7e80037de35c2609232f4574bc9d03c80
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837605"
---
<a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="e4a74-104">ASP.NET MVC 2 ASP.NET MVC 1.0 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e4a74-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>
====================
> <span data-ttu-id="e4a74-105">이 문서에서는 모두 수동으로 하 고 마법사를 사용 하 여 ASP.NET MVC 2를 ASP.NET MVC 1.0 응용 프로그램을 업그레이드 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="e4a74-106">이 문서에 대 한도 [다운로드](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span><span class="sxs-lookup"><span data-stu-id="e4a74-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>


## <a name="introduction"></a><span data-ttu-id="e4a74-107">소개</span><span class="sxs-lookup"><span data-stu-id="e4a74-107">Introduction</span></span>

<span data-ttu-id="e4a74-108">ASP.NET MVC 2는 동일한 서버에 ASP.NET MVC 1.0 나란히 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="e4a74-109">이렇게 하면 응용 프로그램 개발자가 유연 하 게 ASP.NET MVC 2를 ASP.NET MVC 1.0 응용 프로그램을 업그레이드 하는 경우 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="e4a74-110">Visual Studio 2010에서 ASP.NET MVC 2 Visual Studio 2008을 사용 하 여 기존 ASP.NET MVC 1.0 프로젝트 작성 하는 업그레이드 마법사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="e4a74-111">Visual Studio 2010의 ASP.NET MVC 1.0 프로젝트를 열어 업그레이드 마법사 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="e4a74-112">Visual Studio 2008 SP1에서 ASP.NET MVC 1.0에 대 한 마법사를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="e4a74-113">Visual Studio 2008 SP1에서 ASP.NET MVC 2를 ASP.NET MVC 1.0 응용 프로그램을 업그레이드 하려면 (지원 되지 않는) MvcAppConverter 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="e4a74-114">다음 URL에서이 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="e4a74-115">ASP.NET MVC 1.0 프로젝트를 수동으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e4a74-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="e4a74-116">기존 ASP.NET MVC 1.0 응용 프로그램 버전 2 수동으로 업그레이드 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="e4a74-117">기존 프로젝트의 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="e4a74-118">텍스트 편집기에서 프로젝트 파일 (.csproj 또는.vbproj 파일 확장명과 파일)를 열고 ProjectTypeGuid 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="e4a74-119">해당 요소의 값으로 GUID를 {603c0e0b-db56-11dc-be95-000d561079b0} {F85E285D-A4E0-4152-9332-AB1D724D3325}를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="e4a74-120">완료 되 면 해당 요소의 값은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="e4a74-121">웹 응용 프로그램 루트 폴더에 Web.config 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="e4a74-122">System.Web.Mvc, 버전에 대 한 검색 System.Web.Mvc, 버전을 사용 하 여 모든 인스턴스를 바꾸고 1.0.0.0 = 2.0.0.0 =.</span><span class="sxs-lookup"><span data-stu-id="e4a74-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="e4a74-123">Views 폴더에 있는 Web.config 파일에 대 한 이전 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="e4a74-124">Visual Studio를 사용 하 여 프로젝트를 열 및 **솔루션 탐색기**를 확장 합니다 **참조** 노드.</span><span class="sxs-lookup"><span data-stu-id="e4a74-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="e4a74-125">System.Web.Mvc (버전 1.0 어셈블리 가리킴 함)에 대 한 참조를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="e4a74-126">System.Web.Mvc (v2.0.0.0)에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="e4a74-127">구성 섹션에서 응용 프로그램 루트에서 Web.config 파일에 다음 bindingRedirect 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="e4a74-128">새 빈 ASP.NET MVC 2 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="e4a74-129">기존 응용 프로그램의 스크립트 폴더에 새 응용 프로그램의 스크립트 폴더에서 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="e4a74-130">기존 응용 프로그램의 업데이트™ Site.css 파일에서 CSS 스타일 정의 사용 하 여 s CSS 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="e4a74-131">응용 프로그램을 컴파일하고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-131">Compile the application and run it.</span></span> <span data-ttu-id="e4a74-132">오류가 발생 하는 경우의 주요 변경 내용 섹션을 참조 합니다 [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e4a74-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
