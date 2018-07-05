---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 웹 페이지와 twitter 도우미 | Microsoft Docs
author: tfitzmac
description: 이 항목에서 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미를 호출 하는 방법을 보여 줍니다....
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 2c84a986a39f6802a78df53510847cb70efbb0f2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373025"
---
<a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET 웹 페이지와 twitter 도우미
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에서 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미 메서드를 호출 하는 방법을 보여 줍니다.
> 
> Twitter.cshtml 파일에 대 한이 코드에서 개발한 **Tian 팬** Microsoft입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="introduction"></a>소개

이 항목에서는 Twitter 도우미 응용 프로그램에 추가 하 고 Razor 구문을 사용 하 여 도우미 메서드를 호출 하는 방법을 보여 줍니다. Twitter 도우미 쉽게 Twitter 단추 및 응용 프로그램에 대 한 위젯을 통합할 수 있습니다. 사용자의 타임 라인 또는 검색 결과는 해시 태그와 같은 Twitter 위젯을 사용 하려면 먼저 만들어야 합니다 [twitter 위젯을](https://twitter.com/settings/widgets)합니다. 위젯을 만들면 위젯 id를 받게 됩니다. 위젯에서 표시 하는 도우미 메서드를 호출할 때이 위젯 id를 매개 변수로 전달 합니다.

이 항목에서는 Twitter API의 버전 1.1에 대 한 작성 되었습니다. Twitter API 변경 되 면 Twitter 도우미 코드를 프로젝트에 직접 추가 도우미 코드를 업데이트할 수 있습니다.

WebMatrix를 설치 하는 방법에 대 한 내용은 [Introducing ASP.NET 웹 페이지 2-Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)합니다.

## <a name="add-twitter-helper-to-your-project"></a>Twitter 도우미 프로젝트에 추가

Twitter 도우미를 추가 하려면 먼저 폴더 추가 **앱\_코드** 프로젝트입니다. 그런 다음 파일을 만듭니다 **Twitter.cshtml**합니다.

![App_Code 폴더](twitter-helper/_static/image1.png)

Twitter.cshtml의 기본 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>웹 페이지에서 Twitter 메서드를 호출 합니다.

다음 예제에서는 프로젝트의 페이지에서 Twitter 도우미 메서드를 사용 하는 방법을 보여 줍니다. 프로젝트에서 요구 사항과 관련 된 값으로 매개 변수 값을 대체 해야 합니다. 메서드 작동 방식을 탐색할 때 제공 된 위젯 id를 사용할 수 있습니다 하지만 프로젝트에 대 한 고유한 widget을 생성 하려고 합니다.

아래에 표시 된 매개 변수 중 일부는 필요 합니다. 선택적 매개 변수는 단추 또는 위젯에 표시 되는 방식을 사용자 지정 하는 데 사용 됩니다. 예를 들어 필요에 따라 사용자 이름에 따라 단추를 있지만 단추와 언어의 크기를 지정 하는 방법 및 팔로 워 수를 포함 하는 방법을 보여 합니다.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>결과 참조 하세요.

위의 코드에 다음 단추 및 위젯을 생성합니다. 이러한 단추 및 위젯은 완벽 하 게 작동, 스크린 샷이 없습니다. Language 매개 변수 설정 되었기 때문에 스페인어에 따라 단추가 표시 되는지 **es**합니다.

### <a name="follow-button"></a>단추 수행

[에 따라 @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>트 윗 단추

[트 윗](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>사용자 타임 라인 (프로필)

[트 윗 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>즐겨찾기

[즐겨 찾는 트 윗 @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>목록

[트 윗 @Microsoft/MS \_소비자\_밴드](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>검색

[에 대 한 트 윗 &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
