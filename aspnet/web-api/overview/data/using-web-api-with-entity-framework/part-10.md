---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Azure 앱 서비스를 Azure에 앱 게시 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: cc8a9199144e9fac041435938ea8899374ea199f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30867816"
---
<a name="publish-the-app-to-azure-azure-app-service"></a>Azure 앱 서비스를 Azure에 앱을 게시
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

마지막 단계로, Azure에 응용 프로그램을 게시 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

![](part-10/_static/image1.png)

클릭 하면 **게시** 호출는 **웹 게시** 대화 상자. 선택한 경우에 **클라우드의 호스트에에서** 프로젝트에 다음 연결 처음 만든 시점과 설정이 이미 구성 되었습니다. 이 경우 클릭는 **설정** 탭 하 고 확인 &quot;Code First 마이그레이션 실행&quot;합니다. (검사 하지 않을 경우 **클라우드의 호스트에에서** 를 시작할 때의 단계에 따라 다음의 [다음 섹션](#new-website).)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

앱을 배포 하려면 **게시**합니다. 게시 진행률을 볼 수는 **웹 게시 동작** 창. (에서 **보기** 메뉴 선택 **다른 창**을 선택한 후 **웹 게시 동작**.)

![](part-10/_static/image4.png)

Visual Studio에서 앱 배포를 완료 하는 경우의 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL에 열리고 만든 응용 프로그램은 클라우드에서 실행 중인. 브라우저 주소 표시줄에 URL에서 사이트 인터넷에서 로드 되 고 있음을 보여 줍니다.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>새 웹 사이트에 배포

선택 하지 않은 경우 **클라우드의 호스트에에서** 프로젝트를 처음 만들 경우 새 웹 응용 프로그램을 지금 구성할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 선택 된 **프로필** 탭을 클릭 **Microsoft Azure 웹 사이트**합니다. Azure에 로그인 되어 현재 있지, 로그인 하 라는 메시지가 표시 됩니다.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

에 **기존 웹 사이트** 대화 상자에서 클릭 **새로**합니다.

![](part-10/_static/image9.png)

사이트 이름을 입력 합니다. Azure 구독 및 지역 선택 합니다. 아래 **데이터베이스 서버**선택, **새 서버 만들기**을 하거나 기존 서버를 선택 합니다. **만들기**를 클릭합니다.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

클릭는 **설정** 탭 하 고 확인 &quot;Code First 마이그레이션 실행&quot;합니다. 클릭 **게시**합니다.

> [!div class="step-by-step"]
> [이전](part-9.md)
