---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 자체 호스팅 ASP.NET Web API 1 (C#) | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에 IIS를 사용할 필요가 없습니다. 사용자 고유의 호스트 프로세스에서 web API를 자체 호스트할 수 있습니다. 이 자습서에서는 합 하는 콘솔 내에서 web API를 호스트 하는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 01/26/2012
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 50681dcd89dfed480cf343f753371af384fd3e68
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811739"
---
<a name="self-host-aspnet-web-api-1-c"></a>자체 호스팅 ASP.NET Web API 1 (C#)
====================
[Mike Wasson](https://github.com/MikeWasson)

> ASP.NET Web API에 IIS를 사용할 필요가 없습니다. 사용자 고유의 호스트 프로세스에서 web API를 자체 호스트할 수 있습니다. 이 자습서에서는 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.
> 
> **새 응용 프로그램 자체 호스트 하는 Web API OWIN을 사용 해야 합니다.** 참조 [OWIN을 사용 하 여 ASP.NET Web API 2 자체 호스팅에](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API 1
> - Visual Studio 2012


## <a name="create-the-console-application-project"></a>콘솔 응용 프로그램 프로젝트 만들기

Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다. 또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **Windows**합니다. 프로젝트 템플릿 목록에서 선택 **콘솔 응용 프로그램**합니다. 프로젝트 이름을 &quot;SelfHost&quot; 누릅니다 **확인**합니다.

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>대상 프레임 워크 (Visual Studio 2010) 설정

Visual Studio 2010을 사용 하는 경우.NET Framework 4.0 대상 프레임 워크를 변경 합니다. (기본적으로 프로젝트 템플릿의 대상 합니다 [.NET Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 에 **대상 프레임 워크** 드롭다운 목록에서.NET Framework 4.0 대상 프레임 워크를 변경 합니다. 변경 내용을 적용 하 라는 메시지가 표시를 클릭 **예**합니다.

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>NuGet 패키지 관리자 설치

NuGet 패키지 관리자는 비 ASP.NET 프로젝트에 어셈블리를 웹 API를 추가 하려면 가장 쉬운 방법입니다.

NuGet 패키지 관리자가 설치 되어 있는지를 확인 하려면 클릭 합니다 **도구** Visual Studio의 메뉴. 항목 이라는 메뉴가 나타나면 **라이브러리 패키지 관리자**, NuGet 패키지 관리자를 해야 합니다.

NuGet 패키지 관리자를 설치 합니다.

1. Visual Studio를 시작합니다.
2. **도구** 메뉴에서 **확장 및 업데이트**합니다.
3. 에 **확장 및 업데이트** 대화 상자에서 **Online**합니다.
4. "NuGet 패키지 관리자"를 보이지 않으면 검색 상자에 "nuget 패키지 관리자"를 입력 합니다.
5. NuGet 패키지 관리자를 선택 하 고 클릭 **다운로드**합니다.
6. 다운로드가 완료 되 면 설치를 묻는 메시지가 나타납니다.
7. 설치가 완료 되 면 Visual Studio를 다시 시작 하 라는 메시지가 될 수 있습니다.

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>웹 API NuGet 패키지 추가

NuGet 패키지 관리자를 설치한 후 웹 API 여 패키지를 프로젝트에 추가 합니다.

1. **도구** 메뉴에서 **라이브러리 패키지 관리자**합니다. *참고*: 경우 하면이 메뉴가 표시 되지 않으면이 항목을 해당 NuGet 패키지 관리자를 제대로 설치 되어 있는지 확인 합니다.
2. 선택 **솔루션용 NuGet 패키지 관리...**
3. 에 **NugGet 패키지 관리** 대화 상자에서 **Online**합니다.
4. 검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.SelfHost&quot;합니다.
5. ASP.NET 웹 API 자체 호스트 패키지를 선택 하 고 클릭 **설치**합니다.
6. 패키지를 설치한 후 클릭 **닫습니다** 는 대화 상자를 닫습니다.

> [!NOTE]
> Microsoft.AspNet.WebApi.SelfHost, 없습니다 AspNetWebApi.SelfHost 라는 패키지를 설치 해야 합니다.


![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>모델 및 컨트롤러 만들기

이 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다 [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다.

라는 공용 클래스를 추가 `Product`합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

라는 공용 클래스를 추가 `ProductsController`합니다. 이 클래스를 파생 **System.Web.Http.ApiController**합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

이 컨트롤러의 코드에 대 한 자세한 내용은 참조는 [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다. 이 컨트롤러 3 개의 가져오기 작업을 정의합니다.

| URI | 설명 |
| --- | --- |
| api 제품 | 모든 제품의 목록을 가져옵니다. |
| /api/products/*id* | 제품 id 가져오기 |
| /api/products/?category=*category* | 범주별으로 제품의 목록을 가져옵니다. |

## <a name="host-the-web-api"></a>Web API 호스팅

Program.cs 파일을 열고 다음 코드를 추가 문을 사용 하 여:

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

다음 코드를 추가 합니다 **프로그램** 클래스입니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>(선택 사항) HTTP URL Namespace 예약을 추가 합니다.

이 응용 프로그램에서 수신 하 `http://localhost:8080/`합니다. 기본적으로 특정 HTTP 주소에서 수신 대기 하려면 관리자 권한이 필요 합니다. 이 자습서를 실행 하면 따라서이 오류가 발생할 수 있습니다이: "HTTP URL을 등록 하지 못했습니다 http://+:8080/" 두 가지 방법으로이 오류를 방지 하려면:

- 관리자 권한으로 Visual Studio를 실행 하거나
- URL 예약에 사용자 계정 권한을 부여 하려면 Netsh.exe를 사용 합니다.

Netsh.exe를 사용 하려면 관리자 권한으로 명령 프롬프트를 열고 및 명령 다음 명령을 입력 합니다.:

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

여기서 *컴퓨터 \* 는 사용자 계정입니다.

자체 호스팅 완료 되 면 예약을 삭제 해야 합니다.

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>클라이언트 응용 프로그램 (C#)에서 웹 API를 호출 합니다.

Web API를 호출 하는 간단한 콘솔 응용 프로그램을 작성해 보겠습니다.

새 콘솔 응용 프로그램 프로젝트를 솔루션에 추가 합니다.

- 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로젝트 추가**합니다.
- 라는 새 콘솔 응용 프로그램을 만듭니다 &quot;ClientApp&quot;합니다.

![](self-host-a-web-api/_static/image5.png)

NuGet 패키지 관리자를 사용 하 여 ASP.NET 웹 API Core 라이브러리 패키지를 추가 하려면:

- 도구 메뉴에서 선택 **라이브러리 패키지 관리자**합니다.
- 선택 **솔루션용 NuGet 패키지 관리...**
- 에 **NuGet 패키지 관리** 대화 상자에서 **Online**합니다.
- 검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.Client&quot;합니다.
- Microsoft ASP.NET 웹 API 클라이언트 라이브러리 패키지를 선택 하 고 클릭 **설치**합니다.

ClientApp에 SelfHost 프로젝트에 대 한 참조를 추가 합니다.

- 솔루션 탐색기에서 ClientApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.
- **참조 추가**를 선택합니다.
- 에 **참조 관리자** 대화 상자 아래에 있는 **솔루션**를 선택 **프로젝트**합니다.
- SelfHost 프로젝트를 선택 합니다.
- **확인**을 클릭합니다.

![](self-host-a-web-api/_static/image6.png)

Client/Program.cs 파일을 엽니다. 다음을 추가 합니다 **를 사용 하 여** 문:

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

추가 정적 **HttpClient** 인스턴스:

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

모든 제품 ID 기준으로 제품 목록 및 목록 제품 범주별으로 나열 하려면 다음 메서드를 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

이러한 메서드는 각각 동일한 패턴을 따릅니다.

1. 호출 **HttpClient.GetAsync** 적합 한 URI에 GET 요청을 보내도록 합니다.
2. 호출 **HttpResponseMessage.EnsureSuccessStatusCode**합니다. 이 메서드는 HTTP 응답 상태 오류 코드 이면 예외가 throw 됩니다.
3. 호출 **ReadAsAsync&lt;T&gt;**  를 HTTP 응답에서 CLR 형식을 역직렬화 합니다. 이 메서드는 확장 메서드를 정의 **System.Net.Http.HttpContentExtensions**합니다.

합니다 **GetAsync** 하 고 **ReadAsAsync** 메서드는 둘 다 비동기 방식입니다. 돌아왔을 **태스크** 비동기 작업을 나타내는 개체입니다. 시작 합니다 **결과** 속성 작업이 완료 될 때까지 스레드를 차단 합니다.

비차단 호출을 수행 하는 방법을 비롯 한 HttpClient를 사용 하는 방법에 대 한 자세한 내용은 참조 [Web API에서는.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.

이러한 메서드를 호출 하기 전에 HttpClient 인스턴스에서 BaseAddress 속성 설정 "`http://localhost:8080`"입니다. 예를 들어:

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

다음 출력 해야 합니다. (SelfHost 응용 프로그램을 먼저 실행 해야 합니다.)

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
