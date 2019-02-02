---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN 자체 호스트 하는 ASP.NET Web API 사용 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다. Open Web Interface for.NET (OWIN) d...
ms.author: riande
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 59ce24aa47ca590fbe9b617dbbe8bc6b3711849e
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667390"
---
<a name="use-owin-to-self-host-aspnet-web-api"></a>OWIN을 사용 하 여 자체 호스트 하는 ASP.NET Web API 
====================

> 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.
>
> [Open Web Interface for.NET](http://owin.org) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN 이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - 웹 API 5.2.7


> [!NOTE]
> 이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다 [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)합니다.


## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

에 **파일** 메뉴에서 **새로 만들기**을 선택한 후 **프로젝트**합니다. **설치 됨**아래에 있는 **Visual C#** 선택 **Windows Desktop** 선택한 후 **콘솔 앱 (.NET Framework)**. "OwinSelfhostSample" 프로젝트 이름을 선택한 **확인**합니다.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 및 OWIN 패키지 추가

**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

이 WebAPI OWIN selfhost 패키지 및 모든 필수 OWIN 패키지가 설치 됩니다.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>Web API를 구성에 대 한 자체 호스트

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다. 클래스 이름을 `Startup`로 지정합니다.

![](use-owin-to-self-host-web-api/_static/image5.png)

모두이 파일의 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Web API 컨트롤러 추가

다음으로, Web API 컨트롤러 클래스를 추가 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다. 클래스 이름을 `ValuesController`로 지정합니다.

모두이 파일의 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>OWIN 호스트를 시작 하 고 HttpClient 사용 하 여 요청을 만듭니다

다음을 사용 하 여 모든 Program.cs 파일의 상용구 코드를 대체 합니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>애플리케이션 실행

Visual Studio에서 F5 키를 눌러 응용 프로그램을 실행 합니다. 출력은 다음과 같습니다.

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>추가 자료

[프로젝트 Katana 개요](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure 작업자 역할에서 ASP.NET Web API 호스팅](host-aspnet-web-api-in-an-azure-worker-role.md)
