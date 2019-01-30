---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 사용 하 여 Web API 2 사용 하 여 | Microsoft Docs
author: MikeWasson
description: 이 자습서는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램 만들기의 기본 사항을 백 엔드 배우게를 보여 줍니다. 이 자습서에서는 데이터 레이아웃에 대 한 Entity Framework 6을 사용 하는 중...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 266c808e3525787181038d2de473194989039e02
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236525"
---
<a name="using-web-api-2-with-entity-framework-6"></a>Entity Framework 6 사용 하 여 Web API 2 사용 하 여
====================

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

> 이 자습서에서는 백 엔드는 ASP.NET Web API를 사용 하 여 웹 응용 프로그램 만들기의 기본 사항을 설명 합니다. 자습서를 사용 하면 데이터 계층 Knockout.js 위해 Entity Framework 6을 사용 하는 클라이언트 쪽 JavaScript 응용 프로그램에 대 한 합니다. 또한 자습서에는 Azure App Service Web Apps에 앱을 배포 하는 방법을 보여 줍니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
> - Web API 2.1
> - Visual Studio 2017 (Visual Studio 2017 다운로드 [여기](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.7
> - [Knockout.js](http://knockoutjs.com/) 3.1

이 자습서에서는 백 엔드 데이터베이스를 조작 하는 웹 응용 프로그램을 만드는 Entity Framework 6을 사용 하 여 ASP.NET Web API 2를 사용 합니다. 만들려는 응용 프로그램의 스크린샷은 다음과 같습니다.

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

앱에는 단일 페이지 응용 프로그램 (SPA) 디자인을 사용합니다. "단일 페이지 응용 프로그램"은 하나의 HTML 페이지를 로드 하 고 그런 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반 용어입니다. 초기 페이지 로드 후 앱은 AJAX 요청을 통해 서버를 사용 하 여 설명합니다. AJAX 요청 앱 UI 업데이트를 사용 하 여 JSON 데이터를 반환 합니다.

AJAX 새 없지만 오늘 가지 쉽게 구축 하 고 대형 정교한 SPA 응용 프로그램을 관리 하는 JavaScript 프레임 워크입니다. 이 자습서에서는 [Knockout.js](http://knockoutjs.com/), 하지만 JavaScript 클라이언트 프레임 워크를 사용할 수 있습니다.

이 앱에 대 한 기본 구성 요소는 다음과 같습니다.

- ASP.NET MVC는 HTML 페이지를 만듭니다.
- ASP.NET Web API는 AJAX 요청을 처리 하 고 JSON 데이터를 반환 합니다.
- Knockout.js 데이터 바인딩 HTML 요소를 JSON 데이터로 합니다.
- Entity Framework는 데이터베이스에 설명합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 참조

라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까? 다음 단추를 선택 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션:

- [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio를 엽니다. **파일** 메뉴에서 **새로 만들기**을 선택한 후 **프로젝트**합니다. (선택 하거나 **새 프로젝트** 시작 페이지에서.)

에 **새 프로젝트** 대화 상자에서 **웹** 왼쪽된 창에서와 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 가운데 창에서. 프로젝트 이름을 **BookService** 선택한 **확인**합니다.

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **Web API** 템플릿.

[![](part-1/_static/image12.png)](part-1/_static/image12.png)


**확인**을 선택하여 프로젝트를 만듭니다.

## <a name="configure-azure-settings-optional"></a>(선택 사항) Azure 설정 구성

프로젝트를 만든 후 언제 든 지 Azure App Service Web Apps에 배포할 수 있습니다. 

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 하면 프로젝트를 마우스 **게시**합니다.

2. 표시 되는 창에서 선택 **시작**합니다. 합니다 **게시 대상 선택** 대화 상자가 나타납니다.

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. **프로필 만들기**를 선택합니다. **App Service 만들기** 대화 상자가 나타납니다.

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   기본값을 적용 하거나 응용 프로그램 이름, 리소스 그룹을 호스팅 계획, Azure 구독 및 지역에 대 한 다른 값을 입력 합니다. 

4. 선택 **SQL database 만들기**합니다. 합니다 **SQL Server 구성** 대화 상자가 나타납니다. 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   기본값을 사용 하거나 다른 값을 입력 합니다. 입력을 **관리자 사용자 이름** 하 고 **관리자 암호** 새 데이터베이스에 대 한 합니다. 선택 **확인** 완료 되 면 합니다. 합니다 **App Service 만들기** 페이지 다시 나타납니다.

5. 선택 **만들기** 프로필을 만들려고 합니다. 배포 진행에서 중임을 나타내는 오른쪽 아래 모서리에 메시지가 표시 됩니다. 짧은 시간이 지나면 합니다 **게시** 창이 다시 나타납니다.

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    앱을 배포 하 여 만든 프로필 출시 되었습니다. 


> [!div class="step-by-step"]
> [다음](part-2.md)
