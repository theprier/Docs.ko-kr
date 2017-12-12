---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: "ASP.NET MVC-1 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: 9320c8a2aadb3b3c5bd6cd90b59d8a72db384c0c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>ASP.NET MVC-1 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.


이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery를 사용 하는 방법의 기본 사항은 설명 [UI datepicker 팝업 일정](http://plugins.jquery.com/project/datepicker) ASP.NET MVC 웹 응용 프로그램에서 합니다. 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용할 수 있습니다 (&quot;Visual Web Developer&quot;), Microsoft Visual Studio의 무료 버전 또는 이미 있는 경우에 Visual Studio 2010 s p 1을 사용할 수 있습니다.

시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필요한 소프트웨어를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Studio 2010 대신 Visual Web Developer를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.

이 자습서를 마쳤습니다 가정는 [MVC 3으로 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는 ASP.NET MVC 개발 고쳐야 합니다. 이 자습서에서 완성 된 프로젝트로 시작는 [MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다.

이 자습서에서 C# 코드를 보여 줍니다. 그러나는 [시작 프로젝트](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) 및 완료 된 프로젝트를 Visual Basic에서 사용할 수 있습니다.

C# 및 Visual Basic 소스 코드를 Visual Studio 프로젝트는이 항목에 수반: [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다.

### <a name="what-youll-build"></a>만들 것인지

서식 파일을 추가 합니다 (특히, 편집 및 템플릿을 표시)에서 만든 단순 영화 목록 응용 프로그램에는 [MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다. 또한 추가 합니다는 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 일정 날짜를 입력 하는 간편 하 게 합니다. 다음 스크린샷에 표시 jQuery UI datepicker 팝업 일정으로 수정 된 응용 프로그램을 보여 줍니다.

![완성 된 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>기술을 알아봅니다

학습할 다음과 같습니다.

- 특성을 사용 하는 방법의 [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) 표시 되는 데이터의 형식을 제어 하 고 편집 모드에 있을 때 네임 스페이스입니다.
- 템플릿을 만드는 방법 (편집 및 템플릿을 표시) 데이터의 서식을 제어할 수 있습니다.
- 추가 하는 방법의 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 필드를 입력 하는 방법으로 합니다.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트에서 영화 목록 응용 프로그램을 아직 없는 경우 다운로드할: [다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다. 다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭는 *MvcMovie.zip* 파일을 선택 **속성**합니다. 에 **MvcMovie.zip 속성** 대화 상자에서 **차단 해제**합니다. (사용 하려고 할 때 발생 하는 보안 경고가 표시 되지 않도록 차단 해제는 *.zip* 웹에서 다운로드 한 파일입니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

마우스 오른쪽 단추로 클릭는 *MvcMovie.zip* 파일을 선택 **압축 풀기** 에 파일 압축을 풉니다. Visual Web Developer 또는 Visual Studio 2010에서 엽니다는 *MvcMovieCS\_TU.sln* 파일입니다.

**솔루션 탐색기**, 두 번 클릭은 *Views\Shared\\_Layout.cshtml* 엽니다. 변경 된 `H1` 헤더를 **MVC 만든 동영상 앱** 를 **영화 jQuery**합니다. CTRL + f 5를 눌러 응용 프로그램을 실행 하 고 클릭 하 고 **홈** 탭을 사용 하는 `Index` 영화 컨트롤러의 메서드. 응용 프로그램을 사용 하려면 선택은 **편집** 링크 및 **세부 정보** 동영상 중 하나에 대 한 링크입니다. 인덱스에서 값을 편집한 다음에 유의 하 고 세부 정보 보기, 릴리스 날짜 및 가격 원활 하 게 형식이 지정:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

사용 하 여 결과은 날짜 및 가격에 대 한 서식을 [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성의 속성에는 `Movie` 클래스입니다.

열기는 *Movie.cs* 파일을 주석으로 처리는 `DisplayFormat` 특성에 `ReleaseDate` 및 `Price` 속성입니다. 그 결과 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

다시 응용 프로그램을 실행 하 고 선택 하려면 CTRL + f 5는 **홈** 동영상 목록을 보려면 탭 합니다. 이 이번 릴리스 날짜에서 날짜 및 시간을 나타내고 price 필드의 통화 기호를 더 이상 표시 합니다. 변경 내용을 `Movie` 클래스 취소 했 듯이, 좋은 서식을 있지만 잠시 후에를 수정 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>DataAnnotations 데이터 형식 특성을 사용 하 여 데이터 형식을 지정 하려면

주석 처리를 대체 `DisplayFormat` 특성에 대 한는 `ReleaseDate` 속성을는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하 여는 `Date` 열거형입니다. 대체는 `DisplayFormat` 특성에 대 한는 `Price` 속성을는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성 다시 사용 하 여이 시간은 `Currency` 열거형입니다. 다음은 완성 된 코드의 모양을입니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

응용 프로그램을 실행합니다. 이제 릴리스 날짜 및 가격 속성은 형식이 잘못 (사용 하 여 적절 한 날짜 및 통화 형식). [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성 형식 메타 데이터를 제공 기본 제공 ASP.NET MVC에 대 한 서식 파일 필드를 올바른 형식으로 렌더링 되도록 합니다. 사용 하는 `DataType` 특성은 사용 하는 것이 좋습니다는 `DisplayFormat` 때문에 코드에서는 원래 특성의 `DataType` 깔끔하고 국제화 등의 목적에 대해 더 융통성이 특성 모델을 사용 합니다.

다음 섹션의 날짜 필드를 표시할 사용자 지정 서식 파일을 확인 하는 방법을 배웁니다.

>[!div class="step-by-step"]
[다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
