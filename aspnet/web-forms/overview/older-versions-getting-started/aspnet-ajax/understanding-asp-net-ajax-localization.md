---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: "ASP.NET AJAX 지역화 이해 | Microsoft Docs"
author: scottcate
description: "지역화는 프로세스를 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에는 특정 언어와 문화권에 대 한 지원을 통합입니다. Mic 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 5b801586ea77af78284f780fe47fe09cafb984af
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-aspnet-ajax-localization"></a>ASP.NET AJAX 지역화 이해
====================
으로 [Scott 인증서](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 지역화는 프로세스를 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에는 특정 언어와 문화권에 대 한 지원을 통합입니다. Microsoft ASP.NET 플랫폼, 표준.NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램에 대 한 지역화에 대 한 포괄적인 지원을 제공합니다 Microsoft AJAX Framework 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하도록 통합된 모델을 사용 합니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 기반 프로그래밍 모델을 가져오며 컴파일된 코드의 장점을 함께 결합 합니다. 그러나 해당 서버 쪽 처리 모델에는.NET Framework에는 Microsoft AJAX 서비스를 캡슐화 하는 System.Web.Extensions 네임 스페이스에 포함 된 새로운 기능으로 처리할 수 있으며이 중 대다수가 기술에 내재 된 몇 가지 단점 3.5입니다. 이러한 확장명 많은 리치 클라이언트 기능을 ASP.NET 2.0 AJAX 확장의 일부 이지만 Framework 기본 클래스 라이브러리의 일부 이제으로 사용할 수 있었던를 활성화합니다. 이 네임 스페이스의 기능과 컨트롤 전체 페이지 새로 고침 (프로 파일링 API는 ASP.NET 포함)는 클라이언트 스크립트를 통해 웹 서비스에 액세스 하는 기능을 요구 하지 않고 페이지의 부분 렌더링을 포함 하 고 미러링할 다양 한 광범위 한 클라이언트 쪽 API 설계 되었습니다. ASP.NET 서버측 컨트롤 집합의 표시 제어 구성표가 있습니다.

이 백서 지역화 지원 하 고 웹에서 지역화에 대 한 지원을 이미 통합 검토에 대 한 비즈니스 요구의 컨텍스트에서 Microsoft AJAX Framework 및 Microsoft AJAX 스크립트 라이브러리에 있는 지역화 기능 검사 .NET Framework에서 제공 하는 응용 프로그램입니다. Microsoft AJAX 스크립트 라이브러리 활용.resx 파일 형식과.NET 응용 프로그램에서 이미 사용 하는 통합 된 IDE 지원 및 공유할 수 있는 리소스 종류를 제공 합니다.

이 백서는 기반 Beta 2 버전의 Microsoft Visual Studio 2008에 있습니다. 이 백서는 또한 하지 Visual Web Developer Express, Visual Studio 2008을 사용 하 고 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 합니다 가정 합니다. 일부 코드 샘플에는 Visual Web Developer Express에서 사용할 수 있는 프로젝트 템플릿을 사용 합니다.

## <a name="the-need-for-localization"></a>*지역화 필요*

특히 엔터프라이즈 응용 프로그램 개발자와 구성 요소 개발자에 culture 및 언어 간의 차이점을 확인할 수 있는 도구를 만들 수는 점점 더 필요한 사항이 되었습니다. 클라이언트의 로캘과에 맞게 조정 하는 기능을 사용 하 여 구성 요소를 디자인 개발자 생산성 증가 하 고 조정 구성 요소에 전체적으로 작동 하는 데 필요한 작업의 양이 줄어듭니다.

지역화는 프로세스를 디자인 하 고 응용 프로그램 또는 응용 프로그램 구성 요소에는 특정 언어와 문화권에 대 한 지원을 통합입니다. Microsoft ASP.NET 플랫폼, 표준.NET 지역화 모델을 통합 하 여 표준 ASP.NET 응용 프로그램에 대 한 지역화에 대 한 포괄적인 지원을 제공합니다 Microsoft AJAX Framework 지역화를 수행할 수 있는 다양 한 시나리오를 지원 하도록 통합된 모델을 사용 합니다. Microsoft AJAX framework 스크립트 하거나 지역화할 수 위성 어셈블리로 배포 하거나 정적 파일 시스템 구조를 활용 하 여 합니다.

## <a name="embedding-scripts-with-satellite-assemblies"></a>*위성 어셈블리를 사용 하 여 스크립트를 포함합니다.*

표준.NET Framework 지역화 전략와 일치, 리소스 위성 어셈블리에 포함 될 수 있습니다. 위성 어셈블리에 여러 가지 장점이 이진 파일에 기존 리소스 포함 주어진된 지역화할을 업데이트할 수 있습니다 더 큰 이미지를 업데이트 하지 않고 추가 지역화 위성 어셈블리를 설치 하 여 배포할 수 있습니다 프로젝트 폴더와 위성 어셈블리를 주 프로젝트 어셈블리가 다시 로드 하는 발생 하지 않고 배포할 수 있습니다. ASP.NET 프로젝트에서 특히 증분 업데이트를 사용 하는 시스템 리소스의 시간을 크게 줄일 수 있으므로 유용이 고 최소한으로 프로덕션 웹 사이트를 사용 중단 시킵니다.

스크립트가 포함 하 여 어셈블리에 포함 된 관리 되는.resx (또는 컴파일된.resources) 컴파일 타임에 어셈블리에 포함 되어 있는 파일입니다. 해당 리소스 AJAX 런타임에 생성 된 코드를 통해 어셈블리 수준 특성을 통해 스크립트 응용 프로그램에 사용할 수

*포함 된 스크립트 파일에 대 한 명명 규칙*

Microsoft AJAX Framework 스크립트 관리 배포 및 스크립트의 테스트에서 사용 하기 위한 다양 한 옵션을 지원 하 고 이러한 옵션을 용이 하 게 지침이 제공 됩니다.

*쉽게 디버깅할 수 있습니다.*

릴리스 (프로덕션) 스크립트를 포함 하면 안는 `.debug` 파일 이름에는 한정자입니다. 스크립트 디버깅에 포함할지 용으로 설계 `.debug` 는 파일 이름에서.

*지역화 용이 하 게 하려면:*

중립 문화권 스크립트에 모든 문화권 식별자는 파일의 이름을 포함 되지 않습니다. 지역화 된 리소스를 포함 하는 스크립트, 파일 이름에 ISO 언어 코드를 지정 해야 합니다. 예를 들어 `es-CO` 스페인어, 콜롬비아에 대 한 의미 합니다.

다음 표에서 파일을 명명 규칙 예제와 함께 요약 되어 있습니다.

| 파일 이름 | 의미 |
| --- | --- |
| Script.js | 릴리스 버전 중립 문화권 스크립트입니다. |
| Script.debug.js | 디버그 버전 중립 문화권 스크립트입니다. |
| Script.en US.js | 릴리스 버전 영어 미국 스크립트입니다. |
| Script.debug.es CO.js | 디버그 버전에 스페인어, 콜롬비아 스크립트입니다. |

## <a name="walkthrough-create-an-localized-embedded-script"></a>연습: 지역화 된, 포함 된 스크립트를 만듭니다.

*참고:이 연습에서는 Visual Web Developer Express 클래스 라이브러리 프로젝트에 대 한 프로젝트 템플릿을 포함 하지 않는 Visual Studio 2008을 사용 해야 합니다.*

1. ASP.NET AJAX 확장 통합 새 웹 사이트 프로젝트를 만듭니다. 다른 프로젝트를 LocalizingResources 라는 솔루션 내에서 클래스 라이브러리 프로젝트를 만듭니다.
2. VerifyDeletion.js LocalizingResources 프로젝트에 라는 Jscript 파일 뿐 아니라 DeletionResources.resx 및 DeletionResources.es.resx 라는.resx 리소스 파일을 추가 합니다. 전자는 culture 중립 리소스가; 포함 됩니다. 후자 스페인어 언어 리소스가 포함 됩니다.
3. VerifyDeletion.js에 다음 코드를 추가 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

JavaScript Regex 구문, 단일 슬래시 내에서 텍스트에 잘 교환과 (이전 예제의 /FILENAME/는 예) RegExp 개체를 나타냅니다. MSDN 라이브러리에 대 한 광범위 한 JavaScript 참조 및 네이티브 JavaScript 개체에서 리소스를 온라인으로 찾을 수 있습니다.

1. DeletionResources.resx에 다음과 같은 리소스 문자열을 추가 합니다. 

    **VerifyDelete**: FILENAME을 삭제 하 시겠습니까?

    **삭제**: FILENAME 삭제 되었습니다.

1. DeletionResources.es.resx에 다음과 같은 리소스 문자열을 추가 합니다. 

    **VerifyDelete**: Est seguro 까지의 desee quitar 파일 이름?

    **삭제**: FILENAME se ha quitado 합니다.
2. 어셈블리 정보 파일을 코드의 다음 줄을 추가 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. LocalizingResources 프로젝트에 System.Web 및 System.Web.Extensions에 대 한 참조를 추가 합니다.
2. 웹 사이트 프로젝트에서 LocalizingResources 프로젝트에 대 한 참조를 추가 합니다.
3. Default.aspx의 웹 사이트 프로젝트 아래에서 다음 추가 태그로 ScriptManager 컨트롤을 업데이트 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Default.aspx 페이지에서 원하는 위치에서이 태그를 포함 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. F5 키를 누릅니다. 메시지가 표시 되 면 디버깅을 사용 합니다. 페이지가 로드 될 때 삭제 단추를 누르면 됩니다. Note 묻는 영어로 (컴퓨터가 설정 되어 있지 않으면 스페인어 언어 리소스 작업을 사용 하려면 기본적으로)에 대 한 확인 합니다.
2. 브라우저 창을 닫고 default.aspx로 돌아갑니다. 에 @Page ES-ES와 Culture 및 UICulture 바꾸기 자동 헤더 지시문을 사용 합니다. F5 키를 눌러 브라우저에서 웹 응용 프로그램 다시 시작을 다시 합니다. 이 이번에 스페인어로 파일을 삭제 하 라는 메시지가 note:


[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-localization/_static/image3.png))


[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-localization/_static/image6.png))


이 연습에 대 한 여러 변형이 참고 합니다. 예를 들어 스크립트 등록 못했습니다 ScriptManager 컨트롤에서 프로그래밍 방식으로 페이지를 로드 하는 동안 합니다.

## <a name="including-a-static-script-file-structure"></a>*정적 스크립트 파일 구조를 포함 하 여*

배포에 대 한 정적 스크립트 파일을 사용할 경우 내재 된.NET 지역화 체계를 사용 하는 이점 중 일부 손실 됩니다. 스크립트 리소스 파일을 비롯 하 여 생성 하는 자동 형식이 손실 주로 표시입니다. 예를 들어 위의 연습에서 리소스 ScriptManager 컨트롤에서 메시지를 호출 하는 자동으로 생성 된 형식에 의해 노출 되었습니다.

혜택이 있으며, 이때 일부는 정적 스크립트 파일 구조를 사용 하 여 합니다. 컴파일하여 다시 위성 어셈블리를 배포 하지 않고 업데이트를 수행할 수 있습니다 및는 구성 요소와 부 부분의 하지 제공 되었을 수 있는 기능을 통합 하 포함 된 스크립트를 재정의 하는 정적 파일 구조를 사용 하는 수행할 수 있습니다.

프로젝트를 컴파일하는 동안 스크립트 리소스를 자동으로 생성 하 여 버전 제어 문제를 방지 하는 것이 좋습니다. 광범위 한 스크립트 코드를 기본 유지 관리 하는 경우 각 지역화 된 스크립트에 코드 변경 내용이 반영 되었는지 확인 하기가 점점 어려워집니다 될 수 있습니다. 대신 단순히 유지 관리할 수 있습니다 하나의 논리 스크립트 및 여러 지역화 스크립트 프로젝트를 빌드하는 동안 파일을 병합 합니다.

선언적으로 포함 하도록 리소스 없기 때문이 파일은 되어야 하는 정적 스크립트 참조를 추가 하 여 `<asp:ScriptElement>` 의 자식으로 요소는 `<Scripts>` ScriptManager 컨트롤 또는 프로그래밍 방식으로 추가 하 여 태그 `ScriptReference` 개체 에 `Scripts` 의 속성은 `ScriptManager` 런타임에 페이지에 컨트롤입니다.

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager과 지역화에서의 역할*

ScriptManager는 지역화 된 응용 프로그램에 대 한 몇 가지 자동 동작을 활성화합니다.

- 설정 및; 명명 규칙에 따라 스크립트 파일을 자동으로 찾습니다. 예를 들어, 디버깅 모드에 있을 때 디버그 가능 스크립트를 로드 하 고 로드 브라우저의 사용자 인터페이스 선택에 따라 스크립트를 지역화 합니다.
- 사용자 지정 문화권을 포함 하 여 문화권의 정의 수 있습니다.
- HTTP를 통해 스크립트 파일의 압축을 사용합니다.
- 많은 요청을 효율적으로 관리 하는 스크립트를 캐시 합니다.
- 암호화 된 URL을 통해에 파이프 하 여 스크립트에는 간접 참조 계층을 추가 합니다.

프로그래밍 방식으로 또는 선언적 태그 ScriptManager 컨트롤에 스크립트 참조를 추가할 수 있습니다. 선언적 태그 특히 유용 이외의 웹 사이트 프로젝트 자체에 포함 된 어셈블리를 스크립트와 함께 작업 하는 경우 스크립트의 이름을 수정 버전을 통해 전달 되는 대로 되지 변경 될 예정 대로 합니다.

## <a name="summary"></a>요약

웹 응용 프로그램으로 크게 증가 하는 광범위 한 대상에 도달 광범위 한 문화권 및 커뮤니티에 연결할 수 있어야 필요가 비즈니스 모델;의 필수 요소 콘텐츠 관리 시스템 수 뿐 아니라 present 콘텐츠 하지만 자신의 탐색 힌트와 다른 언어 및 회사에 양식 필드를이 이와 같이 인지 알아야 할 필요가, 전자 상거래 웹 응용 프로그램 외래 통화 처리할 수 있도록 해야 합니다. 액세스할 수 있습니다.

기본적으로.NET Framework 리소스 문자열 및 이미지를 조회 하는 일관 된 방식으로 표시 하는 위성 어셈블리 및 XML 리소스 (.resx) 파일을 활용 하는 풍부한 지역화 프레임 워크를 지원 합니다. Microsoft AJAX Framework 및 Microsoft AJAX 스크립트 라이브러리를 포함 하 여 ASP.NET AJAX 확장에 지원을 제공이 프로그래밍 모델에 대 한 클라이언트 쪽 코드를 쉽게 문자열 조회를 사용 하도록 설정 합니다. 위성 어셈블리 따르기만 파일 이름이 지정된 하는 이름 지정 체계를 ScriptResource.axd 통해 스크립트 리소스 (실제.js 파일)의 자동 포함을 지원 합니다. 이 기능을 ASP.NET AJAX 확장에는 스크립트의 지역화 및 전역화 응용 프로그램의 단순화합니다.

## <a name="bio"></a>*약력*

Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)

>[!div class="step-by-step"]
[이전](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[다음](understanding-asp-net-ajax-web-services.md)
