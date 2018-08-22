---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 사용자 지정 경로 (C#) 만들기 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다. 이 자습서에서는 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 1d7a25f9d257320c252408ae251e2f9f620930d8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829624"
---
<a name="creating-custom-routes-c"></a>사용자 지정 경로 만들기 (C#)
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다. 이 자습서에서는 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법을 알아봅니다.


이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법을 알아봅니다. 사용자 지정 경로 사용 하 여 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법에 알아봅니다.

많은 간단한 ASP.NET MVC 응용 프로그램에 대 한 기본 경로 테이블을 문제 없이 작동 합니다. 그러나 라우팅 요구를 특수 발견할 수 있습니다. 이 경우 사용자 지정 경로 만들 수 있습니다.

예를 들어 블로그 응용 프로그램을 빌드하고 있다고 가정해 보겠습니다. 다음과 같은 들어오는 요청을 처리 하는 것이 좋습니다.

월 보관 2009 년 12-25-

날짜에 해당 하는 블로그 항목을 반환 하려는 사용자가이 요청에 입력 하면 2009 년 12 월 25입니다. 이 유형의 요청을 처리 하기 위해 사용자 지정 경로를 만들고 지정 해야 합니다.

목록 1에서 Global.asax 파일에 블로그, /Archive/ 처럼 보이는 요청을 처리는 명명 된 새 사용자 지정 경로*입력 날짜*합니다.

**1-(사용자 정의 경로)와 함께 Global.asax 나열**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

경로 테이블에 추가 하는 경로 순서가 중요 합니다. 이 새 사용자 지정 블로그 경로 기존 기본 경로 앞에 추가 됩니다. 순서 반대로 하는 경우 다음 기본 경로 항상 호출 됩니다는 사용자 지정 경로 대신 합니다.

사용자 지정 블로그 경로/보관/로 시작 하는 모든 요청을 찾습니다. 따라서 다음 Url은 모두 일치합니다.

- 월 보관 2009 년 12-25-

- / 보관/10 2004 년 6 월 일

- / 보관/apple

사용자 지정 경로 들어오는 요청 archive 컨트롤러에 매핑되고 Entry() 작업을 호출 합니다. Entry() 메서드가 호출 될 때 입력 날짜 entryDate 명명 된 매개 변수로 전달 됩니다.

목록 2의 컨트롤러를 사용 하 여 블로그 사용자 지정 경로 사용할 수 있습니다.

**2-ArchiveController.cs 나열**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

목록 2에서 Entry() 메서드를 DateTime 형식의 매개 변수를 허용 하는지 확인 합니다. MVC 프레임 워크는 입력 날짜 URL에서 날짜/시간 값으로 자동 변환 하지 못합니다. URL에서 항목 날짜 매개 변수를 날짜/시간으로 변환할 수 없습니다, 오류 발생 (그림 1 참조).

**그림 1-매개 변수 변환 오류**


[![새 프로젝트 대화 상자](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**그림 01**: 매개 변수 변환에서 오류 ([큰 이미지를 보려면 클릭](creating-custom-routes-cs/_static/image2.png))


## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 경로 만드는 방법을 보여 주기 위해 했습니다. 블로그 항목을 나타내는 Global.asax 파일에 경로 테이블에 사용자 지정 경로 추가 하는 방법을 알아보았습니다. 블로그 항목에 대 한 요청 ArchiveController 라는 컨트롤러 및 Entry() 라는 컨트롤러 작업에 매핑하는 방법에 설명 했습니다.

> [!div class="step-by-step"]
> [이전](aspnet-mvc-controllers-overview-cs.md)
> [다음](creating-a-route-constraint-cs.md)
