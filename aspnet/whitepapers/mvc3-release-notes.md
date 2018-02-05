---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/06/2010
ms.topic: article
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 92a6dee24b8942d721e3537a712be141155e61df
ms.sourcegitcommit: d8aa1d314891e981460b5e5c912afb730adbb3ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2018
---
<a name="aspnet-mvc-3"></a>ASP.NET MVC 3
====================
- [개요](#overview)
- [설치 참고 사항](#installation-notes)
- [소프트웨어 요구 사항](#software-requirements)
- [문서](#documentation)
- [지원](#support)
- [ASP.NET MVC 2 프로젝트 업그레이드 하는 ASP.NET mvc 3 도구 업데이트](#upgrading)
- [ASP.NET MVC 3 도구 업데이트 (2011 년 4 월 12 일)](#tu-changes)

    - ["컨트롤러 추가" 대화 상자에 컨트롤러를 뷰 및 데이터 액세스 코드와 함께 스 캐 폴딩할 수 있습니다.](#tu-AddControllerDialog)
    - [향상 된 기능에서 "ASP.NET MVC 3 새 프로젝트" 대화 상자](#tu-ImprovementsNewDialogBox)
    - [프로젝트 템플릿에 Modernizr 1.7이 포함](#tu-Modernizr)
    - [프로젝트 템플릿에 jQuery, jQuery UI 및 jQuery의 업데이트 된 버전이 포함 되어 유효성 검사](#tu-UpdatedJQuery)
    - [프로젝트 템플릿에 이제 ADO.NET Entity Framework 4.1 사전 설치 NuGet 패키지로 포함](#tu-EF)
    - [프로젝트 템플릿에 JavaScript 라이브러리를 사전 설치 된 NuGet 패키지로 포함](#tu-JavaScriptLibsNuget)
    - [알려진 문제](#tu-KI)
- [ASP.NET MVC 3 RTM (2011 년 1 월 13 일)](#MVC3RTM)

    - [변경 사항: 1.8.7 버전의 jQuery UI 업데이트](#RTM-1)
    - [ModelMetadataProvider DataAnnotationsModelMetadataProvider로 다시 기본값을 변경 하는 변경 사항:](#RTM-2)
    - [공백 결과 거꾸로를 포함 하는 Razor 식의 일부를 붙여 넣는 방법 문제가 해결 됨](#RTM-3)
    - [구문 색 지정 및 IntelliSense 고정: 편집기에서 열려 있는 Razor 파일의 이름 바꾸기 해제](#RTM-4)
    - [알려진 문제](#RTM-KI)
    - [주요 변경 내용](#RTM-BC)
- [ASP.NET MVC 3 Release Candidate 2 (2010 년 12 월 10 일)](#_Toc2)

    - [프로젝트 템플릿이 1.4.4 jQuery, jQuery 유효성 검사 1.7 및 jQuery UI 1.8.6y UI 1.8.6 포함 하도록 변경](#_Toc2_1)
    - [추가 된 "AdditionalMetadataAttribute" 클래스](#_Toc2_2)
    - [향상 된 보기 스 캐 폴딩](#_Toc2_3)
    - [추가 된 Html.Raw 메서드](#_Toc2_3)
    - [이름이 바뀐된 "Controller.ViewModel" 속성과 "ViewBag"을 "보기" 속성](#_Toc2_4)
    - [이름이 바뀐된 "ControllerSessionStateAttribute" 클래스 "SessionStateAttribute"를](#_Toc2_5)
    - [이름이 바뀐된 RemoteAttribute "Fields" 속성을 "AdditionalFields"](#_Toc2_6)
    - ["AllowHtmlAttribute"를 "SkipRequestValidationAttribute" 이름이 변경](#_Toc2_7)
    - [첫 번째 유용한 오류 메시지를 표시 하려면 변경 된 "Html.ValidationMessage" 메서드](#_Toc2_8)
    - [고정 @model 문서에 공백을 추가 하지 않는 선언](#_Toc2_9)
    - [엔진-특정 파일 이름을 지원 하도록 뷰 엔진에 추가 된 "FileExtensions" 속성](#_Toc2_10)
    - ["For" 특성에 대 한 올바른 값을 내보내는 데 고정된 "LabelFor" 도우미](#_Toc2_11)
    - [모델 바인딩 중 명시적 값 우선 순위 RenderAction"고정된" 메서드](#_Toc2_12)
    - [주요 변경 내용](#_Toc2_BC)
    - [알려진 문제](#_Toc2_KI)
- [ASP.NET MVC 3 릴리스 후보 (2010 년 11 월 9 일)](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC의 새로운 기능](#_Toc276711785)
    - [NuGet 패키지 관리자](#_Toc276711786)
    - [향상 "새 프로젝트" 대화 상자](#_Toc276711787)
    - [Sessionless 컨트롤러](#_Toc276711788)
    - [새 유효성 검사 특성](#_Toc276711789)
    - ["LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드](#_Toc276711790)
    - [자식 동작 출력 캐싱](#_Toc276711791)
    - ["뷰 추가" 대화 상자 개선 사항](#_Toc276711792)
    - [Granular Request Validation](#_Toc276711793)
    - [주요 변경 내용](#_Toc276711794)
    - [알려진 문제](#_Toc276711795)
- [ASP입니다. MVC 3 베타 정보 (2010 년 10 월 6 일)](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 베타의 새로운 기능](#0.1__Toc274034215)
    - [NuPack 패키지 관리자](#0.1__Toc274034216)
    - [향상 된 새 프로젝트 대화 상자](#0.1__Toc274034217)
    - [강력 하 게 지정 하는 간단한 방법은 입력 Razor 뷰 모델](#0.1__Toc274034218)
    - [새 ASP.NET 웹 페이지에 대 한 도우미 메서드를 지원](#0.1__Toc274034219)
    - [추가 종속성 주입 지원](#0.1__Toc274034220)
    - [비 가시적인 jQuery 기반 Ajax에 대 한 새로운 지원](#0.1__Toc274034221)
    - [비 가시적인 jQuery 유효성 검사에 대 한 새로운 지원](#0.1__Toc274034222)
    - [클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그](#0.1__Toc274034223)
    - [뷰를 실행 하기 전에 실행 되는 코드에 대 한 새로운 지원](#0.1__Toc274034224)
    - [VBHTML Razor 구문에 대 한 새로운 지원](#0.1__Toc274034225)
    - [ValidateInputAttribute 보다 세부적으로 제어](#0.1__Toc274034226)
    - [도우미 밑줄 하이픈에 대 한 변환 익명 개체를 사용 하 여 지정 된 HTML 특성 이름](#0.1__Toc274034227)
    - [버그 수정](#0.1__Toc274034228)
    - [주요 변경 내용](#0.1__Toc274034229)
    - [알려진 문제](#0.1__Toc274034230)
- [Disclaimer](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>개요

이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 3 rtm 릴리스를 설명 합니다. ASP.NET MVC는 모델-뷰-컨트롤러 (MVC) 패턴을 사용 하는 웹 응용 프로그램을 개발 하기 위한 프레임 워크. ASP.NET MVC 3 설치 관리자는 다음 구성 요소가 포함 되어 있습니다.

- ASP.NET MVC 3 런타임 구성 요소
- ASP.NET MVC 3 Visual Studio 2010 도구
- ASP.NET 웹 페이지 런타임 구성 요소
- ASP.NET 웹 페이지 Visual Studio 2010 도구
- .NET (NuGet) 용 Microsoft 패키지 관리자
- Razor 구문에 대 한 지원을 활성화 하는 Visual Studio 2010에 대 한 업데이트 합니다. (세부 정보를 기술 자료 문서 2483190 참조).

다음 URL의 ASP.NET 웹 사이트에서 ASP.NET MVC 3의 시험판 버전 각각에 대 한 릴리스 정보의 전체 집합을 찾을 수 있습니다.

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET MVC 3 RTM 웹 플랫폼 설치 관리자 (웹 PI)를 사용 하 여를 설치 하려면 다음 페이지를 방문 합니다.

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

또는 다음 페이지에서 Visual Studio 2010 용 ASP.NET MVC 3 RTM 용 설치 관리자를 다운로드할 수 있습니다.

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 설치할 수 있고-함께 실행할 수 있는 ASP.NET MVC 2입니다.

<a id="software-requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET MVC 3 런타임 구성 요소는 다음과 같은 소프트웨어가 필요합니다.

- .NET framework 버전 4입니다. 

    ASP.NET MVC 3 Visual Studio 2010 도구에는 다음과 같은 소프트웨어가 필요합니다.
- Visual Studio 2010 또는 Visual Web Developer 2010 Express입니다.

<a id="documentation"></a>
## <a name="documentation"></a>설명서

ASP.NET MVC에 대 한 설명서는 다음 URL에서 MSDN 웹 사이트에서 사용할 수 있습니다.

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

자습서 및 ASP.NET MVC에 대 한 기타 정보는 다음 URL에서 ASP.NET 웹 사이트의 MVC 페이지에서 사용할 수 있습니다.

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>Support(지원)

이 완전히 지원 되는 릴리스입니다. 기술 지원을 받는 방법에 대 한 정보를 찾을 수 있습니다는 [Microsoft 지원 웹 사이트](https://support.microsoft.com/)합니다.

또한 자유롭게 ASP.NET 커뮤니티의 구성원은 자주 비공식적인 지원을 제공할 수 있는 ASP.NET MVC 포럼에이 릴리스에 대 한 질문을 게시 합니다.

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 2 프로젝트 업그레이드 하는 ASP.NET mvc 3 도구 업데이트

ASP.NET MVC 3 ASP.NET MVC 3을 ASP.NET MVC 2 응용 프로그램을 업그레이드 하는 시기 선택에 유연성을 제공 하 여 동일한 컴퓨터에 ASP.NET MVC 2와 함께 설치할 수 있습니다.

기존 ASP.NET MVC 2 응용 프로그램 버전 3를 수동으로 업그레이드 하려면 다음을 수행 합니다.

1. 컴퓨터에 비어 있는 새 ASP.NET MVC 3 프로젝트를 만듭니다. 이 프로젝트는 업그레이드에 필요한 일부 파일을 포함 됩니다.
2. ASP.NET MVC 3 프로젝트에서 ASP.NET MVC 2 프로젝트의 해당 위치에 다음 파일을 복사 합니다. 새 파일 이름 (jquery-1.5.1.js)을 설명 하기 위해 jQuery 라이브러리에 대 한 참조를 업데이트 해야 합니다. 

    - /Views/Web.config
    - /packages.config
    - /scripts/\*.js
    - /내용/테마/\*합니다.\*
3. 복사는 *패키지* 솔루션의.sln 파일이 있는 디렉터리에 있는 솔루션의 루트에 빈 ASP.NET MVC 3 프로젝트 솔루션의 루트에는 폴더입니다.
4. ASP.NET MVC 2 프로젝트에 영역이 포함 된, 경우 /Views/Web.config 파일을 복사는 *뷰* 각 영역의 폴더입니다.
5. ASP.NET MVC 2 프로젝트에서 두 Web.config 파일에서 검색 하 고 ASP.NET MVC 버전이 대체 되는 전역적으로. 다음을 찾습니다. 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    다음으로 바꿉니다.

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. 솔루션 탐색기에서 삭제에 대 한 참조 *System.Web.Mvc* (점을 DLL 버전 2), 다음에 대 한 참조를 추가 *System.Web.Mvc* (v3.0.0.0).
7. System.Web.WebPages.dll 및 System.Web.Helpers.dll에 대 한 참조를 추가 합니다. 이러한 어셈블리는 다음 폴더에 있습니다. 

    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다. 그런 다음 프로젝트 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.
9. 찾을 *ProjectTypeGuids* 요소 및 {F85E285D-A4E0-4152-9332-AB1D724D3325} {E53F8FEA-EAE0-44A6-8774-FFD645390401}로 대체 합니다.
10. 변경 내용을 저장, 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.
11. 응용 프로그램의 루트 Web.config 파일에 추가 하려면 다음 설정의 *어셈블리* 섹션. 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. ASP.NET MVC 2를 사용 하 여 컴파일되는 모든 타사 라이브러리를 프로젝트에서 참조 하는 경우 강조 표시 된 다음 추가 *bindingRedirect* 응용 프로그램 루트에 있는 Web.config 파일에는 요소는  *구성* 섹션: 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>변경 내용을 in ASP.NET MVC 3 도구 업데이트

이 섹션에서는 ASP.NET MVC 3 RTM 릴리스 이후의 ASP.NET MVC 3 도구 업데이트 릴리스에서 변경에 설명 합니다.

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>"컨트롤러 추가" 대화 상자에 컨트롤러를 뷰 및 데이터 액세스 코드와 함께 스 캐 폴딩할 수 있습니다.

스 캐 폴딩은 방법은 응용 프로그램에 대 한 뷰와 컨트롤러를 신속 하 게 생성 합니다. 코드 생성 된 후 프로젝트의 요구 사항에 맞게 편집할 수 있습니다.

시작 하는 *컨트롤러 추가* 대화 상자에서 ASP.NET MVC 3 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더에 *솔루션 탐색기*, 클릭 *추가*, 클릭 하 고 *컨트롤러*합니다. 대화 상자 추가적인 스 캐 폴딩 옵션을 제공 하도록 향상 되었습니다.

![](mvc3-release-notes/_static/image1.png)

기본적으로 사용 가능한 세 개의 스 캐 폴딩 템플릿이 있습니다.

#### <a name="empty-controller"></a>빈 컨트롤러

이 템플릿은 빈 컨트롤러 파일을 생성합니다. 이 템플릿을 선택 하지 않는 것 같습니다. *만들기, 편집, 세부 정보에 대 한 작업을 추가, 삭제 시나리오* 이전 버전의 ASP.NET MVC에서 합니다. 이 선택 하면 없습니다 추가 옵션을 사용할 수 있습니다.

#### <a name="controller-with-empty-readwrite-actions"></a>빈 읽기/쓰기 동작이 포함 된 컨트롤러

이 템플릿은 방법의 모든 필요한 동작 메서드에 구현 코드가 없는 되어 있는 컨트롤러 파일을 생성 합니다. 이 템플릿을 확인 하는 것 *만들기, 편집, 세부 정보에 대 한 작업을 추가, 삭제 시나리오* 이전 버전의 ASP.NET MVC에서 합니다. 이 선택 하면 없습니다 추가 옵션을 사용할 수 있습니다.

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>읽기/쓰기 동작 및 Entity Framework를 사용 하 여 뷰, 컨트롤러

이 서식 파일을 사용 하면 신속 하 게 작업 데이터 입력 사용자 인터페이스를 만들 수 있습니다. 다양 한 일반 요구 사항 및 다음과 같은 시나리오를 처리 하는 코드를 생성 합니다.

- *데이터 액세스*합니다. 생성 된 코드를 읽고 엔터티는 데이터베이스에 씁니다. 기존 데이터 컨텍스트 클래스를 선택 하거나 템플릿에서 새 생성 하도록 하면 Entity Framework Code First 접근 방식으로 작동 *DbContext* 클래스입니다. 기존 선택도 Entity Framework Database First 또는 Model First 접근 방식으로 작동 *ObjectContext* 클래스입니다.
- *유효성 검사*합니다. 생성 된 코드 모델 클래스에 선언 된 규칙에 따라 폼 전송의 유효성이 검사 됩니다 되도록 ASP.NET MVC 모델 바인딩 및 메타 데이터 기능을 사용 합니다. 같은 기본 제공 유효성 검사 규칙이 포함 됩니다는 *필요한* 및 *StringLength* 특성 및 사용자 지정 유효성 검사 규칙입니다.
- *1 대 다 관계*합니다. 모델 클래스 간에 일대다에 외래 키 관계를 정의 하면 생성된 된 코드는 관련된 엔터티를 선택 하기 위한 드롭 다운 목록을 생성 합니다. 예를 들어, Entity Framework Code First 규칙을 따르는 다음과 같은 모델 클래스를 정의할 수 있습니다. 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    경우 다음 스 캐 폴드 할에 대 한 컨트롤러는 *제품* 클래스, 해당 뷰를 통해 사용자가 선택할 수는 *범주* 각각에 대 한 개체 *제품* 인스턴스.

    이 서식 파일의 추가 옵션을 사용 하면는 *컨트롤러 추가* 대화 상자. 에 대 한 *모델 클래스*, 사용자가을 만들거나 편집할 수 있는 데이터 형식을 결정 하는 솔루션의 모든 모델 클래스를 선택할 수 있습니다.
- Entity Framework Code First를 사용 하려는 경우 아무 모델 클래스나를 선택할 수 있습니다.
- Entity Framework Database First 또는 Entity Framework Model First를 사용 하는 경우 개념적 모델에 정의 된 엔터티 클래스를 선택 해야 합니다.

에 대 한 *데이터 컨텍스트 클래스*, 이러한 선택 항목을 만들 수 있습니다.

- Code First 사용 하 여 않으며 없는 기존 데이터 컨텍스트 클래스를 선택 하려는 경우 * * 새 데이터 컨텍스트에 * *입니다. 데이터 컨텍스트 클래스를 다음 생성 됩니다.
- Code First를 사용 하 여 기존 데이터 컨텍스트 클래스가 하려는 경우 여기에서 선택한 것입니다. 선택한 모델 클래스를 유지 하도록 업데이트 됩니다.
- Database First 또는 Model First를 사용 하는 경우 여기서 개체 컨텍스트 클래스를 선택 합니다.

뷰를 사용 하려는 뷰 엔진을 선택 하거나 모든 뷰를 스 캐 폴드 하려면 없음을 선택 합니다.

고급 하려면을 선택 하면 추가 생성 된 뷰에 대 한 옵션을 지정 합니다. 예를 들어 레이아웃 또는 마스터 페이지를 사용 하 여 선택할 수 있습니다.

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>향상 된 기능에서 "ASP.NET MVC 3 새 프로젝트" 대화 상자

새 ASP.NET MVC 3 프로젝트를 만드는 데 사용 하 여 대화 상자 아래에 나열 된 향상 된 여러 기능이 포함 됩니다.

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>새 "인트라넷 프로젝트" 템플릿

프로젝트 템플릿 목록에는 새 인트라넷 응용 프로그램 템플릿이 포함 됩니다. 이 템플릿에 폼 인증 대신 Windows 인증을 사용 하 여 웹 응용 프로그램에 대 한 설정을 포함 합니다. 인트라넷 응용 프로그램 프로젝트 템플릿에서 캡슐화 할 수 없는 일부 IIS 설정이 필요로 하므로 서식 파일에는 추가 정보 파일을 IIS에서 프로젝트 템플릿을 만드는 방법에 대 한 지침이 포함 됩니다. 에 대 한 설명서는 새 인트라넷 응용 프로그램 서식 파일은 다음 URL의 MSDN 웹 사이트에서 사용할 수 있습니다.

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>프로젝트 템플릿에 HTML5 사용 하도록 설정 됩니다.

새 프로젝트 대화 상자에 이제 프로젝트 템플릿에 HTML5 특정 기능을 추가할 수 있는 옵션이 포함 되어 있습니다. 옵션을 선택 하면 새 HTML5를 포함 하는 뷰가 생성 될 `<header>`, `<footer>`, 및 `<navigation>` 요소입니다. 요소입니다.

참고가 이전 버전의 브라우저 HTML5 특정 태그를 지원 하지 않습니다. 이 한계를 해결 하기 위해 HTML5 프로젝트 템플릿에 Modernizr 라이브러리에 대 한 참조를 포함 합니다. (다음 섹션 참조).

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>프로젝트 템플릿에 Modernizr 1.7이 포함

Modernizr은 아직 이러한 기능을 지원 하지 않는 브라우저에서 CSS 3 및 HTML5 지원이 가능한 JavaScript 라이브러리입니다. 이 라이브러리는 ASP.NET MVC 3 프로젝트용 템플릿에 사전 설치 NuGet 패키지로 포함 되어 있습니다. Modernizr에 대 한 자세한 내용은 참조 [http://www.modernizr.com/](http://www.modernizr.com/)합니다.

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>프로젝트 템플릿에 jQuery, jQuery UI 및 jQuery의 업데이트 된 버전이 포함 되어 유효성 검사

프로젝트 템플릿에 jQuery 스크립트의 다음 버전 포함:

- 1.5.1 jQuery
- jQuery 유효성 검사 1.8
- jQuery UI 1.8.11

이러한 라이브러리는 사전 설치 된 NuGet 패키지로 포함 됩니다.

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>프로젝트 템플릿에 이제 ADO.NET Entity Framework 4.1 사전 설치 NuGet 패키지로 포함

ADO.NET Entity Framework 4.1 Code First 기능이 포함 되어 있습니다. 코드는 먼저 기존 Database First 및 Model First 패턴에 대 한 대안을 제공 하는 ADO.NET Entity Framework에 대 한 새로운 개발 패턴입니다.

코드 먼저은 집중 Visual Basic 또는 C#에서 작성 된 POCO 클래스 ("일반 이전 CLR 개체")를 사용 하 여 모델을 정의 합니다. 이러한 클래스 다음 기존 데이터베이스에 매핑할 수 있습니다 또는 데이터베이스 스키마를 생성 하는 데 사용 됩니다. 사용 하 여 추가 구성을 제공 될 수 있습니다 *DataAnnotations* 특성 또는 fluent Api를 사용 합니다.

코드 Firstwith ASP.NET MVC를 사용 하 여에 대 한 설명서는 다음 Url에서 ASP.NET 웹 사이트에서 사용할 수 있습니다.

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>프로젝트 템플릿에 JavaScript 라이브러리를 사전 설치 된 NuGet 패키지로 포함

프로젝트에 설치 하 여 앞에서 언급 한 JavaScript 파일 (예: Modernizr 라이브러리)을 포함 하는 새 ASP.NET MVC 3 프로젝트를 만들면 직접 프로젝트 템플릿에 있는 스크립트 폴더에 스크립트를 추가 하는 대신 NuGet을 사용 하 여 내용입니다. 따라서 NuGet을 사용 하 여 스크립트의 새 버전이 릴리스되면 최신 버전으로 스크립트를 업데이트할 수 있습니다.

예를 들어 새 jQuery 릴리스 빈도가 제공 프로젝트 템플릿에 포함 된 jQuery 버전은 특정 시점에 됩니다 만료. 그러나 jQuery가 설치 된 NuGet 패키지로 포함 하기 때문에 알려 NuGet 대화 상자에서 최신 버전의 jQuery 사용할 수 없는 경우.

JQuery 파일 이름에 버전 번호를 포함 하므로 jQuery를 최신 버전으로 업데이트 하려면 업데이트 해야는 `<script>` 새 파일 이름을 사용 하기 위해 jQuery 파일을 참조 하는 태그입니다. 다른 포함된 스크립트 라이브러리 스크립트 이름을 할 버전 번호를 포함 하지 않으므로 최신 버전으로 더 쉽게 업데이트할 수 있습니다.

<a id="tu-KI"></a>
## <a name="known-issues"></a>알려진 문제

- 일부 경우에는 오류 메시지 "설치 실패 오류 코드 (0x80070643)"으로 설치가 실패할 수 있습니다. 이 문제를 해결 하는 방법에 대 한 정보를 참조 하십시오. [기술 자료 문서 2531566](https://support.microsoft.com/kb/2531566)합니다.
- 컨트롤러 추가 대 한 스 캐 폴딩 Entity Framework에서 엔터티 상속 지원 기능을 활용 하는 엔터티 스 캐 폴딩 하지 않습니다. 예를 들어 기본 제공 *사람* 클래스에 상속 되는 *학생* 클래스를 스 캐 폴딩는 *학생* 클래스 컴파일되지 않습니다. 생성 된 코드에서 발생 합니다.
- 원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.
- ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다. ReSharper가 설치 되어 ASP.NET MVC 3의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.
- 설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.
- Razor 뷰를 편집할 때 (.cshtml 또는. *vbhtml* 파일), 뷰. ASP.NET MVC 3 Razor 뷰의 코드 조각이 포함 되지 않습니다. ASP.NET MVC 용 코드 조각 aspxselecting 조각이 표시 됩니다.
- 여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다. Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM의 변경 내용

이 섹션에서는 RC2 릴리스 이후의 ASP.NET MVC 3 RTM 릴리스에서 만든 버그 수정 및 변경 내용을 설명 합니다.

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>변경 사항: 1.8.7 버전의 jQuery UI 업데이트

ASP.NET MVC 프로젝트 템플릿은 Visual Studio에 대 한 최신 버전의 jQuery UI 라이브러리를 포함 하도록 업데이트 되었습니다. 템플릿에 jQuery UI 관련된 CSS 및 이미지 파일과 같은 필요한 리소스 파일의 최소 집합도 포함 됩니다.

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>ModelMetadataProvider DataAnnotationsModelMetadataProvider로 다시 기본값을 변경 하는 변경 사항:

도입 된 ASP.NET MVC 3의 RC2 릴리스는 *CachedDataAnnotationsMetadataProvider* 는 제공 된 기존 위에 캐싱 클래스 *DataAnnotationsModelMetadataProvider* 으로 클래스는 성능이 향상 되었습니다. 그러나 몇 가지 버그 된 보고이 프로세스를 구현 하므로 변경 내용이 되돌릴 되었으며에서 제공 되는 MVC 미래 프로젝트로 이동할 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)합니다.

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>공백 결과 거꾸로를 포함 하는 Razor 식의 일부를 붙여 넣는 방법 문제가 해결 됨

ASP.NET MVC 3의 시험판 버전에서는 Razor 파일에 공백이 포함 된 Razor 식의 부분을 붙여 넣을 때 결과 식 속도가 반대로 바뀝니다. 예를 들어, 다음 Razor 코드 블록을 살펴보겠습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

첫 번째 방법은 "첫 번째 param" 텍스트를 선택 하 고 두 번째 방법에 대 한 인수로 붙여 경우 결과 다음과 같습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

정확한 동작은 붙여넣기 작업 다음에 발생 합니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

붙여넣기 작업 동안 식이 제대로 유지 되도록 RTM 릴리스에서이 문제가 해결 되었습니다.

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>구문 색 지정 및 IntelliSense 고정: 편집기에서 열려 있는 Razor 파일의 이름 바꾸기 해제

구문 강조 표시 및 IntelliSense 해당 파일에 대 한 작동을 중지 하면 편집기 창에서 파일이 열릴 때 솔루션 탐색기를 사용 하 여 Razor 파일의 이름을 변경 합니다. 이 강조 표시 되도록 고정 및 IntelliSense는 이름 바꾸기 후 유지 됩니다.

<a id="RTM-KI"></a>
## <a name="known-issues"></a>알려진 문제

- NuGet 패키지 관리자 콘솔이 열려 있는 동안 Visual Studio 2010 SP1 베타를 닫으면 Visual Studio가 충돌 하 고 다시 시작 하려고 합니다. 이 문제가 해결 RTM 버전의 Visual Studio 2010 s p 1입니다.
- ASP.NET MVC 3 설치 프로그램은 초기 버전의 NuGet 패키지 관리자를 설치할 수만 있습니다. 초기 버전을 설치한 후 NuGet을 설치할 수 있고 Visual Studio 확장 관리자를 사용 하 여 업데이트 합니다. NuGet이 설치를 이미 있는 경우 NuGet의 최신 버전으로 업데이트 하려면 Visual Studio 확장 갤러리로 이동 합니다.
- 원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.
- 설치 관리자는 이전 버전의 ASP.NET MVC를 완료 하려면 보다 훨씬 더 오래 걸릴 수 있습니다. Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.
- ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다. ReSharper가 설치 되어 ASP.NET MVC 3의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.
- ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CCSHTML 및 VBHTML 뷰 빌드 작업이 제대로 설정 하지 않은, 이러한 보기에서 결과로 형식 프로젝트를 게시할 때 생략 됩니다. 이러한 파일에 대 한 빌드 작업 값 "콘텐츠"를 설정 해야 합니다. ASP.NET MVC 3 RTM 새 파일에 대해이 문제를 해결할 수 있지만 시험판 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.
- ![](mvc3-release-notes/_static/image3.png)
- 설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.
- Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.
- 여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다. Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>주요 변경 사항

- 이전 버전의 ASP.NET MVC에서는 작업 필터는 몇 가지 경우에서를 제외 하 고 요청에 따라 만듭니다. 이 동작은 되지 보장 된 동작은 하지만 단순히 구현 정보 이며 필터에 대 한 계약 상태 비저장 고려 합니다. ASP.NET MVC 3에서 필터는 보다 적극적으로 캐시 됩니다. 따라서 잘못 인스턴스 상태를 저장 하는 모든 사용자 지정 작업 필터는 손상 될 수 있습니다.
- 동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다. 예외 필터 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 값의 동작 메서드는 작업 메서드의 예외 필터 전에 실행 됩니다. 일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다. ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다. 이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.
- 라는 새 속성이 *FileExtensions* 에 추가 된는 *VirtualPathProviderViewEngine* 기본 클래스입니다. ASP.NET에서는 보기를 경로 의해 (이름)가 아니라을 때 뷰만이 새 속성으로 지정 된 목록에 포함 된 파일 확장명으로 간주 됩니다. 웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 사용자 지정 빌드 공급자가 등록 된와 공급자는 이름이 아니라 전체 경로 사용 하 여 이러한 뷰를 참조 하는 경우 응용 프로그램의 주요 변경 내용입니다. 해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.
- 직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현을 *IControllerFactory* 인터페이스의 새 구현을 제공 해야 *GetControllerSessionBehavior* 했던 메서드 이 릴리스에서 인터페이스에 추가 합니다. 일반적으로 것이 좋습니다 수행 하지이 인터페이스를 직접 구현 하는 대신에서 클래스를 파생 *DefaultControllerFactory*합니다.

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 r c 2의 변경 내용

이 섹션에서는 변경 (새로운 기능 및 버그 수정) RC 릴리스 이후의 ASP.NET MVC 3 RC2 릴리스에서 내용을 설명 합니다.

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>프로젝트 템플릿이 1.4.4 jQuery, jQuery 유효성 검사 1.7 및 jQuery UI 1.8.6 포함 하도록 변경

ASP.NET MVC 3 용 프로젝트 템플릿을 포함 최신 버전의 jQuery, jQuery 유효성 검사 및 jQuery UI입니다. jQuery UI 프로젝트 템플릿을 새로 추가 하 고 유용한 사용자 인터페이스 도구를 제공 합니다. JQuery UI에 대 한 자세한 내용은 참조의 홈 페이지: [http://jqueryui.com/](http://jqueryui.com/)합니다.

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>추가 된 "AdditionalMetadataAttribute" 클래스

사용할 수는 *AdditionalMetadataAttribute* 를 채우는 클래스는 *ModelMetadata.AdditionalValues* 모델 속성에 대 한 사전입니다.

예를 들어 뷰 모델에만 관리자에 게 표시 되어야 하는 속성이 있습니다. 해당 모델 키와 true로 AdminOnly를 사용 하 여 다음 예제와 같이 값으로 새 특성으로 주석을 지정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

이 메타 데이터를 사용할 수 있는 표시 또는 편집기 템플릿을 제품 보기 모델을 렌더링 하는 경우. 이 프로토콜은 사용자의 책임으로 응용 프로그램 개발자가 메타 데이터 정보를 해석 합니다.

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>향상 된 보기 스 캐 폴딩

뷰에 사용 되는 스 캐 폴딩 이제 T4 템플릿 템플릿 도우미 메서드를 호출을와 같은 생성 *EditorFor* 와 같은 도우미 대신 *TextBoxFor*합니다. 이 변경 개선 뷰 추가 대화 상자는 뷰를 생성할 때 데이터 주석 특성의 형태로 모델에 대 한 메타 데이터에 대 한 지원이 됩니다.

뷰 추가 스 캐 폴딩 규칙에 따라 모델에 기본 키 정보의 사용 및 향상 된 검색에도 포함 됩니다. 예를 들어 뷰 추가 대화 상자는이 정보를 사용 하 여는 기본 키 값은 하지 스 캐 폴드 된 편집 가능한 폼 필드와 되도록 합니다.

기본 편집 및 템플릿 만들기 클라이언트 유효성 검사에 필요한 jQuery 스크립트에 대 한 참조를 포함 합니다.

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>추가 된 Html.Raw 메서드

기본적으로 Razor 모든 값을 HTML로 인코딩하고 엔진을 봅니다. 와 페이지에 표시 되도록 다음 코드 조각의 인사말 변수 내부 HTML를 인코딩하는 예를 들어 `<strong>Hello World!</strong>`합니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

새 *Html.Raw* 메서드 콘텐츠가 안전한 것으로 알려져 있는 경우 인코딩되지 않은 HTML을 표시 하는 간단한 방법을 제공 합니다. 다음 예제에서는 동일한 문자열을 표시 하지만 문자열 태그로 렌더링 됩니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>이름이 바뀐된 "Controller.ViewModel" 속성과 "ViewBag"을 "보기" 속성

이전에 *ViewModel* 속성 *컨트롤러* 에 상응는 *보기* 보기의 속성입니다. 액세스 값의 하는 방법을 제공 두이 속성 모두는 *ViewDataDictionary* 동적 속성 접근자 구문을 사용 하 여 개체입니다. 두 속성이 동일 하 게 혼동을 피하기 위해와 보다 일치 하도록 변경 되었습니다.

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>이름이 바뀐된 "ControllerSessionStateAttribute" 클래스 "SessionStateAttribute"를

*ControllerSessionStateAttribute* 클래스는 ASP.NET MVC 3의 RC 버전에서 도입 되었습니다. 더 간결한 되도록 속성 이름이 변경 되었습니다.

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>이름이 바뀐된 RemoteAttribute "Fields" 속성을 "AdditionalFields"

*RemoteAttribute* 클래스의 *필드* 속성 사용자 간에 일부 혼란이 발생 합니다. 이 속성을 이름 바꾸기 *AdditionalFields* 의도 된을 명확히 보여 줍니다.

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>"AllowHtmlAttribute"를 "SkipRequestValidationAttribute" 이름이 변경

*SkipRequestValidationAttribute* 특성으로 변경 되어 *AllowHtmlAttribute* 해당 용도 더 잘 나타내기 위해.

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>첫 번째 유용한 오류 메시지를 표시 하려면 변경 된 "Html.ValidationMessage" 메서드

*Html.ValidationMessage* 메서드는 단순히 첫 번째 오류를 표시 하는 대신 첫 번째 유용한 오류 메시지를 표시 하도록 수정 되었습니다.

모델 바인딩 중에서 *ModelState* 사전 모델 자체를 포함 하는 속성에 대 한 오류 메시지와 함께 여러 소스에서 채울 수 있습니다 (구현 하는 경우 *IValidatableObject* )를 속성에 적용 되는 유효성 검사 특성 및 속성을 액세스 하는 동안 발생 한 예외입니다.

경우는 *Html.ValidationMessage* 유효성 검사 메시지를 표시 하는 메서드, 아니기 때문에이 일반적으로 최종 사용자에 대 한 예외를 포함 하는 모델 상태 항목을 건너뜁니다. 대신, 메서드는 예외와 연결 되지 않으며 해당 메시지를 표시 하는 첫 번째 유효성 검사 메시지를 찾습니다. 이러한 메시지가 없는 항목이 있으면 첫 번째 예외와 관련 된 일반 오류 메시지에 기본값입니다.

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>고정 @model 문서에 공백을 추가 하지 않는 선언

이전 릴리스에서  *@model*  보기의 맨 위에 선언은 렌더링된 된 HTML 출력에 빈 줄을 추가 합니다. 이 선언에 공백이 발생 하지 않도록 있도록 수정 되었습니다.

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>엔진-특정 파일 이름을 지원 하도록 뷰 엔진에 추가 된 "FileExtensions" 속성

뷰 엔진 다음 예제와 같이 명시적 뷰 경로 사용 하는 보기를 반환할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

뷰를 렌더링 하는 첫 번째 뷰 엔진이 항상 시도 합니다. 기본적으로 Web Forms 뷰 엔진은 첫 번째 뷰 엔진입니다. Web Forms 엔진 Razor 뷰를 렌더링할 수 없으면 때문에 오류가 발생 합니다. 뷰 엔진 생깁니다는 *FileExtensions* 지 원하는 파일 확장명을 지정 하는 데 사용 되는 속성입니다. ASP.NET 뷰 엔진 파일을 렌더링할 수 있는지 여부를 결정 하는 경우이 속성을 검사 합니다. 이 주요 변경 내용 및에 포함 된 자세한 세부 정보는 [주요 변경 내용](#_Toc2_BC) 이 문서의 섹션.

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>"For" 특성에 대 한 올바른 값을 내보내는 데 고정된 "LabelFor" 도우미

버그 수정 위치는 *LabelFor* 렌더링 하는 메서드는 *에 대 한* 일치 하는 특성의 *입력* 요소의 *이름* 특성을 대신 ID W3C에 따라는 *에 대 한* 특성이 일치 해야는 *입력* 요소의 id입니다.

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>모델 바인딩 중 명시적 값 우선 순위 RenderAction"고정된" 메서드

이전 버전에서는에 전달 된 명시적 값은 *RenderAction* 메서드는 자식 작업 내 모델 바인딩 중 현재 폼 값 무시 되 고 되었습니다. 수정이 반영 명시적 값 모델 바인딩 중 우선 있는지 확인 합니다.

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>주요 변경 사항

- 이전 버전의 ASP.NET MVC에서는 작업 필터 몇 가지 경우에서를 제외 하 고 요청에 따라 만들어졌습니다. 이 동작은 되지 보장 된 동작은 하지만 단순히 구현 정보 이며 필터에 대 한 계약 상태 비저장 고려 합니다. ASP.NET MVC 3에서 필터는 보다 적극적으로 캐시 됩니다. 따라서 잘못 인스턴스 상태를 저장 하는 모든 사용자 지정 작업 필터는 손상 될 수 있습니다.
- 동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다. 예외 필터를 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 는 작업 메서드의 예외 필터 전에 실행의 동작 메서드 같이 합니다. 일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다. ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다. 이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.
- 라는 새 속성이 *FileExtensions* 에 추가 된는 *VirtualPathProviderViewEngine* 기본 클래스입니다. ASP.NET에서는 보기를 경로 의해 (이름)가 아니라을 때 뷰만이 새 속성으로 지정 된 목록에 포함 된 파일 확장명으로 간주 됩니다. 웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 사용자 지정 빌드 공급자가 등록 된와 공급자는 이름이 아니라 전체 경로 사용 하 여 이러한 뷰를 참조 하는 경우 응용 프로그램의 주요 변경 내용입니다. 해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.
- 직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현을 *IControllerFactory* 인터페이스의 새 구현을 제공 해야 *GetControllerSessionBehavior * *에 추가 된 메서드는 이 릴리스에서 인터페이스*합니다. 일반적으로 것이 좋습니다 수행 하지이 인터페이스를 직접 구현 하는 대신에서 클래스를 파생 *DefaultControllerFactory*합니다.

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>알려진 문제

- ASP.NET MVC 3 설치 프로그램은 초기 버전의 NuGet 패키지 관리자를 설치할 수만 있습니다. 초기 버전을 설치한 후 NuGet을 설치할 수 있고 Visual Studio 확장 관리자를 사용 하 여 업데이트 합니다. NuGet이 설치를 이미 있는 경우 NuGet의 최신 버전으로 업데이트 하려면 Visual Studio 확장 갤러리로 이동 합니다.
- 원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.
- 설치 관리자는 이전 버전의 ASP.NET MVC를 완료 하려면 보다 훨씬 더 오래 걸릴 수 있습니다. Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.
- ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다. ReSharper가 설치 되어 ASP.NET MVC 3 r c 2의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.
- ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CSHTML 및 VBHTML 뷰 빌드 작업이 제대로 설정 하지 않은, 이러한 보기에서 결과로 형식 프로젝트를 게시할 때 생략 됩니다. *빌드 작업* 콘텐츠를 설정 해야 이러한 파일에 대 한 값 "입니다. ASP.NET MVC 3 RC2 새 파일에 대해이 문제를 해결할 수 있지만 베타 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.![](mvc3-release-notes/_static/image4.png)
- 설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.
- Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.
- 여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다. Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.
- ASP.NET MVC 3 RC 2를 설치 합니다. 이미 설치 되어 있는 경우 NuGet을 업데이트 하지 않습니다. NuGet을 업그레이드 하는 Visual Studio 확장 관리자으로 이동 하세요.으로 표시 되어야 사용 가능한 업데이트가 있습니다. NuGet에서에서 최신 버전으로 업그레이드할 수 있습니다.

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 릴리스 후보

ASP.NET MVC 릴리스 후보는 2010 년 11 월 9 일에 출시 되었습니다.

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC의 새로운 기능

이 섹션에 도입 된 기능에 설명에서 베타 릴리스 이후의 ASP.NET MVC 3 RC 릴리스 합니다.

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet 패키지 관리자

ASP.NET MVC 3에는 NuGet 패키지 관리자 (이전의 NuPack)는 Visual Studio 프로젝트에 라이브러리와 도구를 추가 하기 위한 통합된 패키지 관리 도구에 포함 됩니다. 이 도구는 개발자가 해당 원본 트리로 라이브러리를 지금 수행 하는 단계를 자동화 합니다.

NuGet 명령줄 도구, Visual Studio 상황에 맞는 메뉴에서 Visual Studio 2010 내는 통합된 콘솔 창 및 PowerShell cmdlet 집합으로 작업할 수 있습니다.

NuGet에 대 한 자세한 내용은 참조는 [Nuget 설명서](https://docs.microsoft.com/nuget/)합니다.

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>향상 "새 프로젝트" 대화 상자

새 프로젝트를 만들 때 새 프로젝트 대화 상자 이제 수 있습니다는 뷰 엔진이 뿐만 아니라 ASP.NET MVC 프로젝트 형식을 지정 합니다.

![](mvc3-release-notes/_static/image5.png)

이 릴리스에서 템플릿과 보기 대화 상자에 나열 된 엔진의 목록을 수정에 대 한 지원이 포함 되어 있습니다.

기본 템플릿에 다음과 같습니다.

빈 합니다. ASP.NET MVC 스타일, 기본 및 기본 JavaScript 파일을 포함 하는 스크립트 디렉터리를 포함 하는 Site.css 파일 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 파일의 최소 집합을 포함 합니다.

인터넷 응용 프로그램입니다. ASP.NET MVC와 함께 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.

대화 상자에 표시 되는 프로젝트 템플릿 목록에서 Windows 레지스트리가에 지정 됩니다.

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>Sessionless 컨트롤러

새 *ControllerSessionStateAttribute* 더 제어할 세션 상태 동작을 통해 컨트롤러에 대 한 지정 하 여 한 [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) 열거형 값입니다.

다음 예제에는 컨트롤러에 대 한 모든 요청에 대 한 세션 상태를 해제 하는 방법을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

다음 예제에서는 컨트롤러에 대 한 모든 요청에 대 한 읽기 전용 세션 상태를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>새 유효성 검사 특성

#### <a name="compareattribute"></a>CompareAttribute

새 *CompareAttribute* 유효성 검사 특성을 사용 하면 모델의 두 가지 다른 속성의 값을 비교 합니다. 다음 예제에서는 *ComparePassword* 속성 일치 해야 합니다는 *암호* 필드 유효화 됩니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

새 *RemoteAttribute* 유효성 검사 특성에서는 클라이언트 쪽 유효성 검사 메서드를 호출 하는 실제 유효성 검사 논리를 수행 하는 서버에 매핑함으로써 jQuery 유효성 검사 플러그 인의 원격 검사기 활용 합니다.

다음 예제에서는 *UserName* 속성에는 *RemoteAttribute* 적용 합니다. 클라이언트 유효성 검사는 작업을 호출 합니다 편집 보기에서이 속성을 편집할 때 *UserNameAvailable* 에 *UsersController* 이 필드의 유효성을 검사 하기 위해 클래스입니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

다음 예제에서는 해당 컨트롤러를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

기본적으로 특성에 적용 되는 속성 이름 쿼리 문자열 매개 변수로 작업 메서드에 전송 됩니다.

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드

에 대 한 추가 된 새 오버 로드는 *LabelFor* 및 *LabelForModel* 레이블 텍스트를 지정할 수 있는 메서드. 다음 예제에서는 이러한 오버 로드를 사용 하는 방법을 보여 줍니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>자식 동작 출력 캐싱

*OutputCacheAttribute* 자식 작업을 사용 하 여 호출의 출력 캐싱을 지원는 *Html.RenderAction* 또는 *Html.Action* 도우미 메서드. 다음 예제에서는 다른 작업을 호출 하는 뷰를 보여 줍니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate* 동작으로 주석이 추가 된 *OutputCacheAttribute*:

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

이 코드를 실행 하는 경우 Html.Action("GetDate")에 대 한 호출의 결과 100 초 동안 캐시 됩니다.

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>"뷰 추가" 대화 상자 개선 사항

강력한 형식의 뷰를 추가 하면 보기 추가 대화 상자를 이제 많은 코어.NET Framework 형식과 같은 이전 릴리스에서 보다 더 많은 적용 되지 형식을 필터링 합니다. 또한 목록 클래스 이름으로 더욱 쉽게 형식을 찾을 정규화 된 형식 이름으로 정렬 됩니다. 예를 들어 유형 이름 다음 예제와 같이 이제 표시 됩니다.

응용 프로그램 이름 (네임 스페이스)

이전 릴리스에서이 되어 표시 된 다음과 같이 합니다.

Namespace.ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>Granular Request Validation

*제외* 속성 *ValidateInputAttribute* 더 이상 없습니다. 대신, 모델 바인딩 중에 모델의 특정 속성에 대 한 생략 요청 유효성 검사를 사용 하 여 새 *SkipRequestValidationAttribute*합니다.

예를 들어 동작 메서드가 블로그 게시물을 편집 하는 데는 있다고 가정 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

다음 예제는 블로그 게시물에 대 한 뷰 모델을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

사용자가 Description 속성에 대 한 일부 태그, 모델 바인딩 요청 유효성 검사로 인해 실패 합니다. 블로그 게시물 설명에 대 한 모델 바인딩 중 요청 유효성 검사를 사용 하지 않으려면 적용 된 *SkipRequpestValidationAttribute* 이 예제에 나와 있는 것 처럼 속성에: 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

모델의 모든 속성에 대 한 요청 유효성 검사를 해제 하려면 적용 해도 *ValidateInputAttribute* 값 *false* 동작 메서드에:

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>주요 변경 사항

- 동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다. 예외 필터를 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 는 작업 메서드의 예외 필터 전에 실행의 동작 메서드 같이 합니다. 일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다. ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다. 이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.
- 라는 새 속성이 추가 *FileExtensions* 에 *VirtualPathProviderViewEngine* 기본 클래스입니다. 조회할 때 뷰 경로 의해 (및 이름으로)에 포함 된 파일 확장명을 가진 뷰만이 새 속성으로 지정 된 목록으로 간주 됩니다. 웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 공급자를 빌드하는 사용자 지정 등록 사용자에 게 이것은 주요 변경 내용 및 보기는 이름이 아니라 전체 경로 사용 하 여 참조 해 합니다. 해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>알려진 문제

- 설치 관리자는 이전 버전의 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 완료 하려면 ASP.NET MVC 보다 훨씬 더 오래 걸릴 수 있습니다.
- 뷰 추가 폴딩을 astrongly를 선택 하는 경우 스 캐 폴드 쓰기 전용 속성 보기를 입력 합니다. 이러한 항상에서 무시할 스 캐 폴딩 합니다. 뷰 추가 대화 상자도 스 캐 폴드 읽기 전용 속성 "Edit" 또는 "만들기" 보기를 생성 하는 경우. 읽기 전용 속성 표시 및 목록 보기에 대 한 스 캐 폴드 수만 해야 합니다.
- 디버깅 ASP.NET MVC 3 비동기 CTP와 함께 설치 된 경우 작동 하지 않습니다. ASP.NET MVC 3 비동기 CTP와 함께 설치할된 수 없습니다. 디버깅을 복구 하려면 비동기 CTP를 제거 합니다. 자세한 내용은 읽기 [이 블로그 게시물](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) ASP.NET MVC 3 RC의 모든 조각을 제거에 대 한 합니다.
- Resharper가 설치 된 경우에 razor Intellisense 작동 하지 않습니다. ReSharper가 설치 되어 읽으십시오 ASP.NET MVC 3 RC의 Razor intellisense 지원을 활용 하려고 하는 경우 [이 블로그 게시물](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) 에서 JetBrains를 함께 사용 하는 방법을 설명 합니다.
- ASP.NET MVC 3 베타를 사용 하 여 만든 CSHTML 및 VBHTML 뷰 없는 빌드 작업이 제대로 게시에서이 생략 하 합니다. *빌드 작업* 에 이러한 파일을 "콘텐츠"로 설정 해야 합니다. ASP.NET MVC 3 RC의 새로운 파일을이 문제를 해결할 수 있지만 베타 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.
- 설치 관리자는 이전 버전의 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 완료 하려면 ASP.NET MVC 보다 훨씬 더 오래 걸릴 수 있습니다.
- 뷰 추가 폴딩을 보기 스 캐 폴드 입력 강력한 "Edit"를 선택 했을 때 읽기 전용 속성입니다. 마찬가지로, 쓰기 전용 속성은 "" 보기에 대 한 스 캐 폴드 됩니다.
- 설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.
- ASP.NET MVC 3 도구 설치의 일부분으로 포함 된 Razor 릴리스로 충돌이 발생 Visual Studio 비동기 CTP를 설치 합니다. Visual Studio 비동기 CTP와 Razor 릴리스를 모두 동일한 컴퓨터에 설치 하려고 하지 마십시오 있는지 확인 합니다.
- Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 베타

ASP.NET MVC 3 베타는 2010 년 10 월 6 일에 출시 되었습니다. 다음 내용은 베타 릴리스 버전 관련 되어 있으며 업데이트 또는 위의 ASP.NET MVC 3 릴리스 후보 섹션에서 참조 하는 변경 사항이 적용 됩니다.

## <a id="0.1__Toc274034215"></a>새 Featuresin ASP.NET MVC 3 베타

<a id="0.1__Default_validation_system"></a>이 섹션에 도입 된 기능에 설명 ASP.NET MVC 3 베타 릴리스 버전에서 합니다.

### <a id="0.1__Toc274034216"></a>NuGet 패키지 관리자

ASP.NET MVC 3 추가 라이브러리는 통합된 패키지 관리 도구 및 Visual Studio 프로젝트에는 도구는 NuGet 패키지 관리자를 포함 합니다. 대부분의 경우 개발자가 해당 원본 트리로 라이브러리를 지금 수행 하는 단계를 자동화 합니다.

NuGet 명령줄 도구, Visual Studio 상황에 맞는 메뉴에서 Visual Studio 2010 내는 통합된 콘솔 창 및 PowerShell cmdlet 집합을 작업할 수 있습니다.

NuGet에 대 한 자세한 내용은 참조는 [NuGet 설명서](https://docs.microsoft.com/nuget/)합니다.

### <a id="0.1__Toc274034217"></a>향상 된 새 프로젝트 대화 상자

새 프로젝트를 만들 때 새 프로젝트 대화 상자 이제 수 있습니다는 뷰 엔진이 뿐만 아니라 ASP.NET MVC 프로젝트 형식을 지정 합니다.

![](mvc3-release-notes/_static/image6.png)

이 릴리스에서 템플릿과 보기 대화 상자에 나열 된 엔진의 목록을 수정에 대 한 지원이 포함 되지 않습니다.

기본 템플릿에 다음과 같습니다.

빈 합니다. ASP.NET MVC 스타일, 기본 및 기본 JavaScript 파일을 포함 하는 스크립트 디렉터리를 포함 하는 작은 Site.css 파일 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 파일의 최소 집합을 포함 합니다.

인터넷 응용 프로그램입니다. ASP.NET MVC 내에서 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.

### <a id="0.1__Toc274034218"></a>강력 하 게 지정 하는 간단한 방법은 입력 Razor 뷰 모델

강력한 형식의 Razor 뷰의 모델 유형을 지정 하는 방법은 new를 사용 하 여 간단해졌습니다 @model CSHTML 뷰에 대 한 지시문 및 @ModelType VBHTML 뷰에 대 한 지시문입니다. 이전 버전의 ASP.NET MVC에서는 Razor에 대 한 강력한 형식의 모델에는 이러한 방식으로 뷰를 지정 합니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

이 릴리스에서 다음 구문을 사용할 수 있습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>새 ASP.NET 웹 페이지에 대 한 도우미 메서드를 지원

새 ASP.NET 웹 페이지 기술을 뷰 및 컨트롤러에 일반적으로 사용 되는 기능을 추가 하는 데 도움이 되는 도우미 메서드 집합이 포함 되어 있습니다. ASP.NET MVC 3에서는 이러한 도우미 메서드를 컨트롤러와 뷰 내에서 사용할 수 (필요한 경우). 이러한 메서드는 System.Web.Helpers 어셈블리에 포함 되어 있습니다. 다음 표에서 몇 가지 ASP.NET 웹 페이지 도우미 메서드를 나열합니다.

| **Helper** | **설명** |
| --- | --- |
| 차트 | 보기 내에서 차트를 렌더링합니다. Chart.ToWebImage, Chart.Save, Chart.Write 등 메서드를 포함합니다. |
| 암호화 | 해시를 올바르게 만들려면 알고리즘을 사용 하 여 솔트된 및 해시 된 암호입니다. |
| WebGrid | 그리드로 개체 (일반적으로 데이터베이스의 데이터)의 컬렉션을 렌더링합니다. 페이징 및 정렬을 지원 합니다. |
| WebImage | 이미지를 렌더링합니다. |
| WebMail | 전자 메일 메시지를 보냅니다. |

도우미와 기본 구문을 나열 하는 빠른 참조 항목을 사용할 수는 다음 URL에서 ASP.NET Razor 구문 문서의 일부로:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>추가 종속성 주입 지원

현재 버전을 ASP.NET MVC 3 Preview 1 릴리스를 기반으로 구축 두 개의 새로운 서비스 및 4 개의 기존 서비스에 대 한 지원 추가 및 종속성 확인 및 공통 서비스 로케이터에 대 한 향상 된 지원 포함 됩니다.

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>세분화 된 컨트롤러 인스턴스화에 대 한 새로운 IControllerActivator 인터페이스

새 IControllerActivator 인터페이스는 종속성 주입을 통해 컨트롤러를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다. 다음 예제에서는 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

이와 반대로 컨트롤러 팩터리 역할을 합니다. 컨트롤러 팩터리는 해당 컨트롤러 형식의 인스턴스를 인스턴스화하고를 고 컨트롤러 종류를 찾기 위한 IControllerFactory 인터페이스의 구현입니다.

컨트롤러 활성기는 컨트롤러 형식의 인스턴스를 인스턴스화하고 담당 합니다. 컨트롤러 유형 조회를 수행 하지 않습니다. 찾은 후에 적절 한 컨트롤러 종류, 컨트롤러 팩터리 IControllerActivator 인스턴스에 컨트롤러의 실제 인스턴스에 처리를 위임 해야 합니다.

DefaultControllerFactory 클래스 IControllerFactory 인스턴스를 허용 하는 새 생성자를 있습니다. 이 기본 컨트롤러 형식 조회 동작을 재정의 하지 않고 컨트롤러 만들기의 이러한 측면을 관리 하는 종속성 주입을 적용할 수 있습니다.

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>IServiceLocator 인터페이스 되며 IDependencyResolver로 대체

커뮤니티 피드백에 따라 ASP.NET MVC 3 베타 릴리스 버전은 대체 IServiceLocator 인터페이스를 사용 하는 ASP.NET MVC의 요구에 맞게 맞춤화 되며 IDependencyResolver 인터페이스 합니다. 다음 예제에서는 새 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

또한이 변경의 일부로 ServiceLocator 클래스 DependencyResolver 클래스 대체 되었습니다. 종속성 확인자를 등록 하는 것은 이전 버전의 ASP.NET MVC 유사 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

이 인터페이스의 구현 하기만 하면 요청된 된 형식에 대 한 등록 된 서비스 제공 하기 위해 기본 종속성 주입 컨테이너를 위임 해야 합니다.

요청 된 형식의 등록 된 서비스 때 ASP.NET MVC에서는 GetService에서 null을 반환 하 고 GetServices에서 빈 컬렉션을 반환 하려면이 인터페이스의 구현 해야 합니다.

새 DependencyResolver 클래스를 사용 하면 새 되며 IDependencyResolver 인터페이스 또는 공통 서비스 로케이터 인터페이스 (IServiceLocator)를 구현 하는 클래스를 등록할 수 있습니다. 공통 서비스 로케이터에 대 한 자세한 내용은 참조 [GitHub에서 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)합니다.

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>세분화 된 뷰 페이지 인스턴스화에 대 한 새로운 IViewActivator 인터페이스

새 IViewPageActivator 인터페이스는 종속성 주입을 통해 페이지 보기를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다. 이 WebFormView 인스턴스와 RazorView 인스턴스 모두에 적용 됩니다. 다음 예제에서는 새 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

이러한 클래스는 이제 ViewPage, ViewUserControl, 및 WebViewPage 형식이 인스턴스화되고 방법을 제어 하려면 종속성 주입을 사용할 수 있는 IViewPageActivator 생성자 인수를 수락 합니다.

#### <a name="new-dependency-resolver-support-for-existing-services"></a>기존 서비스에 대 한 새 종속성 확인자 지원

새 릴리스는 다음과 같은 서비스에 대 한 종속성 확인 지원을 포함 됩니다.

- 모델 유효성 검사 공급자입니다. ModelValidatorProvider를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 클라이언트 및 서버 쪽 유효성 검사를 지 원하는 데 사용 합니다.
- 모델 메타 데이터 공급자입니다. ModelMetadataProvider를 구현 하는 단일 클래스를 종속성 확인자에 등록할 수 있으며 시스템에서이 파일 템플릿 및 유효성 검사 시스템에 대 한 메타 데이터를 제공 하 사용 합니다.
- 값 공급자입니다. ValueProviderFactory를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 컨트롤러에 의해 및 모델 바인딩 중에 사용 되는 값 공급자를 만드는 사용 합니다.
- 모델 바인더입니다. IModelBinderProvider를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 모델 바인딩 시스템에서 사용 하는 모델 바인더를 만드는 사용 합니다.

### <a id="0.1__Toc274034221"></a>비 가시적인 jQuery 기반 Ajax에 대 한 새로운 지원

ASP.NET MVC Ajax 도우미 메서드를 다음과 같은 포함 되어 있습니다.

- Ajax.ActionLink
- Ajax.RouteLink
- Ajax.BeginForm
- Ajax.BeginRouteForm

이러한 메서드는 JavaScript를 사용 하 여 전체 포스트백을 사용 하는 대신 서버에서 작업 메서드를 호출 합니다. 이 기능은 방식으로 비 가시적인 jQuery을 활용 하려면 업데이트 되었습니다. 영향을 주지 않고 내보내기 인라인 클라이언트 스크립트 하는 대신 이러한 도우미 메서드 동작에서에서 분리 태그를 사용 하 여 HTML5 특성을 생성 함으로써는 *데이터 ajax* 접두사입니다. 동작에서는 적절 한 JavaScript 파일을 참조 하 여 태그에 적용 됩니다. 다음 JavaScript 파일이 참조 되 고 있는지 확인 합니다.

- jquery-1.4.1.js
- jquery.unobtrusive.ajax.js

이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿이에서 Web.config 파일에서 기본적으로 설정 되어 있지만 기존 프로젝트에 기본적으로 비활성화 됩니다. 자세한 내용은 참조 [클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 응용 프로그램 수준 플래그를 추가](#0.1_AddedApplicationWideFlagsForClientValida) 이 문서의 뒷부분에 나오는 합니다.

### <a id="0.1__Toc274034222"></a>비 가시적인 jQuery 유효성 검사에 대 한 새로운 지원

기본적으로 ASP.NET MVC 3 베타 방식으로 비 가시적인 jQuery 유효성 검사 클라이언트 쪽 유효성 검사를 수행 하는 데 사용 됩니다. 비 가시적인 클라이언트 유효성 검사를 사용 하려면 보기 내에서 다음와 같은 호출을 확인 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

그러려면 ViewContext.UnobtrusiveJavaScriptEnabled 속성이 다음 호출 하 여 수행할 수 있는 true로 설정 됩니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

또한 다음 JavaScript 파일이 참조를 확인 합니다.

- jquery-1.4.1.js
- jquery.validate.js
- jquery.validate.unobtrusive.js

이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿이에서 Web.config 파일에서 기본적으로에서 사용 되지만 기존 프로젝트에 기본적으로 비활성화 됩니다. 자세한 내용은 참조 [클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그](#0.1_AddedApplicationWideFlagsForClientValida) 이 문서의 뒷부분에 나오는 합니다.

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그

클라이언트 유효성 검사 및 전체적으로 다음 예제와 같이 HtmlHelper 클래스의 정적 멤버를 사용 하 여 비간섭 JavaScript를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

기본적으로 비간섭 JavaScript를 사용 하는 기본 프로젝트 템플릿. 또한 다음 설정을 사용 하 여 응용 프로그램의 루트 Web.config 파일에서 이러한 기능을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

기본적으로 이러한 기능을 활성화할 수 있습니다, 때문에 새 오버 로드는 다음 예제에 나와 있는 것 처럼 기본 설정을 재정의할 수 있도록 하는 HtmlHelper 클래스에 도입 된:

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

이전 버전과 호환성을 위해 이러한 기능은 모두 기본적으로 비활성화 됩니다.

### <a id="0.1__Toc274034224"></a>뷰를 실행 하기 전에 실행 되는 코드에 대 한 새로운 지원

이제 라는 파일을 넣을 수 있습니다 \_viewstart.cshtml (또는 \_viewstart.vbhtml) Views 디렉터리의 코드를 해당 디렉터리와 하위 디렉터리에 있는 여러 뷰 간에 공유 되는 추가 합니다. 예를 들어에 다음 코드를 넣을 수 있습니다는 \_viewstart.cshtml 페이지 ~/Views 폴더에서:

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

Views 폴더 내의 모든 보기 및 모든 해당 하위 폴더를 재귀적으로 대 한 레이아웃 페이지를 설정 합니다. 경우 뷰 렌더링 되는 코드에는 \_코드 보기를 실행 하기 전에 viewstart.cshtml 파일을 실행 합니다. \_viewstart.cshtml 코드에 해당 폴더의 모든 뷰에 적용 됩니다.

기본적으로의 코드는 \_viewstart.cshtml 파일 하위 폴더에 보기에도 적용 됩니다. 그러나 개별 하위 폴더의 고유 버전을 포함할 수는 \_viewstart.cshtml 파일의 경우 로컬 버전이 우선 한다는 점에서;. 예를 들어 HomeController에 대 한 모든 뷰에 공통 되는 코드를 실행 하려면 배치는 \_viewstart.cshtml 파일 ~/Views/Home 폴더에 있습니다.

### <a id="0.1__Toc274034225"></a>VBHTML Razor 구문에 대 한 새로운 지원

이전 ASP.NET MVC 미리 보기에는 Razor 구문을 기반으로 C#을 사용 하 여 보기에 대 한 지원이 포함 되어 있습니다. 이러한 뷰는.cshtml 파일 확장명을 사용 합니다. Razor를 지원 하기 위해 진행 중인 작업의 일환으로, ASP.NET MVC 3 베타에서는.vbhtml 파일 확장명을 사용 하 여 Visual Basic의 경우에 Razor 구문 지원 합니다.

에 대 한 소개를 Visual Basic 구문의 VBHTML 페이지에서 사용 하는 다음 URL에서 자습서를 참조:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>ValidateInputAttribute 보다 세부적으로 제어

ASP.NET MVC에는 항상 들어오는 요청에 악의적인 입력 포함 되어 있지 않은지를 핵심 ASP.NET 요청 유효성 검사 인프라를 호출 하는 ValidateInputAttribute 클래스를 포함 됩니다. 입력된 유효성 검사는 기본적으로 사용 됩니다. 다음 예제와 같이 ValidateInputAttribute 특성을 사용 하 여 요청 유효성 검사를 비활성화 하는 것이 불가능:

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

그러나 많은 웹 응용 프로그램 할 나머지 필드 하지 않아야 하는 동안 HTML을 허용 해야 하는 개별 양식 필드. 이제 ValidateInputAttribute 클래스 요청 유효성 검사에 포함 되지 않아야 하는 필드 목록을 지정할 수 있습니다.

예를 들어 블로그 엔진을 개발 하는 경우 본문 및 요약 필드에 태그를 허용 하는 것이 좋습니다. 이러한 필드는 각각 속성 이름 ("Body" 및 "요약")에 해당 하는 name 특성이 있는 두 개의 입력된 요소에 의해 표현 될 수 있습니다. 요청을 사용 하지 않도록 설정 하려면 이러한 필드에 대 한 유효성 검사 (쉼표로 구분) 다음 예제와 같이 ValidateInput 클래스의 제외 속성에 이름 으로만 지정:

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>도우미 밑줄 하이픈에 대 한 변환 익명 개체를 사용 하 여 지정 된 HTML 특성 이름

도우미 메서드는 다음 예제 처럼 익명 개체를 사용 하 여 특성 이름/값 쌍을 지정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

ASP.NET에서 속성 이름에 대 한 하이픈을 사용할 수 없으므로이 접근 방식을 특성 이름에서 하이픈을 사용 하 여 사용 하지 않습니다. 그러나 하이픈은 사용자 지정 HTML5 특성;에 대 한 중요 한 예를 들어 HTML5 "데이터-" 접두사를 사용합니다.

같은 시간에 밑줄 html에서 특성 이름에 대 한 사용할 수 없지만 속성 이름 내에서 유효 합니다. 따라서 익명 개체를 사용 하 여 특성을 지정 하는 경우 및 특성 이름에 밑줄을 포함 하는 경우, 도우미 메서드는 하이픈을 밑줄을 변환 합니다. 예를 들어 다음 도우미 구문을 밑줄을 사용합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

앞의 예제 도우미를 실행할 때 다음 태그를 렌더링 합니다.

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>버그 수정

EditorFor 및 DisplayFor 템플릿 도우미에 대 한 기본 개체 템플릿을 이제 DisplayAttribute.Order 속성에 지정 된 순서 지정을 지원 합니다. (이전 버전에서는 순서 설정을 사용 하지 않았습니다.)

클라이언트 유효성 검사는 이제 유효성 검사 특성이 적용 하는 재정의 된 속성의 유효성 검사를 지원 합니다.

JsonValueProviderFactory은 이제 기본적으로 등록 됩니다.

## <a id="0.1__Toc274034229"></a>주요 변경 내용

예외 필터에 대 한 실행 순서 값이 동일한 예외 필터에 대 한 변경 되었습니다. ASP.NET MVC 2 및 이전 버전에서는 예외는 작업 메서드의 예외 필터 전에 실행 된 동작 메서드에 따라 동일한 순서를 가진 컨트롤러에서 필터링 합니다. 지정된 된 순서 값 없이 예외 필터가 적용 된 경우의 경우 일반적으로 것 수 있습니다. ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다. 이전 버전에서와 Order 속성을 명시적으로 지정 하는 경우 필터가 지정 된 순서로 실행 됩니다.

## <a id="0.1__Toc274034230"></a>알려진된 문제

설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.

Razor 뷰 구문 강조 표시 및 IntelliSense 지원이 필요는 없습니다. Visual Studio에서 Razor 구문에 대 한 지원을 이후 버전의 일부로 포함 된다는 것으로 예상 됩니다.

Razor 뷰 (CSHTML 파일)를 편집 하는 경우는 <a id="0.1__Toc224729061"> </a> <a id="0.1__Toc238051347"> </a> Visual Studio에서 메뉴 항목 이동에 컨트롤러를 사용할 수 없으며 되며 코드 조각이 없습니다.

사용 하는 경우는 @model 강력한 형식의 CSHTML 지정 하려면 다음 구문을 사용 보기, 형식에 대 한 언어별 바로 가기를 인식 되지 않습니다. 예를 들어 @model int 작동 하지 것입니다 되지만 @model Int32 작동 합니다. 이 버그에 대 한 해결 방법은 모델 유형을 지정 하는 경우 실제 형식 이름을 사용 하는 것입니다.

사용 하는 경우는 @model 강력한 형식의 CSHTML 뷰를 지정 하는 구문 (또는 @ModelType VBHTML 강력한 형식의 뷰를 지정 하려면), nullable 형식 및 배열 선언과 지원 되지 않습니다. 예를 들어 @model int? 지원 되지 않습니다. 대신를 사용 하 여 `@model Nullable<Int32>`합니다. 구문을 @model string 지원 되지 않습니다; 대신, `@model IList<string>`합니다.

ASP.NET MVC 2 프로젝트를 ASP.NET MVC 3으로 업그레이드 하는 경우에 다음 Web.config 파일의 appSettings 섹션을 추가 해야 합니다.

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

폼 인증을 항상 Web.config에 사용 되는 폼 인증 설정 무시 ~/Account/로그인에 인증 되지 않은 사용자를 리디렉션 시키는 알려진된 문제가 있습니다. 이를 해결 하려면 다음 응용 프로그램 설정을 추가 합니다.

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>  Disclaimer

© 2011 Microsoft Corporation. All rights reserved. 이 설명서는 제공 "로-됩니다." URL 및 기타 인터넷 웹 사이트 참조를 포함 한이 문서의 내용과 관점은 예 고 없이 변경 될 수 있습니다. 정보의 사용으로 발생하는 위험은 귀하의 책임입니다.

이 문서는 귀하에게 Microsoft 제품의 어떠한 지적 재산에 대한 법적 권리도 부여하지 않습니다. 귀하는 참조를 위해 내부적으로 이 문서를 복사하고 사용할 수 있습니다.
