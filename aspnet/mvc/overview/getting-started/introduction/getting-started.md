---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 시작 | Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2cc9364b815cae0207fc59784303c6a0906f1b94
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578447"
---
<a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 시작
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [consider RP](../../../../includes/razor.md)]

이 자습서에서는 ASP.NET MVC 5 웹 앱 사용 하 여 프로그램을 빌드하는 기본 사항 설명 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)합니다. 이 자습서의 최종 소스 코드에 위치한 [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)합니다.

이 자습서를 통해 작성 했습니다 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )

이 앱을 Azure에 배포 하려면 Azure 계정이 필요 합니다.

- 할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- 할 수 있습니다 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

## <a name="get-started"></a>시작

먼저 [Visual Studio 2017을 설치](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)합니다. 그런 다음 Visual Studio를 엽니다.

Visual Studio IDE 또는 통합된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다. Visual Studio에서 사용할 수 있는 다양 한 옵션을 보여 주는 아래쪽 목록이 있습니다. IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다. 예를 들어, 선택 하는 대신 **새 프로젝트** 에 **시작 페이지**, 메뉴 모음을 사용 하 고 선택할 수 **파일** > **새프로젝트**.

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>첫 번째 앱 만들기

에 **시작 페이지**를 선택 **새 프로젝트**합니다. 에 **새 프로젝트** 대화 상자에서를 **Visual C#** 다음 왼쪽의 범주 **웹**를 선택한 후는 **ASP.NET 웹 응용 프로그램 (.NET Framework)**  프로젝트 템플릿. "MvcMovie" 프로젝트 이름을 선택한 후 **확인**합니다.

![](getting-started/_static/image2.png)

에 **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 선택 **MVC** 를 선택한 후 **확인**합니다.

![](getting-started/_static/image3.png)

있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio! 이는 간단한 "Hello World!" 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.

![](getting-started/_static/image4.png)

**F5** 키를 눌러 디버깅을 시작합니다. 누르면 **F5**, Visual Studio 시작 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 하 고 웹 앱을 실행 합니다. 그런 다음 visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost:port#` 등은 표시 되지 않습니다 및 `example.com`합니다. 있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다. Visual Studio 웹 프로젝트를 실행할 때 임의 포트를 웹 서버에 사용 됩니다. 아래 이미지에서 포트 번호가 1234입니다. 응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.

![](getting-started/_static/image5.png)

이 기본 템플릿을 사용 하면 즉시 `Home`하십시오 `Contact`, 및 `About` 페이지입니다. 위의 이미지에 표시 되지 않으면 합니다 **홈**, **에 대 한**, 및 **연락처** 링크. 브라우저 창의 크기에 따라 다음이 링크를 보려면 탐색 아이콘을 클릭 해야 합니다.

![](getting-started/_static/image6.png)

응용 프로그램 등록 및 로그인 하는 지원도 제공 합니다. 다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 하는 것입니다. ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경해 보겠습니다.

현재 자습서 목록은 참조 하세요 [문서를 권장 하는 MVC](../mvc-learning-sequence.md)합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 참조

라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까? 다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없다면 하나 만들려면 다음 옵션 중 하나를 사용 합니다.

- [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) -Visual Studio 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

> [!div class="step-by-step"]
> [다음](adding-a-controller.md)
