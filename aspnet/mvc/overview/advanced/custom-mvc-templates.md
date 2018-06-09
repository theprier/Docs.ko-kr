---
uid: mvc/overview/advanced/custom-mvc-templates
title: 사용자 지정 MVC 템플릿 | Microsoft Docs
author: joeloff
description: VSIX 확장으로 템플릿을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/10/2012
ms.topic: article
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: c3ddd4e341511f520927e924b25d890088adb69e
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "28034609"
---
<a name="custom-mvc-template"></a><span data-ttu-id="cf246-103">사용자 지정 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="cf246-103">Custom MVC Template</span></span>
====================
<span data-ttu-id="cf246-104">으로 [Jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="cf246-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="cf246-105">Visual Studio 2010 for MVC 3 도구 업데이트 릴리스에서 MVC 프로젝트에 대 한 별도 프로젝트 마법사를 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="cf246-106">변경 된 두 요소에 의해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-106">The change was driven by two factors.</span></span> <span data-ttu-id="cf246-107">첫째, 새 템플릿 MVC 3 및 Razor 같은 추가 뷰 엔진에 대 한 지원을 도입 될 복잡해 Visual Studio에서 새 프로젝트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cf246-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="cf246-108">그런 다음 고객은 확장 지점을 무엇입니까 했습니다 하 고 새 MVC 프로젝트 마법사는 쓸모 우리 이러한 요청에 응답 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="cf246-109">사용자 지정 템플릿 추가 레지스트리를 사용 하 여 볼 수 있도록 하려면 새 템플릿을 MVC 프로젝트 마법사에 의존 하는 한 힘든 작업 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="cf246-110">새 서식 파일의 작성자는 설치 중에 필요한 레지스트리 항목을 만들 수는 확인 하기 위해 MSI를 래핑합니다 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="cf246-111">ZIP 파일을 사용할 수 있는 템플릿이 포함 된 필수 레지스트리 항목을 수동으로 만드는 최종 사용자가를 대체가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="cf246-112">앞에서 언급 한 접근 방식 중 이므로 이상적인에서 제공 하는 기존 인프라 중 일부를 활용할 하기로 결정 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) 작성자를 쉽게 수행할 수 있도록 확장 배포 및 MVC 4로 시작 하는 사용자 지정 MVC 템플릿 설치 Visual Studio 2012입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="cf246-113">이 방법을 사용 하 여 제공 하는 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="cf246-114">VSIX 확장 (C# 및 Visual Basic) 서로 다른 언어를 지 원하는 여러 서식 파일의 여러 뷰 엔진 (ASPX 및 Razor)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="cf246-115">VSIX 확장에는 여러 Sku의 Visual Studio Express Sku를 포함 하 여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="cf246-116">[Visual Studio 갤러리](https://visualstudiogallery.msdn.microsoft.com/) 사용자에 게 확장 배포를 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="cf246-117">VSIX 확장 작성 수정 및 사용자 지정 서식 파일에 대 한 업데이트를 더욱 쉽게 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf246-118">전제 조건</span><span class="sxs-lookup"><span data-stu-id="cf246-118">Prerequisites</span></span>

- <span data-ttu-id="cf246-119">사용자는 프로젝트 템플릿, vstemplate 파일 등의 필요한 태그를 포함 하 여 제작 숙지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="cf246-120">사용자는 Visual Studio Professional가 필요 하 고 이상이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="cf246-121">Express Sku에서 VSIX 프로젝트를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="cf246-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="cf246-123">예</span><span class="sxs-lookup"><span data-stu-id="cf246-123">Example</span></span>

<span data-ttu-id="cf246-124">첫 번째 단계는 C# 또는 Visual Basic을 사용 하 여 새 VSIX 프로젝트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="cf246-125">선택 **파일 > 새 프로젝트**, 클릭 **확장성** 고 왼쪽된 창에서는 **VSIX 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![새 프로젝트](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="cf246-127">프로젝트를 만든 후 VSIX 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-127">After the project is created, the VSIX designer will be opened.</span></span>

![프로젝트 디자이너 메타 데이터](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="cf246-129">디자이너 확장을 설치 하거나 Visual Studio에서 설치 된 확장을 찾아볼 때 사용자에 게 표시 되는 확장 프로그램의 일반 속성 중 일부를 편집할 데 사용할 수 있습니다 (**도구 > 확장 및 업데이트**).</span><span class="sxs-lookup"><span data-stu-id="cf246-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="cf246-130">일반 정보 클릭 완료 하는 **설치 대상 탭**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="cf246-132">Sku 및 확장 프로그램에서 지원 되는 버전의 Visual Studio를 지정 하려면이 탭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="cf246-133">에 대 한 확인란을 선택 **이 VSIX가 모든 사용자에 대해 설치 되어** VSIX의 컴퓨터 단위 설치에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="cf246-134">클릭는 **새로** 추가 Sku Web Developer Express (VWD) 등을 추가 하려면 오른쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![새 설치 대상 추가](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="cf246-136">최소 SKU 제품군에서 선택 해야 모든 Professional 이상 Sku (Professional, Premium 및 Ultimate)를 지원 하려는 경우 **Microsoft.VisualStudio.Pro**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="cf246-137">설치 대상을 완료 한 후 변경 내용을 모두 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="cf246-139">**자산** 탭 VSIX에 모든 콘텐츠 파일을 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="cf246-140">MVC 사용자 지정 메타 데이터를 필요 하므로 편집기를 사용 하지 않고 VSIX 매니페스트 파일의 원시 XML을는 **자산** 콘텐츠 추가를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="cf246-141">템플릿 내용을 VSIX 프로젝트에 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="cf246-142">폴더 및 내용을의 구조는 프로젝트의 레이아웃을 미러링 하 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="cf246-143">다음 예제에서는 기본 MVC 프로젝트 템플릿에서 파생 된 있는 4 개의 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="cf246-144">프로젝트 템플릿을 (ProjectTemplates 폴더 아래 모든 항목)를 구성 하는 모든 파일에 추가 되어 있는지 확인은 **콘텐츠** VSIX에 itemgroup 프로젝트 파일 및 각 항목에 포함 되어 있는지는  **출력 디렉터리로 복사** 및 **IncludeInVsix** 아래 예에 나와 있는 것 처럼 메타 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="cf246-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="cf246-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="cf246-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="cf246-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="cf246-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="cf246-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="cf246-148">&lt;/Content&gt;</span><span class="sxs-lookup"><span data-stu-id="cf246-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="cf246-149">그렇지 않으면 IDE VSIX 빌드하고 오류가 표시 될 가능성이 때 서식 파일의 내용을 컴파일할 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="cf246-150">서식 파일에서 코드 파일에 종종 특수 포함 [템플릿 매개 변수](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) 때 프로젝트 템플릿이 인스턴스화될 및 IDE에서 컴파일할 수 없습니다 Visual Studio에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![솔루션 탐색기](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="cf246-152">VSIX 디자이너를 닫은 다음 마우스 오른쪽 단추로 클릭는 **source.extension.manifest** 파일 **솔루션 탐색기** 선택 **프로그램** 선택 하 고는 **XML ( 텍스트) 편집기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![대화 상자 열기](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="cf246-154">만들기는 **&lt;자산&gt;** 요소를 추가 하 고는 **&lt;자산&gt;** VSIX에 포함 되어야 하는 각 파일에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="cf246-155">**형식** 각 특성 **&lt;자산&gt;** 요소도 설정 되어 있어야 **Microsoft.VisualStudio.Mvc.Template**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="cf246-156">MVC 프로젝트 마법사에 대 한 이해 하는 사용자 지정 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="cf246-157">매니페스트 파일의 레이아웃과 구조에 대 한 자세한 내용은 VSIX 2.0 스키마 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cf246-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="cf246-158">방금 VSIX에 파일을 추가 MVC 마법사로 서식 파일을 등록 하는 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="cf246-159">MVC 마법사 템플릿 이름, 설명, 지원 되는 뷰 엔진 및 프로그래밍 언어와 같은 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="cf246-160">이 정보에 연결 된 사용자 지정 특성에 전달 되는 **&lt;자산&gt;** 요소 각각에 대해 **vstemplate** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="cf246-161">&lt;자산 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="cf246-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="cf246-163">d:Source=&quot;File&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="cf246-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="cf246-165">ProjectType=&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="cf246-166">Language=&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="cf246-167">ViewEngine=&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="cf246-168">TemplateId=&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="cf246-169">제목 =&quot;기본 사용자 지정 웹 응용 프로그램&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="cf246-170">설명 =&quot;기본 MVC 웹 응용 프로그램 (Razor)에서 파생 된 사용자 지정 서식 파일&quot;</span><span class="sxs-lookup"><span data-stu-id="cf246-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="cf246-171">Version=&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="cf246-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="cf246-172">다음은 나타나야 하는 사용자 지정 특성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="cf246-173">**ProjectType** MVC로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="cf246-174">**언어** 서식 파일에서 지 원하는 개발 언어를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="cf246-175">유효한 값은 C# 또는 VB.</span><span class="sxs-lookup"><span data-stu-id="cf246-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="cf246-176">**Viewengine이 제공 됨** Aspx 또는 Razor 같은 서식 파일에서 지 원하는 뷰 엔진을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="cf246-177">이 필드에 대 한 사용자 지정 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="cf246-178">**TemplateId** 서식 파일을 그룹화 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="cf246-179">값이 기존 템플릿 ID는 것과 일치 하는 경우 이전에 MVC 마법사에 등록 하는 서식 파일을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="cf246-180">**제목** 아래에 있는 각 프로젝트 템플릿은 MVC 마법사에 표시 되는 간단한 설명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="cf246-181">**설명** 서식 파일에 대 한 더 자세한 설명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="cf246-182">매니페스트에 포함 된 모든 파일을 추가한 후, 저장 점을 확인할 수 있습니다는 **자산** 하지 사용자 지정 특성에 추가 하지만 디자이너의 탭에는 모든 파일 표시 됩니다는 **&lt;자산&gt;** 에 대 한 요소는 **vstemplate** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![디자이너의 프로젝트 자산이](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="cf246-184">이제 남았습니다을 VSIX 프로젝트를 컴파일하고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="cf246-185">컴퓨터에 Visual Studio의 모든 인스턴스가 닫혀 있는지 VSIX 확장을 테스트 하려는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="cf246-186">Visual Studio 스캔을 새로운 확장에 대 한 시작 하는 동안 IDE VSIX를 설치 하는 동안 열려 있으면 Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="cf246-187">시작 하려면 VSIX 파일 탐색기에서 두 번 클릭은 **VSIX 설치 관리자**, 클릭 **설치** 다음 Visual Studio를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 설치 관리자](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="cf246-189">메뉴에서 선택 **도구 > 확장 및 업데이트** 확장이 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="cf246-190">VSIX 설치 관리자는 확장의 설치 하는 동안 모든 오류를 보고 했습니다. 자세한 내용은 VSIX 설치 관리자 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="cf246-191">일반적으로 로그가에서 생성 되는 **%temp%** 예를 들어 확장을 설치 하는 사용자의 폴더 **C:\Users\Bob\AppData\Local\Temp**합니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![확장 및 업데이트](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="cf246-193">창을 닫은 후 새 템플릿을 MVC 마법사에 표시 되는지 여부를 확인 하려면 프로그램 MVC 4 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![새 ASP.NET MVC 4 프로젝트](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="cf246-195">제한 사항</span><span class="sxs-lookup"><span data-stu-id="cf246-195">Limitations</span></span>

1. <span data-ttu-id="cf246-196">MVC 마법사는 지역화 된 사용자 지정 서식 파일을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="cf246-197">마법사는 사용자 지정 템플릿을 찾을 수 없는 경우 오류를 보고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="cf246-198">필수 사용자 지정 특성 가지가 모두 없을 경우 서식 파일 하기만 하면 마법사에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf246-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
