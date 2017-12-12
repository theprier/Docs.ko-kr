---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: "에서 만들고 사용 하는 도우미 ASP.NET 웹 페이지 (Razor) 사이트 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 한 도우미를 만드는 방법을 설명 합니다. 도우미는 코드와 성능에 태그를 포함 하는 재사용 가능한 구성 요소 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 5d0c1ae09d8fbc91ff76cd4045d439abafee7736
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>에서 만들고 사용 하는 도우미 ASP.NET 웹 페이지 (Razor) 사이트
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 한 도우미를 만드는 방법을 설명 합니다. A *도우미* 코드와 길거나 복잡 한 될 수 있는 작업을 수행 하는 태그를 포함 하는 재사용 가능한 구성 요소입니다.
> 
> **학습 내용:** 
> 
> - 만들고 간단한 도우미를 사용 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `@helper` 구문입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="overview-of-helpers"></a>도우미의 개요

사이트의 여러 페이지에 동일한 작업을 수행 해야 할 경우에 도우미를 사용할 수 있습니다. ASP.NET 웹 페이지 다양 한 도우미 클래스를 포함 되며 다운로드 하 여 설치할 수 있는 더 많은 있습니다. (ASP.NET 웹 페이지에서 기본 제공 도우미의 목록에 나열 됩니다는 [ASP.NET API 빠른 참조](https://go.microsoft.com/fwlink/?LinkId=202907).) 기존 도우미 중 적합 한 사용자 고유의 도우미를 만들 수 있습니다.

도우미를 사용 하면 공통 코드 블록을 사용 하 여 여러 페이지에 걸쳐 수 있습니다. 페이지에 종종 되도록 일반 단락 외에도 설정 되어 있는 참고 항목을 만들 가정 합니다. 메모가으로 작성 되는 아마도 `<div>` 요소는 테두리가 있는 상자도 스타일이 지정 합니다. 메모를 표시 하려고 할 때마다 페이지에이 동일한 태그를 추가, 하기 보다는 태그 도우미로 패키지할 수 있습니다. 그런 다음 코드의 한 줄에 나오는 참고를 삽입할 수 필요한 모든 위치 합니다.

다음과 같은 도우미 사용 코드 페이지의 각 간단 하 고 쉽게 읽을 수 있습니다. 것도 이용 하면 쉽게 사이트 유지 관리 참고 모양을 변경 해야 할 경우 한 곳에서 태그를 변경할 수 있습니다.

## <a name="creating-a-helper"></a>도우미 만들기

이 절차 바로 언급 된 메모를 만드는 도우미를 만드는 방법을 보여 줍니다. 예제는 간단 하지만 사용자 지정 도우미 모든 태그 및 ASP.NET 코드를 포함할 수 있습니다.

1. 웹 사이트의 루트 폴더에 라는 폴더를 만듭니다 *앱\_코드*합니다. 도우미와 같은 구성 요소에 대 한 코드를 입력할 수 있는 ASP.NET에서 예약 된 폴더 이름입니다.
2. 에 *앱\_코드* 폴더를 새로 만듭니다. *.cshtml* 파일 하 고 이름을 *MyHelpers.cshtml*합니다.
3. 기존 콘텐츠를 다음으로 바꿉니다.

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    코드를 사용 하 여는 `@helper` 라는 새 도우미를 선언 하는 구문을 `MakeNote`합니다. 이 특정 도우미를 사용 하면 라는 매개 변수를 전달할 `content` 텍스트와 태그의 조합을 포함할 수 있는 합니다. 사용 하 여 참고 본문에 문자열을 삽입 하는 도우미는 `@content` 변수입니다.

    파일 이름이 *MyHelpers.cshtml*, 도우미 이름은 같지만 `MakeNote`합니다. 단일 파일에 여러 사용자 지정 도우미를 넣을 수 있습니다.
4. 파일을 저장한 후 닫습니다.

## <a name="using-the-helper-in-a-page"></a>도우미 페이지의 사용

1. 루트 폴더에 라는 새 빈 파일을 만듭니다 *TestHelper.cshtml*합니다.
2. 파일에 다음 코드를 추가합니다.

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    사용 하 여 만든 도우미를 호출 하려면 `@` 여기서 도우미는, 점, 파일 이름 및 도우미 이름이 옵니다. (사용한 경우 여러 폴더에서는 *앱\_코드* 폴더를 구문을 사용할 수 있습니다 `@FolderName.FileName.HelperName` 중첩 된 폴더 수준 내에서 도우미 호출). 괄호 안에 따옴표를 추가 하는 텍스트 도우미는 웹 페이지에 나와 있는 참고의 일부로 표시 될 텍스트가입니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. 도우미 항목을 생성 하는 참고 오른쪽 도우미를 호출 하는 위치: 두 단락 사이입니다.

    ![페이지는 브라우저 및 도우미에서 지정 된 텍스트를 둘러싸는 상자의 배치 하는 태그를 생성 하는 방법을 보여 주는 스크린샷](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.jpg)

## <a name="additional-resources"></a>추가 리소스


[Razor 도우미로 가로 메뉴](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)합니다. Mike 서 하 여이 블로그 항목에 태그, CSS 및 코드를 사용 하 여 도우미로 가로 메뉴를 만드는 방법을 보여 줍니다.

[WebMatrix 및 ASP.NET mvc 3을 위한 도우미 페이지를 ASP.NET 웹에서 HTML5를 활용 하 여](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)합니다. 이 블로그 항목 Sam Abraham에서 HTML5 렌더링 하는 도우미를 보여 줍니다. `Canvas` 요소입니다.

[차이 @Helpers 및 @Functions WebMatrix에서](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)합니다. Mike Brind 하 여이 블로그 항목 설명 `@helper` 구문 및 `@function` 구문 및 각각을 사용 하는 경우.
