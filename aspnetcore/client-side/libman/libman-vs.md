---
title: Visual Studio에서 ASP.NET Core와 함께 사용 하 여 LibMan
author: scottaddie
description: LibMan Visual Studio를 사용 하 여 ASP.NET Core 프로젝트에서 사용 하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 08/20/2018
uid: client-side/libman/libman-vs
ms.openlocfilehash: 727bd80b7f37f6ebd9d37b7aab1aa6c33b85678c
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206729"
---
# <a name="use-libman-with-aspnet-core-in-visual-studio"></a><span data-ttu-id="d2401-103">Visual Studio에서 ASP.NET Core와 함께 사용 하 여 LibMan</span><span class="sxs-lookup"><span data-stu-id="d2401-103">Use LibMan with ASP.NET Core in Visual Studio</span></span>

<span data-ttu-id="d2401-104">작성자: [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="d2401-104">By [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="d2401-105">Visual Studio는 기본 제공 [LibMan](xref:client-side/libman/index) 포함 하 여 ASP.NET Core 프로젝트에서:</span><span class="sxs-lookup"><span data-stu-id="d2401-105">Visual Studio has built-in support for [LibMan](xref:client-side/libman/index) in ASP.NET Core projects, including:</span></span>

* <span data-ttu-id="d2401-106">구성 하 고 빌드 시 LibMan 복원 작업 실행을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-106">Support for configuring and running LibMan restore operations on build.</span></span>
* <span data-ttu-id="d2401-107">LibMan 복원 및 정리 작업을 트리거하기 위한 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-107">Menu items for triggering LibMan restore and clean operations.</span></span>
* <span data-ttu-id="d2401-108">라이브러리를 찾고 파일을 프로젝트에 추가 하기 위한 검색 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-108">Search dialog for finding libraries and adding the files to a project.</span></span>
* <span data-ttu-id="d2401-109">편집에 대 한 지원과 *libman.json*&mdash;LibMan 매니페스트 파일.</span><span class="sxs-lookup"><span data-stu-id="d2401-109">Editing support for *libman.json*&mdash;the LibMan manifest file.</span></span>

<span data-ttu-id="d2401-110">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/libman/samples/) [(다운로드 방법)](xref:index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="d2401-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/client-side/libman/samples/) [(how to download)](xref:index#how-to-download-a-sample)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2401-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="d2401-111">Prerequisites</span></span>

* <span data-ttu-id="d2401-112">Visual Studio 2017 버전 15.8 이상 합니다 **ASP.NET 및 웹 개발** 워크 로드</span><span class="sxs-lookup"><span data-stu-id="d2401-112">Visual Studio 2017 version 15.8 or later with the **ASP.NET and web development** workload</span></span>

## <a name="add-library-files"></a><span data-ttu-id="d2401-113">라이브러리 파일 추가</span><span class="sxs-lookup"><span data-stu-id="d2401-113">Add library files</span></span>

<span data-ttu-id="d2401-114">라이브러리 파일은 두 가지 방법으로 ASP.NET Core 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-114">Library files can be added to an ASP.NET Core project in two different ways:</span></span>

1. [<span data-ttu-id="d2401-115">클라이언트 쪽 라이브러리 추가 대화 상자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-115">Use the Add Client-Side Library dialog</span></span>](#use-the-add-client-side-library-dialog)
1. [<span data-ttu-id="d2401-116">LibMan 매니페스트 파일 항목을 수동으로 구성</span><span class="sxs-lookup"><span data-stu-id="d2401-116">Manually configure LibMan manifest file entries</span></span>](#manually-configure-libman-manifest-file-entries)

### <a name="use-the-add-client-side-library-dialog"></a><span data-ttu-id="d2401-117">클라이언트 쪽 라이브러리 추가 대화 상자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-117">Use the Add Client-Side Library dialog</span></span>

<span data-ttu-id="d2401-118">클라이언트 쪽 라이브러리를 설치 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-118">Follow these steps to install a client-side library:</span></span>

* <span data-ttu-id="d2401-119">**솔루션 탐색기**, 파일을 추가 해야 합니다는 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-119">In **Solution Explorer**, right-click the project folder in which the files should be added.</span></span> <span data-ttu-id="d2401-120">선택할 **추가할** > **클라이언트 쪽 라이브러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-120">Choose **Add** > **Client-Side Library**.</span></span> <span data-ttu-id="d2401-121">합니다 **클라이언트 쪽 라이브러리 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-121">The **Add Client-Side Library** dialog appears:</span></span>

  ![추가 클라이언트 쪽 라이브러리 대화 상자](_static/add-library-dialog.png)

* <span data-ttu-id="d2401-123">라이브러리 공급자를 선택 합니다 **공급자** 드롭다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-123">Select the library provider from the **Provider** drop down.</span></span> <span data-ttu-id="d2401-124">CDNJS 기본 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-124">CDNJS is the default provider.</span></span>
* <span data-ttu-id="d2401-125">형식 라이브러리 이름 대로 인출 하는 **라이브러리** 입력란입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-125">Type the library name to fetch in the **Library** text box.</span></span> <span data-ttu-id="d2401-126">IntelliSense는 제공된 된 텍스트를 사용 하 여 시작 하는 라이브러리의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-126">IntelliSense provides a list of libraries beginning with the provided text.</span></span>
* <span data-ttu-id="d2401-127">IntelliSense 목록에서 라이브러리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-127">Select the library from the IntelliSense list.</span></span> <span data-ttu-id="d2401-128">라이브러리 이름이 붙습니다 통지를 `@` 기호 및 선택한 공급자에 게 알려진 안정적인 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-128">Notice the library name is suffixed with the `@` symbol and the latest stable version known to the selected provider.</span></span>
* <span data-ttu-id="d2401-129">포함할 파일을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-129">Decide which files to include:</span></span>
  * <span data-ttu-id="d2401-130">선택 된 **모든 라이브러리 파일을 포함** 라디오 단추를 포함 하는 모든 라이브러리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-130">Select the **Include all library files** radio button to include all of the library's files.</span></span>
  * <span data-ttu-id="d2401-131">선택 된 **특정 파일 선택** 라이브러리의 파일 하위 집합을 포함 하려면 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-131">Select the **Choose specific files** radio button to include a subset of the library's files.</span></span> <span data-ttu-id="d2401-132">라디오 단추를 선택 하 고, 파일 선택기 트리에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-132">When the radio button is selected, the file selector tree is enabled.</span></span> <span data-ttu-id="d2401-133">다운로드 파일 이름의 왼쪽에 있는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-133">Check the boxes to the left of the file names to download.</span></span>
* <span data-ttu-id="d2401-134">파일을 저장 하는 것에 대 한 프로젝트 폴더를 지정 합니다 **대상 위치** 입력란입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-134">Specify the project folder for storing the files in the **Target Location** text box.</span></span> <span data-ttu-id="d2401-135">권장 구성으로 각 라이브러리를 별도 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-135">As a recommendation, store each library in a separate folder.</span></span>

  <span data-ttu-id="d2401-136">제안 **대상 위치** 폴더 대화 상자 시작 된 위치를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-136">The suggested **Target Location** folder is based on the location from which the dialog launched:</span></span>

  * <span data-ttu-id="d2401-137">프로젝트 루트에서 시작:</span><span class="sxs-lookup"><span data-stu-id="d2401-137">If launched from the project root:</span></span>
    * <span data-ttu-id="d2401-138">*wwwroot/lib* 경우에 사용 됩니다 *wwwroot* 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-138">*wwwroot/lib* is used if *wwwroot* exists.</span></span>
    * <span data-ttu-id="d2401-139">*lib* 경우에 사용 됩니다 *wwwroot* 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-139">*lib* is used if *wwwroot* doesn't exist.</span></span>
  * <span data-ttu-id="d2401-140">프로젝트 폴더에서 시작 하는 경우에 해당 폴더 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-140">If launched from a project folder, the corresponding folder name is used.</span></span>

  <span data-ttu-id="d2401-141">폴더 제안 라이브러리 이름이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-141">The folder suggestion is suffixed with the library name.</span></span> <span data-ttu-id="d2401-142">다음 표에서 Razor 페이지 프로젝트에 jQuery를 설치 하는 경우 폴더 제안을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-142">The following table illustrates folder suggestions when installing jQuery in a Razor Pages project.</span></span>
  
  |<span data-ttu-id="d2401-143">시작 위치</span><span class="sxs-lookup"><span data-stu-id="d2401-143">Launch location</span></span>                           |<span data-ttu-id="d2401-144">제안 된 폴더</span><span class="sxs-lookup"><span data-stu-id="d2401-144">Suggested folder</span></span>      |
  |------------------------------------------|----------------------|
  |<span data-ttu-id="d2401-145">프로젝트 루트 (하는 경우 *wwwroot* 존재)</span><span class="sxs-lookup"><span data-stu-id="d2401-145">project root (if *wwwroot* exists)</span></span>        |<span data-ttu-id="d2401-146">*jquery/wwwroot/lib /*</span><span class="sxs-lookup"><span data-stu-id="d2401-146">*wwwroot/lib/jquery/*</span></span> |
  |<span data-ttu-id="d2401-147">프로젝트 루트 (하는 경우 *wwwroot* 존재 하지 않는)</span><span class="sxs-lookup"><span data-stu-id="d2401-147">project root (if *wwwroot* doesn't exist)</span></span> |<span data-ttu-id="d2401-148">*lib/jquery /*</span><span class="sxs-lookup"><span data-stu-id="d2401-148">*lib/jquery/*</span></span>         |
  |<span data-ttu-id="d2401-149">*페이지* 프로젝트의 폴더</span><span class="sxs-lookup"><span data-stu-id="d2401-149">*Pages* folder in project</span></span>                 |<span data-ttu-id="d2401-150">*페이지/jquery /*</span><span class="sxs-lookup"><span data-stu-id="d2401-150">*Pages/jquery/*</span></span>       |

* <span data-ttu-id="d2401-151">클릭 합니다 **설치** 에서 구성에 따라 파일을 다운로드 하려면 단추 *libman.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-151">Click the **Install** button to download the files, per the configuration in *libman.json*.</span></span>
* <span data-ttu-id="d2401-152">검토 합니다 **라이브러리 관리자** 의 피드 합니다 **출력** 설치 세부 정보 창.</span><span class="sxs-lookup"><span data-stu-id="d2401-152">Review the **Library Manager** feed of the **Output** window for installation details.</span></span> <span data-ttu-id="d2401-153">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d2401-153">For example:</span></span>

  ```console
  Restore operation started...
  Restoring libraries for project LibManSample
  Restoring library jquery@3.3.1... (LibManSample)
  wwwroot/lib/jquery/jquery.min.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.min.map written to destination (LibManSample)
  Restore operation completed
  1 libraries restored in 2.32 seconds
  ```

### <a name="manually-configure-libman-manifest-file-entries"></a><span data-ttu-id="d2401-154">LibMan 매니페스트 파일 항목을 수동으로 구성</span><span class="sxs-lookup"><span data-stu-id="d2401-154">Manually configure LibMan manifest file entries</span></span>

<span data-ttu-id="d2401-155">Visual Studio에서 모든 LibMan 작업은 프로젝트 루트의 LibMan 매니페스트의 내용에 따라 (*libman.json*).</span><span class="sxs-lookup"><span data-stu-id="d2401-155">All LibMan operations in Visual Studio are based on the content of the project root's LibMan manifest (*libman.json*).</span></span> <span data-ttu-id="d2401-156">수동으로 편집할 수 있습니다 *libman.json* 프로젝트에 대 한 라이브러리 파일을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-156">You can manually edit *libman.json* to configure library files for the project.</span></span> <span data-ttu-id="d2401-157">Visual Studio 모든 라이브러리 파일을 한 번 복원 *libman.json* 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-157">Visual Studio restores all library files once *libman.json* is saved.</span></span>

<span data-ttu-id="d2401-158">열려는 *libman.json* 편집을 위해 다음 옵션 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-158">To open *libman.json* for editing, the following options exist:</span></span>

* <span data-ttu-id="d2401-159">두 번 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-159">Double-click the *libman.json* file in **Solution Explorer**.</span></span>
* <span data-ttu-id="d2401-160">프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택한 **클라이언트 쪽 라이브러리 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-160">Right-click the project in **Solution Explorer** and select **Manage Client-Side Libraries**.</span></span> <span data-ttu-id="d2401-161">**&#8224;**</span><span class="sxs-lookup"><span data-stu-id="d2401-161">**&#8224;**</span></span>
* <span data-ttu-id="d2401-162">선택 **클라이언트 쪽 라이브러리 관리** Visual studio에서 **프로젝트** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="d2401-162">Select **Manage Client-Side Libraries** from the Visual Studio **Project** menu.</span></span> <span data-ttu-id="d2401-163">**&#8224;**</span><span class="sxs-lookup"><span data-stu-id="d2401-163">**&#8224;**</span></span>

<span data-ttu-id="d2401-164">**&#8224;** 경우는 *libman.json* 파일은 프로젝트 루트에 존재 하지 않는 경우 기본 항목 템플릿 콘텐츠를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-164">**&#8224;** If the *libman.json* file doesn't already exist in the project root, it will be created with the default item template content.</span></span>

<span data-ttu-id="d2401-165">Visual Studio는 다양 한 JSON 색 지정 등의 지원 편집, 서식 지정, IntelliSense 및 스키마 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-165">Visual Studio offers rich JSON editing support such as colorization, formatting, IntelliSense, and schema validation.</span></span> <span data-ttu-id="d2401-166">LibMan 매니페스트의 JSON 스키마의 위치 [ http://json.schemastore.org/libman ](http://json.schemastore.org/libman)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-166">The LibMan manifest's JSON schema is found at [http://json.schemastore.org/libman](http://json.schemastore.org/libman).</span></span>

<span data-ttu-id="d2401-167">LibMan 다음 매니페스트 파일을 사용 하 여에 정의 된 구성에 따라 파일을 검색 합니다 `libraries` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-167">With the following manifest file, LibMan retrieves files per the configuration defined in the `libraries` property.</span></span> <span data-ttu-id="d2401-168">내에 정의 된 개체 리터럴에서 설명은 `libraries` 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-168">An explanation of the object literals defined within `libraries` follows:</span></span>

* <span data-ttu-id="d2401-169">하위 집합 [jQuery](https://jquery.com/) 버전 3.3.1 CDNJS 공급자에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-169">A subset of [jQuery](https://jquery.com/) version 3.3.1 is retrieved from the CDNJS provider.</span></span> <span data-ttu-id="d2401-170">하위 집합에 정의 되어는 `files` 속성&mdash;*jquery.min.js*에 *jquery.js*, 및 *jquery.min.map*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-170">The subset is defined in the `files` property&mdash;*jquery.min.js*, *jquery.js*, and *jquery.min.map*.</span></span> <span data-ttu-id="d2401-171">프로젝트의 파일이 배치 되도록 *wwwroot/lib/jquery* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-171">The files are placed in the project's *wwwroot/lib/jquery* folder.</span></span>
* <span data-ttu-id="d2401-172">전체 [부트스트랩](https://getbootstrap.com/) 4.1.3 버전을 검색 하 고 배치를 *wwwroot/lib/부트스트랩* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-172">The entirety of [Bootstrap](https://getbootstrap.com/) version 4.1.3 is retrieved and placed in a *wwwroot/lib/bootstrap* folder.</span></span> <span data-ttu-id="d2401-173">개체 리터럴의 `provider` 속성 재정의 `defaultProvider` 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-173">The object literal's `provider` property overrides the `defaultProvider` property value.</span></span> <span data-ttu-id="d2401-174">LibMan은 unpkg 공급자에서 부트스트랩 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-174">LibMan retrieves the Bootstrap files from the unpkg provider.</span></span>
* <span data-ttu-id="d2401-175">하위 집합 [및 Lodash](https://lodash.com/) 조직 내 관리 본문을 승인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-175">A subset of [Lodash](https://lodash.com/) was approved by a governing body within the organization.</span></span> <span data-ttu-id="d2401-176">*lodash.js* 하 고 *lodash.min.js* 파일에 로컬 파일 시스템에서 검색 됩니다 *c:\\temp\\및 lodash\\*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-176">The *lodash.js* and *lodash.min.js* files are retrieved from the local file system at *C:\\temp\\lodash\\*.</span></span> <span data-ttu-id="d2401-177">프로젝트의 파일을 복사할 *wwwroot/lib/및 lodash* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-177">The files are copied to the project's *wwwroot/lib/lodash* folder.</span></span>

[!code-json[](samples/LibManSample/libman.json)]

> [!NOTE]
> <span data-ttu-id="d2401-178">LibMan는만 각 공급자의 각 라이브러리의 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-178">LibMan only supports one version of each library from each provider.</span></span> <span data-ttu-id="d2401-179">합니다 *libman.json* 파일 지정된 된 공급자에 대 한 라이브러리 이름이 같은 두 라이브러리가 포함 된 경우 스키마 유효성 검사에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-179">The *libman.json* file fails schema validation if it contains two libraries with the same library name for a given provider.</span></span>

## <a name="restore-library-files"></a><span data-ttu-id="d2401-180">라이브러리 파일 복원</span><span class="sxs-lookup"><span data-stu-id="d2401-180">Restore library files</span></span>

<span data-ttu-id="d2401-181">Visual Studio 내에서 라이브러리 파일을 복원 하려면 있어야 유효한 *libman.json* 프로젝트 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-181">To restore library files from within Visual Studio, there must be a valid *libman.json* file in the project root.</span></span> <span data-ttu-id="d2401-182">복원 된 파일은 각 라이브러리에 대해 지정 된 위치에서 프로젝트에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-182">Restored files are placed in the project at the location specified for each library.</span></span>

<span data-ttu-id="d2401-183">두 가지 방법으로 ASP.NET Core 프로젝트에서 라이브러리 파일을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-183">Library files can be restored in an ASP.NET Core project in two ways:</span></span>

1. [<span data-ttu-id="d2401-184">빌드 중 파일을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-184">Restore files during build</span></span>](#restore-files-during-build)
1. [<span data-ttu-id="d2401-185">파일을 수동으로 복원</span><span class="sxs-lookup"><span data-stu-id="d2401-185">Restore files manually</span></span>](#restore-files-manually)

### <a name="restore-files-during-build"></a><span data-ttu-id="d2401-186">빌드 중 파일을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-186">Restore files during build</span></span>

<span data-ttu-id="d2401-187">LibMan 빌드 프로세스의 일부로 정의 된 라이브러리 파일을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-187">LibMan can restore the defined library files as part of the build process.</span></span> <span data-ttu-id="d2401-188">기본적으로 *빌드 시 복원* 동작을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-188">By default, the *restore-on-build* behavior is disabled.</span></span>

<span data-ttu-id="d2401-189">사용 하도록 설정 하 고 빌드 시 복원 동작을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-189">To enable and test the restore-on-build behavior:</span></span>

* <span data-ttu-id="d2401-190">마우스 오른쪽 단추로 클릭 *libman.json* 에 **솔루션 탐색기** 선택한 **빌드 시 복원 클라이언트 쪽 라이브러리를 사용 하도록 설정** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-190">Right-click *libman.json* in **Solution Explorer** and select **Enable Restore Client-Side Libraries on Build** from the context menu.</span></span>
* <span data-ttu-id="d2401-191">클릭 합니다 **예** NuGet 패키지를 설치 하 라는 메시지가 나타나면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-191">Click the **Yes** button when prompted to install a NuGet package.</span></span> <span data-ttu-id="d2401-192">합니다 [Microsoft.Web.LibraryManager.Build](https://www.nuget.org/packages/Microsoft.Web.LibraryManager.Build/) NuGet 패키지를 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-192">The [Microsoft.Web.LibraryManager.Build](https://www.nuget.org/packages/Microsoft.Web.LibraryManager.Build/) NuGet package is added to the project:</span></span>

  [!code-xml[](samples/LibManSample/LibManSample.csproj?name=snippet_RestoreOnBuildPackage)]

* <span data-ttu-id="d2401-193">LibMan 파일 복원이 수행 되는 확인 하려면 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2401-193">Build the project to confirm LibMan file restoration occurs.</span></span> <span data-ttu-id="d2401-194">`Microsoft.Web.LibraryManager.Build` 패키지 LibMan 프로젝트의 빌드 작업 중 실행 되는 MSBuild 대상을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-194">The `Microsoft.Web.LibraryManager.Build` package injects an MSBuild target that runs LibMan during the project's build operation.</span></span>
* <span data-ttu-id="d2401-195">검토 합니다 **빌드** 의 피드 합니다 **출력** LibMan 활동 로그 창:</span><span class="sxs-lookup"><span data-stu-id="d2401-195">Review the **Build** feed of the **Output** window for a LibMan activity log:</span></span>

  ```console
  1>------ Build started: Project: LibManSample, Configuration: Debug Any CPU ------
  1>
  1>Restore operation started...
  1>Restoring library jquery@3.3.1...
  1>Restoring library bootstrap@4.1.3...
  1>
  1>2 libraries restored in 10.66 seconds
  1>LibManSample -> C:\LibManSample\bin\Debug\netcoreapp2.1\LibManSample.dll
  ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
  ```

<span data-ttu-id="d2401-196">빌드 시 복원 동작을 사용 하는 경우는 *libman.json* 상황에 맞는 메뉴 표시를 **빌드 시 복원 클라이언트 쪽 라이브러리 사용 안 함** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-196">When the restore-on-build behavior is enabled, the *libman.json* context menu displays a **Disable Restore Client-Side Libraries on Build** option.</span></span> <span data-ttu-id="d2401-197">이 옵션을 선택 하면 제거를 `Microsoft.Web.LibraryManager.Build` 패키지는 프로젝트 파일에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-197">Selecting this option removes the `Microsoft.Web.LibraryManager.Build` package reference from the project file.</span></span> <span data-ttu-id="d2401-198">따라서 클라이언트 쪽 라이브러리는 더 이상 각 빌드에 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-198">Consequently, the client-side libraries are no longer restored on each build.</span></span>

<span data-ttu-id="d2401-199">빌드 시 복원 설정에 관계 없이 수동으로 복원한에서 언제 든 지 합니다 *libman.json* 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-199">Regardless of the restore-on-build setting, you can manually restore at any time from the *libman.json* context menu.</span></span> <span data-ttu-id="d2401-200">자세한 내용은 [파일을 수동으로 복원](#restore-files-manually)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-200">For more information, see [Restore files manually](#restore-files-manually).</span></span>

### <a name="restore-files-manually"></a><span data-ttu-id="d2401-201">파일을 수동으로 복원</span><span class="sxs-lookup"><span data-stu-id="d2401-201">Restore files manually</span></span>

<span data-ttu-id="d2401-202">파일을 수동으로 복원할 라이브러리:</span><span class="sxs-lookup"><span data-stu-id="d2401-202">To manually restore library files:</span></span>

* <span data-ttu-id="d2401-203">솔루션의 모든 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="d2401-203">For all projects in the solution:</span></span>
  * <span data-ttu-id="d2401-204">솔루션 이름을 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-204">Right-click the solution name in **Solution Explorer**.</span></span>
  * <span data-ttu-id="d2401-205">선택 된 **클라이언트 쪽 라이브러리 복원** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-205">Select the **Restore Client-Side Libraries** option.</span></span>
* <span data-ttu-id="d2401-206">특정 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="d2401-206">For a specific project:</span></span>
  * <span data-ttu-id="d2401-207">마우스 오른쪽 단추로 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-207">Right-click the *libman.json* file in **Solution Explorer**.</span></span>
  * <span data-ttu-id="d2401-208">선택 된 **클라이언트 쪽 라이브러리 복원** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-208">Select the **Restore Client-Side Libraries** option.</span></span>

<span data-ttu-id="d2401-209">복원 작업이 실행 하는 동안:</span><span class="sxs-lookup"><span data-stu-id="d2401-209">While the restore operation is running:</span></span>

* <span data-ttu-id="d2401-210">작업 상태 센터 (TSC) Visual Studio 상태 표시줄에 애니메이션이 적용 될 아이콘과 읽을지를 *복원 작업이 시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-210">The Task Status Center (TSC) icon on the Visual Studio status bar will be animated and will read *Restore operation started*.</span></span> <span data-ttu-id="d2401-211">아이콘을 클릭 하는 알려진된 백그라운드 작업을 나열 하는 도구 설명이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-211">Clicking the icon opens a tooltip listing the known background tasks.</span></span>
* <span data-ttu-id="d2401-212">상태 표시줄에 메시지를 전송할 하며 **라이브러리 관리자** 의 피드 합니다 **출력** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-212">Messages will be sent to the status bar and the **Library Manager** feed of the **Output** window.</span></span> <span data-ttu-id="d2401-213">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d2401-213">For example:</span></span>

  ```console
  Restore operation started...
  Restoring libraries for project LibManSample
  Restoring library jquery@3.3.1... (LibManSample)
  wwwroot/lib/jquery/jquery.min.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.js written to destination (LibManSample)
  wwwroot/lib/jquery/jquery.min.map written to destination (LibManSample)
  Restore operation completed
  1 libraries restored in 2.32 seconds
  ```

## <a name="delete-library-files"></a><span data-ttu-id="d2401-214">라이브러리 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="d2401-214">Delete library files</span></span>

<span data-ttu-id="d2401-215">수행 하는 *정리* 이전에 Visual Studio에서 복원 하는 라이브러리 파일을 삭제 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="d2401-215">To perform the *clean* operation, which deletes library files previously restored in Visual Studio:</span></span>

* <span data-ttu-id="d2401-216">마우스 오른쪽 단추로 클릭 합니다 *libman.json* 파일 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-216">Right-click the *libman.json* file in **Solution Explorer**.</span></span>
* <span data-ttu-id="d2401-217">선택 된 **정리 클라이언트 쪽 라이브러리** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-217">Select the **Clean Client-Side Libraries** option.</span></span>

<span data-ttu-id="d2401-218">라이브러리가 아닌 파일의 의도 하지 않게 제거를 방지 하려면 정리 작업 전체 디렉터리를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-218">To prevent unintentional removal of non-library files, the clean operation doesn't delete whole directories.</span></span> <span data-ttu-id="d2401-219">이전 복원 작업에서 포함 된 파일이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-219">It only removes files that were included in the previous restore.</span></span>

<span data-ttu-id="d2401-220">정리 작업 실행 하는 동안:</span><span class="sxs-lookup"><span data-stu-id="d2401-220">While the clean operation is running:</span></span>

* <span data-ttu-id="d2401-221">TSC Visual Studio 상태 표시줄에 애니메이션이 적용 될 아이콘과 읽을지를 *클라이언트 라이브러리 작업을 시작할*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-221">The TSC icon on the Visual Studio status bar will be animated and will read *Client libraries operation started*.</span></span> <span data-ttu-id="d2401-222">아이콘을 클릭 하는 알려진된 백그라운드 작업을 나열 하는 도구 설명이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-222">Clicking the icon opens a tooltip listing the known background tasks.</span></span>
* <span data-ttu-id="d2401-223">상태 표시줄 메시지와 **라이브러리 관리자** 의 피드를 **출력** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-223">Messages are sent to the status bar and the **Library Manager** feed of the **Output** window.</span></span> <span data-ttu-id="d2401-224">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d2401-224">For example:</span></span>

```console
Clean libraries operation started...
Clean libraries operation completed
2 libraries were successfully deleted in 1.91 secs
```

<span data-ttu-id="d2401-225">만 정리 작업 프로젝트에서 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-225">The clean operation only deletes files from the project.</span></span> <span data-ttu-id="d2401-226">라이브러리 파일은 이후 복원 작업에서 빠른 검색을 위해 캐시에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-226">Library files stay in the cache for faster retrieval on future restore operations.</span></span> <span data-ttu-id="d2401-227">로컬 컴퓨터의 캐시에 저장 된 라이브러리 파일을 관리 하려면 사용 합니다 [LibMan CLI](xref:client-side/libman/libman-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-227">To manage library files stored in the local machine's cache, use the [LibMan CLI](xref:client-side/libman/libman-cli).</span></span>

## <a name="uninstall-library-files"></a><span data-ttu-id="d2401-228">라이브러리 파일을 제거</span><span class="sxs-lookup"><span data-stu-id="d2401-228">Uninstall library files</span></span>

<span data-ttu-id="d2401-229">라이브러리 파일을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-229">To uninstall library files:</span></span>

* <span data-ttu-id="d2401-230">오픈 *libman.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-230">Open *libman.json*.</span></span>
* <span data-ttu-id="d2401-231">해당 내부 캐럿 배치 `libraries` 리터럴 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-231">Position the caret inside the corresponding `libraries` object literal.</span></span>
* <span data-ttu-id="d2401-232">왼쪽된 여백에 표시 되는 전구 아이콘을 클릭 하 고 선택 **제거 \<library_name > @\<library_version >**:</span><span class="sxs-lookup"><span data-stu-id="d2401-232">Click the light bulb icon that appears in the left margin, and select **Uninstall \<library_name>@\<library_version>**:</span></span>

  ![라이브러리 상황에 맞는 메뉴 옵션을 제거 합니다.](_static/uninstall-menu-option.png)

<span data-ttu-id="d2401-234">또는 수동으로 편집 하 고 저장할 수 LibMan 매니페스트 (*libman.json*).</span><span class="sxs-lookup"><span data-stu-id="d2401-234">Alternatively, you can manually edit and save the LibMan manifest (*libman.json*).</span></span> <span data-ttu-id="d2401-235">합니다 [복원 작업](#restore-library-files) 파일을 저장할 때 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-235">The [restore operation](#restore-library-files) runs when the file is saved.</span></span> <span data-ttu-id="d2401-236">라이브러리 파일에서 더 이상 정의한 *libman.json* 프로젝트에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-236">Library files that are no longer defined in *libman.json* are removed from the project.</span></span>

## <a name="update-library-version"></a><span data-ttu-id="d2401-237">라이브러리 버전 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2401-237">Update library version</span></span>

<span data-ttu-id="d2401-238">확인 하려면 업데이트 된 라이브러리 버전:</span><span class="sxs-lookup"><span data-stu-id="d2401-238">To check for an updated library version:</span></span>

* <span data-ttu-id="d2401-239">오픈 *libman.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-239">Open *libman.json*.</span></span>
* <span data-ttu-id="d2401-240">해당 내부 캐럿 배치 `libraries` 리터럴 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-240">Position the caret inside the corresponding `libraries` object literal.</span></span>
* <span data-ttu-id="d2401-241">왼쪽된 여백에 표시 되는 전구 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-241">Click the light bulb icon that appears in the left margin.</span></span> <span data-ttu-id="d2401-242">마우스로 **업데이트 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-242">Hover over **Check for updates**.</span></span>

<span data-ttu-id="d2401-243">LibMan 설치 된 버전 보다 최신 라이브러리 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-243">LibMan checks for a library version newer than the version installed.</span></span> <span data-ttu-id="d2401-244">다음 결과 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-244">The following outcomes can occur:</span></span>

* <span data-ttu-id="d2401-245">A **업데이트를 찾을 수 없는** 최신 버전이 이미 설치 되어 있는 경우 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-245">A **No updates found** message is displayed if the latest version is already installed.</span></span>
* <span data-ttu-id="d2401-246">안정적인 최신 버전은 아직 설치 되지 않으면 표시.</span><span class="sxs-lookup"><span data-stu-id="d2401-246">The latest stable version is displayed if not already installed.</span></span>

  ![업데이트 상황에 맞는 메뉴 옵션에 대 한 확인](_static/update-menu-option.png)

* <span data-ttu-id="d2401-248">설치 된 버전 보다 최신 시험판 사용 가능한 경우 시험판 버전 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-248">If a pre-release newer than the installed version is available, the pre-release is displayed.</span></span>

<span data-ttu-id="d2401-249">이전 라이브러리 버전으로 다운 그레이드 하려면 수동으로 편집 하 여 *libman.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-249">To downgrade to an older library version, manually edit the *libman.json* file.</span></span> <span data-ttu-id="d2401-250">파일 저장 될 경우에 LibMan [복원 작업](#restore-library-files):</span><span class="sxs-lookup"><span data-stu-id="d2401-250">When the file is saved, the LibMan [restore operation](#restore-library-files):</span></span>

* <span data-ttu-id="d2401-251">이전 버전에서 중복 파일을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-251">Removes redundant files from the previous version.</span></span>
* <span data-ttu-id="d2401-252">새 버전에서 새로운 기능과 업데이트 된 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2401-252">Adds new and updated files from the new version.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2401-253">추가 자료</span><span class="sxs-lookup"><span data-stu-id="d2401-253">Additional resources</span></span>

* <xref:client-side/libman/libman-cli>
* [<span data-ttu-id="d2401-254">LibMan GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="d2401-254">LibMan GitHub repository</span></span>](https://github.com/aspnet/LibraryManager)
