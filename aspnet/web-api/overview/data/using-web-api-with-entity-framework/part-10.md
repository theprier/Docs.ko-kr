---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Azure의 Azure App Service에 앱 게시 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: 0290b392c1b292d0f3cc080dbfa25ec6103b2751
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400806"
---
<a name="publish-the-app-to-azure-azure-app-service"></a>Azure의 Azure App Service에 앱 게시
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

마지막 단계로, Azure에 응용 프로그램을 게시 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

![](part-10/_static/image1.png)

클릭 **게시** 를 호출 하는 **웹 게시** 대화 합니다. 선택한 경우 **클라우드에서 호스트** 때 먼저 프로젝트에 다음 연결을 만든 설정이 이미 구성 되었습니다. 이 경우 클릭 합니다 **설정을** 탭을 확인 &quot;Execute Code First Migrations&quot;합니다. (확인 하지 않은 경우 **클라우드에서 호스트** 를 시작할 때의 단계에 따라 다음을 [다음 섹션에서는](#new-website).)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

앱을 배포 하려면 **게시**합니다. 게시 진행률을 볼 수는 **웹 게시 활동** 창입니다. (에서 합니다 **보기** 메뉴에서 **다른 Windows**을 선택한 후 **웹 게시 활동**.)

![](part-10/_static/image4.png)

Visual Studio는 앱 배포 완료 되 면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열립니다 및 사용자가 만든 응용 프로그램은 이제 클라우드에서 실행 됩니다. 브라우저 주소 표시줄에서 URL 사이트는 인터넷에서 로드 되 고 있음을 보여 줍니다.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>새 웹 사이트에 배포

확인 하지 않은 경우 **클라우드에서 호스트** 프로젝트를 처음 만들 때 새 웹 앱을 지금 구성할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 선택 된 **프로필** 탭을 클릭 **Microsoft Azure Websites**합니다. Azure에 로그인 현재 없는 경우 로그인을 묻는 메시지가 나타납니다.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

에 **기존 웹 사이트** 대화 상자에서 클릭 **새로 만들기**합니다.

![](part-10/_static/image9.png)

사이트 이름을 입력 합니다. Azure 구독 및 지역을 선택 합니다. 아래 **데이터베이스 서버**를 선택 **새 서버 만들기**, 또는 기존 서버를 선택 합니다. **만들기**를 클릭합니다.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

클릭 합니다 **설정을** 탭을 확인 &quot;Execute Code First Migrations&quot;합니다. 누른 **게시**합니다.

> [!div class="step-by-step"]
> [이전](part-9.md)
