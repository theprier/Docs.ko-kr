---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter 도우미 ASP.NET 웹 페이지와 | Microsoft Docs
author: tfitzmac
description: 이 항목 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미를 호출 하는 방법을 보여 줍니다. 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 07d9c4d485c42b78a42c54c9740af5f67cb44763
ms.sourcegitcommit: 1b94305cc79843e2b0866dae811dab61c21980ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2018
---
<a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET 웹 페이지와 twitter 도우미
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미 메서드를 호출 하는 방법을 보여 줍니다.
> 
> Twitter.cshtml 파일에 대 한이 코드에서 개발한 **Tian 팬** microsoft 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="introduction"></a>소개

이 항목에서는 응용 프로그램에 Twitter 도우미 추가 도우미 메서드를 호출 하려면 Razor 구문을 사용 하는 방법을 보여 줍니다. Twitter 도우미를 사용 하면 쉽게 Twitter 단추 및 응용 프로그램에 대 한 위젯을 통합할 수 있습니다. 사용자의 시간 표시 막대 또는 hashtag에 대 한 검색 결과 같은 Twitter 위젯을 사용 하려면 먼저 만들어야 합니다는 [Twitter 위젯](https://twitter.com/settings/widgets)합니다. 위젯의 만든 후에 필요한 위젯 id가 표시 됩니다. 필요한 위젯 id가이 위젯의 표시 하는 도우미 메서드를 호출할 때 매개 변수로 전달 합니다.

이 항목에서는 Twitter API의 버전 1.1에 대 한 작성 되었습니다. Twitter 도우미 코드를 프로젝트에 직접 추가 Twitter API 변경 되 면 도우미 코드를 업데이트할 수 있습니다.

WebMatrix를 설치 하는 방법에 대 한 정보를 참조 하십시오. [Introducing ASP.NET 웹 페이지 2-시작](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)합니다.

## <a name="add-twitter-helper-to-your-project"></a>Twitter 도우미 프로젝트에 추가

Twitter 도우미를 추가 하려면 먼저 라는 폴더를 추가 **앱\_코드** 프로젝트에 있습니다. 그런 다음 라는 파일을 만들어 **Twitter.cshtml**합니다.

![App_Code 폴더](twitter-helper/_static/image1.png)

Twitter.cshtml의 기본 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>웹 페이지에서 Twitter 메서드를 호출 합니다.

다음 예제에서는 프로젝트의 페이지에서 Twitter 도우미 메서드를 사용 하는 방법을 보여 줍니다. 프로젝트 매개 변수 값으로 자신의 요구에 관련 된 값으로 바꿔야 합니다. 제공 된 위젯 id를 사용 하 여 메서드 작동 하는 방법을 탐색할 수 있지만 프로젝트에 대 한 위젯을 직접 생성 하려는.

아래 표시 된 매개 변수 중 일부만 필요 하며 선택적 매개 변수는 단추 또는 위젯 표시 방식을 사용자 지정 하는 데 사용 됩니다. 예를 들어에 따라 단추만을 수행 하려면 사용자 이름 이어야 하는데 단추와 해당 언어의 크기를 지정 하는 방법 및 후속 작업이, 수를 포함 하는 방법을 설명 합니다.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>결과 참조 하십시오.

위의 코드는 다음과 같은 단추와 위젯을 생성합니다. 이러한 단추와 위젯은 완벽 하 게 작동, 스크린 샷이 되지 않습니다. Language 매개 변수 설정 되었기 때문에 스페인어에 따라 단추가 표시 되는지를 **es**합니다.

### <a name="follow-button"></a>단추

[에 따라 @aspnet)](https://twitter.com/aspnet)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>

### <a name="tweet-button"></a>트 윗 단추

[트 윗](https://twitter.com/share)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>

### <a name="user-timeline-profile"></a>사용자 타임 라인 (프로필)

[하 여 트 윗 @aspnet](https://twitter.com/aspnet)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>

### <a name="favorites"></a>즐겨찾기

[즐겨 찾는 트 윗 @Microsoft](https://twitter.com/Microsoft/favorites)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>

### <a name="list"></a>목록

[트 윗에서 @Microsoft/MS \_소비자\_밴드](https://twitter.com/microsoft/ms-consumer-brands/)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>

### <a name="search"></a>검색

[에 대 한 트 윗 &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>
