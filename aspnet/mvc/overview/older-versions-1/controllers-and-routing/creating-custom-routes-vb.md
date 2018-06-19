---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 사용자 지정 경로 (VB)를 만드는 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다. 이 자습서에서는 Global.asax 파일에 기본 경로 테이블을 수정 하는 방법에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2009
ms.topic: article
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: e827725ab7ce54c86ae9f4193d0a8a7ef4af8512
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872327"
---
<a name="creating-custom-routes-vb"></a>사용자 지정 경로 (VB) 만들기
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다. 이 자습서에서는 Global.asax 파일에 기본 경로 테이블을 수정 하는 방법에 설명 합니다.


이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 설명 합니다. 사용자 지정 경로 사용 하 여 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법을 배웁니다.

ASP.NET MVC 응용 프로그램 기본 경로 테이블 문제 없이 작동 합니다. 라우팅 요구를 특수 발견할 수 있습니다. 이 경우 사용자 지정 경로 만들 수 있습니다.

예를 들어 작성할 수 있도록 블로그 응용 프로그램을 가정해 보세요. 다음과 같은 들어오는 요청을 처리 하도록 설정할 수 있습니다.

/ 보관/12-25-2009

날짜에 해당 하는 블로그 항목을 반환 하려면 사용자가이 요청을 입력 12/25/2009 합니다. 이 유형의 요청을 처리 하려면 사용자 지정 경로를 만들 필요 합니다.

블로그, /Archive/ 처럼 보이는 핸들이 요청 라는 새 사용자 지정 경로 포함 하는 목록 1의 Global.asax 파일*게시일*합니다.

**1-Global.asax (된 사용자 지정 경로)를 나열합니다.**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

경로 테이블에 추가 하는 경로 순서가 중요 합니다. 이 새 사용자 지정 블로그 경로 기존 기본 경로 앞에 추가 됩니다. 순서를 반대로 하는 경우 다음 기본 경로 항상 호출 됩니다는 대신 사용자 지정 경로.

사용자 지정 블로그 경로/보관/로 시작 하는 모든 요청을 찾습니다. 따라서 다음 Url의 모든 일치합니다.

- / 보관/12-25-2009

- / 보관/10-6-2004

- / 보관/apple

사용자 지정 경로 들어오는 요청 archive 컨트롤러에 매핑하고 Entry() 작업을 호출 합니다. Entry() 메서드를 호출할 때 입력 날짜 entryDate 명명 된 매개 변수로 전달 됩니다.

목록 2에 컨트롤러와 블로그 사용자 지정 경로 사용할 수 있습니다.

**2-ArchiveController.vb 나열**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

알림 목록 2에서 Entry() 메서드는 날짜/시간 형식의 매개 변수를 받아들입니다. MVC 프레임 워크는 입력 날짜 URL에서 날짜/시간 값으로 자동 변환 합니다. URL에서 항목 날짜 매개 변수는 DateTime로 변환할 수 없습니다, 오류 발생 (그림 1 참조).

**그림 1-오류를 매개 변수를 변환 하 여**


[![새 프로젝트 대화 상자](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**그림 01**: 매개 변수 변환에서 오류 ([전체 크기 이미지를 보려면 클릭](creating-custom-routes-vb/_static/image2.png))


## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 경로 만드는 방법을 보여 주기 위해 했습니다. 블로그 항목을 표시 하는 Global.asax 파일에 경로 테이블에 사용자 지정 경로 추가 하는 방법을 배웠습니다. ArchiveController 라는 컨트롤러 및 컨트롤러 작업이 Entry() 라는 블로그 항목에 대 한 요청을 매핑하는 방법에 설명 했습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-controller-overview-vb.md)
> [다음](creating-a-route-constraint-vb.md)
