---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 웹 서비스 백 엔드 (VB)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기 | Microsoft Docs
author: wenz
description: 확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (Windows 및 다른 운영 체제에 있음)을 더 많은 c 중일 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 690fd89c552407ec5d77419aae2488e4832efe44
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871391"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>웹 서비스 백 엔드 (VB)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (에 있는 Windows 및 기타 운영 체제) 중일 더 많은 방법을 잘 알고 있습니다. 기본적으로 항상 증가 또는 감소 값을 1, NumericUpDown 컨트롤 하지만 더 많은 융통성을 증명 하는 웹 서비스입니다.


## <a name="overview"></a>개요

확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (에 있는 Windows 및 기타 운영 체제) 중일 더 많은 방법을 잘 알고 있습니다. 기본적으로는 `NumericUpDown` 하지만 더 많은 융통성을 증명 하는 웹 서비스 제어는 항상 증가 또는 값 1, 감소 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 Toolkit에 포함 되어는 `NumericUpDown` extender를 텍스트 상자에 두 개의 단추를 자동으로 추가: 감소에 대 한 해당 값이 증가 대 한 합니다. 그러나 컨트롤 웹 서비스 호출 (또는 페이지 메서드 호출)도 지원합니다. 때마다의 위 또는 아래로 단추를 클릭 하면 JavaScript 코드는 웹 서버에 연결 하 고 있는 메서드를 실행 합니다. 메서드 시그니처는 다음 중:

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` 인수는 텍스트 상자의; 현재 값의 `tag` 특성은의 속성으로 설정할 수 있는 추가 컨텍스트 데이터는 `NumericUpDown` extender (하지만 필요 하지 않습니다).

이 샘플에 대 한 숫자 위로/아래로 컨트롤은 허용 2의 거듭제곱 값: 1, 2, 4, 8, 16, 32, 64, 및 등입니다. 따라서 메서드가 값을 늘리려면 다음 사용자가를 실행 해야 double 이전 값입니다. 또 다른 방법은 두 값을 나눕니다 해야 합니다. 따라서 여기에 전체 웹 서비스:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

마지막으로 새 ASP.NET 페이지를 만듭니다. 필요한 일반적으로 `ScriptManager` 컨트롤은 `TextBox` 제어 및 `NumericUpDownExtender` 컨트롤입니다. 후자의 경우 웹 서비스 정보를 제공 해야 합니다.

- `ServiceDownMethod` 웹 메서드 또는 메서드 페이지를 아래로의 이름
- `ServiceDownPath` 아래쪽 서비스 메서드로; 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우 생략
- `ServiceUpMethod` 위쪽의 이름을 웹 메서드 또는 메서드를 페이지
- `ServiceUpPath` 최신 서비스 메서드로; 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우 생략

페이지에 대 한 전체 태그는 다음과 같습니다.

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

페이지를 실행 하는 경우 어떻게 값 텍스트 상자에 항상 두 배로 만듭니다 위쪽 단추를 클릭 하 고는 아래쪽 단추를 클릭할 때 반 축소 확인 합니다.


[![2의 거듭제곱 번호만 표시](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

2의 거듭제곱 번호만 표시 ([전체 크기 이미지를 보려면 클릭](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
