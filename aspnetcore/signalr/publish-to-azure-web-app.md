---
title: 게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱
author: tdykstra
description: 게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/20/2018
uid: signalr/publish-to-azure-web-app
ms.openlocfilehash: a6a0e44f5c67fefdac6bd26b3772c23e75f8bfc1
ms.sourcegitcommit: 32f5ee0690604d451f61e9a5c28881c9fcf85738
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454728"
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a>게시는 ASP.NET Core SignalR 앱을 Azure 웹 앱

[Azure Web App](/azure/app-service/app-service-web-overview) 되는 [Microsoft 클라우드 컴퓨팅](https://azure.microsoft.com/) ASP.NET Core를 포함 하 여 웹 앱을 호스트 하기 위한 플랫폼 서비스입니다.

> [!NOTE]
> 이 문서에서는 Visual Studio에서 ASP.NET Core SignalR 앱을 게시 합니다. 방문 [azure SignalR service](https://azure.microsoft.com/en-gb/services/signalr-service?) SignalR을 사용 하 여 Azure에 대 한 자세한 내용은 합니다.

## <a name="publish-the-app"></a>앱 게시

Visual Studio를 Azure 웹 앱 게시에 대 한 기본 제공 도구를 제공합니다. Visual Studio Code 사용자 사용할 수 있습니다 [Azure CLI](/cli/azure) Azure에 앱을 게시 하는 명령입니다. 이 문서에서는 Visual Studio에서 도구를 사용 하 여 게시에 대해 설명 합니다. Azure CLI를 사용 하 여 앱을 게시 하려면 참조 [명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 앱을 게시](/azure/app-service/app-service-web-get-started-dotnet)합니다.

프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택한 **게시**합니다. 확인 **새로 만들기** 체크 인 합니다 **게시 대상 선택** 대화 상자에서 선택한 **게시**합니다.

![게시 대상 선택](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

다음 정보를 입력 합니다 **App Service 만들기** 대화 상자와 선택 **만들기**합니다.

| 항목 | 설명 |
| ---- | ----------- |
| **앱 이름** | 앱의 고유 이름입니다. |
| **구독** | 앱을 사용 하는 Azure 구독입니다. |
| **리소스 그룹** | 앱이 속해 있는 관련된 리소스의 그룹입니다.  |
| **호스팅 계획** | 웹 앱에 대 한 가격 책정 계획입니다. |

![App service 만들기](publish-to-azure-web-app/_static/create-app-service-dialog.png)

Visual Studio에는 다음 작업을 완료 합니다.

* 게시 프로필을 만들고 게시 설정을 포함 합니다.
* 만들거나 기존 사용 *Azure Web App* 제공된 된 정보를 사용 하 여 합니다.
* 앱을 게시합니다.
* 게시 된 웹 앱 로드를 사용 하 여 브라우저를 시작 합니다.

앱에 대 한 URL의 형식을 확인할 수 있습니다 *{앱 이름}.azurewebsites.net*합니다. 예를 들어, 명명 된 앱 `SignalRChattR` 같은 URL이 `https://signalrchattr.azurewebsites.net`합니다.

HTTP 502.2 오류가 발생 하는 경우 참조 [Azure App Service에 ASP.NET Core 배포 미리 보기 릴리스](xref:host-and-deploy/azure-apps/index) 해결 합니다.

## <a name="configure-signalr-web-app"></a>SignalR 웹 앱 구성

Azure 웹 앱을가지고 있어야 게시 된 ASP.NET Core SignalR 앱 [ARR 선호도](https://en.wikipedia.org/wiki/Application_Request_Routing) 사용 하도록 설정 합니다. [Websocket](xref:fundamentals/websockets) 하면 Websocket 전송에서 함수를 허용 하도록 설정 해야 합니다.

Azure portal로 이동 **앱 설정** 웹 앱에 대 한 합니다. 설정 **Websocket** 를 **에**를 확인 하 고 **ARR 선호도** 는 **에서**합니다.

![Azure portal에서 azure 웹 앱 설정](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 Websocket 및 다른 전송 [App Service 계획에 따라 제한 됩니다](/azure/azure-subscription-service-limits#app-service-limits)합니다.

## <a name="related-resources"></a>관련 참고 자료

* [명령줄 도구를 사용 하 여 Azure에 ASP.NET Core 앱 게시](/azure/app-service/app-service-web-get-started-dotnet)
* [Visual Studio 사용 하 여 Azure에 ASP.NET Core 앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)
* [호스트 및 Azure에서 ASP.NET Core 미리 보기 앱 배포](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
