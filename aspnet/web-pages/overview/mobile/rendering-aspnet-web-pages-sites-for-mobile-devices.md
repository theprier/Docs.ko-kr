---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: "모바일 장치를 위한 사이트 (Razor) 페이지를 렌더링 하는 ASP.NET 웹 | Microsoft Docs"
author: tfitzmac
description: "이 문서에는 모바일 장치에 적절 하 게 렌더링 하는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다. 학습할: 있습니다 하는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: 08b714eb2ffaefc7c7e2e5c9a7428106b231e5b7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>모바일 장치에 대 한 ASP.NET 웹 페이지 (Razor) 사이트 렌더링
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에는 모바일 장치에 적절 하 게 렌더링 하는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다.
> 
> 학습 내용:
> 
> - 페이지를 사용 하는 명명 규칙을 지정 하는 방법은 모바일 장치용으로 설계 되었습니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


ASP.NET 웹 페이지를 사용 하면 모바일 또는 다른 장치에 대 한 콘텐츠 렌더링 방식을 사용자 지정할 수 있습니다.

ASP.NET 웹 페이지 사이트에서 장치 관련 페이지를 만드는 가장 간단한 방법은 다음과 같이 파일 명명 패턴을 사용 하 여이: *파일 이름.* *모바일**.cshtml*합니다. 페이지의 두 가지 버전을 만들 수 있습니다 (예를 들어 여러 개 이름은 *MyFile.cshtml* 고 이라는 하나 *MyFile.Mobile.cshtml*). 런타임 시 모바일 장치를 요청할 때 *MyFile.cshtml*, ASP.NET에서 콘텐츠를 렌더링 *MyFile.Mobile.cshtml*합니다. 그렇지 않으면 *MyFile.cshtml* 렌더링 됩니다.

다음 예제에서는 모바일 장치에 대 한 콘텐츠 페이지를 추가 하 여 모바일 렌더링을 활성화 하는 방법을 보여 줍니다. *Page1.cshtml* 콘텐츠 및 탐색 세로 막대를 포함 합니다. *Page1.Mobile.cshtml* 동일한 콘텐츠를 포함 하지만 세로 막대를 생략 합니다.

1. ASP.NET 웹 페이지 사이트에서는 라는 파일을 만들어 *Page1.cshtml* 현재 콘텐츠를 다음 태그로 바꿉니다.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. 라는 파일을 만들어 *Page1.Mobile.cshtml* 기존 콘텐츠를 다음 태그로 바꿉니다. 확인 페이지의 모바일 버전이 더 작은 화면에 보다 나은 렌더링에 대 한 탐색 절을 생략 합니다.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. 데스크톱 브라우저를 실행 하 고 *Page1.cshtml*합니다. ![mobilesites 1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. 모바일 브라우저 (또는 모바일 장치 에뮬레이터)를 실행 하 고 *Page1.cshtml*합니다. (포함 되지 않은 통지 *.mobile 합니다.* 일부로 URL입니다.) 요청 하는 것도 *Page1.cshtml*, ASP.NET 렌더링 *Page1.Mobile.cshtml*합니다.

    ![mobilesites 2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> 모바일 페이지를 테스트 하려면 데스크톱 컴퓨터에서 실행 되는 모바일 장치 시뮬레이터에서 앱을 사용할 수 있습니다. 이 도구를 사용 하면 모바일 장치에서 유사할 것 처럼 웹 페이지를 테스트할 수 있습니다 (즉, 일반적으로 훨씬 더 작은와 표시 영역). 시뮬레이터에서 앱의 한 가지 예는 [사용자 에이전트 전환기 추가 기능](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/) Mozilla Firefox에 대 한 수 있는 데스크톱 버전의 Firefox에서 다양 한 모바일 브라우저 에뮬레이션 합니다.


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[Windows Phone 에뮬레이터](https://msdn.microsoft.com/en-us/library/ff402563(v=VS.92).aspx)
