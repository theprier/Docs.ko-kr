---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: "ASP.NET MVC 5 응용 프로그램의 수명 주기 | Microsoft Docs"
author: cephalin
description: "ASP.NET MVC 5 응용 프로그램의 수명 주기를 차트를 PDF 문서를 다운로드 합니다. 이 주기 문서에서는 MVC 수명 주기를 간략하게 제공는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/28/2014
ms.topic: article
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 50d58d10c11677fa72ede6a03e686cbde4cbae1d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a>ASP.NET MVC 5 응용 프로그램의 수명 주기
====================
으로 [Cephas 링크](https://github.com/cephalin)

[PDF 문서를 다운로드 합니다.](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

여기에서 HTTP 수신 모든 ASP.NET MVC 5 응용 프로그램의 수명 주기는 HTTP 응답을 보내는 것에 요청 하는 차트를 다시 클라이언트에 PDF 문서를 다운로드할 수 있습니다. ASP.NET MVC와 접하는 사용자에 게 교육 도구로도 응용 프로그램의 특정 측면을 드릴 필요로 하는 사람들에 대 한 참조로 설계 되었습니다. PDF 문서에는 다음 기능이 있습니다.

- 관련 [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) MVC에 통합 하는 위치를 쉽게 이해할 수 있도록 하는 단계는 [ASP.NET 응용 프로그램 수명 주기](https://msdn.microsoft.com/library/bb470252.aspx)합니다.
- 높은 수준의 MVC 응용 프로그램 수명 주기 모든 MVC 응용 프로그램 요청 처리 파이프라인의를 통해 전달 되는 주요 단계를 이해할 수 있습니다.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 요청 처리 파이프라인의 세부 정보를 드릴 다운 표시 하는 세부 정보 보기입니다. 상위 수준 뷰와 여러 단계로 주기 정보가 수집 되는 방법을 보려면 세부 정보 보기를 비교할 수 있습니다. [PDF 다운로드](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) 더 크게 보려면 볼 수 있습니다.
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 에 있는 모든 재정의 가능한 메서드가의 목적 및 배치는 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) 요청 처리 파이프라인에서 개체입니다. 수도 한 모든 메서드를 재정의 필요가 없을 수 있습니다 하지만 결과 얻기에 대 한 적절 한 수명 주기 단계에서 코드를 작성할 수 있도록 응용 프로그램 수명 주기에서 자신의 역할을 이해 하는 것이 유용 합니다.
- 각 필터 형식 (예: 인증, 권한 부여, 동작 및 결과)이 호출 하는 방법을 보여 주는 나간 접속 다이어그램.
- 세부 정보 보기에 대 한 관심의 각 지점에서 유용한 문서 또는 블로그를 연결 합니다.


## <a name="next-steps"></a>다음 단계

이 문서에 요구 사항에 충족 됩니까? 여러분의 의견 보내 주셔서 감사 합니다. 응용 프로그램에서 ASP.NET MVC 수명 주기 궁금한 사항이 있는 경우 [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 하 게 합니다. 에 따라 [me](https://twitter.com/Cephas_MSFT) 에서 twitter 때문 내 최신 자습서에 대 한 업데이트를 가져올 수 있습니다.
