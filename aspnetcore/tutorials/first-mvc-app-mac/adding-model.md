---
title: Mac용 Visual Studio을 사용하여 ASP.NET Core MVC 앱에 모델 추가
author: rick-anderson
description: 간단한 ASP.NET Core 앱에 모델을 추가합니다.
manager: wpickett
ms.author: riande
ms.date: 09/22/2017
ms.devlang: csharp
ms.prod: .net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-mac/adding-model
ms.openlocfilehash: 6792dbc7c9ab063d85c0c4145481b8fd6b40da63
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app-with-visual-studio-for-mac"></a><span data-ttu-id="ad3bb-103">Mac용 Visual Studio을 사용하여 ASP.NET Core MVC 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="ad3bb-103">Add a model to an ASP.NET Core MVC app with Visual Studio for Mac</span></span>

[!INCLUDE [adding-model](../../includes/mvc-intro/adding-model1.md)]

* <span data-ttu-id="ad3bb-104">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-104">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span> 
* <span data-ttu-id="ad3bb-105">**새 파일** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="ad3bb-105">In the **New File** dialog:</span></span>

  * <span data-ttu-id="ad3bb-106">왼쪽 창에서 **일반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-106">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="ad3bb-107">가운데 창에서 **빈 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-107">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="ad3bb-108">클래스 이름을 **Movie**로 지정하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-108">Name the class **Movie** and select **New**.</span></span>

<span data-ttu-id="ad3bb-109">`Movie` 클래스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-109">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="ad3bb-110">`ID` 필드는 데이터베이스에서 기본 키 대신 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-110">The `ID` field is required by the database for the primary key.</span></span>

<span data-ttu-id="ad3bb-111">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-111">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="ad3bb-112">이제 **M**VC 앱에 **모**델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-112">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="prepare-the-project-for-scaffolding"></a><span data-ttu-id="ad3bb-113">프로젝트에서 스캐폴딩을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-113">Prepare the project for scaffolding</span></span>

- <span data-ttu-id="ad3bb-114">프로젝트 파일을 마우스 오른쪽 단추로 클릭하고 **도구 > 파일 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-114">Right click on the project file, and then select **Tools > Edit File**.</span></span>

  ![위의 단계 보기](adding-model/_static/1.png)

- <span data-ttu-id="ad3bb-116">다음 강조 표시된 NuGet 패키지를 *MvcMovie.csproj* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-116">Add the following highlighted NuGet packages to the *MvcMovie.csproj* file:</span></span>
             
  [!code-csharp[](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- <span data-ttu-id="ad3bb-117">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-117">Save the file.</span></span>

- <span data-ttu-id="ad3bb-118">*Models/MvcMovieContext.cs* 파일을 만들고 다음 `MvcMovieContext` 클래스를 추가합니다. [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span><span class="sxs-lookup"><span data-stu-id="ad3bb-118">Create a *Models/MvcMovieContext.cs* file and add the following `MvcMovieContext` class:  [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span></span>
   
- <span data-ttu-id="ad3bb-119">*Startup.cs* 파일을 열고 두 개의 using을 추가합니다. [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span><span class="sxs-lookup"><span data-stu-id="ad3bb-119">Open the *Startup.cs* file and add two usings:  [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span></span>

- <span data-ttu-id="ad3bb-120">데이터베이스 컨텍스트를 *Startup.cs* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-120">Add the database context to the *Startup.cs* file:</span></span>

   [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  <span data-ttu-id="ad3bb-121">이 코드는 데이터 모델에 포함되는 모델 클래스를 Entity Framework에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-121">This tells Entity Framework which model classes are included in the data model.</span></span> <span data-ttu-id="ad3bb-122">데이터베이스에서 Movie 테이블을 표현할 Movie 개체의 *엔터티 집합* 하나를 정의하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-122">You're defining one *entity set* of Movie objects, which will be represented in the database as a Movie table.</span></span>

- <span data-ttu-id="ad3bb-123">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-123">Build the project to verify there are no errors.</span></span>

## <a name="scaffold-the-moviecontroller"></a><span data-ttu-id="ad3bb-124">MovieController 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="ad3bb-124">Scaffold the MovieController</span></span>

<span data-ttu-id="ad3bb-125">프로젝트 폴더에서 터미널 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-125">Open a terminal window in the project folder and run the following commands:</span></span>

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
<span data-ttu-id="ad3bb-126">오류 `No executable found matching command "dotnet-aspnet-codegenerator", verify`가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="ad3bb-126">If you get the error `No executable found matching command "dotnet-aspnet-codegenerator", verify`:</span></span>

 * <span data-ttu-id="ad3bb-127">현재 위치가 프로젝트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-127">You are in the project directory.</span></span> <span data-ttu-id="ad3bb-128">프로젝트 디렉터리에는 *Program.cs*, *Startup.cs* 및 *.csproj* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-128">The project directory has the *Program.cs*, *Startup.cs* and *.csproj* files.</span></span>
 * <span data-ttu-id="ad3bb-129">dotnet 버전이 1.1 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-129">Your dotnet version is 1.1 or higher.</span></span> <span data-ttu-id="ad3bb-130">`dotnet`을 실행하여 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-130">Run `dotnet` to get the version.</span></span>
 * <span data-ttu-id="ad3bb-131">`<DotNetCliToolReference>` 요소를 [MvcMovie.csproj 파일](#prepare-the-project-for-scaffolding)에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-131">You have added the `<DotNetCliToolReference>` element to the [MvcMovie.csproj file](#prepare-the-project-for-scaffolding).</span></span>
 
<!--
> [!NOTE]
> If you get an error when the scaffolding command runs, see [issue 444 in the scaffolding repository](https://github.com/aspnet/scaffolding/issues/444) for a workaround.
-->

<span data-ttu-id="ad3bb-132">스캐폴딩 엔진은 다음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-132">The scaffolding engine creates the following:</span></span>

* <span data-ttu-id="ad3bb-133">동영상 컨트롤러(*Controllers/MoviesController.cs*)</span><span class="sxs-lookup"><span data-stu-id="ad3bb-133">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="ad3bb-134">만들기, 삭제, 세부 정보, 편집 및 인덱스 페이지에 대한 Razor 뷰 파일(*Views/Movies/\*.cshtml*)</span><span class="sxs-lookup"><span data-stu-id="ad3bb-134">Razor view files for Create, Delete, Details, Edit and Index pages (*Views/Movies/\*.cshtml*)</span></span>

<span data-ttu-id="ad3bb-135">[CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)(만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 자동으로 만드는 작업을 *스캐폴딩*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-135">The automatic creation of [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="ad3bb-136">동영상 데이터베이스를 관리할 수 있는 완벽하게 작동하는 웹 응용 프로그램이 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-136">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

### <a name="add-the-files-to-visual-studio"></a><span data-ttu-id="ad3bb-137">Visual Studio에 파일 추가</span><span class="sxs-lookup"><span data-stu-id="ad3bb-137">Add the files to Visual Studio</span></span>

* <span data-ttu-id="ad3bb-138">*MovieController.cs* 파일을 Visual Studio 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-138">Add the *MovieController.cs* file to the Visual Studio project:</span></span>

  * <span data-ttu-id="ad3bb-139">*Controllers* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 > 파일 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-139">Right-click on the *Controllers* folder and select **Add > Add Files**.</span></span>
  * <span data-ttu-id="ad3bb-140">*MovieController.cs* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-140">Select the *MovieController.cs* file.</span></span>

* <span data-ttu-id="ad3bb-141">*Movies* 폴더 및 뷰를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-141">Add the *Movies* folder and views:</span></span>

  * <span data-ttu-id="ad3bb-142">*Views* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 > 기존 폴더 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-142">Right-click on the *Views* folder and select **Add > Add Existing Folder**.</span></span>
  * <span data-ttu-id="ad3bb-143">*Views* 폴더로 이동하고, *Views\Movies*를 선택하고 나서, **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-143">Navigate to the *Views* folder, select *Views\Movies*, and then select **Open**.</span></span>
  * <span data-ttu-id="ad3bb-144">**Movies에서 추가할 파일 선택** 대화 상자에서 **모두 포함**, **확인**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-144">In the **Select files to add from Movies** dialog, select **Include All**, and then **OK**.</span></span>

[!INCLUDE [adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE [adding-model](../../includes/mvc-intro/adding-model3.md)]

<span data-ttu-id="ad3bb-145">이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-145">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="ad3bb-146">다음 자습서에서는 데이터베이스 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad3bb-146">In the next tutorial, we'll work with the database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad3bb-147">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ad3bb-147">Additional resources</span></span>

* [<span data-ttu-id="ad3bb-148">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ad3bb-148">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="ad3bb-149">전역화 및 지역화</span><span class="sxs-lookup"><span data-stu-id="ad3bb-149">Globalization and localization</span></span>](xref:fundamentals/localization)

> [!div class="step-by-step"]
> <span data-ttu-id="ad3bb-150">[이전 뷰 추가](adding-view.md)
> [다음 SQL 사용](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="ad3bb-150">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  
