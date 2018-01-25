---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: "ASP.NET 오류 처리 | Microsoft Docs"
author: Erikre
description: "이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: c5ec43ac78be4a9452ebaa6495a6883506ac162f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-error-handling"></a>ASP.NET 오류 처리
====================
으로 [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 오류 처리 및 오류 로그를 포함 하도록 Wingtip Toys 샘플 응용 프로그램을 수정 합니다. 오류 처리를 사용 하면 응용 프로그램을 정상적으로 오류를 처리 하 고 그에 따라 오류 메시지를 표시 합니다. 오류 로깅을 사용 하면 발생 한 오류를 해결할 수 있습니다. 이 자습서에서는 이전 자습서 "URL 라우팅"를 바탕으로 하며 Wingtip Toys 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습 내용:

- 전역 오류 처리 응용 프로그램의 구성에 추가 하는 방법입니다.
- 오류 처리 응용 프로그램, 페이지 및 코드 수준에 추가 하는 방법.
- 나중에 검토할 수에 대 한 오류를 기록 하는 방법.
- 보안을 손상 하지 않은 오류 메시지를 표시 하는 방법.
- 오류 로깅 모듈 및 처리기 (ELMAH) 오류 로깅을 구현 하는 방법.

## <a name="overview"></a>개요

ASP.NET 응용 프로그램에 일관 된 방식으로 실행 하는 동안 발생 하는 오류를 처리할 수 있어야 합니다. ASP.NET 일관 된 방식으로 응용 프로그램에 오류를 알리는 방법을 제공 하는 공용 언어 런타임 (CLR)를 사용 합니다. 오류가 발생 하면 예외가 throw 됩니다. 예외에는 모든 오류, 조건 또는 응용 프로그램에서 발생 하는 예기치 않은 동작입니다.

.NET Framework에서 예외는 `System.Exception`에서 상속받은 개체입니다. 예외는 문제가 발생한 코드 영역에서 throw됩니다. 예외는 예외를 처리 하는 코드를 응용 프로그램을 제공 하는 위치로 호출 스택에서 전달 됩니다. 응용 프로그램 예외를 처리 하지 않는 브라우저는 오류 세부 정보를 표시 하려면 강제 합니다.

모범 사례로, 코드 수준에서 오류를 처리 하 `Try` / `Catch` / `Finally` 코드 내에서 블록입니다. 사용자 컨텍스트에서 발생 하는 문제를 해결할 수 있도록 이러한 블록을 삽입 하려고 합니다. 오류 처리 블록에서 오류가 발생 한 위치에서 너무 멀리 떨어져 경우에 문제를 해결 하는 데 필요한 정보를 제공 하는 것이 어려워집니다.

### <a name="exception-class"></a>Exception 클래스

예외 클래스는 예외 상속할 기본 클래스입니다. 와 같은 대부분 예외 개체는 Exception 클래스의 일부 파생된 클래스의 인스턴스는 `SystemException` 클래스는 `IndexOutOfRangeException` 클래스 또는 `ArgumentNullException` 클래스입니다. Exception 클래스에 속성을 같은 `StackTrace` 속성을는 `InnerException` 속성 및 `Message` 발생 한 오류에 대 한 특정 정보를 제공 하는 속성입니다.

### <a name="exception-inheritance-hierarchy"></a>예외 상속 계층

런타임 예외에서 파생의 기본 집합이 `SystemException` 런타임 예외가 발생할 때 throw 한 클래스입니다. 대부분의 클래스와 같은 예외 클래스에서 상속 되는 `IndexOutOfRangeException` 클래스 및 `ArgumentNullException` 클래스, 추가 멤버를 구현 하지 않습니다. 따라서 예외, 예외 이름 및 예외에 포함 된 정보의 계층 구조에는 예외에 대 한 가장 중요 한 정보를 찾을 수 있습니다.

### <a name="exception-handling-hierarchy"></a>예외 처리 계층

ASP.NET Web Forms 응용 프로그램에서 특정 처리 계층에 따라 예외를 처리할 수 있습니다. 예외는 다음 수준에서 처리 될 수 있습니다.

- 응용 프로그램 수준
- 페이지 수준
- 코드 수준

응용 프로그램에서 예외를 처리할 때 예외 클래스에서 상속 되는 예외에 대 한 추가 정보 검색 및 사용자에 게 표시 종종 수 있습니다. 응용 프로그램, 페이지 및 코드 수준, 외에도 HTTP 모듈 수준 및 IIS 사용자 지정 처리기를 사용 하 여 예외를 처리할 수 있습니다.

### <a name="application-level-error-handling"></a>응용 프로그램 수준 오류 처리

응용 프로그램의 구성을 수정 하거나 추가 하 여 응용 프로그램 수준에서 기본 오류를 처리할 수는 `Application_Error` 의 처리기는 *Global.asax* 응용 프로그램의 파일입니다.

추가 하 여 기본 오류 및 HTTP 오류를 처리할 수는 `customErrors` 섹션에 *Web.config* 파일입니다. `customErrors` 섹션에서는 사용자가 리디렉션됩니다 오류가 있을 때 기본 페이지를 지정할 수 있습니다. 또한 특정 상태 코드 오류에 대 한 개별 페이지를 지정할 수 있습니다.

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

반면 구성을 사용 하 여 다른 페이지로 사용자를 리디렉션할 때에 발생 한 오류의 세부 정보 필요가 없습니다.

그러나 코드를 추가 하 여 응용 프로그램에서 발생 하는 오류를 트래핑할 수는는 `Application_Error` 의 처리기는 *Global.asax* 파일입니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>페이지 수준 오류 이벤트 처리

더 이상 됩니다 아무 것도 페이지에서 한 페이지 수준 처리기 하지만 컨트롤의 인스턴스는 유지 되지 않는다는 없기 때문에 오류가 발생 한 경우 페이지에 사용자를 반환 합니다. 응용 프로그램의 사용자에 게 오류 세부 정보를 제공 하려면 구체적으로 페이지에 오류 세부 정보를 작성 해야 합니다.

일반적으로 유용한 정보를 표시할 수 있는 페이지에 사용자 또는 처리 되지 않은 오류를 기록 하는 페이지 수준 오류 처리기를 사용 합니다.

이 코드 예제에서는 ASP.NET 웹 페이지에서 오류 이벤트에 대 한 처리기를 보여 줍니다. 이 처리기 내에서 처리 되지 않는 모든 예외를 catch `try` / `catch` 페이지에 차단 합니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

오류를 처리 한 후 지워야 호출 하 여는 `ClearError` 서버 개체의 메서드 (`HttpServerUtility` 클래스), 그렇지 않으면 이전에 발생 한 오류가 나타납니다.

### <a name="code-level-error-handling"></a>수준 오류 처리 코드

Try catch 문의 try 블록 다음에 하나 구성 되거나 이상의 서로 다른 예외에 대 한 처리기를 지정 하는 절을 catch 합니다. 예외가 throw 되 면 공용 언어 런타임 (CLR)이 예외를 처리 하는 catch 문을 찾습니다. 현재 실행 중인 메서드는 catch 블록에 들어 있지 않으면 경우 CLR은 현재 메서드 및 호출 스택을 이런 식으로 호출 하는 메서드를 살펴봅니다. Catch 블록이 없는 경우 CLR 사용자에 게 처리 되지 않은 예외 메시지를 표시 및 프로그램의 실행을 중지 합니다.

다음 코드 예제에서는 사용 하는 일반적인 방법 `try` / `catch` / `finally` 오류 처리 합니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

Try 블록 위의 코드에서 발생 가능한 예외를 방지 하는 코드를 포함 합니다. 블록은 예외가 발생 하거나 블록은 성공적으로 완료 될 때까지 실행 됩니다. 경우는 `FileNotFoundException` 예외 또는 `IOException` 다른 페이지의 실행이 넘어갑니다 예외가 발생 합니다. 그런 다음에 포함 된 코드는 finally 블록이 실행 된 오류가 발생 여부.

## <a name="adding-error-logging-support"></a>오류 로깅 지원 추가

Wingtip Toys 샘플 응용 프로그램에 오류 처리를 추가 하기 전에 추가 하 여 오류 로깅 지원을 추가 합니다는 `ExceptionUtility` 클래스는 *논리* 폴더입니다. 응용 프로그램 오류를 처리할 때마다가를 수행 하 여 오류 세부 정보를 오류 로그 파일에 추가 됩니다.

1. 마우스 오른쪽 단추로 클릭는 *논리* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.   
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **코드** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **클래스**중간에서 나열 하 고 이름을 **ExceptionUtility.cs**합니다.
3. **추가**를 선택합니다. 새 클래스 파일이 표시 됩니다.
4. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

예외를 호출 하 여 예외 로그 파일에 쓸 있습니다 예외가 발생할 때의 `LogException` 메서드. 이 메서드는 두 개의 매개 변수, 예외 개체 및 예외의 원인에 대 한 세부 정보를 포함 하는 문자열을 사용 합니다. 예외 로그에 기록 됩니다는 *ErrorLog.txt* 파일에 *앱\_데이터* 폴더입니다.

### <a name="adding-an-error-page"></a>오류 페이지 추가

Wingtip Toys 예제 응용 프로그램에서는 한 페이지 오류를 표시 하려면 사용 됩니다. 오류 페이지는 사이트의 사용자에 게 보안 오류 메시지를 표시 하도록 설계 되었습니다. 그러나 사용자가 컴퓨터에서 로컬로 제공 하는 HTTP 요청을 만드는 코드 거주 하는 개발자, 오류 페이지에 추가 오류 세부 정보 표시 됩니다.

1. 프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택 **추가**  - &gt; **새 항목**.   
 **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 중간 목록에서 선택 **마스터 페이지가 있는 웹 폼**, 하 고 이름을 **ErrorPage.aspx**합니다.
3. **추가**를 클릭합니다.
4. 선택 된 *Site.Master* 마스터 페이지로 파일을 다음 선택 **확인**합니다.
5. 기존 태그를 다음 코드로 바꿉니다.   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 코드 숨김의 기존 코드를 바꿉니다 (*ErrorPage.aspx.cs*) 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

오류 페이지가 표시 되 면는 `Page_Load` 이벤트 처리기가 실행 됩니다. 에 `Page_Load` 처리기의 오류가 처리 먼저 되었음을 위치 결정 됩니다. 그런 다음의 마지막 발생 한 오류에 따라 사용자가 호출 된 `GetLastError` 서버 개체의 메서드. 예외가 더 이상 존재 하는 경우 일반적인 예외가 생성 됩니다. 그런 다음 HTTP 요청을 로컬에서 수행한, 모든 오류 세부 정보가 표시 됩니다. 이 경우 웹 응용 프로그램을 실행 하는 로컬 컴퓨터만 이러한 오류 세부 정보가 표시 됩니다. 오류 정보가 표시 된 후에 오류 로그 파일에 추가 되 고 오류 서버에서 지워집니다.

### <a name="displaying-unhandled-error-messages-for-the-application"></a>응용 프로그램에 대 한 처리 되지 않은 오류 메시지를 표시합니다.

추가 하 여 한 `customErrors` 섹션에 *Web.config* 파일을 신속 하 게 처리할 수는 응용 프로그램에서 발생 하는 간단한 오류입니다. 또한 404-파일을 찾을 수 등 해당 상태 코드 값에 기반 하 여 오류를 처리 하는 방법을 지정할 수 있습니다.

#### <a name="update-the-configuration"></a>구성 업데이트

추가 하 여 구성을 업데이트 한 `customErrors` 섹션에 *Web.config* 파일입니다.

1. **솔루션 탐색기**찾기 및 열기는 *Web.config* Wingtip Toys 샘플 응용 프로그램의 루트에 파일입니다.
2. 추가 `customErrors` 섹션에 *Web.config* 내에 파일이 `<system.web>` 다음과 같이 노드:   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. 저장 된 *Web.config* 파일입니다.

`customErrors` 섹션 "On"으로 설정 된 모드를 지정 합니다. 또한 지정 된 `defaultRedirect`, 응용 프로그램 페이지 오류가 발생할 때 탐색할를 지시 합니다. 또한 페이지를 찾지 못한 경우 404 오류를 처리 하는 방법을 지정 하는 특정 오류 요소를 추가 했습니다. 이 자습서의 뒷부분에 나오는 추가 오류 처리 응용 프로그램 수준에서 오류 세부 정보를 캡처합니다 추가 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

업데이트 된 경로 볼 수 있는 지금 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 브라우저가 열리고 표시는 *Default.aspx* 페이지.
2. 브라우저에 다음 URL을 입력 (사용 해야 **프로그램** 포트 번호):  
    `https://localhost:44300/NoPage.aspx`
3. 검토는 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-페이지 찾을 수 없습니다. 오류](aspnet-error-handling/_static/image1.png)

요청 하는 경우는 *NoPage.aspx* 존재 하지 않는 페이지 오류 페이지에는 표시 간단한 오류 메시지와 자세한 오류 정보 추가 세부 정보가 사용할 수 있는 경우. 그러나 원격 위치에서 존재 하지 않는 페이지를 요청한 경우 오류 페이지만를 표시 하면 오류 메시지가 빨간색으로 표시 합니다.

### <a name="including-an-exception-for-testing-purposes"></a>예외를 포함 하 여 테스트 용도로

발생 시 응용 프로그램이 어떻게 작동 하는지 확인 하려면, ASP.NET에서 오류 조건을 신중 하 게 만들 수 있습니다. Wingtip Toys 예제 응용 프로그램에서는 현상을 보려면 기본 페이지가 로드 될 때 한 테스트 예외를 throw 합니다.

1. 관련 코드를 열고는 *Default.aspx* Visual Studio에서 페이지입니다.   
 *Default.aspx.cs* 코드 숨김 페이지에 표시 됩니다.
2. 에 `Page_Load` 처리기 처리기는 다음과 같이 표시 되도록 코드를 추가 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

다양 한 다른 유형의 예외를 만드는 것 같습니다. 위의 코드에서 만드는 프로그램 `InvalidOperationException` 때는 *Default.aspx* 페이지가 로드 됩니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램에서 예외를 처리 하는 방법을 확인 하도록 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **CTRL + f 5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 InvalidOperationException을 throw합니다. 

    > [!NOTE] 
    > 
    > 눌러야 **CTRL + f 5** 소스를 보려면 오류 Visual Studio에서 코드를 중단 하지 않고 페이지를 표시할 수 있습니다.
2. 검토는 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-오류 페이지](aspnet-error-handling/_static/image2.png)

예외를 포착 오류 세부 정보에 보시는 `customError` 섹션은 *Web.config* 파일입니다.

### <a name="adding-application-level-error-handling"></a>응용 프로그램 수준 오류 처리를 추가합니다.

대신 사용 하 여 예외 트랩은 `customErrors` 섹션은 *Web.config* 파일, 응용 프로그램 수준에서 오류를 트래핑 하 고 오류 세부 정보를 검색할 수 있는 예외에 대 한 정보만 확보 합니다.

1. **솔루션 탐색기**찾기 및 열기는 *Global.asax.cs* 파일입니다.
2. 추가 **응용 프로그램\_오류** 처리기 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

응용 프로그램에서 오류가 발생 하는 경우는 `Application_Error` 처리기가 호출 됩니다. 이 처리기의 마지막 예외는 검색 및 검토 합니다. 예외 처리 되지 않았습니다. 예외는 내부 예외 세부 정보를 포함 하는 경우 (즉, `InnerException` null이 아닌), 응용 프로그램 실행을 이동 하면 오류 페이지가 예외 세부 정보가 표시 됩니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램 수준 예외를 처리 하 여 제공 된 추가 오류 세부 정보를 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **CTRL + f 5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.
2. 검토는 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-응용 프로그램 수준 오류](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>페이지 수준 오류 처리를 추가합니다.

에 추가할 수 있습니다 페이지 수준 오류 처리는 페이지 추가 사용 하 여는 `ErrorPage` 특성을 `@Page` 페이지의 하거나 추가 하 여 지시문는 `Page_Error` 페이지의 코드 숨김에 이벤트 처리기입니다. 이 섹션에서는 추가 됩니다 한 `Page_Error` 실행을 전송 하는 이벤트 처리기는 *ErrorPage.aspx* 페이지.

1. **솔루션 탐색기**찾기 및 열기는 *Default.aspx.cs* 파일입니다.
2. 추가 `Page_Error` 처리기 코드 숨김으로 나타나도록 따릅니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

페이지에서 오류가 발생할 때의 `Page_Error` 이벤트 처리기가 호출 됩니다. 이 처리기의 마지막 예외는 검색 및 검토 합니다. 경우는 `InvalidOperationException` 발생는 `Page_Error` 이벤트 처리기 실행 이동 오류 페이지에 예외 세부 정보가 표시 됩니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

업데이트 된 경로 볼 수 있는 지금 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **CTRL + f 5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.
2. 검토는 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![페이지 수준 오류-ASP.NET 오류 처리](aspnet-error-handling/_static/image4.png)
3. 브라우저 창을 닫습니다.

### <a name="removing-the-exception-used-for-testing"></a>테스트에 사용 되는 예외를 제거 합니다.

이 자습서의 앞부분에서 추가한 예외를 throw 하지 않고 작동 하는 데 통상 샘플 응용 프로그램 예외를 제거 합니다.

1. 관련 코드를 열고는 *Default.aspx* 페이지.
2. 에 `Page_Load` 처리기를 처리기 다음과 같이 나타나도록 예외를 발생 시키는 코드를 제거 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>코드 수준 오류 로깅 추가

이 자습서의 앞부분에서 설명 했 듯이 코드의 섹션을 실행 하 고 발생 하는 첫 번째 오류를 처리 하려고 하는 try/catch 문을 추가할 수 있습니다. 이 예제에서는 작성 합니다 오류 세부 정보 오류 로그 파일에 오류를 나중에 검토할 수 있도록 합니다.

1. **솔루션 탐색기**에 *논리* 찾기 및 열기, 폴더는 *PayPalFunctions.cs* 파일입니다.
2. 업데이트는 `HttpCall` 메서드 코드도 나타나도록 따릅니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

위의 코드 호출은 `LogException` 에 포함 된 메서드는 `ExceptionUtility` 클래스입니다. 추가한는 *ExceptionUtility.cs* 클래스 파일을 여 *논리* 이 자습서의 앞부분에 나오는 폴더입니다. `LogException` 메서드는 두 개의 매개 변수를 사용 합니다. 첫 번째 매개 변수는 예외 개체입니다. 두 번째 오류의 출처를 인식 하는 데 사용 하는 문자열입니다.

### <a name="inspecting-the-error-logging-information"></a>오류 로깅 정보를 검사합니다.

앞에서 설명한 대로 응용 프로그램에서 오류를 먼저 수정 해야 확인 하려면 오류 로그를 사용할 수 있습니다. 물론, 트래핑 되 고 오류 로그에 기록 된 오류만 기록 됩니다.

1. **솔루션 탐색기**찾기 및 열기는 *ErrorLog.txt* 파일에 *앱\_데이터* 폴더입니다.   
 선택 해야는 "**모든 파일 표시**" 옵션 또는 "**새로 고침**" 맨 위부터 옵션 **솔루션 탐색기** 볼 수는 *ErrorLog.txt*파일입니다.
2. Visual Studio에 표시 된 오류 로그를 검토 합니다. 

    ![ASP.NET 오류 처리-ErrorLog.txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>안전한 오류 메시지

**유의** 는 오류 메시지를 표시 하는 응용 프로그램 경우 것 해야를 제공 하지 정보를 악의적인 사용자는 응용 프로그램을 공격 하는 데 도움이 찾을 수 있습니다. 예를 들어 응용 프로그램는 데이터베이스에 기록 하지 못한를 사용 하는 사용자 이름을 포함 하는 오류 메시지가 표시 되지 해야 합니다. 이러한 이유로 일반 오류 메시지가 빨간색으로 사용자에 게 표시 됩니다. 모든 추가 오류 세부 정보는 로컬 컴퓨터에서 개발자에 게 표시 됩니다.

## <a name="using-elmah"></a>ELMAH를 사용 하 여

ELMAH (오류 로깅 모듈 및 처리기)에 NuGet 패키지로 ASP.NET 응용 프로그램에 연결 하는 오류 로깅 기능입니다. ELMAH는 다음과 같은 기능을 제공합니다.

- 처리 되지 않은 예외의 로깅을 구성 합니다.
- 기록 된 처리 되지 않은 예외에 대 한 전체 로그를 보려는 웹 페이지입니다.
- 각각의 전체 세부 정보를 보려면 웹 페이지 예외를 기록 합니다.
- 메일 알림을 각 오류 발생 시.
- 마지막 15 오류 로그에서 RSS 피드입니다.

ELMAH 작업할 수 있습니다, 전에 설치 해야 합니다. 이것은 쉽게 사용 하 여는 *NuGet* 패키지 설치 관리자입니다. 이 자습서 시리즈의 앞부분에 나오는 설명 했 듯이 NuGet은 쉽게 설치 하 고 Visual Studio에서 오픈 소스 라이브러리와 도구를 업데이트 하는 Visual Studio 확장 합니다.

1. Visual Studio 내에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**  - &gt; **솔루션에 대 한 NuGet 패키지 관리**합니다. 

    ![ASP.NET 오류 처리-솔루션용 NuGet 패키지 관리](aspnet-error-handling/_static/image6.png)
2. **NuGet 패키지 관리** Visual Studio 내에서 대화 상자가 표시 됩니다.
3. 에 **NuGet 패키지 관리** 대화 상자에서 **온라인** 왼쪽에서 선택한 후 **nuget.org**합니다. 그런 다음, 찾기 및 설치는 **ELMAH** 사용 가능한 패키지를 온라인의 목록에서 패키지 합니다. 

    ![ASP.NET 오류 처리-ELMA NuGet 패키지](aspnet-error-handling/_static/image7.png)
4. 패키지를 다운로드 하려면 인터넷에 연결 해야 합니다.
5. 에 **프로젝트 선택** 대화 상자의 **WingtipToys** 선택 영역을 선택한 다음 클릭 **확인**합니다. 

    ![ASP.NET 오류 처리-프로젝트 대화 상자를 선택 합니다.](aspnet-error-handling/_static/image8.png)
6. 클릭 **닫기** 에 **NuGet 패키지 관리** 필요한 경우 대화 상자.
7. Visual Studio에서 열려 있는 모든 파일을 다시 로드를 요청 하는 경우 선택 "**모두 예**"입니다.
8. ELMAH 패키지 자체에 대 한 항목 추가 *Web.config* 프로젝트의 루트에 파일입니다. Visual Studio 묻는 수정 된 다시 로드 하려면 *Web.config* 파일에서 클릭 **예**합니다.

ELMAH 발생 하는 처리 되지 않은 오류를 저장할 준비가 되었습니다.

### <a name="viewing-the-elmah-log"></a>ELMAH 로그 보기

ELMAH 로그를 확인 하는 것은 간단 하지만 먼저 ELMAH 로그에 기록 될는 처리 되지 않은 예외가 만들어집니다.

1. 키를 눌러 **CTRL + f 5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.
2. 처리 되지 않은 예외가 ELMAH 로그에 쓰려는 (포트 번호를 사용 하 여) 다음 URL 브라우저에서 이동 합니다.  
    `https://localhost:44300/NoPage.aspx`오류 페이지가 표시 됩니다.
3. ELMAH 로그를 표시 하려면 (포트 번호를 사용 하 여) 다음 URL 브라우저에서 이동 합니다.  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 오류 처리-ELMAH 오류 로그](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 응용 프로그램 수준, 페이지 수준 및 코드 수준에서 발생 한 오류를 처리 하는 방법에 대 한 배웠습니다. 또한 나중에 검토할 수에 대 한 처리 및 처리 되지 않은 오류를 기록 하는 방법을 배웠습니다. ELMAH 유틸리티를 예외 로깅 및 NuGet을 사용 하 여 응용 프로그램에 대 한 알림을 제공 하기 위해 추가 했습니다. 또한 안전한 오류 메시지의 중요도 대 한 배웠습니다.

## <a name="tutorial-series-conclusion"></a>자습서 시리즈 결론

*보지 주셔서 감사 합니다. 자습서의이 집합에 대해 ASP.NET Web Forms 하는 데 도움이 바랍니다. ASP.NET 4.5 및 Visual Studio 2013에서 사용할 수 있는 Web Forms 기능에 대 한 자세한 정보를 보려면 참고* [ *ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보* ](../../../../visual-studio/overview/2013/release-notes.md)  *. 또한에 언급 된 자습서를 살펴보려면 않아야는* ***다음 단계 * * * 섹션과 defintely 사용해는* [ *무료 Azure 평가판* ](https://azure.microsoft.com/pricing/free-trial/)*.*

![감사-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>다음 단계

Microsoft Azure에 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 [Secure ASP.NET Web Forms 앱 배포 멤버 자격, OAuth, SQL 데이터베이스와 Azure 웹 사이트를](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)합니다.

## <a name="free-trial"></a>무료 평가판

[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)  
 Microsoft Azure에 웹 사이트를 게시할 저장 하면 시간과 유지 관리 비용. Azure에 웹 앱을 배포 하는 빠른 프로세스입니다. 유지 관리 하 고 웹 응용 프로그램을 모니터링 하려는 경우 Azure는 다양 한 도구 및 서비스를 제공 합니다. 데이터, 트래픽, identity, 메시징, 미디어 및 Azure에서 성능 백업을 관리 합니다. 및이 모두는 매우 비용 효율적인 방식으로 제공 됩니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 상태 모니터링을 사용 하 여 오류 세부 정보를 로깅](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>감사의 글

이 자습서 시리즈의 내용에 중요 한 기여를 수행한 다음 사람에 게 감사 하 고 싶습니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen, 네덜란드](http://blog.alexthissen.nl/) (twitter: [ @alexthissen ](http://twitter.com/alexthissen))
- [Andre Tournier, USA](http://andret503.wordpress.com/)
- Apurva Joshi, Microsoft
- [Bojan Vrhovnik, 슬로베니아](http://twitter.com/bvrhovnik)
- [Bruno Sonnino, 브라질](http://msmvps.com/blogs/bsonnino) (twitter: [ @bsonnino ](http://twitter.com/bsonnino))
- [Carlos dos Santos, 브라질](http://www.carloscds.net/)
- [Dave Campbell, 미국](http://www.wynapse.com/) (twitter: [ @windowsdevnews ](http://twitter.com/windowsdevnews))
- [Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))
- [Michael 정자, USA](http://www.930solutions.com/) (twitter: [ @mrsharps ](http://twitter.com/mrsharps))
- Mike 서
- [Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [ @MitchelSellers ](http://twitter.com/MitchelSellers))
- [Paul Cociuba, Microsoft](http://linqto.me/Links/pcociuba)
- [Paulo Morgado, Portugal](http://paulomorgado.net/)
- [Pranav Rastogi, Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann, Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra, Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>커뮤니티 기여

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
 Visual Studio 2012 관련 msdn 코드 샘플: [탐색 Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
 Visual Studio 2012 관련 msdn 코드 샘플: [Visual Basic의 ASP.NET 4.5 Web Forms 자습서 시리즈](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 기술 Audience 참가자 (twitter: @driazevedo)  
 Visual Studio 2012 번역: [Iniciando com Visão Geral ASP.NET Web Forms 4.5-Parte 1-Introdução e](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

>[!div class="step-by-step"]
[이전](url-routing.md)
