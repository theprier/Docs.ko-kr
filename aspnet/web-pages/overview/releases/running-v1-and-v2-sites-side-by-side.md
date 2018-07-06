---
uid: web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
title: 다른 버전의 ASP.NET 웹 페이지 (Razor) Side-by-side 실행 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 웹 사이트는 서로 다른 버전을 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET Web Pages (Razor) 웹 사이트를 실행 하는 방법에 설명 하는 중...
ms.author: aspnetcontent
ms.date: 02/10/2014
ms.assetid: a861409b-4ae6-4868-9e09-87edfac3535f
msc.legacyurl: /web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
msc.type: authoredcontent
ms.openlocfilehash: 86b1d5babac747eb4fa7ba8abde0e6155c8b17fb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810058"
---
<a name="running-different-versions-of-aspnet-web-pages-razor-side-by-side"></a>ASP.NET 웹 페이지 (Razor)의 다른 버전을 나란히 실행
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 웹 사이트는 서로 다른 버전의 ASP.NET 웹 페이지를 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET Web Pages (Razor) 웹 사이트를 실행 하는 방법에 설명 합니다.
> 
> 학습할 내용:
> 
> - 기본 동작 이란 ASP.NET에서 ASP.NET 웹 페이지를 사용 하 여 구축 된 사이트에 있는 경우.
> - 이전 버전의 ASP.NET 웹 페이지를 사용 하 여 실행 하려면 새 사이트를 구성 하는 방법입니다.
>   
> 
> 문서에 도입 된 ASP.NET 기능은 다음과 같습니다.
> 
> - `webPages:Version` 구성 설정입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 또한 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0과 함께 작동합니다.


ASP.NET 웹 페이지를 함께 웹 사이트를 실행 하는 기능을 지원 합니다. 이렇게 하면 계속 이전 ASP.NET Web Pages 응용 프로그램을 실행, 새 ASP.NET 웹 페이지 응용 프로그램을 빌드 및 모두 동일한 컴퓨터에서 실행할 수 있습니다.

WebMatrix를 사용 하 여 웹 페이지를 설치할 때 기억해 야 할 몇 가지 사항은 다음과 같습니다.

- 기본적으로 기존 웹 페이지 응용 프로그램은 컴퓨터에 최신 버전으로 실행 됩니다. (어셈블리가 전역 어셈블리 캐시 (GAC)에 설치 되 고 자동으로 사용 됩니다.)
- 다른 버전의 ASP.NET 웹 페이지를 사용 하 여 사이트를 실행 하려는 경우에 작업을 수행 하는 사이트를 구성할 수 있습니다. 사이트에 아직 없는 경우는 *web.config* 사이트의 루트에 파일, 새로 만들고, 기존 콘텐츠를 덮어씁니다를 다음 XML을 복사 합니다. 해당 사이트에 이미 포함 하는 경우는 *web.config* 파일을 추가 `<appSettings>` 에 다음과 같은 요소는 `<configuration>` 섹션입니다.

    [!code-xml[Main](running-v1-and-v2-sites-side-by-side/samples/sample1.xml)]
  '-의 버전을 지정 하지 않으면 경우는 *web.config* 사이트 파일은 최신 버전으로 배포 됩니다. (어셈블리 복사 되는 *bin* 배포 된 사이트의 폴더입니다.)
- 사이트의 웹 페이지 버전 어셈블리를 포함 하는 Web Matrix에서 사이트 템플릿을 사용 하 여 만드는 새 응용 프로그램 *bin* 폴더입니다.

일반적으로 제어할 수 있습니다. 항상 웹 페이지 사이트에 적절 한 어셈블리를 설치 하려면 NuGet을 사용 하 여 사이트를 사용 하는 버전 *bin* 폴더입니다. 패키지를 방문 [NuGet.org](http://NuGet.org)합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 2의에서 주요 기능](top-features-in-web-pages-2.md)
