---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[어떻게 할까요?] Reponse.Filter 속성을 사용 하 여 ASP.NET 페이지의 HTML 바꾸기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오 Chris Pels을 가로채는 HTML 페이지로 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다. 먼저 샘플 페이지를 w를 만듭니다...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 0e8ae8b62bbb4ac1fc7e942cf3dd0438383cb510
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827782"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[어떻게 할까요?] Reponse.Filter 속성을 사용 하 여 ASP.NET 페이지의 HTML 바꾸기
====================
[Chris Pels](https://twitter.com/chrispels)

이 비디오 Chris Pels을 가로채는 HTML 페이지로 전송 되 고 alter Reponse.Filter 속성을 사용 하는 방법을 보여 줍니다. 먼저 샘플 페이지는 몇 가지 간단한 텍스트를 사용 하 여 생성 됩니다. 그런 다음 사용자 지정 Stream 클래스는 사용자의 브라우저에 전송할 현재 스트림에 대 한 대체 스트림으로 역할을 하는 생성 됩니다. 사용자 지정 스트림 클래스는 페이지의 내용은 변경 하 고 다음 응답 스트림에 작성 된 스트림, 검색 됩니다. 이 사용자 지정 Stream 클래스의 Write 메서드가 있으므로 사용자의 브라우저에 전달 되는 내용 변경 기본 응답 스트림에 HTML 바꾸려면 사용자 지정 됩니다. 새 스트림 클래스 페이지에서 Response.Filter 속성에 할당 된 마지막으로,\_이벤트를 로드, 따라서 페이지 콘텐츠를 변경 하는 메커니즘을 제공 합니다.

[&#9654;비디오 (13 분)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
