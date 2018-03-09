---
uid: web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
title: "다른 버전의 ASP.NET 웹 페이지 (Razor) 나란히 실행 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 웹 사이트는 서로 다른 버전을 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET 웹 페이지 (Razor) 웹 사이트를 실행 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: a861409b-4ae6-4868-9e09-87edfac3535f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
msc.type: authoredcontent
ms.openlocfilehash: c11399b0bde59d18fa378ed48c15844454c1f956
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="running-different-versions-of-aspnet-web-pages-razor-side-by-side"></a>ASP.NET 웹 페이지 (Razor)의 서로 다른 버전을 Side-by-side 실행
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 웹 사이트는 서로 다른 버전의 ASP.NET 웹 페이지를 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET 웹 페이지 (Razor) 웹 사이트를 실행 하는 방법에 설명 합니다.
> 
> 학습 내용:
> 
> - 기본 동작 이란 ASP.NET에서 ASP.NET 웹 페이지를 작성 하는 사이트가 있는 경우.
> - 이전 버전의 ASP.NET 웹 페이지를 사용 하 여 실행 하도록 새 사이트를 구성 하는 방법.
>   
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `webPages:Version` 구성 설정입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서에서는 ASP.NET 웹 페이지 2에서 ASP.NET 웹 페이지 1.0 에서도 작동합니다.


ASP.NET 웹 페이지 웹 사이트 나란히 실행 하는 기능을 지원 합니다. 이렇게 하면 이전 ASP.NET 웹 페이지 응용 프로그램 실행, 새로운 ASP.NET 웹 페이지 응용 프로그램을 빌드 및 동일한 컴퓨터에서 실행 하는 모든 계속 수 있습니다.

WebMatrix로 웹 페이지를 설치할 때 기억해 야 할 일부의 원인 다음과 같습니다.

- 기본적으로 기존 웹 페이지 응용 프로그램 컴퓨터에 최신 버전으로 실행 됩니다. (어셈블리가 전역 어셈블리 캐시 (GAC)에 설치 되 고 자동으로 사용 됩니다.)
- 다른 버전의 ASP.NET 웹 페이지를 사용 하 여 사이트를 실행 하려는 경우에 작업을 수행 하는 사이트를 구성할 수 있습니다. 사이트에 지문이 아직 없으면는 *web.config* 사이트의 루트에서 파일을 새로 만들고 메서드를 다음과 같은 XML을 복사 기존 내용을 덮어씁니다. 사이트에 이미 포함 되어 있는 경우는 *web.config* 파일에서 추가 `<appSettings>` 에 다음과 같은 요소는 `<configuration>` 섹션.

    [!code-xml[Main](running-v1-and-v2-sites-side-by-side/samples/sample1.xml)]
'-의 버전을 지정 하지 않는 경우는 *web.config* 파일, 한 사이트에서 최신 버전으로 배포 됩니다. (의 어셈블리에 복사 되는 *bin* 배포 된 사이트의 폴더입니다.)
- 사이트의 웹 페이지 버전 어셈블리를 포함 하는 웹 매트릭스에서 사이트 템플릿을 사용 하 여 만든 새 응용 프로그램 *bin* 폴더입니다.

버전은 사이트에 적절 한 어셈블리를 설치 하려면 NuGet을 사용 하 여 사이트와 함께 사용할 웹 페이지에 항상 제어할 수는 일반적으로 *bin* 폴더입니다. 패키지를 찾으려고 방문 [NuGet.org](http://NuGet.org)합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 2에서에서 최상위 기능](top-features-in-web-pages-2.md)
