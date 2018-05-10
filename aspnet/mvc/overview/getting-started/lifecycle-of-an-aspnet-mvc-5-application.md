---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 응용 프로그램의 수명 주기 | Microsoft Docs
author: cephalin
description: ASP.NET MVC 5 응용 프로그램의 수명 주기를 차트로 보여주는 PDF 문서를 다운로드합니다. 이 수명 주기 문서는 MVC 수명 주기에 대한 개요를 제공합니다.
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
작성자: [Cephas Lin](https://github.com/cephalin)

[PDF 문서 다운로드](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

HTTP 요청을 받고 HTTP 요청을 다시 클라이언트로 보내는 ASP.NET MVC 5 응용 프로그램의 수명 주기를 차트로 보여주는 PDF 문서를 여기서 다운로드할 수 있습니다. 이 문서는 ASP.NET MVC를 처음 접하는 분들을 위한 교육 도구이자 응용 프로그램의 특정 기능을 자세히 알아보려는 분들을 위한 참조 자료로 작성되었습니다. PDF 문서의 특징은 다음과 같습니다.

- MVC가 [ASP.NET 응용 프로그램 수명 주기](https://msdn.microsoft.com/library/bb470252.aspx)의 어느 부분에 통합되는지 이해를 도와주는 관련 [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) 단계.
- 요청 처리 파이프라인에서 모든 MVC 응용 프로그램이 통과하는 주요 단계를 이해할 수 있는 MVC 응용 프로그램 수명 주기에 대한 개요 보기.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 요청 처리 파이프라인의 세부 정보를 보여주는 세부 정보 보기. 개요 보기와 세부 정보 보기를 비교하여 수명 주기에 대한 상세 정보가 다양한 단계로 수집되는 원리를 볼 수 있습니다. 더 크게 보려면 [PDF를 다운로드](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)하세요.
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 요청 처리 파이프라인의 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) 개체에서 재정의 가능한 모든 메서드의 배치 및 목적. 어떤 메서드를 재정의해야 할 수도 있고 재정의할 필요가 없을 수도 있지만, 응용 프로그램 수명 주기에서 메서드가 하는 역할을 이해하면 적절한 수명 주기 단계에서 코드를 작성하여 원하는 효과를 얻을 수 있습니다.
- 각 필터 유형(예: 인증, 권한 부여, 작업, 결과)이 호출되는 방식을 보여주는 확대 다이어그램.
- 세부 정보 보기의 각 관심 지점에 제공되는 유용한 문서 또는 블로그.


## <a name="next-steps"></a>다음 단계

이 문서로 요구 사항이 충족되었습니까? 소중한 의견에 감사합니다. 응용 프로그램의 ASP.NET MVC 수명 주기에 대해 궁금한 사항이 있는 경우 [Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx)에 질문을 올려주세요. twitter에서 [저](https://twitter.com/Cephas_MSFT)를 팔로우하시면 최신 자습서 업데이트를 받으실 수 있습니다.
