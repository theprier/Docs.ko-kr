---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 사용자 지정 경로 제약 조건 (VB) 만들기 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다. 간단한 구현 되는 경로 방지 하는 사용자 지정 제약 조건 w 일치 하는 중...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: d088380152adcb025857176b4396cab48fa64b66
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835475"
---
<a name="creating-a-custom-route-constraint-vb"></a>사용자 지정 경로 제약 조건 (VB) 만들기
====================
[Stephen walther가](https://github.com/StephenWalther)

> Stephen walther가 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다. 경로 원격 컴퓨터에서 브라우저 요청이 수행 될 때 일치 하는 것을 방지 하는 간단한 사용자 지정 제약 조건을 구현 합니다.


사용자 지정 경로 제약 조건을 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다. 사용자 지정 경로 제약 조건을 사용 하면 일부 사용자 지정 조건 일치 하지 않으면 일치에서 경로 방지할 수 있습니다.

이 자습서에서는 Localhost 경로 제약 조건을 만듭니다. Localhost 경로 제약 조건에는 로컬 컴퓨터에서 수행 된 요청의와 일치 합니다. 인터넷을 통해 원격 요청에서 일치 되지 않습니다.

또한 IRouteConstraint 인터페이스를 구현 하 여 사용자 지정 경로 제약 조건을 구현 합니다. 다음은 단일 메서드를 설명 하는 매우 간단한 인터페이스입니다.

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

메서드는 부울 값을 반환 합니다. False를 반환 하는 경우 제약 조건이 있는 연결 된 경로 브라우저 요청이 일치 하지 않습니다.

Localhost 제약 조건 목록 1에 포함 됩니다.

**1-LocalhostConstraint.vb 나열**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

목록 1에서 제약 조건을 HttpRequest 클래스에 의해 노출 IsLocal 속성을 활용 합니다. 요청 IP 주소가 두 127.0.0.1 또는 요청의 IP 서버의 IP 주소와 같은 경우이 속성은 true를 반환 합니다.

Global.asax 파일에 정의 된 경로 내에서 사용자 지정 제약 조건을 사용할 수 있습니다. 목록 2에서 Global.asax 파일 누구나 로컬 서버에서 요청을 할 하지 않는 한 관리 페이지를 요청 하지 않도록 하려면 Localhost 제약 조건을 사용 합니다. 예를 들어 원격 서버에서 수행 하는 경우 /Admin/DeleteAll 요청 실패 합니다.

**2-Global.asax 나열**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

Localhost 제약 조건은 관리 경로 정의에 사용 됩니다. 원격 브라우저 요청에서이 경로 일치 시킬 수 없습니다. 그러나 궁극적인 Global.asax에 정의 된 다른 경로 동일한 요청에 일치 될 수 있습니다. 제약 조건으로 인해 일치 요청에서 특정 경로 Global.asax 파일에 정의 된 모든 경로 이해 하는 것이 반드시 합니다.

기본 경로 주석 처리 된 목록 2의 Global.asax 파일에서 확인할 수 있습니다. 기본 경로 포함 하는 경우 기본 경로 요청 관리 컨트롤러에 대 한 검색 합니다. 이 경우 원격 사용자가 해당 요청에는 관리 경로 일치 하지 않습니다. 경우에 관리 컨트롤러의 작업을 계속 호출할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-a-route-constraint-vb.md)
