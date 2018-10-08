---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: ASP.NET MVC-파트 1에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: a9a373a54458faa21199019a4adbe69c0b94cb60
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577348"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>ASP.NET MVC-파트 1에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.


이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery를 사용 하는 방법의 기본 사항을 설명 [UI datepicker 팝업 일정](http://plugins.jquery.com/project/datepicker) ASP.NET MVC 웹 응용 프로그램에서 합니다. 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용할 수 있습니다 (&quot;Visual Web Developer&quot;), Microsoft Visual Studio의 무료 버전 또는 이미 있는 경우에 Visual Studio 2010 SP1을 사용할 수 있습니다.

시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 소프트웨어를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Studio 2010 대신 Visual Web Developer를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.

이 자습서를 완료 했다고 가정 합니다 [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는 Asp.net 개발 친숙 하다는 것입니다. 이 자습서에서 완성된 된 프로젝트를 시작 합니다 [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다.

이 자습서에서 C# 코드를 보여 줍니다. 그러나 합니다 [시작 프로젝트](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) 완성 된 프로젝트는 Visual Basic에서 사용할 수 있습니다.

C# 및 Visual Basic 소스 코드를 사용 하 여 Visual Studio 프로젝트는 다음이 항목과 함께 사용할 수 있습니다: [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다.

### <a name="what-youll-build"></a>만들 내용

템플릿을 추가할 수 있습니다 (특히, 편집 및 템플릿 표시)에서 만든 간단한 영화 목록 응용 프로그램에는 [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다. 또한 추가 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력 날짜를 입력 하는 간편 하 게 합니다. 다음 스크린 샷에서 표시 jQuery UI datepicker 팝업 일정을 사용 하 여 수정 된 응용 프로그램을 보여 줍니다.

![완성 된 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>학습할 기술

학습할 다음과 같습니다.

- 특성을 사용 하는 방법을 합니다 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 표시 되는 데이터의 형식을 제어 하 여 편집 모드에 있을 때 네임 스페이스입니다.
- 템플릿을 만드는 방법 (편집 및 템플릿 표시) 데이터의 서식을 제어할 수 있습니다.
- 추가 하는 방법의 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 필드를 입력 하는 방법으로 합니다.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트에서 영화 목록 응용 프로그램에 아직 없는 경우 다운로드 합니다. [다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx? https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다. 그런 다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *MvcMovie.zip* 파일을 선택 **속성**합니다. 에 **MvcMovie.zip 속성** 대화 상자에서 **차단 해제**합니다. (사용 하려고 할 때 발생 하는 보안 경고를 방지 차단 해제 된 *.zip* 웹에서 다운로드 한 파일입니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

마우스 오른쪽 단추로 클릭 합니다 *MvcMovie.zip* 파일을 선택 **풀기** 파일 압축을 풀 합니다. Visual Studio 2010, Visual Web Developer에서 엽니다는 *MvcMovieCS\_TU.sln* 파일입니다.

**솔루션 탐색기**를 두 번 클릭 합니다 *Views\Shared\\_Layout.cshtml* 하 여 엽니다. 변경 된 `H1` 헤더 **MVC 동영상 앱** 에 **영화 jQuery**. CTRL + f5를 눌러 응용 프로그램을 실행 하 고 클릭 합니다 **홈** 탭을 사용 하는 `Index` 동영상 컨트롤러의 메서드에. 응용 프로그램을 사용해 선택 합니다 **편집** 링크와 **세부 정보** 영화 중 하나에 대 한 링크입니다. 인덱스를 편집 하 고 세부 정보 보기, 릴리스 날짜 및 가격 보기 좋게 서식이 지정:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

사용의 결과인 날짜 및 가격에 대 한 서식 지정 된 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성의 속성에는 `Movie` 클래스.

열기를 *Movie.cs* 파일을 주석으로 처리를 `DisplayFormat` 특성을 `ReleaseDate` 및 `Price` 속성. 결과 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

CTRL + f5 키를 눌러 다시 응용 프로그램을 실행 하 고 선택 합니다 **홈** 영화 목록을 보려면 탭 합니다. 이 이번 릴리스 날짜에 날짜 및 시간을 표시 및 가격 필드에는 더 이상 통화 기호를 표시 합니다. 변경을 `Movie` 클래스를 깔끔하게 서식이 정리 앞에서 본 내용을 취소 하지만 잠시 후 해결 해 보겠습니다 있습니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>DataAnnotations DataType 특성을 사용 하 여 데이터 형식을 지정 하려면

주석으로 바꿉니다 `DisplayFormat` 특성에 대 한는 `ReleaseDate` 속성을 합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하 여를 `Date` 열거형. 대체는 `DisplayFormat` 특성에 대 한는 `Price` 속성을 합니다 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 다시 사용 하 여이 시간을 `Currency` 열거형. 다음은 완성 된 코드의 모습입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

응용 프로그램을 실행합니다. 이제 릴리스 날짜 및 가격 속성은 형식이 올바르게 지정 (사용 하 여 적절 한 날짜 및 통화 형식). 합니다 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성 형식 메타 데이터 기본 제공 ASP.NET MVC에 대 한 템플릿을 제공 필드를 올바른 형식으로 렌더링 되도록 합니다. 사용 하 여는 `DataType` 특성은 사용 하는 것이 좋습니다는 `DisplayFormat` 특성 때문에 코드에서 원래의 `DataType` 특성 깔끔하고 국제화 등의 목적에 대 한 유연한 모델을 사용 하면 합니다.

다음 섹션에서 사용자 지정 템플릿을 날짜 필드를 표시 하는 방법을 배웁니다.

> [!div class="step-by-step"]
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
