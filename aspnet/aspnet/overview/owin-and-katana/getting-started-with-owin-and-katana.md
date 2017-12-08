---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: "OWIN 및 Katana 시작 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/27/2013
ms.topic: article
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 8922aada723da9b149ec111902fcd883c8241dfb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-owin-and-katana"></a>OWIN 및 Katana 시작
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[.NET (OWIN)에 대 한 웹 인터페이스를 열고](http://owin.org/) .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. 응용 프로그램에서 웹 서버를 분리 하 여 OWIN 쉽게.NET 웹 개발에 대 한 미들웨어를 만들려고 합니다. 또한, OWIN 쉽게 다른 호스트 &#8212; 포트 웹 응용 프로그램에 예를 들어 Windows 서비스 또는 다른 프로세스에서 자체 호스트 합니다.

OWIN는 커뮤니티 소유 사양, 구현 되지 않습니다. Katana 프로젝트가 Microsoft에서 개발 된 오픈 소스 OWIN 구성 요소 집합이 있습니다. OWIN 프로그램과 Katana의 일반적인 개요를 참조 하십시오. [An 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다. 이 문서에서 시작 하는 코드를 바로 됩니다 I.

이 자습서에서는 [Visual Studio 2013 릴리스 후보](https://go.microsoft.com/fwlink/?LinkId=306566), 하지만 Visual Studio 2012를 사용할 수도 있습니다. 일부 단계는 아래 언급 있는 Visual Studio 2012 서로 다릅니다.

## <a name="host-owin-in-iis"></a>OWIN IIS에서 호스트

이 섹션에서는 IIS에서 OWIN 호스팅할 합니다. 이 옵션에는 유연성과 함께 IIS의 완성도 높은 기능 집합 OWIN 파이프라인의 작성 제공합니다. OWIN 응용 프로그램이이 옵션을 사용 하는 ASP.NET 요청 파이프라인에서 실행 됩니다.

먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다. (Visual Studio 2012에서 ASP.NET 빈 웹 응용 프로그램 프로젝트 형식을 사용 합니다.)

![](getting-started-with-owin-and-katana/_static/image1.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다.

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>NuGet 패키지 추가

다음으로 데 필요한 NuGet 패키지를 추가 합니다. **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>시작 클래스 추가

OWIN 시작 클래스 다음에 추가 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다. 에 **새 항목 추가** 대화 상자에서 **Owin 시작 클래스**합니다. 시작 클래스를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [OWIN 시작 클래스 검색](owin-startup-class-detection.md)합니다.

![](getting-started-with-owin-and-katana/_static/image4.png)

`Startup1.Configuration` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

이 코드를 수신 하는 함수로 구현 OWIN 파이프라인에 미들웨어의 간단한 조각 추가 **Microsoft.Owin.IOwinContext** 인스턴스. 서버에서 HTTP 요청을 받으면 OWIN 파이프라인 미들웨어를 호출 합니다. 미들웨어의 응답에 대 한 콘텐츠 형식을 설정 하 고 응답 본문을 씁니다.

> [!NOTE]
> OWIN 시작 클래스 템플릿을 Visual Studio 2013에서 ´ ù. Visual Studio 2012를 사용 하는 경우 라는 새 빈 클래스 추가 `Startup1`, 다음 코드에 붙여 넣습니다.


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>응용 프로그램 실행

F5 키를 눌러 디버깅을 시작 합니다. Visual Studio에 대 한 브라우저 창을 열립니다 `http://localhost:*port*/`합니다. 페이지는 다음과 같이 표시 됩니다.

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>콘솔 응용 프로그램에서 자체 호스트 OWIN

이 응용 프로그램에서 사용자 지정 프로세스의 자체 호스팅에 IIS 호스팅에서 변환 하는 것이 쉽습니다. IIS 호스팅을 사용 IIS 역할 모두에서 HTTP 서버와 프로세스 서버를 호스트 하 합니다. 자체 호스팅을 사용 응용 프로그램 프로세스에서 만들고 사용 하는 **HttpListener** 클래스는 HTTP 서버입니다.

Visual Studio에서 새 콘솔 응용 프로그램을 만듭니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.Owin.SelfHost -Pre`

추가 `Startup1` 이 자습서의 1 단계에서 프로젝트에 클래스입니다. 이 클래스를 수정할 필요가 없습니다.

응용 프로그램의 구현 `Main` 메서드를 다음과 같이 합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

서버를 수신 하기 시작 하는 콘솔 응용 프로그램을 실행 하면 `http://localhost:9000`합니다. 웹 브라우저에서이 주소로 이동 하는 경우에 "Hello world" 페이지가 표시 됩니다.

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>OWIN Diagnostics 추가

Microsoft.Owin.Diagnostics 패키지용 처리 되지 않은 예외를 catch 하는 HTML 페이지 오류 세부 정보를 표시 하는 미들웨어를 포함 합니다. 이 페이지 함수과 거의 동일한이 라고도 하는 ASP.NET 오류 페이지는 "[사망의 노란색 화면](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD). YSOD와 같은 개발 하는 동안 Katana 오류 페이지는 유용 하지만 프로덕션 모드에서 해제 하는 것이 좋습니다.

프로젝트에서 진단 패키지를 설치 하려면 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`install-package Microsoft.Owin.Diagnostics –Pre`

코드를 변경 하면 `Startup1.Configuration` 메서드를 다음과 같이 합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

이제 Visual Studio 예외에서 중단 하지 않는다는 되도록 디버깅 하지 않고 응용 프로그램을 실행 하려면 CTRL + f 5를 사용 합니다. 응용 프로그램 동일 하 게 작동 이전 처럼로 이동 될 때까지 `http://localhost/fail`, 이때 응용 프로그램에 예외를 throw 합니다. 오류 페이지 미들웨어 되는 예외를 catch 하 고 HTML 페이지 오류에 대 한 정보가 표시 됩니다. 스택, 쿼리 문자열, 쿠키, 요청 헤더 및 OWIN 환경 변수를 참조 하려면 해당 탭을 클릭 수 있습니다.

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>다음 단계

- [OWIN 시작 클래스 검색](owin-startup-class-detection.md)
- [OWIN 자체 호스트 하는 ASP.NET Web API를 사용 하 여](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [OWIN를 사용 하 여 자체 호스트 하는 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
