---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: ASP.NET Web API 2 Azure 작업자 역할에 호스트 | Microsoft Docs
author: MikeWasson
description: 이 자습서 OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할에 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다. .NET (OWIN) de에 대 한 웹 인터페이스를 열기...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/02/2014
ms.topic: article
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 7ba1dc850e2f9d9c88e6ddf263a796e1867a98be
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>ASP.NET Web API 2 Azure 작업자 역할에 호스트
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 이 자습서 OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할에 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.
> 
> [.NET 용 웹 인터페이스를 열고](http://owin.org/) (OWIN).NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN를 자체 IIS 외부의 사용자가 소유한 프로세스에는 웹 응용 프로그램을 호스트 하기에 이상적인는 서버에서 웹 응용 프로그램을 분리 하는 OWIN – Azure 작업자 역할 내 예를 들어 있습니다.
> 
> 이 자습서를 사용 하 여 Microsoft.Owin.Host.HttpListener 패키지 자체 OWIN 응용 프로그램을 호스트 하는 데 사용 될 HTTP 서버를 제공 하는 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - Web API 2
> - [Azure SDK for.NET 2.3](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure 프로젝트 만들기

관리자 권한으로 Visual Studio를 시작 합니다. Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.

에 **파일** 메뉴를 클릭 **새로**, 클릭 **프로젝트**합니다. **설치 된 템플릿**, Visual C#, 클릭 **클라우드** 클릭 하 고 **Windows Azure 클라우드 서비스**합니다. "AzureApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 두 번 클릭 **작업자 역할**합니다. 기본 이름 ("WorkerRole1")을 그대로 둡니다. 이 단계는 솔루션에는 작업자 역할을 추가합니다. **확인**을 클릭합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

만든 Visual Studio 솔루션에 두 개의 프로젝트가 포함 되어 있습니다.

- &quot;AzureApp&quot; 역할 및 Azure 응용 프로그램에 대 한 구성을 정의 합니다.
- &quot;WorkerRole1&quot; 작업자 역할에 대 한 코드를 포함 합니다.

일반적으로 단일 역할을 사용 하 여이 자습서는 Azure 응용 프로그램 여러 역할에 포함할 수 있습니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 및 OWIN 패키지 추가

**도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자**, 클릭 **패키지 관리자 콘솔**합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP 끝점을 추가

솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다. 역할 노드를 확장, WorkerRole1, 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

클릭 **끝점**, 클릭 하 고 **끝점 추가**합니다.

에 **프로토콜** 드롭다운 목록에서 선택 "http"입니다. **공용 포트** 및 **개인 포트**, 80을 입력 합니다. 이러한 포트 번호는 다를 수 있습니다. 공용 포트는 클라이언트 역할에는 요청을 보낼 때 사용 합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>Web API에 대 한 구성 자체 호스트

솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다. 클래스 이름을 `Startup`로 지정합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

다음으로이 파일에 있는 상용구 코드의 모든를 대체 합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>웹 API 컨트롤러 추가

다음으로, 웹 API 컨트롤러 클래스를 추가 합니다. WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스**합니다. TestController 클래스를 이름을 지정 합니다. 다음으로이 파일에 있는 상용구 코드의 모든를 대체 합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

간단한 설명을 위해이 컨트롤러 방금 일반 텍스트를 반환 하는 두 개의 GET 메서드를 정의 합니다.

## <a name="start-the-owin-host"></a>OWIN 호스트 시작

WorkerRole.cs 파일을 엽니다. 이 클래스는 작업자 역할 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.

다음 추가 문을 사용 하 여:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

추가 **IDisposable** 멤버는 `WorkerRole` 클래스:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

에 `OnStart` 메서드를 호스트 하려면 다음 코드를 추가 합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp.Start** 메서드 OWIN 호스트를 시작 합니다. 이름에서 `Startup` 클래스는 메서드 형식 매개 변수입니다. 규칙에 따라 호스트 호출 됩니다는 `Configure` 이 클래스의 메서드.

재정의 `OnStop` 를 삭제 하는  *\_앱* 인스턴스:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

WorkerRole.cs에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

솔루션을 작성 하 고 f5 키를 눌러 Azure 계산 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다. 방화벽 설정에 따라 방화벽을 통해 에뮬레이터를 허용 하도록 할 수 있습니다.

> [!NOTE]
> 다음과 같은 예외가 발생 하는 경우를 참조 하세요 [이 블로그 게시물](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) 해결 방법에 대 한 합니다. "파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.Owin, 버전 = 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35' 또는 해당 종속성 중 하나 합니다. 찾은 어셈블리의 매니페스트 정의가 어셈블리 참조를 일치 하지 않습니다. (HRESULT의 예외: 0x80131040) "


계산 에뮬레이터는 끝점에 로컬 IP 주소를 할당합니다. 계산 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다. 작업 표시줄 알림 영역에서에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **계산 에뮬레이터 UI 표시**합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

서비스 배포, 배포 [id] 서비스 세부 정보 아래에 IP 주소를 찾습니다. 웹 브라우저를 열고 http:// 이동<em>주소</em>/테스트/1, 여기서 <em>주소</em> 는 계산 에뮬레이터에서 할당 된 IP 주소 예를 들어 `http://127.0.0.1:80/test/1`합니다. Web API 컨트롤러에서 응답이 표시 됩니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Azure에 배포

이 단계에서는 Azure 계정이 있어야 합니다. 아직 없는 하나, 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.

솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Azure 계정에 로그인 하지 않은 경우 클릭 **로그인**합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

에 로그인 한 후 구독을 선택 하 고 클릭 **다음**합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

클라우드 서비스에 대 한 이름을 입력 하 고 지역을 선택 합니다. **만들기**를 클릭합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

**게시**를 클릭합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

Azure 활동 로그 창에는 배포의 진행률이 표시 됩니다. 로 이동 하는 응용 프로그램을 배포할 때 http://appname.cloudapp.net/test/1합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>추가 자료

- [프로젝트 Katana 개요](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub에서 Katana 프로젝트](https://github.com/aspnet/AspNetKatana)
