---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 8 응용 프로그램 (C#)는 Windows Phone에서 Web API를 호출 합니다. | Microsoft Docs
author: rmcmurray
description: Windows Phone 8 응용 프로그램에는 책 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램의 구성 된 전체 종단 간 시나리오를 만듭니다.
ms.author: riande
ms.date: 10/09/2013
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: ca2b5f41f6c3bd38faacd1e15c4dee6f6210aff7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828345"
---
<a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="37efe-103">Windows Phone 8 응용 프로그램 (C#)에서 웹 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>
====================
<span data-ttu-id="37efe-104">[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="37efe-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="37efe-105">이 자습서에서는 Windows Phone 8 응용 프로그램에는 책 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램의 구성 된 전체 종단 간 시나리오를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="37efe-106">개요</span><span class="sxs-lookup"><span data-stu-id="37efe-106">Overview</span></span>

<span data-ttu-id="37efe-107">ASP.NET Web API와 같은 rESTful 서비스는 서버 쪽 및 클라이언트 쪽 응용 프로그램에 대 한 아키텍처를 추상화 하 여 HTTP 기반 응용 프로그램 개발자를 위한 생성을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="37efe-108">통신을 위한 전용 소켓 기반 프로토콜을 만드는 대신 웹 API 개발자가 단순히 게시 해야 해당 응용 프로그램에 대 한 필수 HTTP 메서드 (예: GET, POST, PUT, DELETE), 클라이언트 응용 프로그램 개발자만 사용 해야 하 고 응용 프로그램에 필요한 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="37efe-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="37efe-109">이 종단 간 자습서에서는 다음 프로젝트를 만들려면 Web API를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="37efe-110">에 [이 자습서의 첫 번째 부분](#STEP1), 모든 책 카탈로그를 관리 하는 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업을 지 원하는 ASP.NET Web API 응용 프로그램을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="37efe-111">이 응용 프로그램은 사용 된 [샘플 XML 파일 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) MSDN에서.</span><span class="sxs-lookup"><span data-stu-id="37efe-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="37efe-112">에 [이 자습서의 두 번째 부분](#STEP2), Web API 응용 프로그램에서 데이터를 검색 하는 대화형 Windows Phone 8 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="37efe-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="37efe-113">Prerequisites</span></span>

- <span data-ttu-id="37efe-114">Windows Phone 8 SDK가 설치 된 visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="37efe-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="37efe-115">Windows 8 또는 나중에 Hyper-v가 설치 되어 있는 64 비트 시스템</span><span class="sxs-lookup"><span data-stu-id="37efe-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="37efe-116">목록을 추가 요구 사항에 대 한 참조를 *시스템 요구 사항* 섹션에서 합니다 [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) 다운로드 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="37efe-117">Web API 및 로컬 시스템에서 Windows Phone 8 프로젝트 간의 연결을 테스트 하려는 경우의 지침을 수행 해야 합니다는 *[Windows Phone 8 에뮬레이터는 로컬에서 웹 API 응용 프로그램에 연결 컴퓨터](https://go.microsoft.com/fwlink/?LinkId=324014)* 테스트 환경을 설정 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>


<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="37efe-118">1 단계: 웹 API Bookstore 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="37efe-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="37efe-119">이 종단 간 자습서의 첫 번째 단계는 모든 CRUD 작업; 지 원하는 Web API 프로젝트를 만들려면 Windows Phone 응용 프로그램 프로젝트에서이 솔루션에 추가 됩니다 [2 단계](#STEP2) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="37efe-120">오픈 **Visual Studio 2013**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="37efe-121">클릭 **파일**, 한 다음 **새**를 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="37efe-122">경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **설치 됨**, 한 다음 **템플릿**, 다음 **Visual C#**, 차례로 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="37efe-123">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-123">Click image to expand</span></span>                                                                |


4. <span data-ttu-id="37efe-124">강조 표시 **ASP.NET 웹 응용 프로그램**를 입력 **BookStore** 클릭 한 다음 확인 하 고 프로젝트 이름에 대 한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="37efe-125">경우는 **새 ASP.NET 프로젝트** 대화 상자가 표시 됩니다, 선택 합니다 **Web API** 템플릿과 클릭 **확인**.</span><span class="sxs-lookup"><span data-stu-id="37efe-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="37efe-126">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-126">Click image to expand</span></span>                                                                |


6. <span data-ttu-id="37efe-127">Web API 프로젝트를 열면 프로젝트에서 샘플 컨트롤러를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="37efe-128">확장 된 **컨트롤러** 솔루션 탐색기에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="37efe-129">마우스 오른쪽 단추로 클릭 합니다 **ValuesController.cs** 파일을 선택한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="37efe-130">클릭 **확인** 삭제 확인 메시지가 표시 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="37efe-131">Web API 프로젝트에 XML 데이터 파일 추가 이 파일에는 bookstore 카탈로그의 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="37efe-132">마우스 오른쪽 단추로 클릭 합니다 **앱\_데이터** 솔루션 탐색기에서 폴더를 차례로 클릭 **추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="37efe-133">경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 강조 표시 합니다 **XML 파일** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="37efe-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="37efe-134">파일 이름을 **Books.xml**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="37efe-135">경우는 **Books.xml** 파일을 열, 파일의 코드 샘플에서 XML로 바꿉니다 **books.xml** MSDN의 파일:</span><span class="sxs-lookup"><span data-stu-id="37efe-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="37efe-136">저장 하 고 XML 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="37efe-137">Web API 프로젝트에 bookstore 모델 추가 이 모델 bookstore 응용 프로그램에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="37efe-138">마우스 오른쪽 단추로 클릭 합니다 **모델** 솔루션 탐색기에서 폴더를 클릭 **추가**를 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="37efe-139">경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 클래스 파일의 이름을 **BookDetails.cs**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="37efe-140">경우는 **BookDetails.cs** 파일이 열려, 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="37efe-141">저장 후 닫기 합니다 **BookDetails.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="37efe-142">Web API 프로젝트는 bookstore 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="37efe-143">마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 솔루션 탐색기에서 폴더를 클릭 **추가**를 클릭 하 고 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="37efe-144">경우는 **스 캐 폴드 추가** 대화 상자가 표시 됩니다, 강조 표시 **Web API 2 컨트롤러-비어 있음**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="37efe-145">경우는 **컨트롤러 추가** 대화 상자가 표시 됩니다, 컨트롤러 이름을 **BooksController**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="37efe-146">경우는 **BooksController.cs** 파일이 열려, 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="37efe-147">저장 후 닫기 합니다 **BooksController.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="37efe-148">오류를 확인 하려면 Web API 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="37efe-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="37efe-149">2 단계: Windows Phone 8 Bookstore 카탈로그 프로젝트를 추가.</span><span class="sxs-lookup"><span data-stu-id="37efe-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="37efe-150">이 종단 간 시나리오의 다음 단계를 Windows Phone 8에 대 한 카탈로그 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="37efe-151">이 응용 프로그램은 사용 합니다 *Windows Phone 데이터 바인딩된 앱* 서식 파일에 대 한 기본 사용자 인터페이스에서 만든 웹 API 응용 프로그램을 사용할지 [1 단계](#STEP1) 이 자습서에서는 데이터 원본으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="37efe-152">마우스 오른쪽 단추로 클릭 합니다 **BookStore** 솔루션에는 솔루션 탐색기에서 클릭 **추가**, 차례로 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="37efe-153">경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **설치 됨**, 다음 **Visual C#** 를 차례로 **Windows Phone**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="37efe-154">강조 표시 **Windows Phone 데이터 바인딩된 앱**를 입력 **BookCatalog** 이름과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="37efe-155">Json.NET NuGet 패키지를 추가 합니다 **BookCatalog** 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="37efe-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="37efe-156">마우스 오른쪽 단추로 클릭 **참조가** 에 대 한 합니다 **BookCatalog** 솔루션 탐색기에서 프로젝트 및 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="37efe-157">경우는 **NuGet 패키지 관리** 대화 상자가 표시 됩니다, 확장을 **Online** 섹션을 강조 표시 **nuget.org**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="37efe-158">입력 **Json.NET** 검색에 필드 및 검색 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="37efe-159">강조 표시 **Json.NET** 검색 결과 및 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="37efe-160">설치가 완료 되 면 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="37efe-161">추가 된 **BookDetails** 모델을 **BookCatalog** 프로젝트; bookstore 클래스의 일반 모델을 포함:</span><span class="sxs-lookup"><span data-stu-id="37efe-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="37efe-162">마우스 오른쪽 단추로 클릭 합니다 **BookCatalog** 클릭 한 다음 솔루션 탐색기에서 프로젝트 **추가**를 클릭 하 고 **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="37efe-163">새 폴더의 이름을 **모델**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="37efe-164">마우스 오른쪽 단추로 클릭 합니다 **모델** 솔루션 탐색기에서 폴더를 클릭 **추가**를 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="37efe-165">경우는 **새 항목 추가** 대화 상자가 표시 됩니다, 클래스 파일의 이름을 **BookDetails.cs**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="37efe-166">경우는 **BookDetails.cs** 파일이 열려, 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="37efe-167">저장 후 닫기 합니다 **BookDetails.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="37efe-168">업데이트를 **MainViewModel.cs** BookStore Web API 응용 프로그램과 통신 하는 기능을 포함 하도록 클래스:</span><span class="sxs-lookup"><span data-stu-id="37efe-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="37efe-169">확장을 **ViewModels** 폴더의 솔루션 탐색기에서 마우스 두 번 클릭 합니다 **MainViewModel.cs** 파일.</span><span class="sxs-lookup"><span data-stu-id="37efe-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="37efe-170">경우는 **MainViewModel.cs** 파일을 열면 파일의 코드를 다음으로 바꿉니다; 값을 업데이트 해야 하는 `apiUrl` Web API의 실제 URL을 사용 하 여 상수:</span><span class="sxs-lookup"><span data-stu-id="37efe-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="37efe-171">저장 후 닫기 합니다 **MainViewModel.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="37efe-172">업데이트를 **MainPage.xaml** 응용 프로그램 이름에 맞게 파일:</span><span class="sxs-lookup"><span data-stu-id="37efe-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="37efe-173">두 번 클릭 합니다 **MainPage.xaml** 솔루션 탐색기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="37efe-174">경우는 **MainPage.xaml** 파일이 열려, 코드의 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="37efe-175">다음을 사용 하 여 해당 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="37efe-176">저장 후 닫기 합니다 **MainPage.xaml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="37efe-177">업데이트를 **DetailsPage.xaml** 표시 된 항목을 사용자 지정 파일:</span><span class="sxs-lookup"><span data-stu-id="37efe-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="37efe-178">두 번 클릭 합니다 **DetailsPage.xaml** 솔루션 탐색기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="37efe-179">경우는 **DetailsPage.xaml** 파일이 열려, 코드의 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="37efe-180">다음을 사용 하 여 해당 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="37efe-181">저장 후 닫기 합니다 **DetailsPage.xaml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="37efe-182">오류를 확인 하려면 Windows Phone 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="37efe-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="37efe-183">종단 간 솔루션을 테스트 하는 3 단계:</span><span class="sxs-lookup"><span data-stu-id="37efe-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="37efe-184">에 설명 된 대로 합니다 *필수 구성 요소* 의 지침에 따라 해야, 로컬 시스템에서이 자습서에서는 Web API 및 Windows Phone 8 간의 연결을 테스트 하는 경우 부분 프로젝트를 *[ 로컬 컴퓨터에서 웹 API 응용 프로그램에 연결 하는 Windows Phone 8 Emulator](https://go.microsoft.com/fwlink/?LinkId=324014)* 테스트 환경을 설정 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="37efe-185">구성 테스트 환경을 만든 후에 Windows Phone 응용 프로그램을 시작 프로젝트로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="37efe-186">이렇게 하려면 강조 표시 합니다 **BookCatalog** 솔루션 탐색기를 클릭 한 다음 응용 프로그램 **시작 프로젝트로 설정**:</span><span class="sxs-lookup"><span data-stu-id="37efe-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="37efe-187">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-187">Click image to expand</span></span> |

<span data-ttu-id="37efe-188">F5 키를 눌러 Visual Studio 모두에서 Windows Phone 에뮬레이터를 표시 하는 시작 됩니다는 &quot;기다리십시오&quot; 응용 프로그램 데이터를 검색 하는 동안 웹 API에서 메시지:</span><span class="sxs-lookup"><span data-stu-id="37efe-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="37efe-189">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-189">Click image to expand</span></span> |

<span data-ttu-id="37efe-190">모든 항목이 성공 하면 표시 되는 카탈로그를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="37efe-191">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-191">Click image to expand</span></span> |

<span data-ttu-id="37efe-192">모든 책 제목을 누르면, 책 설명 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="37efe-193">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-193">Click image to expand</span></span> |

<span data-ttu-id="37efe-194">응용 프로그램은 Web API와 통신할 수 없습니다, 하는 경우 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="37efe-195">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-195">Click image to expand</span></span> |

<span data-ttu-id="37efe-196">오류 메시지를 누르면 오류에 대 한 추가 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>


| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="37efe-197">확장 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37efe-197">Click image to expand</span></span>                                                                 |

