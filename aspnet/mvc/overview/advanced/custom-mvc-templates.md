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
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 715990e2d7151ad1ce8288169ef4bdd5c4243369
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367246"
---
<a name="custom-mvc-template"></a>사용자 지정 MVC 템플릿
====================
[Jacques Eloff](https://github.com/joeloff)

Visual Studio 2010에 대 한 MVC 3 Tools 업데이트 릴리스의 MVC 프로젝트에 대 한 별도 프로젝트 마법사를 도입 되었습니다. 변경 된 두 가지 요인에 의해 결정 됩니다. 먼저 MVC 3 Razor 같은 추가 뷰 엔진에 대 한 지원에 새 템플릿 도입 될 복잡해 Visual Studio에서 새 프로젝트 대화 상자. 둘째, 확장성 지점에 대 한 고객에 게 요청한가 있으며 새 MVC 프로젝트 마법사는 이용할 우리 이러한 요청에 응답할 수 있도록 합니다.

사용자 지정 템플릿을 추가 레지스트리를 사용 하 여 새 템플릿을 MVC 프로젝트 마법사에서 볼 수 있도록 의존 않는 험난 한 프로세스가 되었습니다. 새 템플릿 만든 MSI 설치 시 필요한 레지스트리 항목이 발생할 수 있도록 내에서 래핑하여 해야 했습니다. 대신 필요한 레지스트리 항목을 수동으로 만들어야 하는 최종 사용자가 있고 사용할 수 있는 템플릿이 포함 된 ZIP 파일을 확인 하는 것 이었습니다.

앞서 언급 한 방법 중 어느 이므로 이상적인 제공한 기존 인프라의 일부를 활용 하기로 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) 확장을 쉽게 작성, 배포 및 MVC 4를 사용 하 여 시작 하는 사용자 지정 MVC 템플릿 설치 Visual Studio 2012. 이 방식으로 제공 되는 혜택은 다음과 같습니다.

- VSIX 확장 (C# 및 Visual Basic) 다른 언어를 지 원하는 여러 템플릿 및 여러 뷰 엔진 (ASPX 및 Razor)에 포함할 수 있습니다.
- VSIX 확장을 여러 Sku의 Visual Studio Express Sku를 포함 하 여 대상으로 지정할 수 있습니다.
- 합니다 [Visual Studio 갤러리](https://visualstudiogallery.msdn.microsoft.com/) 를 많은 사람들이 확장 배포를 용이 하 게 합니다.
- VSIX 확장 수정 및 사용자 지정 서식 파일에 대 한 업데이트 작성 쉽게 업그레이드할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

- 사용자는 프로젝트 템플릿, vstemplate 파일에 대 한 필수 태그를 포함 하 여 작성 숙지 해야 합니다.
- 사용자가 Visual Studio professional 해야 하며 이상이 설치 되어 있습니다. Express Sku는 VSIX 프로젝트를 지원 하지 않습니다.
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 설치 합니다.

## <a name="example"></a>예

먼저 C# 또는 Visual Basic을 사용 하 여 새 VSIX 프로젝트를 만드는 것입니다. 선택 **파일 > 새 프로젝트**, 클릭 **확장성** 왼쪽된 창에서 선택 합니다 **VSIX 프로젝트**합니다.

![새 프로젝트](custom-mvc-templates/_static/image1.jpg)

프로젝트를 만든 후 VSIX 디자이너가 열립니다.

![프로젝트 디자이너 메타 데이터](custom-mvc-templates/_static/image2.jpg)

디자이너 확장을 설치 하거나 Visual Studio에서 설치 된 확장을 검색 하는 경우 사용자에 게 표시 되는 확장의 일반 속성 중 일부를 편집할 데 사용할 수 있습니다 (**도구 > 확장 및 업데이트**). 완료 한 일반 정보를 클릭 합니다 **설치 대상 탭**합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image3.jpg)

Sku 및 확장에 의해 지원 되는 버전의 Visual Studio를 지정 하려면이 탭을 사용 합니다. 에 대 한 확인란을 선택 **모든 사용자에 대해이 VSIX 설치 되어** 컴퓨터별 VSIX 설치를 사용 하도록 설정 합니다. 클릭 합니다 **새로 만들기** Web Developer Express (VWD)와 같은 추가 Sku를 추가 하려면 오른쪽에는 단추입니다.

![새 설치 대상 추가](custom-mvc-templates/_static/image4.jpg)

모든 Professional 이상 Sku (Professional, Premium 및 Ultimate)를 지원 하려는 경우만 선택 해야 최소 SKU 제품군에서 **Microsoft.VisualStudio.Pro**합니다. 설치 대상 완료 한 후 모든 변경 내용을 저장 해야 합니다.

![프로젝트 디자이너 설치 대상](custom-mvc-templates/_static/image5.jpg)

합니다 **자산** 탭 VSIX에 모든 콘텐츠 파일을 추가 하는 데 사용 됩니다. MVC는 사용자 지정 메타 데이터를 필요 하므로 편집기 원시 XML을 사용 하는 대신 VSIX 매니페스트 파일의 합니다 **자산** 내용을 추가할 탭 합니다. VSIX 프로젝트 템플릿 콘텐츠를 추가 하 여 시작 합니다. 폴더 및 내용을 구조의 프로젝트의 레이아웃을 미러링는 반드시 합니다. 아래 예제에는 기본 MVC 프로젝트 템플릿에서 파생 된 4 개의 프로젝트 템플릿이 들어 있습니다. (ProjectTemplates 폴더 아래에 있는 모든 항목) 프로젝트 템플릿을 구성 하는 모든 파일에 추가 되어 있는지 확인 합니다 **콘텐츠** itemgroup VSIX에 파일 및 각 항목에 포함 된 프로젝트는  **출력 디렉터리로 복사** 하 고 **IncludeInVsix** 메타 데이터는 아래 예제와 같이 설정 합니다.

&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/Content&gt;

그렇지 않은 경우 IDE는 VSIX 빌드하고 오류가 상자가 표시 됩니다 될 때 템플릿의 내용의 컴파일되지 시도 합니다. 템플릿에서 코드 파일은 종종 특수를 포함 [템플릿 매개 변수](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) 프로젝트 템플릿이 인스턴스화될 고 IDE에서 컴파일할 수 없습니다 Visual Studio에서 사용 합니다.

![솔루션 탐색기](custom-mvc-templates/_static/image6.jpg)

VSIX 디자이너를 닫은 후 마우스 오른쪽 단추로 클릭 합니다 **source.extension.manifest** 파일 **솔루션 탐색기** 선택한 **연결** 선택 하 고는 **XML ( 텍스트) 편집기** 옵션입니다.

![대화 상자 열기](custom-mvc-templates/_static/image7.jpg)

만들기는 **&lt;자산&gt;** 요소 추가 **&lt;자산&gt;** VSIX에 포함 되어야 하는 각 파일에 대 한 요소입니다. 합니다 **형식** 각각의 특성 **&lt;자산&gt;** 요소 설정 해야 합니다 **Microsoft.VisualStudio.Mvc.Template**합니다. 이것이 MVC 프로젝트 마법사에서 인식할 수 있는 사용자 지정 네임 스페이스입니다. 구조 및 매니페스트 파일의 레이아웃에 대 한 자세한 내용은 VSIX 2.0 스키마 설명서를 참조 하십시오.

VSIX에 파일을 방금 추가 MVC 마법사를 사용 하 여 템플릿을 등록 하는 충분 하지 않습니다. MVC 마법사 템플릿 이름, 설명, 지원 되는 뷰 엔진 및 프로그래밍 언어와 같은 정보를 제공 해야 합니다. 이 정보는 연관 된 사용자 지정 특성에 전달 되는 **&lt;자산&gt;** 요소입니다 **vstemplate** 파일입니다.

&lt;자산 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;

d:Source=&quot;File&quot;

Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType=&quot;MVC&quot;

Language=&quot;C#&quot;

ViewEngine=&quot;Aspx&quot;

TemplateId=&quot;MyMvcApplication&quot;

제목 =&quot;사용자 지정 기본 웹 응용 프로그램&quot;

설명 =&quot;기본 MVC 웹 응용 프로그램 (Razor)에서 파생 된 사용자 지정 템플릿&quot;

Version=&quot;4.0&quot;/&gt;

다음 설명은 나타나야 하는 사용자 지정 특성은입니다.

- **ProjectType** MVC로 설정 해야 합니다.
- **언어** 템플릿에서 지 원하는 개발 언어를 지정 합니다. 유효한 값은 C# 또는 VB.
- **Viewengine이 제공 됨** Aspx 등 Razor 템플릿에서 지원 되는 뷰 엔진을 지정 합니다. 이 필드에 대 한 사용자 지정 값을 지정할 수 있습니다.
- **TemplateId** 템플릿을 그룹화 하는 데 사용 됩니다. 값이 기존 템플릿 ID는 것과 일치 하는 경우 MVC 마법사를 사용 하 여 이전에 등록 하는 서식 파일을 재정의 합니다.
- **제목** 아래 각 프로젝트 템플릿은 MVC 마법사에서 표시 되는 간단한 설명을 지정 합니다.
- **설명** 템플릿의 자세한 설명을 지정 합니다.

매니페스트에 포함 된 모든 파일을 추가한 후, 저장 점을 확인할 수 있습니다 합니다 **자산** 디자이너의 탭에는 모든 파일 표시 됩니다 있지만에 추가 하지 사용자 지정 특성을 **&lt;자산&gt;** 에 대 한 요소를 **vstemplate** 파일입니다.

![프로젝트 디자이너 자산](custom-mvc-templates/_static/image8.jpg)

이제는 VSIX 프로젝트를 컴파일 및 설치 합니다.

Visual Studio의 모든 인스턴스가 닫혀 있는지 컴퓨터에서 VSIX 확장을 테스트 하려는 경우. Visual Studio 스캔을 새 확장에 대 한 시작 하는 동안 VSIX 설치 하는 동안 IDE가 열려 있으면 Visual Studio를 다시 시작 해야 합니다. 시작 하려면 VSIX 파일 탐색기에서 두 번 클릭 합니다 **VSIX 설치 관리자**, 클릭 **설치** Visual Studio를 시작 합니다.

![VSIX 설치 관리자](custom-mvc-templates/_static/image9.jpg)

메뉴에서 선택 **도구 > 확장 및 업데이트** 확장이 설치 되어 있는지 확인 합니다. VSIX 설치 관리자 확장을 설치 하는 동안 오류를 보고 하는 경우 자세한 정보는 VSIX 설치 관리자 로그를 볼 수 있습니다. 로그에 일반적으로 만들어집니다 합니다 **%temp%** 예를 들어 확장을 설치 하는 사용자의 폴더 **C:\Users\Bob\AppData\Local\Temp**합니다.

![확장 및 업데이트](custom-mvc-templates/_static/image10.jpg)

창을 닫은 후 새 템플릿을 MVC 마법사에 표시 되는지 여부를 확인 하려면 MVC 4 프로젝트를 만들 수 있습니다.

![새 ASP.NET MVC 4 프로젝트](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>제한 사항

1. MVC 마법사에는 지역화 된 사용자 지정 템플릿을 지원 하지 않습니다.
2. 마법사는 사용자 지정 템플릿을 찾을 수 없는 경우 오류를 보고 하지 않습니다. 필수 사용자 지정 특성이 있는 없는 경우 템플릿은 하기만 하면 마법사에서 제외 됩니다.
