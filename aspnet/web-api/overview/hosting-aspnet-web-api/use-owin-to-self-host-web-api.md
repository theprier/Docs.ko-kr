---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN을 사용 하 여 ASP.NET Web API 2 자체 호스팅에 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다. Open Web Interface for.NET (OWIN) d...
ms.author: aspnetcontent
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9fba2774e3873d32115a14fa0c84b99466eda04f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830913"
---
<a name="use-owin-to-self-host-aspnet-web-api-2"></a>OWIN를 사용 하 여 ASP.NET Web API 2 자체 호스팅
====================
[Kanchan Mehrotra](https://twitter.com/kanchanmeh)

> 이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.
> 
> [Open Web Interface for.NET](http://owin.org) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN 이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (Visual Studio 2012를 사용 하 여 작동)
> - Web API 2


> [!NOTE]
> 이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다 [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)합니다.


## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

에 **파일** 메뉴에서 클릭 **새로 만들기**, 클릭 **프로젝트**합니다. **설치 된 템플릿**, Visual C#에서 클릭 **Windows** 을 클릭 한 다음 **콘솔 응용 프로그램**합니다. "OwinSelfhostSample" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

[![](use-owin-to-self-host-web-api/_static/image2.png)](use-owin-to-self-host-web-api/_static/image1.png)

## <a name="add-the-web-api-and-owin-packages"></a>웹 API 및 OWIN 패키지를 추가 합니다.

**도구** 메뉴에서 클릭 **라이브러리 패키지 관리자**, 클릭 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

이 WebAPI OWIN selfhost 패키지 및 모든 필수 OWIN 패키지가 설치 됩니다.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>웹 API에 대 한 구성 자체 호스트

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다. 클래스 이름을 `Startup`로 지정합니다.

![](use-owin-to-self-host-web-api/_static/image5.png)

모두이 파일의 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>웹 API 컨트롤러 추가

다음으로, Web API 컨트롤러 클래스를 추가 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다. 클래스 이름을 `ValuesController`로 지정합니다.

모두이 파일의 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-using-httpclient"></a>OWIN 호스트를 시작 하 고 HttpClient를 사용 하 여 요청을 만듭니다

다음을 사용 하 여 모든 Program.cs 파일의 상용구 코드를 대체 합니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

Visual Studio에서 F5 키를 눌러 응용 프로그램을 실행 합니다. 출력은 다음과 같습니다.

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>추가 리소스

[프로젝트 Katana 개요](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure 작업자 역할에서 ASP.NET Web API 호스팅](host-aspnet-web-api-in-an-azure-worker-role.md)
