---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 오류 처리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: ed5d7b9b4e61b0289734f4cdef1039b31ddda7a7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837507"
---
<a name="aspnet-error-handling"></a>ASP.NET 오류 처리
====================
[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.


이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 오류 처리 및 오류 로그를 포함 하도록 수정 합니다. 오류 처리 응용 프로그램이 정상적으로 오류를 처리 하 고 오류 메시지를 적절 하 게 표시할 수 있습니다. 오류 로그를 사용 하면을 찾고 발생 한 오류를 해결할 수 있습니다. 이 자습서는 "URL 라우팅" 이전 자습서에서 작성 하 고 Wingtip Toys 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 전역 오류 처리 응용 프로그램의 구성에 추가 하는 방법입니다.
- 응용 프로그램, 페이지 및 코드 수준에서 처리 하는 오류를 추가 하는 방법입니다.
- 나중에 검토할 수에 대 한 오류를 기록 하는 방법입니다.
- 보안이 손상 되지 않는 오류 메시지를 표시 하는 방법.
- 오류 로깅 모듈 및 처리기의 ELMAH () 오류 로깅을 구현 하는 방법.

## <a name="overview"></a>개요

ASP.NET 응용 프로그램은 일관 된 방식으로 실행 하는 동안 발생 하는 오류를 처리할 수 있어야 합니다. ASP.NET 일관 된 방식으로 응용 프로그램에 오류를 알리는 방법을 제공 하는 공용 언어 런타임 (CLR)를 사용 합니다. 오류가 발생 하면 예외가 throw 됩니다. 예외는 오류, 조건 또는 응용 프로그램에서 발생 하는 예기치 않은 동작입니다.

.NET Framework에서 예외는 `System.Exception`에서 상속받은 개체입니다. 예외는 문제가 발생한 코드 영역에서 throw됩니다. 예외는 응용 프로그램에서 예외를 처리 하는 코드를 제공 하는 위치로 호출 스택 위로 전달 됩니다. 응용 프로그램 예외를 처리 하지 않는 브라우저 오류 세부 정보를 표시 하도록 강제 됩니다.

모범 사례로, 코드 수준에서 오류 처리 `Try` / `Catch` / `Finally` 코드 내에서 블록입니다. 사용자 컨텍스트에서 발생 하는 문제를 해결할 수 있도록 이러한 블록을 배치 하려고 합니다. 오류 처리 블록 오류가 발생 한 위치에서 너무 멀리 떨어진 경우 문제를 해결 하는 데 필요한 정보를 제공 하기 위해 더 어려워집니다.

### <a name="exception-class"></a>예외 클래스

예외 클래스에는 예외가 상속 하는 기본 클래스가입니다. 와 같은 대부분의 예외 개체는 예외 클래스의 몇 가지 파생된 클래스의 인스턴스를 `SystemException` 클래스를 `IndexOutOfRangeException` 클래스 또는 `ArgumentNullException` 클래스입니다. 예외 클래스에 속성이 같은 `StackTrace` 속성을 `InnerException` 속성 및 `Message` 발생 한 오류에 대 한 특정 정보를 제공 하는 속성.

### <a name="exception-inheritance-hierarchy"></a>예외가 상속 계층 구조

런타임 예외에서 파생의 기본 집합이 `SystemException` 런타임 예외가 발생할 때 throw 되는 클래스입니다. 대부분의 클래스와 같은 예외 클래스에서 상속 되는 `IndexOutOfRangeException` 클래스 및 `ArgumentNullException` 클래스, 추가 멤버를 구현 하지 않습니다. 따라서 가장 중요 한 정보는 예외에 대 한 예외, 예외 이름 및 예외에 포함 된 정보 계층 구조에 있습니다.

### <a name="exception-handling-hierarchy"></a>예외 처리 계층

ASP.NET Web Forms 응용 프로그램에서는 특정 처리 계층에 따라 예외를 처리할 수 있습니다. 다음 수준에서 예외를 처리할 수 있습니다.

- 응용 프로그램 수준
- 페이지 수준
- 코드 수준

응용 프로그램에서 예외를 처리할 때 예외 클래스에서 상속 되는 예외에 대 한 추가 정보 검색 및 사용자에 게 표시 종종 수 있습니다. 응용 프로그램, 페이지 및 코드 수준, 하는 것 외에도 HTTP 모듈 수준에서 IIS 사용자 지정 처리기를 사용 하 여 예외를 처리할 수도 있습니다.

### <a name="application-level-error-handling"></a>응용 프로그램 수준 오류 처리

응용 프로그램의 구성을 수정 하거나 추가 하 여 응용 프로그램 수준에서 기본 오류를 처리할 수 있습니다는 `Application_Error` 처리기에는 *Global.asax* 응용 프로그램의 파일입니다.

추가 하 여 기본 오류 및 HTTP 오류를 처리할 수 있습니다는 `customErrors` 섹션을 합니다 *Web.config* 파일입니다. `customErrors` 섹션을 사용 하면 사용자가 리디렉션됩니다 오류가 발생 하는 기본 페이지를 지정할 수 있습니다. 또한 특정 상태 코드 오류에 대 한 개별 페이지를 지정할 수 있습니다.

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

그러나 다른 페이지로 사용자를 리디렉션할 구성을 사용 하는 경우에 발생 한 오류의 세부 정보 필요가 없습니다.

코드를 추가 하 여 응용 프로그램에서 발생 하는 오류를 트래핑할 수는 있지만 합니다 `Application_Error` 처리기에는 *Global.asax* 파일입니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>페이지 수준 오류 이벤트 처리

없습니다 더 이상 아무 것도 페이지를 페이지 수준 처리기를 오류가 발생 하지만 컨트롤의 인스턴스는 유지 되지 않으므로 페이지로 사용자를 반환 합니다. 응용 프로그램의 사용자에 게 오류 세부 정보를 제공, 특히 페이지로 오류 세부 정보를 써야 합니다.

일반적으로 유용한 정보를 표시할 수 있는 페이지로 사용자 이동 또는 처리 되지 않은 오류를 기록 하는 페이지 수준 오류 처리기를 사용 합니다.

이 코드 예제에는 ASP.NET 웹 페이지에서 오류 이벤트에 대 한 처리기를 보여 줍니다. 이 처리기 내에서 이미 처리 되지 않은 모든 예외를 포착 `try` / `catch` 페이지에서 차단 합니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

오류를 처리 한 후 호출 하 여 해제 해야 하는 `ClearError` 서버 개체의 메서드 (`HttpServerUtility` 클래스), 그렇지 않으면 이전에 발생 한 오류가 나타납니다.

### <a name="code-level-error-handling"></a>수준 오류 처리 코드

하나가 오는 try 블록의 try / catch 문을 구성 또는 이상의 서로 다른 예외에 대 한 처리기를 지정 하는 절을 catch 합니다. 예외가 throw 되 면는 CLR (공용 언어 런타임)이이 예외를 처리 하는 catch 문을 찾습니다. 현재 실행 중인 메서드 catch 블록이 없으면 CLR은 등과 호출 스택을 확인 하 고 현재 메서드를 호출 하는 메서드를 살펴봅니다. Catch 블록이 없는 있으면 CLR 처리 되지 않은 예외 메시지가 사용자에 게 표시 및 프로그램의 실행을 중지 합니다.

다음 코드 예제를 사용 하 여 일반적인 방법을 보여 줍니다 `try` / `catch` / `finally` 오류를 처리 합니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

위의 코드에서 try 블록이 발생 가능한 예외를 방지 해야 하는 코드를 포함 합니다. 블록은 예외가 있거나 블록을 완료 될 때까지 실행 됩니다. 경우는 `FileNotFoundException` 예외 또는 `IOException` 예외가 발생 하면 실행이 다른 페이지로 전송 됩니다. 그런 다음에 포함 된 코드는 finally 블록이 실행 된 오류가 발생 하는지 여부를 합니다.

## <a name="adding-error-logging-support"></a>오류 로깅 지원 추가

Wingtip Toys 샘플 응용 프로그램에 오류 처리에 추가 하기 전에 추가 하 여 오류 로깅 지원을 추가 합니다는 `ExceptionUtility` 클래스를 *논리* 폴더입니다. 이 응용 프로그램 오류를 처리할 때마다 작업을 수행 하면 오류 세부 정보를 오류 로그 파일을 추가할 수 됩니다.

1. 마우스 오른쪽 단추로 클릭 합니다 *논리* 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **코드** 왼쪽의 템플릿 그룹입니다. 그런 다음 선택 **클래스**가운데에서 나열 하 고 이름을 **ExceptionUtility.cs**합니다.
3. **추가**를 선택합니다. 새 클래스 파일에 표시 됩니다.
4. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

예외를 호출 하 여는 예외 로그 파일에 기록 수 예외가 발생 하는 경우는 `LogException` 메서드. 이 메서드는 두 개의 매개 변수, 예외 개체 및 예외의 원본에 대 한 세부 정보를 포함 하는 문자열을 사용 합니다. 예외 로그에 기록 됩니다 합니다 *ErrorLog.txt* 파일을 *앱\_데이터* 폴더입니다.

### <a name="adding-an-error-page"></a>오류 페이지 추가

Wingtip Toys 샘플 응용 프로그램에서 한 페이지 오류를 표시 하려면 사용 됩니다. 오류 페이지는 사이트의 사용자에 게 보안 오류 메시지를 표시 하도록 설계 되었습니다. 그러나 사용자가 코드의 현재 위치에 컴퓨터에 로컬로 제공 하는 HTTP 요청을 수행 하는 개발자가 추가 오류 세부 정보 오류 페이지에 표시 됩니다.

1. 프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택한 **추가**  - &gt; **새 항목**.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다. 가운데 목록에서 선택 **마스터 페이지를 사용 하 여 Web Form**, 하 고 이름을 **ErrorPage.aspx**합니다.
3. **추가**를 클릭합니다.
4. 선택 된 *Site.Master* 마스터 페이지 파일 및 선택한 **확인**합니다.
5. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 코드 숨김의 기존 코드를 바꿉니다 (*ErrorPage.aspx.cs*) 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

오류 페이지 표시 되 면는 `Page_Load` 이벤트 처리기가 실행 됩니다. 에 `Page_Load` 처리기의 오류가 처리 먼저 될 위치에 따라 결정 됩니다. 발생 한 마지막 오류를 호출 하 여 결정 됩니다 차례로 `GetLastError` 서버 개체의 메서드. 예외를 더 이상 존재 하는 경우에 일반 예외를 생성 됩니다. 그런 다음 HTTP 요청을 로컬로 수행한, 모든 오류 세부 정보가 표시 됩니다. 이 경우 웹 응용 프로그램을 실행 하는 로컬 컴퓨터만 이러한 오류 세부 정보가 표시 됩니다. 오류 정보를 표시 된 후 로그 파일에 추가 하는 오류 및 서버에서 오류가 지워집니다.

### <a name="displaying-unhandled-error-messages-for-the-application"></a>응용 프로그램에 대 한 처리 되지 않은 오류 메시지를 표시합니다.

추가 하 여는 `customErrors` 섹션을 합니다 *Web.config* 파일을 처리할 수 있습니다 신속 하 게 응용 프로그램 전체에서 발생 하는 간단한 오류입니다. 또한 404-찾을 수 없는 파일 등 해당 상태 코드 값을 기반으로 하는 오류를 처리 하는 방법을 지정할 수 있습니다.

#### <a name="update-the-configuration"></a>구성 업데이트 하 고

구성을 추가 하 여 업데이트를 `customErrors` 섹션을 합니다 *Web.config* 파일입니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *Web.config* Wingtip Toys 샘플 응용 프로그램의 루트에 있는 파일입니다.
2. 추가 합니다 `customErrors` 섹션을 *Web.config* 내에서 파일을 `<system.web>` 다음과 같은 노드:   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. 저장 된 *Web.config* 파일입니다.

`customErrors` 섹션 "켜기"로 설정 되는 모드를 지정 합니다. 또한 지정 된 `defaultRedirect`, 지시 하는 응용 프로그램 오류가 발생할 때 탐색할 페이지입니다. 또한 페이지를 찾을 수 없으면 404 오류를 처리 하는 방법을 지정 하는 특정 오류 요소를 추가 했습니다. 이 자습서의 뒷부분에서 추가 오류 처리 응용 프로그램 수준 오류의 세부 정보 캡처를 추가 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

업데이트 된 경로 확인 하려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.
2. 브라우저에 다음 URL을 입력 합니다. (사용 해야 **여** 포트 번호):  
    `https://localhost:44300/NoPage.aspx`
3. 검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-페이지 찾을 수 없음 오류](aspnet-error-handling/_static/image1.png)

요청 하는 경우는 *NoPage.aspx* 존재 하지 않는 페이지 오류 페이지에는 표시 간단한 오류 메시지와 자세한 오류 정보를 추가 세부 정보를 사용할 수 없는 경우. 그러나 사용자는 원격 위치에서 존재 하지 않는 페이지를 요청 하는 경우 오류 페이지는 빨간색에서 오류 메시지를만 표시 됩니다.

### <a name="including-an-exception-for-testing-purposes"></a>테스트 목적에 대 한 예외를 포함 하 여

발생 시 응용 프로그램이 어떻게 작동 하는지 확인 하려면, ASP.NET에서 오류 조건을 의도적으로 만들 수 있습니다. Wingtip Toys 샘플 응용 프로그램을 현상을 보려면 기본 페이지가 로드 하는 경우 테스트 예외를 throw 하는 합니다.

1. 코드 숨김을 엽니다는 *Default.aspx* Visual Studio의 페이지입니다.   
   합니다 *Default.aspx.cs* 코드 숨김 페이지에 표시 됩니다.
2. 에 `Page_Load` 처리기를 처리기는 다음과 같이 표시 되도록 코드를 추가 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

다양 한 유형의 예외를 만들 수는 것입니다. 위의 코드에서 만드는 `InvalidOperationException` 때 합니다 *Default.aspx* 페이지가 로드 됩니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램에서 예외를 처리 하는 방법을 확인 하려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램 InvalidOperationException을 throw합니다. 

    > [!NOTE] 
    > 
    > 눌러야 **ctrl+f5** 소스를 보려면 오류 Visual Studio에서 코드를 중단 하지 않고 페이지를 표시 합니다.
2. 검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-오류 페이지](aspnet-error-handling/_static/image2.png)

예외에 의해 포착 되 된 오류 정보를 보면 합니다 `customError` 섹션의 *Web.config* 파일.

### <a name="adding-application-level-error-handling"></a>응용 프로그램 수준 오류 처리 추가

사용 하 여 예외를 트래핑 하는 대신 합니다 `customErrors` 섹션의 *Web.config* 파일, 예외에 대 한 정보만 확보 하는 경우 응용 프로그램 수준에서 오류를 트래핑 하 고 오류 세부 정보를 검색할 수 있습니다.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *Global.asax.cs* 파일입니다.
2. 추가 **응용 프로그램\_오류** 처리기 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

응용 프로그램에서 오류가 발생 하는 경우는 `Application_Error` 처리기가 호출 됩니다. 이 처리기에서 마지막으로 예외를 검색 하 고 검토 합니다. 예외 처리 되어 예외는 내부 예외 세부 정보를 포함 하는 경우 (즉, `InnerException` null이 아님), 응용 프로그램 실행을 이동 오류 페이지에는 예외 세부 정보에 표시 되는 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램 수준에서 예외를 처리 하 여 제공 된 추가 오류 세부 정보를 보려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.
2. 검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-응용 프로그램 수준 오류](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>페이지 수준 오류 처리 추가

에 추가할 수 있습니다 페이지 수준 오류 처리 페이지 추가 사용 하 여는 `ErrorPage` 특성을 `@Page` 페이지 또는 추가 하 여 지시문을 `Page_Error` 페이지의 코드 숨김에 이벤트 처리기입니다. 이 섹션에서는 추가 된 `Page_Error` 실행을 전송 하는 이벤트 처리기를 *ErrorPage.aspx* 페이지.

1. **솔루션 탐색기**찾기 및 열기, 합니다 *Default.aspx.cs* 파일입니다.
2. 추가 `Page_Error` 처리기로 코드 숨김 표시 되도록 따릅니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

페이지에서 오류가 발생 하는 경우는 `Page_Error` 이벤트 처리기가 호출 됩니다. 이 처리기에서 마지막으로 예외를 검색 하 고 검토 합니다. 경우는 `InvalidOperationException` 발생을 `Page_Error` 이벤트 처리기 실행을 이동 오류 페이지에는 예외 세부 정보에 표시 되는 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

업데이트 된 경로 확인 하려면 응용 프로그램을 실행할 수 있습니다.

1. 키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.
2. 검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다. 

    ![ASP.NET 오류 처리-페이지 수준 오류](aspnet-error-handling/_static/image4.png)
3. 브라우저 창을 닫습니다.

### <a name="removing-the-exception-used-for-testing"></a>테스트에 사용 되는 예외를 제거 합니다.

이 자습서의 앞부분에서 추가한 예외를 throw 하지 않고 함수 Wingtip Toys 샘플 응용 프로그램을 허용 하려면 예외를 제거 합니다.

1. 코드 숨김을 엽니다는 *Default.aspx* 페이지입니다.
2. 에 `Page_Load` 처리기를 처리기는 다음과 같이 표시 되도록 예외를 throw 하는 코드를 제거 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>코드 수준 오류 로깅 추가

이 자습서의 앞부분에서 설명 했 듯이 코드 부분을 실행 하 고 발생 하는 첫 번째 오류를 처리 하려고 try/catch 문을 추가할 수 있습니다. 이 예제에서는 오류 세부 정보를 기록 오류 로그 파일의 오류를 나중에 검토할 수 있도록 합니다.

1. **솔루션 탐색기**를 *논리* 폴더, 찾기 및 열기를 *PayPalFunctions.cs* 파일입니다.
2. 업데이트 된 `HttpCall` 메서드 코드 요소로 다음과 같이 나타나도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

위의 코드 호출을 `LogException` 에 포함 된 메서드는 `ExceptionUtility` 클래스입니다. 추가한 합니다 *ExceptionUtility.cs* 클래스 파일을 합니다 *논리* 이 자습서의 앞부분에서 폴더입니다. `LogException` 메서드는 두 매개 변수를 사용합니다. 첫 번째 매개 변수는 예외 개체입니다. 두 번째는 오류의 소스를 인식 하는 데 사용 하는 문자열입니다.

### <a name="inspecting-the-error-logging-information"></a>오류 로깅 정보를 검사합니다.

이전에 설명한 대로 응용 프로그램에서 오류를 먼저 수정 해야 확인 하려면 오류 로그를 사용할 수 있습니다. 물론, 트랩 및 오류 로그에 기록 된 오류만 기록 됩니다.

1. **솔루션 탐색기**, 찾기 및 열기를 *ErrorLog.txt* 파일을 *앱\_데이터* 폴더입니다.   
 선택 해야 할 수도 있습니다는 "**모든 파일 표시**" 옵션 또는 "**새로 고침**" 옵션의 맨 위에서 **솔루션 탐색기** 보려는 *ErrorLog.txt*파일입니다.
2. Visual Studio에 표시 된 오류 로그를 검토 합니다. 

    ![ASP.NET 오류 처리-ErrorLog.txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>안전한 오류 메시지

것 **알아야** 는 응용 프로그램 오류 메시지를 표시 하는 경우이 해야 하지 포기할 악의적인 사용자는 응용 프로그램을 공격에 유용할 수 있는 정보입니다. 예를 들어, 응용 프로그램 데이터베이스 쓸 실패 시도 사용 하는 사용자 이름을 포함 하는 오류 메시지가 표시 되지 됩니다. 이러한 이유로 빨간색에서 일반 오류 메시지를 사용자에 게 표시 됩니다. 모든 추가 오류 세부 정보는 로컬 컴퓨터의 개발자에 게만 표시 됩니다.

## <a name="using-elmah"></a>ELMAH를 사용 하 여

ELMAH (오류 로깅 모듈 및 처리기)는 NuGet 패키지로 ASP.NET 응용 프로그램에 연결 하는 오류 로깅 기능입니다. ELMAH는 다음과 같은 기능을 제공합니다.

- 처리 되지 않은 예외의 로그입니다.
- 처리 되지 않은 예외를 기록된의 전체 로그를 보려면 웹 페이지입니다.
- 각각의 전체 세부 정보를 보려면 웹 페이지 예외를 기록 합니다.
- 발생 시점에 각 오류의 전자 메일 알림을 합니다.
- 마지막 15 개의 오류 로그에서의 RSS 피드입니다.

ELMAH를 사용 하 여 작업 하려면, 먼저 설치 해야 합니다. 이 작업은 사용 하 여는 *NuGet* 설치 관리자를 패키지 합니다. 이 자습서 시리즈의 앞부분에서 설명 했 듯이 NuGet은 쉽게 설치 하 고 Visual Studio에서 오픈 소스 라이브러리와 도구를 업데이트 하는 Visual Studio 확장입니다.

1. Visual Studio 내에서 **도구** 메뉴에서 **라이브러리 패키지 관리자**  - &gt; **솔루션용 NuGet 패키지 관리**합니다. 

    ![ASP.NET 오류 처리-솔루션용 NuGet 패키지 관리](aspnet-error-handling/_static/image6.png)
2. 합니다 **NuGet 패키지 관리** Visual Studio 내에서 대화 상자가 표시 됩니다.
3. 에 **NuGet 패키지 관리** 대화 상자에서 **Online** 왼쪽에서 선택한 후 **nuget.org**합니다. 그런 다음 찾아서 설치 합니다 **ELMAH** 온라인에서 사용 가능한 패키지의 목록에서 패키지 합니다. 

    ![ASP.NET 오류 처리-ELMA NuGet 패키지](aspnet-error-handling/_static/image7.png)
4. 패키지를 다운로드 하려면 인터넷에 연결 해야 합니다.
5. 에 **프로젝트 선택** 대화 상자를 **WingtipToys** 선택을 선택한 다음 클릭 **확인**합니다. 

    ![ASP.NET 오류 처리-프로젝트 대화 상자를 선택 합니다.](aspnet-error-handling/_static/image8.png)
6. 클릭 **닫습니다** 에 **NuGet 패키지 관리** 필요한 경우 대화 상자.
7. Visual Studio에서 열려 있는 모든 파일을 다시 로드를 요청 하는 경우 선택 "**모두 예**"입니다.
8. ELMAH 패키지 자체에 대 한 항목을 추가 합니다 *Web.config* 프로젝트의 루트에 있는 파일입니다. Visual Studio 묻는 메시지가 수정 된 다시 로드 하려는 경우 *Web.config* 파일에서 클릭 **예**합니다.

ELMAH 발생 하는 처리 되지 않은 오류를 저장할 준비가 되었습니다.

### <a name="viewing-the-elmah-log"></a>ELMAH 로그 보기

ELMAH 로그를 확인 하는 것은 쉽지만 있지만 ELMAH 로그에 기록 될 예외가 먼저 만듭니다.

1. 키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.
2. 처리 되지 않은 예외가 ELMAH 로그에 쓰려면 (포트 번호로 사용) 다음 URL로 브라우저에서 이동 합니다.  
    `https://localhost:44300/NoPage.aspx` 오류 페이지 표시 됩니다.
3. ELMAH 로그를 표시 하려면 (포트 번호로 사용) 다음 URL로 브라우저에서 이동 합니다.  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 오류 처리-ELMAH 오류 로그](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 응용 프로그램 수준, 페이지 수준 및 코드 수준에서 오류를 처리 하는 방법에 대 한 배웠습니다. 또한 나중에 검토할 수에 대 한 처리 및 처리 되지 않은 오류를 기록 하는 방법을 배웠습니다. 예외 로깅 및 NuGet을 사용 하 여 응용 프로그램에 대 한 알림을 제공 ELMAH 유틸리티를 추가 했습니다. 또한 안전한 오류 메시지의 중요성에 배웠습니다.

## <a name="tutorial-series-conclusion"></a>자습서 시리즈 결론

*에 따라 다음에 참여해 주셔서 감사 합니다. 이 자습서 집합을 통해 ASP.NET Web Forms에 더 익숙해질 수 있기를 기대 합니다. ASP.NET 4.5와 Visual Studio 2013에서 사용 가능한 Web Forms 기능에 대 한 자세한 내용은 참조 하세요* [ *ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보* ](../../../../visual-studio/overview/2013/release-notes.md)  *. 또한에 언급 된 자습서를 살펴보려면 해야 합니다* ***다음 단계 * * * 섹션과 defintely 사용해 합니다* [ *무료 Azure 평가판* ](https://azure.microsoft.com/pricing/free-trial/)*.*

![감사-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>다음 단계

Microsoft Azure에 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [보안 ASP.NET Web Forms 앱을 멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure 웹 사이트로 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)합니다.

## <a name="free-trial"></a>무료 평가판

[Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)  
 Microsoft Azure에 웹 사이트를 게시할는 수 고를 덜, 유지 관리 비용. Azure에 웹 앱을 배포 하는 빠른 프로세스입니다. 유지 관리 하 고 웹 앱을 모니터링 해야 할 때 Azure는 다양 한 도구 및 서비스를 제공 합니다. 데이터, 트래픽, id, 백업, 메시징, 미디어 및 Azure에서 성능을 관리 합니다. 및이 모두 매우 경제적인 방식으로 제공 됩니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 상태 모니터링을 사용 하 여 오류 세부 정보 로깅](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>감사의 글

이 자습서 시리즈의 콘텐츠에 중요 한 기여를 수행한 다음 사용자를 감사 하려고 합니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen, 네덜란드](http://blog.alexthissen.nl/) (twitter: [ @alexthissen ](http://twitter.com/alexthissen))
- [Andre Tournier, 미국](http://andret503.wordpress.com/)
- Apurva Joshi, Microsoft
- [Bojan Vrhovnik, 슬로베니아](http://twitter.com/bvrhovnik)
- [Bruno Sonnino, 브라질](http://msmvps.com/blogs/bsonnino) (twitter: [ @bsonnino ](http://twitter.com/bsonnino))
- [Carlos dos Santos, 브라질](http://www.carloscds.net/)
- [Dave Campbell, 미국](http://www.wynapse.com/) (twitter: [ @windowsdevnews ](http://twitter.com/windowsdevnews))
- [Microsoft, Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))
- [Michael 정자, USA](http://www.930solutions.com/) (twitter: [ @mrsharps ](http://twitter.com/mrsharps))
- Mike 되
- [Mitchel 판매자, USA](http://www.mitchelsellers.com/) (twitter: [ @MitchelSellers ](http://twitter.com/MitchelSellers))
- [Paul Cociuba, Microsoft](http://linqto.me/Links/pcociuba)
- [파울로 Morgado, 포르투갈](http://paulomorgado.net/)
- [Pranav Rastogi, Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann, Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Microsoft, Tom Dykstra](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>커뮤니티 기여

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
  Visual Studio 2012 관련 msdn 코드 샘플: [탐색 Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  Visual Studio 2012 관련 msdn 코드 샘플: [Visual Basic에서는 ASP.NET 4.5 Web Forms 자습서 시리즈](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 기술 대상 참가자 (twitter: @driazevedo)  
  Visual Studio 2012 번역: [Iniciando com Visão Geral ASP.NET Web Forms 4.5-Parte 1-Introdução e](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [이전](url-routing.md)
