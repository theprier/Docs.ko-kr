---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: ASP.NET AJAX 지역화 이해 | Microsoft Docs
author: scottcate
description: 지역화는 응용 프로그램 또는 응용 프로그램 구성 요소는 특정 언어와 문화권에 대 한 지원을 통합 및 설계 프로세스입니다. Mic...
ms.author: aspnetcontent
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: ce6404ce4faa1018a4f8118f6167a4f93956abd3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815012"
---
<a name="understanding-aspnet-ajax-localization"></a>ASP.NET AJAX 지역화 이해
====================
[Scott Cate](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 지역화는 응용 프로그램 또는 응용 프로그램 구성 요소는 특정 언어와 문화권에 대 한 지원을 통합 및 설계 프로세스입니다. Microsoft ASP.NET 플랫폼은 표준.NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램에 대 한 지역화에 대 한 광범위 하 게 지원 제공 Microsoft AJAX 프레임 워크는 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하도록 통합된 모델을 활용 합니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 및 컴파일된 코드의 이점과 결합 합니다. 그러나 해당 서버 쪽 처리 모델에는.NET Framework의 Microsoft AJAX 서비스를 캡슐화 하는 System.Web.Extensions 네임 스페이스에 포함 된 새 기능을 통해 해결할 수 있으며이 중 대다수가 기술에 내재 된 몇 가지 단점이 있습니다. 3.5입니다. 이러한 확장 사용 많은 리치 클라이언트 기능을 ASP.NET 2.0 AJAX Extensions, 부분 하지만 Framework 기본 클래스 라이브러리의 일부인 경우 이제으로 이전에 사용할 수 있습니다. 이 네임 스페이스의 기능과 컨트롤 (ASP.NET 프로 파일링 API 포함)는 클라이언트 스크립트를 통해 웹 서비스에 액세스할 수 있도록 전체 페이지 새로 고침 필요 없이 부분 렌더링 페이지의 포함 및 많은 미러 광범위 한 클라이언트 쪽 API 설계 컨트롤 스키마를 ASP.NET 서버측 컨트롤 집합에 표시 합니다.

이 백서에 Microsoft AJAX 스크립트 라이브러리를 확인 하 고 Microsoft AJAX 프레임 워크 지역화 지원과 웹에서 지역화에 대 한 지원이 이미 통합 검토에 대 한 비즈니스 요구의 컨텍스트에서 지역화 기능 검사 .NET Framework에서 제공 하는 응용 프로그램입니다. Microsoft AJAX 스크립트 라이브러리는.resx 파일 형식에서.NET 응용 프로그램을 이미 사용 하는 통합 된 IDE 지원 및 공유할 수 있는 리소스 형식을 제공 하는 활용 합니다.

이 백서는 기반 Microsoft Visual Studio 2008 베타 2 릴리스 합니다. 이 백서는 또한 하지 Visual Web Developer Express를 Visual Studio 2008을 사용 하는 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 하는 가정 합니다. 몇 가지 코드 샘플에는 Visual Web Developer Express에서 사용할 수 있는 프로젝트 템플릿을 사용 합니다.

## <a name="the-need-for-localization"></a>*지역화 필요*

특히에 대 한 엔터프라이즈 응용 프로그램 개발자와 구성 요소 개발자는 culture 및 언어 간의 차이점을 인식 될 수 있는 도구를 만들 수는 점점 더 많이 필요한 되었습니다. 개발자 생산성을 높이고 요소의 조정에 대 한 전역적으로 작동 하는 데 필요한 작업을 줄여 클라이언트의 로캘과에 맞게 조정 하는 기능을 사용 하 여 구성 요소를 디자인 합니다.

지역화는 응용 프로그램 또는 응용 프로그램 구성 요소는 특정 언어와 문화권에 대 한 지원을 통합 및 설계 프로세스입니다. Microsoft ASP.NET 플랫폼은 표준.NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램에 대 한 지역화에 대 한 광범위 하 게 지원 제공 Microsoft AJAX 프레임 워크는 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하도록 통합된 모델을 활용 합니다. Microsoft AJAX 프레임 워크를 사용 하 여 스크립트 하거나 지역화할 수 위성 어셈블리로 배포 또는 정적 파일 시스템 구조를 활용 하 여 합니다.

## <a name="embedding-scripts-with-satellite-assemblies"></a>*위성 어셈블리를 사용 하 여 스크립트를 포함합니다.*

표준.NET Framework 지역화 전략을 사용 하 여 일관 된, 리소스 위성 어셈블리에 포함할 수 있습니다. 위성 어셈블리에 여러 가지 장점이 이진 파일에서 기존 리소스 포함을 통해 모든 지정 된 지역화 업데이트할 수 더 큰 이미지를 업데이트 하지 않고, 위성 어셈블리를 설치 하면 추가 지역화를 배포할 수 있습니다 주 프로젝트 어셈블리가 다시 로드 하지 않고도 프로젝트 폴더 및 위성 어셈블리를 배포할 수 있습니다. ASP.NET 프로젝트의 경우에 특히이 증분 업데이트를 사용 하는 시스템 리소스의 양을 상당히 줄일 수 있기 때문에 유용 하며 최소한으로 프로덕션 웹 사이트 사용 중단 됩니다.

스크립트는 포함 하 여 어셈블리에 포함 된 관리 되는.resx (또는 컴파일된.resources) 파일을 컴파일할 때 어셈블리에 포함 되어 있습니다. 해당 리소스 AJAX 런타임에 생성 된 코드를 통해 어셈블리 수준 특성을 통해 스크립트 응용 프로그램에 사용할 수 있습니다.

*포함 된 스크립트 파일에 대 한 명명 규칙*

Microsoft AJAX 프레임 워크 스크립트 관리 배포 및 테스트 스크립트를 사용 하 여 여러 가지 옵션을 지원 하 고 지침 이러한 옵션을 용이 하 게 제공 됩니다.

*쉽게 디버깅할 수 있습니다.*

릴리스 (프로덕션) 스크립트를 포함 하지 않아야 합니다 `.debug` 파일 이름에는 한정자입니다. 스크립트 디버깅에 포함할지를 위한 `.debug` 파일 이름에서입니다.

*지역화를 위해:*

중립 문화권 스크립트는 모든 문화권 식별자는 파일의 이름을 포함 되지 않습니다. 지역화 된 리소스를 포함 하는 스크립트의 경우 ISO 언어 코드가 파일 이름을 지정 해야 합니다. 예를 들어 `es-CO` 스페인어, Columbia에 대 한 의미 합니다.

다음 표에서 명명 규칙 예제를 사용 하 여 파일을 보여 줍니다.

| 파일 이름 | 의미 |
| --- | --- |
| Script.js | 릴리스 버전 문화권 중립 스크립트입니다. |
| Script.debug.js | 디버그 버전 문화권 중립 스크립트입니다. |
| Script.en-US.js | 릴리스 버전 영어, 미국 스크립트입니다. |
| Script.debug.es-CO.js | 디버그 버전에 스페인어, Columbia 스크립트입니다. |

## <a name="walkthrough-create-an-localized-embedded-script"></a>연습: 지역화 된, 포함 된 스크립트를 만들려면

*참고:이 연습에서는 Visual Web Developer Express 클래스 라이브러리 프로젝트의 프로젝트 템플릿에 포함 하지 않는 Visual Studio 2008을 사용 해야 합니다.*

1. 통합 하는 ASP.NET AJAX Extensions를 사용 하 여 새 웹 사이트 프로젝트를 만듭니다. 다른 프로젝트를 LocalizingResources 라는 솔루션 내에서 클래스 라이브러리 프로젝트를 만듭니다.
2. DeletionResources.resx 및 DeletionResources.es.resx 라는.resx 리소스 파일 뿐만 아니라 VerifyDeletion.js LocalizingResources 프로젝트 라는 Jscript 파일을 추가 합니다. 전자는 culture 중립 리소스가; 포함 됩니다. 후자는 스페인어 리소스를 포함 됩니다.
3. VerifyDeletion.js에 다음 코드를 추가 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

JavaScript 정규식 구문에 단일 슬래시 내의 텍스트를 사용 하 여 알 수 없는 (앞의 예에서 /FILENAME/의 예) RegExp 개체를 나타냅니다. MSDN Library에는 광범위 한 JavaScript 참조를 포함 하 고 네이티브 JavaScript 개체의 리소스를 온라인으로 확인할 수 있습니다.

1. DeletionResources.resx에 리소스 문자열을 추가 합니다. 

    **VerifyDelete**: 파일을 삭제 하 시겠습니까?

    **삭제**: FILENAME 삭제 되었습니다.

1. DeletionResources.es.resx에 리소스 문자열을 추가 합니다. 

    **VerifyDelete**: Est seguro 쿼리 desee quitar FILENAME?

    **삭제**: FILENAME se ha quitado 합니다.
2. AssemblyInfo 파일에 다음 코드 줄을 추가 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. LocalizingResources 프로젝트에 System.Web 및 System.Web.Extensions에 대 한 참조를 추가 합니다.
2. 웹 사이트 프로젝트에서 LocalizingResources 프로젝트에 대 한 참조를 추가 합니다.
3. 웹 사이트 프로젝트에서 default.aspx를 ScriptManager 컨트롤은 다음 추가 태그를 사용 하 여 업데이트 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Default.aspx 페이지에서 원하는 위치에서이 태그를 포함 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. F5 키를 누릅니다. 메시지가 표시 되 면 디버깅을 사용 합니다. 페이지가 로드 될 때 삭제 단추를 누릅니다. Note는 영어에서 (하지 않는 한 컴퓨터는 스페인어 리소스를 사용 하려면 기본적으로 설정 됨)를 묻는 확인 합니다.
2. 브라우저 창을 닫고 default.aspx로 돌아갑니다. 에 @Page 헤더 지시문, ES-ES를 사용 하 여 Culture 및 UICulture에 대 한 대체 자동입니다. F5 키를 눌러 브라우저에서 웹 응용 프로그램 다시 시작을 다시 합니다. 이 이번에는 스페인어에서 파일을 삭제할 것인지 묻는 note:


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-localization/_static/image3.png))


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-localization/_static/image6.png))


이 연습에 대 한 여러 변형이 참고 합니다. 예를 들어 스크립트 등록 못했습니다 ScriptManager 컨트롤을 사용 하 여 프로그래밍 방식으로 페이지를 로드 하는 동안.

## <a name="including-a-static-script-file-structure"></a>*정적 스크립트 파일 구조를 포함 하 여*

정적 스크립트 파일을 사용 하 여 배포, 고유한.NET 지역화 체계를 사용 하는 이점의 일부 손실 됩니다. 스크립트 리소스 파일을 비롯 하 여 생성 된 자동 형식을 손실 주로 표시입니다. 예를 들어, 위의 연습에서 리소스 ScriptManager 컨트롤에서 메시지 호출을 자동으로 생성 유형별로 노출 되었습니다.

그러나 혜택이 있으며, 몇 가지 정적 스크립트 파일 구조를 사용 하 여 합니다. 컴파일하여 위성 어셈블리를 배포할 필요 없이 업데이트를 수행할 수 있습니다 하 고 구성 요소를 사용 하 여 사소한 부분 하지 제공 되었을 수 있는 기능을 통합에 포함 된 스크립트를 재정의 하려면 정적 파일 구조를 사용 하 여 수행할 수도 있습니다.

프로젝트를 컴파일하는 동안 스크립트 리소스를 자동으로 생성 하 여 버전 제어 문제를 방지 하는 것이 좋습니다. 광범위 한 스크립트 코드를 기본 유지 관리 하는 경우에 각 지역화 된 스크립트에 코드 변경 내용이 반영 되었는지 확인 하기가 점점 어려워집니다 될 수 있습니다. 대신 단순히 유지 관리할 수 있습니다 하나의 논리 스크립트 및 여러 지역화 스크립트 프로젝트를 빌드하는 동안 파일을 병합 합니다.

정적 스크립트 파일이 있어야 하거나 추가 하 여 참조 하는 선언적으로 포함 하도록 리소스 없기 때문 `<asp:ScriptElement>` 자식 요소를 `<Scripts>` 태그 또는 ScriptManager 컨트롤을 프로그래밍 방식으로 추가 하 여 `ScriptReference` 개체 에 `Scripts` 의 속성을 `ScriptManager` 런타임 시 페이지에서 컨트롤.

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager과 지역화에서의 역할*

ScriptManager는 지역화 된 응용 프로그램에 대 한 몇 가지 자동 동작을 활성화합니다.

- 설정 및; 명명 규칙에 따라 스크립트 파일을 자동으로 찾습니다. 예를 들어 디버그 가능 스크립트 디버깅 모드에 있을 때 로드 및 로드 브라우저의 사용자 인터페이스 선택에 따라 스크립트를 지역화 합니다.
- 문화권, 사용자 지정 culture를 포함 하 여 정의 수 있습니다.
- HTTP를 통한 스크립트 파일의 압축을 수 있습니다.
- 많은 요청을 효율적으로 관리 하는 스크립트를 캐시 합니다.
- 암호화 된 URL을 통해 파이프 하 여 스크립트에 간접 참조 계층을 추가 합니다.

프로그래밍 방식으로 또는 선언적 태그에서 ScriptManager 컨트롤에 스크립트 참조를 추가할 수 있습니다. 선언적 태그는 특히 유용 이외의 웹 사이트 프로젝트 자체에 포함 된 어셈블리를 스크립트를 사용 하 여 작업 하는 경우 스크립트의 이름을 수정 버전을 통해 전달 되는 대로 없습니다 변경 될 가능성이 됩니다.

## <a name="summary"></a>요약

광범위 한 문화권 및 커뮤니티에 연결할 수는 비즈니스 모델의 핵심은 광범위 한 대상에 연결할 웹 응용 프로그램 증가 함에 따라 콘텐츠 관리 시스템에서 해당 콘텐츠 하지만 해당 탐색 힌트 및 기타 언어 및 회사에 양식 필드를 알아야이 요구 되는 수 뿐만 아니라 현재 해야, 전자 상거래 웹 응용 프로그램 외래 통화를 사용 하 여 처리할 수 있도록 해야 합니다. 액세스할 수 있습니다.

기본적으로.NET Framework 리소스 문자열 및 이미지를 조회 하는 일관 된 방식을 제공 하는 위성 어셈블리 및 XML 리소스 (.resx) 파일을 활용 하 여 다양 한 지역화 프레임 워크를 지원 합니다. Microsoft AJAX 프레임 워크 및 Microsoft AJAX 스크립트 라이브러리를 포함 하 여 ASP.NET AJAX Extensions, 지원을 제공이 프로그래밍 모델에 대 한 클라이언트 쪽 코드를 쉽게 리소스 문자열 조회를 사용 하도록 설정 합니다. 위성 어셈블리 파일 이름을 따라 명명 체계를 지정된 하기만 ScriptResource.axd 통해 스크립트 리소스 (실제.js 파일)의 자동 포함을 지원 합니다. 이 지원을 통해 ASP.NET AJAX Extensions 스크립트 지역화 및 응용 프로그램의 세계화를 간소화합니다.

## <a name="bio"></a>*사용자 정보*

Scott Cate 1997 년부터 Microsoft 웹 기술을 사용 하 여 왔습니다 이며 myKB.com의 대표이사로 서 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 전문적 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott 전자 메일을 통해 연락할 수 있습니다 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 저자의 블로그 또는 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [다음](understanding-asp-net-ajax-web-services.md)
