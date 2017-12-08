---
uid: mvc/overview/getting-started/introduction/getting-started
title: "ASP.NET MVC 5 시작 | Microsoft Docs"
author: Rick-Anderson
description: "참고:이 자습서의 업데이트 된 버전은 Visual Studio 2015를 사용 하 여 사용할 수입니다. 새 자습서에서는 ASP.NET Core MVC 6 많은 improvem 제공 하는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 8f2cb9b3f14ad95acd9e4c7a0ed26228d3c480e0
ms.sourcegitcommit: ec9371e2fbfcb8d62e7e7cae69e7752f3f205385
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2017
---
<a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 시작
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE[consider RP](../../../../includes/razor.md)]

 
 이 자습서는 ASP.NET MVC 5 웹 응용 프로그램 사용 하 여 프로그램을 구축 하는 기초 업무량이 [Visual Studio 2017](https://www.visualstudio.com/)합니다. 자습서에 대 한 최종 소스에 있는 [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)
 
 
 이 자습서에 의해 작성 되었으므로 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )
 
 이 응용 프로그램을 Azure에 배포 하려면 Azure 계정이 필요 합니다.
 
 - 있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
 - 있습니다 수 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.


## <a name="getting-started"></a>시작

설치 하 고 실행 하 여 시작 [Visual Studio 2017](https://www.visualstudio.com/)합니다.

Visual Studio IDE, 또는 통합된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 있는 IDE를 사용 합니다. Visual Studio에는 사용할 수 있는 다양 한 옵션을 보여 주는 아래 목록입니다. IDE에서 작업을 수행 하는 다른 방법은 제공 하는 메뉴가 있습니다. (선택 하는 대신 예를 들어 **새 프로젝트** 에서 **시작** 페이지 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)

   
![](getting-started/_static/image1.png)  
 

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

클릭 **새 프로젝트**을 다음 선택 Visual C#의 왼쪽에서 다음 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램 (.NET Framework)**합니다. "MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![](getting-started/_static/image2.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 클릭 **MVC** 클릭 하 고 **확인**합니다.

![](getting-started/_static/image3.png)

Visual Studio 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 서식 파일을 사용 해야 하므로 응용 프로그램 현재 아무것도 수행 하지 않고! 간단한 "Hello World!"입니다. 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.

![](getting-started/_static/image4.png)

디버깅을 시작 하려면 f5 키를 클릭 합니다. F 5를 눌러 Visual Studio를 시작 하면 [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 웹 앱을 실행 합니다. 그런 다음 visual Studio는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄을 `localhost:port#` 와 하지 것 같은 `example.com`합니다. 때문 `localhost` 항상 방금 빌드한 응용 프로그램을 실행 중인이 예제의 자신의 로컬 컴퓨터를 가리킵니다. Visual Studio 웹 프로젝트를 실행 하면 임의의 포트는 웹 서버에 사용 됩니다. 아래 이미지에 포트 번호가 1234입니다. 응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.

![](getting-started/_static/image5.png)

즉시이 기본 템플릿을 사용 하면 집, 연락처 및 정보 페이지입니다. 위의 그림은 표시 되지 않습니다는 **홈**, **에 대 한** 및 **연락처** 링크 합니다. 브라우저 창의 크기에 따라 이러한 링크를 보려면 탐색 아이콘을 클릭 해야 할 수 있습니다.

![](getting-started/_static/image6.png)  

또한 응용 프로그램에서는 등록 및 로그인를 합니다. 이 응용 프로그램 작동 방식을 변경 하 고 ASP.NET MVC에 대해 약간 자세한 하는 다음 단계가입니다. ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경 해보겠습니다.

목록이 현재 자습서에 대 한 참조 [권장 하는 문서 MVC](../mvc-learning-sequence.md)합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 응용 프로그램 참조

실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까? 다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [무료 Azure 계정을 개설](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.

>[!div class="step-by-step"]
[다음](adding-a-controller.md)
