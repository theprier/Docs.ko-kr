---
uid: mvc/overview/advanced/custom-mvc-templates
title: "사용자 지정 MVC 템플릿 | Microsoft Docs"
author: joeloff
description: "VSIX 확장으로 템플릿을 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/10/2012
ms.topic: article
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: a1fe1844e582f402a1eed9ddf10ee249e856b083
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="custom-mvc-template"></a>사용자 지정 MVC 템플릿
====================
으로 [Jacques Eloff](https://github.com/joeloff)

Visual Studio 2010 for MVC 3 도구 업데이트 릴리스에서 MVC 프로젝트에 대 한 별도 프로젝트 마법사를 도입 되었습니다. 변경 된 두 요소에 의해 이루어집니다. 첫째, 새 템플릿 MVC 3 및 Razor 같은 추가 뷰 엔진에 대 한 지원을 도입 될 복잡해 Visual Studio에서 새 프로젝트 대화 상자. 그런 다음 고객은 확장 지점을 무엇입니까 했습니다 하 고 새 MVC 프로젝트 마법사는 쓸모 우리 이러한 요청에 응답 하도록 합니다.

사용자 지정 템플릿 추가 레지스트리를 사용 하 여 볼 수 있도록 하려면 새 템플릿을 MVC 프로젝트 마법사에 의존 하는 한 힘든 작업 했습니다. 새 서식 파일의 작성자는 설치 중에 필요한 레지스트리 항목을 만들 수는 확인 하기 위해 MSI를 래핑합니다 해야 했습니다. ZIP 파일을 사용할 수 있는 템플릿이 포함 된 필수 레지스트리 항목을 수동으로 만드는 최종 사용자가를 대체가 했습니다.

앞에서 언급 한 접근 방식 중 이므로 이상적인에서 제공 하는 기존 인프라 중 일부를 활용할 하기로 결정 [VSIX](https://msdn.microsoft.com/en-us/library/ff363239.aspx) 작성자를 쉽게 수행할 수 있도록 확장 배포 및 MVC 4로 시작 하는 사용자 지정 MVC 템플릿 설치 Visual Studio 2012입니다. 이 방법을 사용 하 여 제공 하는 이점은 다음과 같습니다.

- VSIX 확장 (C# 및 Visual Basic) 서로 다른 언어를 지 원하는 여러 서식 파일의 여러 뷰 엔진 (ASPX 및 Razor)를 포함할 수 있습니다.
- VSIX 확장에는 여러 Sku의 Visual Studio Express Sku를 포함 하 여 지정할 수 있습니다.
- [Visual Studio 갤러리](https://visualstudiogallery.msdn.microsoft.com/) 사용자에 게 확장 배포를 용이 하 게 합니다.
- VSIX 확장 작성 수정 및 사용자 지정 서식 파일에 대 한 업데이트를 더욱 쉽게 업그레이드할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

- 사용자는 프로젝트 템플릿, vstemplate 파일 등의 필요한 태그를 포함 하 여 제작 숙지 해야 합니다.
- 사용자는 Visual Studio Professional가 필요 하 고 이상이 설치 합니다. Express Sku에서 VSIX 프로젝트를 지원 하지 않습니다.
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 설치 합니다.

## <a name="example"></a>예제

첫 번째 단계는 C# 또는 Visual Basic을 사용 하 여 새 VSIX 프로젝트를 만드는 것입니다. 선택 **파일 > 새 프로젝트**, 클릭 **확장성** 고 왼쪽된 창에서는 **VSIX 프로젝트**합니다.

![새 프로젝트](custom-mvc-templates/_static/image1.jpg)

프로젝트를 만든 후 VSIX 디자이너가 열립니다.

![프로젝트 디자이너 메타 데이터](custom-mvc-templates/_static/image2.jpg)

디자이너 확장을 설치 하거나 Visual Studio에서 설치 된 확장을 찾아볼 때 사용자에 게 표시 되는 확장 프로그램의 일반 속성 중 일부를 편집할 데 사용할 수 있습니다 (**도구 > 확장 및 업데이트**). 일반 정보 클릭 완료 하는 **설치 대상 탭**합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image3.jpg)

Sku 및 확장 프로그램에서 지원 되는 버전의 Visual Studio를 지정 하려면이 탭을 사용 합니다. 에 대 한 확인란을 선택 **이 VSIX가 모든 사용자에 대해 설치 되어** VSIX의 컴퓨터 단위 설치에 사용할 수 있도록 합니다. 클릭는 **새로** 추가 Sku Web Developer Express (VWD) 등을 추가 하려면 오른쪽에 단추입니다.

![새 설치 대상 추가](custom-mvc-templates/_static/image4.jpg)

최소 SKU 제품군에서 선택 해야 모든 Professional 이상 Sku (Professional, Premium 및 Ultimate)를 지원 하려는 경우 **Microsoft.VisualStudio.Pro**합니다. 설치 대상을 완료 한 후 변경 내용을 모두 저장 해야 합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image5.jpg)

**자산** 탭 VSIX에 모든 콘텐츠 파일을 추가 하는 데 사용 됩니다. MVC 사용자 지정 메타 데이터를 필요 하므로 편집기를 사용 하지 않고 VSIX 매니페스트 파일의 원시 XML을는 **자산** 콘텐츠 추가를 탭 합니다. 템플릿 내용을 VSIX 프로젝트에 추가 하 여 시작 합니다. 폴더 및 내용을의 구조는 프로젝트의 레이아웃을 미러링 하 유용 합니다. 다음 예제에서는 기본 MVC 프로젝트 템플릿에서 파생 된 있는 4 개의 프로젝트 템플릿이 포함 되어 있습니다. 프로젝트 템플릿을 (ProjectTemplates 폴더 아래 모든 항목)를 구성 하는 모든 파일에 추가 되어 있는지 확인은 **콘텐츠** VSIX에 itemgroup 프로젝트 파일 및 각 항목에 포함 되어 있는지는  **출력 디렉터리로 복사** 및 **IncludeInVsix** 아래 예에 나와 있는 것 처럼 메타 데이터를 설정 합니다.

&lt;콘텐츠에 포함 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;출력 디렉터리로 복사&gt;항상&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/ 콘텐츠&gt;

그렇지 않으면 IDE VSIX 빌드하고 오류가 표시 될 가능성이 때 서식 파일의 내용을 컴파일할 하려고 합니다. 서식 파일에서 코드 파일에 종종 특수 포함 [템플릿 매개 변수](https://msdn.microsoft.com/en-us/library/eehb4faa(v=vs.110).aspx) 때 프로젝트 템플릿이 인스턴스화될 및 IDE에서 컴파일할 수 없습니다 Visual Studio에서 사용 합니다.

![솔루션 탐색기](custom-mvc-templates/_static/image6.jpg)

VSIX 디자이너를 닫은 다음 마우스 오른쪽 단추로 클릭는 **source.extension.manifest** 파일 **솔루션 탐색기** 선택 **프로그램** 선택 하 고는 **XML ( 텍스트) 편집기** 옵션입니다.

![대화 상자 열기](custom-mvc-templates/_static/image7.jpg)

만들기는  **&lt;자산&gt;**  요소를 추가 하 고는  **&lt;자산&gt;**  VSIX에 포함 되어야 하는 각 파일에 대 한 요소입니다. **형식** 각 특성  **&lt;자산&gt;**  요소도 설정 되어 있어야 **Microsoft.VisualStudio.Mvc.Template**합니다. MVC 프로젝트 마법사에 대 한 이해 하는 사용자 지정 네임 스페이스입니다. 매니페스트 파일의 레이아웃과 구조에 대 한 자세한 내용은 VSIX 2.0 스키마 설명서를 참조 하십시오.

방금 VSIX에 파일을 추가 MVC 마법사로 서식 파일을 등록 하는 충분 하지 않습니다. MVC 마법사 템플릿 이름, 설명, 지원 되는 뷰 엔진 및 프로그래밍 언어와 같은 정보를 제공 해야 합니다. 이 정보에 연결 된 사용자 지정 특성에 전달 되는  **&lt;자산&gt;**  요소 각각에 대해 **vstemplate** 파일입니다.

&lt;자산 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

형식 =&quot;Microsoft.VisualStudio.Mvc.Template&quot;

d:Source =&quot;파일&quot;

경로 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Language =&quot;C#&quot;

Viewengine이 제공 됨 =&quot;Aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

제목 =&quot;기본 사용자 지정 웹 응용 프로그램&quot;

설명 =&quot;기본 MVC 웹 응용 프로그램 (Razor)에서 파생 된 사용자 지정 서식 파일&quot;

버전 =&quot;4.0&quot;/&gt;

다음은 나타나야 하는 사용자 지정 특성에 대해 설명 합니다.

- **ProjectType** MVC로 설정 해야 합니다.
- **언어** 서식 파일에서 지 원하는 개발 언어를 지정 합니다. 유효한 값은 C# 또는 VB.
- **Viewengine이 제공 됨** Aspx 또는 Razor 같은 서식 파일에서 지 원하는 뷰 엔진을 지정 합니다. 이 필드에 대 한 사용자 지정 값을 지정할 수 있습니다.
- **TemplateId** 서식 파일을 그룹화 하는 데 사용 됩니다. 값이 기존 템플릿 ID는 것과 일치 하는 경우 이전에 MVC 마법사에 등록 하는 서식 파일을 재정의 합니다.
- **제목** 아래에 있는 각 프로젝트 템플릿은 MVC 마법사에 표시 되는 간단한 설명을 지정 합니다.
- **설명** 서식 파일에 대 한 더 자세한 설명을 지정 합니다.

매니페스트에 포함 된 모든 파일을 추가한 후, 저장 점을 확인할 수 있습니다는 **자산** 하지 사용자 지정 특성에 추가 하지만 디자이너의 탭에는 모든 파일 표시 됩니다는  **&lt;자산&gt;**  에 대 한 요소는 **vstemplate** 파일입니다.

![디자이너의 프로젝트 자산이](custom-mvc-templates/_static/image8.jpg)

이제 남았습니다을 VSIX 프로젝트를 컴파일하고 설치 합니다.

컴퓨터에 Visual Studio의 모든 인스턴스가 닫혀 있는지 VSIX 확장을 테스트 하려는 확인 합니다. Visual Studio 스캔을 새로운 확장에 대 한 시작 하는 동안 IDE VSIX를 설치 하는 동안 열려 있으면 Visual Studio를 다시 시작 해야 합니다. 시작 하려면 VSIX 파일 탐색기에서 두 번 클릭은 **VSIX 설치 관리자**, 클릭 **설치** 다음 Visual Studio를 실행 합니다.

![VSIX 설치 관리자](custom-mvc-templates/_static/image9.jpg)

메뉴에서 선택 **도구 > 확장 및 업데이트** 확장이 설치 되었는지 확인 합니다. VSIX 설치 관리자는 확장의 설치 하는 동안 모든 오류를 보고 했습니다. 자세한 내용은 VSIX 설치 관리자 로그를 볼 수 있습니다. 일반적으로 로그가에서 생성 되는 **%temp%** 예를 들어 확장을 설치 하는 사용자의 폴더 **C:\Users\Bob\AppData\Local\Temp**합니다.

![확장 및 업데이트](custom-mvc-templates/_static/image10.jpg)

창을 닫은 후 새 템플릿을 MVC 마법사에 표시 되는지 여부를 확인 하려면 프로그램 MVC 4 프로젝트를 만들 수 있습니다.

![새 ASP.NET MVC 4 프로젝트](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>제한 사항

1. MVC 마법사는 지역화 된 사용자 지정 서식 파일을 지원 하지 않습니다.
2. 마법사는 사용자 지정 템플릿을 찾을 수 없는 경우 오류를 보고 하지 않습니다. 필수 사용자 지정 특성 가지가 모두 없을 경우 서식 파일 하기만 하면 마법사에서 제외 됩니다.
