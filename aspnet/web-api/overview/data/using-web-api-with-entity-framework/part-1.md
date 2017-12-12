---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: "Web API 2 사용 하 여 Entity framework 6 | Microsoft Docs"
author: MikeWasson
description: "이 자습서에 대해서는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램을 만드는 기본 사항 백 엔드 설명 됩니다. 이 자습서는 Entity Framework 6을 사용 하 여 데이터 레이아웃에 대 한 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 42139f8c158dd84cfc30f23c013343348b0c008a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-web-api-2-with-entity-framework-6"></a>Web API 2 사용 하 여 Entity framework 6
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

> 이 자습서에 대해서는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램을 만드는 기본 사항 백 엔드 설명 됩니다. 자습서는 클라이언트 쪽 JavaScript 응용 프로그램에 대 한 데이터 계층 및 Knockout.js에 대 한 Entity Framework 6을 사용합니다. 또한 자습서에는 Azure 앱 서비스 웹 앱에 앱을 배포 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2.1
> - [Visual Studio 2013 업데이트 2](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - Entity Framework 6
> - .NET 4.5
> - [Knockout.js](http://knockoutjs.com/) 3.1


이 자습서 Entity Framework 6 ASP.NET Web API 2를 사용 하 여 백 엔드 데이터베이스를 조작 하는 웹 응용 프로그램을 만듭니다. 만들 응용 프로그램의 스크린 샷을 다음과 같습니다.

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

앱을 사용 하는 단일 페이지 응용 프로그램 (SPA) 디자인 합니다. "단일 페이지 응용 프로그램"은 하나의 HTML 페이지를 로드 하 고 다음 새 페이지를 로드 하는 대신 해당 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다. 첫 페이지를 로드 한 후 응용 프로그램 AJAX 요청을 통해 서버와 통신 합니다. AJAX 요청 UI를 업데이트 하는 앱 사용 하 여 JSON 데이터를 반환 합니다.

AJAX 새로 만들었거나, 않지만 오늘 쉽게 작성 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크는 합니다. 이 자습서에서는 [Knockout.js](http://knockoutjs.com/), 하지만 JavaScript 클라이언트 프레임 워크를 사용할 수 있습니다.

다음은이 응용 프로그램에 대 한 기본 구성 요소입니다.

- ASP.NET MVC HTML 페이지를 만듭니다.
- ASP.NET Web API AJAX 요청을 처리 하 고 JSON 데이터를 반환 합니다.
- Knockout.js 데이터 바인딩 HTML 요소는 JSON 데이터에 있습니다.
- Entity Framework 데이터베이스에 통신 합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 응용 프로그램 참조

실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까? 다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [무료 Azure 계정을 개설](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.

## <a name="create-the-project"></a>프로젝트 만들기

Visual Studio를 엽니다. **파일** 메뉴 선택 **새로**을 선택한 후 **프로젝트**합니다. (키를 누르거나 **새 프로젝트** 시작 페이지에서.)

에 **새 프로젝트** 대화 상자에서 클릭 **웹** 왼쪽된 창에서 및 **ASP.NET 웹 응용 프로그램** 가운데 창에서. BookService 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

[![](part-1/_static/image4.png)](part-1/_static/image3.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서는 **웹 API** 템플릿.

[![](part-1/_static/image6.png)](part-1/_static/image5.png)

Azure 앱 서비스에서 프로젝트를 호스트 하려는 경우 둡니다는 **클라우드의 호스트에에서** 확인란을 선택 된 합니다.

클릭 **확인** 프로젝트를 만듭니다.

## <a name="configure-azure-settings-optional"></a>(선택 사항) Azure 설정 구성

두 었으 면는 **클라우드의 호스트에에서** 옵션 선택 하면 Visual Studio Microsoft Azure에 로그인 하 라는 메시지가 나타납니다

[![](part-1/_static/image8.png)](part-1/_static/image7.png)

Azure에 로그인 한 후 Visual Studio 웹 응용 프로그램을 구성 하 라는 메시지를 표시 합니다. 사이트에 대 한 이름을 입력 하 고 Azure 구독을 선택한 지리적 지역을 선택 합니다. 아래 **데이터베이스 서버**선택, **새 서버 만들기**합니다. 관리자 사용자 이름 및 암호를 입력 합니다.

[![](part-1/_static/image10.png)](part-1/_static/image9.png)

>[!div class="step-by-step"]
[다음](part-2.md)
