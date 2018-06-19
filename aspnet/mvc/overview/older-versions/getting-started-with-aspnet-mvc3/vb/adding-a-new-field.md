---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: 영화 모델 및 데이터베이스 테이블 (VB)에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 5927b7d977e375881fe618b4b844cbd708023ba1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877322"
---
<a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a><span data-ttu-id="5c384-103">영화 모델 및 데이터베이스 테이블 (VB)에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="5c384-103">Adding a New Field to the Movie Model and Database Table (VB)</span></span>
====================
<span data-ttu-id="5c384-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5c384-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="5c384-105">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5c384-106">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5c384-107">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5c384-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5c384-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5c384-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5c384-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="5c384-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5c384-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="5c384-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5c384-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5c384-113">이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="5c384-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="5c384-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5c384-115">원하는 경우 C#으로 전환 된 [C# 버전](../cs/adding-a-new-field.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-115">If you prefer C#, switch to the [C# version](../cs/adding-a-new-field.md) of this tutorial.</span></span>


<span data-ttu-id="5c384-116">이 섹션에서는 모델 클래스를 일부 변경 하 고 모델 변경 내용과 일치 하도록 데이터베이스 스키마를 업데이트 하는 방법을 알아보려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-116">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="5c384-117">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="5c384-117">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="5c384-118">추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-118">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="5c384-119">열기는 *Movie.cs* 파일을 추가 `Rating` 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="5c384-119">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

<span data-ttu-id="5c384-120">전체 `Movie` 다음 코드 처럼 이제 보이는 클래스:</span><span class="sxs-lookup"><span data-stu-id="5c384-120">The complete `Movie` class now looks like the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

<span data-ttu-id="5c384-121">사용 하 여 응용 프로그램을 다시 컴파일하는 **디버그** &gt; **빌드 영화** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-121">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="5c384-122">업데이트 한 했으므로 `Model` 클래스도 업데이트 해야는 *\Views\Movies\Index.vbhtml* 및 *\Views\Movies\Create.vbhtml* 새 지원하기위해템플릿을보려면`Rating`속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-122">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.vbhtml* and *\Views\Movies\Create.vbhtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="5c384-123">열기는<em>\Views\Movies\Index.vbhtml</em> 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤의 <strong>가격</strong> 열입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-123">Open the<em>\Views\Movies\Index.vbhtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="5c384-124">다음 추가 `<td>` 열을 렌더링 하는 서식 파일의 끝 부분에서 `@item.Rating` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-124">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="5c384-125">다음은 이러한 어떤 업데이트 된 <em>Index.vbhtml</em> 보기 템플릿은 보입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-125">Below is what the updated <em>Index.vbhtml</em> view template looks like:</span></span>

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

<span data-ttu-id="5c384-126">을 열고는 *\Views\Movies\Create.vbhtml* 파일을 폼의 끝 부분에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-126">Next, open the *\Views\Movies\Create.vbhtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="5c384-127">이 렌더링 하는 텍스트 상자가 새 동영상 만들어질 때에 대 한 등급을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-127">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="5c384-128">데이터베이스 스키마의 차이점 및 모델 관리</span><span class="sxs-lookup"><span data-stu-id="5c384-128">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="5c384-129">새 지원 하기 위해 응용 프로그램 코드를 지금 업데이트 한 `Rating` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-129">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="5c384-130">이제 응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-130">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="5c384-131">이 작업을 수행 하지만 다음과 같은 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-131">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="5c384-132">때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다르면 이제는 `Movie` 기존 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-132">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="5c384-133">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="5c384-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="5c384-134">기본적으로를 사용 하 여 Entity Framework Code First 자동으로 데이터베이스를 만들려면이 자습서의 앞부분에서 마찬가지로 코드 첫 번째 테이블에 추가 데이터베이스는 데이터베이스의 스키마에서 생성 된 모델 클래스 동기화 되어 있는지 여부를 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-134">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="5c384-135">동기화 하지 않을 경우 Entity Framework에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-135">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="5c384-136">이렇게 하면 그렇지 않으면만 찾을 수 (모호한 오류)에 의해 런타임 시 개발 시 문제를 추적 하기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-136">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="5c384-137">방금 표시 된 오류 메시지가 표시 될 놓이게 되어 하는 동기화 확인 기능.</span><span class="sxs-lookup"><span data-stu-id="5c384-137">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="5c384-138">오류를 해결 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-138">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="5c384-139">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-139">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="5c384-140">이 방법은 매우 편리 하 게 테스트 데이터베이스에 대해 개발을 수행할 때 함께 모델 및 데이터베이스 스키마를 신속 하 게 개발할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-140">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="5c384-141">데이터베이스의 기존 데이터 손실의 단점은 하지만입니다-하므로 있습니다 *하지 않는* 는 프로덕션 데이터베이스에서이 방법을 사용!</span><span class="sxs-lookup"><span data-stu-id="5c384-141">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="5c384-142">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-142">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="5c384-143">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-143">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="5c384-144">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-144">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="5c384-145">이 자습서에서는 첫 번째 방법을 사용 합니다-는 Entity Framework Code First 모델이 변경 언제 든 지 자동으로 데이터베이스를 다시 만드는으로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-145">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="5c384-146">자동으로 다시 모델 변경 내용에 데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="5c384-146">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="5c384-147">Code First 자동으로 삭제 하 고 응용 프로그램에 대 한 모델을 변경 하면 언제 든 지 데이터베이스를 다시 생성 되도록 응용 프로그램을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-147">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5c384-148">**경고** 자동으로 삭제 하 고 개발 또는 테스트 데이터베이스를 사용 하는 경우에 데이터베이스를 다시 작성이 접근 방식을 사용 하도록 설정 해야 하 고 *되지* 실제 데이터를 포함 하는 프로덕션 데이터베이스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-148">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="5c384-149">프로덕션 서버에서 사용 하 여 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-149">Using it on a production server can lead to data loss.</span></span>


<span data-ttu-id="5c384-150">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-150">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="5c384-151">클래스의 이름을 &quot;MovieInitializer&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-151">Name the class &quot;MovieInitializer&quot;.</span></span> <span data-ttu-id="5c384-152">업데이트는 `MovieInitializer` 다음 코드를 포함 하는 클래스:</span><span class="sxs-lookup"><span data-stu-id="5c384-152">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

<span data-ttu-id="5c384-153">`MovieInitializer` 클래스 모델에 의해 사용 되는 데이터베이스는 삭제 후 모델 클래스를 변경할 경우 자동으로 다시 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-153">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="5c384-154">코드에는 `Seed` 메서드 시간을 자동으로 추가 하려면 데이터베이스에 있는 일부 기본 데이터를 지정 하는 생성 (또는 다시 생성).</span><span class="sxs-lookup"><span data-stu-id="5c384-154">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="5c384-155">이 데이터베이스를 채우는 예제 데이터를 수동으로 변경 하는 모델을 만들 때마다 채우기 할 필요 없이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-155">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="5c384-156">정의 했으므로 `MovieInitializer` 응용 프로그램이 실행 될 때마다 확인 모델 클래스는 데이터베이스의 스키마와에서 다른 지 있도록를 연결 하려는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-156">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="5c384-157">인 경우에 모델과 일치를 다음 예제 데이터는 데이터베이스를 채우는 데이터베이스를 다시 만들려고 이니셜라이저를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-157">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="5c384-158">열기는 *Global.asax* 의 루트에 있는 파일의 `MvcMovies` 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="5c384-158">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

<span data-ttu-id="5c384-159">*Global.asax* 파일 프로젝트에 대 한 전체 응용 프로그램을 정의 하 고 포함 하는 클래스를 포함 한 `Application_Start` 응용 프로그램을 처음 시작할 때 실행 되는 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-159">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="5c384-160">찾을 `Application_Start` 메서드 호출을 추가 하 고 `Database.SetInitializer` 아래와 같이 메서드의 시작 부분에서:</span><span class="sxs-lookup"><span data-stu-id="5c384-160">Find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

<span data-ttu-id="5c384-161">`Database.SetInitializer` 방금 추가한 문을 나타냅니다 데이터베이스에서 사용 된 `MovieDBContext` 인스턴스를 자동으로 삭제 하 고 일치 하지 않으면 스키마 및 데이터베이스를 다시 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-161">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="5c384-162">예제 데이터에 지정 된 데이터베이스도 채웁니다 살펴본 것 처럼 및는 `MovieInitializer` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-162">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="5c384-163">닫기는 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-163">Close the *Global.asax* file.</span></span>

<span data-ttu-id="5c384-164">응용 프로그램을 다시 실행을 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-164">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="5c384-165">응용 프로그램이 시작 되 면 모델 구조는 데이터베이스 스키마를 더 이상 일치 하는지 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-165">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="5c384-166">자동으로 새 모델 구조와 일치 하도록 데이터베이스를 다시 생성 하 고는 샘플 동영상 데이터베이스에 데이터가 채워지고:</span><span class="sxs-lookup"><span data-stu-id="5c384-166">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

<span data-ttu-id="5c384-168">클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-168">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="5c384-169">참고에 대 한 등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-169">Note that you can add a rating.</span></span>

<span data-ttu-id="5c384-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5c384-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span></span>

<span data-ttu-id="5c384-171">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-171">Click **Create**.</span></span> <span data-ttu-id="5c384-172">등급을 포함 하 여 새 동영상은 이제 나열 영화에서 표시:</span><span class="sxs-lookup"><span data-stu-id="5c384-172">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

<span data-ttu-id="5c384-174">이 섹션에서는 모델 개체를 수정할 데이터베이스의 변경 내용과 동기화 된 상태로 유지 하는 방법을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-174">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="5c384-175">또한 시나리오를 체험할 수 있도록 샘플 데이터로 새로 만든된 데이터베이스를 채우는 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-175">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="5c384-176">다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 해야 할 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5c384-176">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c384-177">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="5c384-177">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
