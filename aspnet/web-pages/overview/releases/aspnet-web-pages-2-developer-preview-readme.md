---
uid: web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
title: ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/14/2011
ms.topic: article
ms.assetid: 159a92e2-e011-4da7-b61d-2edde2a967da
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
msc.type: authoredcontent
ms.openlocfilehash: 1a43b2b12af9cd223d8a3622239743f7c431f617
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보
====================
by [Microsoft](https://github.com/microsoft)

## <a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보

2011 년 9 월 14

### <a name="contents"></a>목차

#### <a id="_Toc303701284"></a>  설치 참고 사항

웹 페이지 2 Developer Preview를 설치 하려면 같은 옵션이 있습니다.

- 사용 하 여 WebMatrix 2 베타 설치는 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=226883)합니다. WebMatrix는 ASP.NET 웹 페이지를 포함 하는 집합의 무료 웹 개발 도구입니다. 자세한 내용은의 "설치" 부분을 참조 하십시오. [ASP.NET 웹 페이지 2 개발자 미리 보기에서의 최상위 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

- 웹 페이지 2 개발자 미리 보기를 사용 하 여 직접 설치는 [다운로드 링크](https://go.microsoft.com/fwlink/?LinkID=226335)합니다. 메모장과 같은 편집기는 텍스트를 사용 하 여 웹 페이지 응용 프로그램을 만들려고 할 경우이 방법을 사용 합니다. 웹 페이지 2 응용 프로그램을 실행 하려면 IIS 7.5 Express 있어야 합니다. (이 WebMatrix에 자동으로 포함 합니다.) IIS Express를 사용 하 여 웹 페이지의 페이지를 테스트 하는 방법에 대 한 팁의 사이드바 "만들기 및 테스트 ASP.NET 페이지를 사용 하 여 사용자 고유의 텍스트 편집기" 참조에 대 한 [WebMatrix 및 ASP.NET 웹 페이지 시작](https://go.microsoft.com/fwlink/?LinkId=202889)합니다.

ASP.NET 웹 페이지 2 개발자 미리 보기 설치할 수 있으며-함께 실행할 수 있는 ASP.NET 웹 페이지 1입니다. <a id="a"></a>자세한 내용은의 "실행 중 웹 페이지 응용 프로그램-함께" 섹션을 참조 [The Top 웹 페이지 2 개발자 미리 보기 기능에에서](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

#### <a id="_Toc303701285"></a>  설명서

ASP.NET 웹 사이트의 웹 페이지 페이지에서 사용할 수 있는 자습서 및 ASP.NET 웹 페이지에 대 한 기타 정보 ([https://www.asp.net/web-pages/](../../index.md)). 새로운 기능 및 웹 페이지 2의 향상 된 기능에 대 한 정보를 참조 하십시오. [The Top 웹 페이지 2 개발자 미리 보기 기능에에서](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

#### <a id="_Toc303701286"></a>  Support

<a id="_Toc209852135"></a><a id="_Toc255833657"></a> 미리 보기 버전 이므로 공식적으로 지원 되지 않습니다. 이 릴리스에서 사용에 대 한 질문이 있으면 ASP.NET 웹 페이지 포럼에 게시 ([ https://forums.asp.net/1224.aspx/1?WebMatrix ](https://forums.asp.net/1224.aspx/1?WebMatrix) )에서 ASP.NET 커뮤니티의 회원과 비공식적인 지원을 제공할 수 있는 경우가 많습니다.

#### <a id="_Toc303701287"></a>  소프트웨어 요구 사항

ASP.NET 웹 페이지 2에는.NET Framework 4 필요 합니다. .NET Framework 4.5 Developer Preview 릴리스와도 작동 합니다.

<a id="_Toc303701288"></a><a id="_Breaking_Changes"></a>

#### <a name="fixes-known-issues-and-breaking-changes"></a>수정, 알려진된 문제 및 주요 변경 내용

<a id="_Toc224729061"></a><a id="_Toc238051347"></a>

- **\* 메서드 (예를 들어 IsDateTime) 이제 올바른 값을 반환 하는 모든 culture에 대 한 합니다.** 와 같은 일부 메서드 *IsDateTime* 이전에 반환 된 *false* 때 이러한 해야 반환한 *true* 이전에 culture 관련 검사 수행 하 고 있던 때문에 있습니다. 이러한 메서드는 이제 문화권을 고려 하 수정 되었습니다. 이 주요 변경 내용. 응용 프로그램 이전 동작을 사용 하는 경우 중단 됩니다.
- **Href 메서드의 동작이 변경 되었습니다.** 이전에 호출 Href("~/SomeFile") 현재 실행 중인 파일을 기준으로 URL을 반환 합니다. 이제 Href("~/SomeFile") 응용 프로그램의 루트에서 절대 경로 항상 반환합니다. 대부분의 경우이 동작 하지 않습니다는 반환 값의 차이 확인 합니다. 특정 Ajax 시나리오를 해결 하려면 변경 되었습니다. 예를 들어 다음 예제 코드를 살펴보세요. 

    [!code-cshtml[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample1.cshtml)]

    이 코드 이전에 것으로 확인 Images/Logo.jpg, Ajax 요청 해당 페이지에 적합 하지 않을 것입니다. 루트에 확인 이제 되는 (/ MySite/Images/Logo.jpg).
- **HttpContext.RedirectLocal 방법이 변경**합니다. 이 메서드는 지금 현재 응용 프로그램에 비례 하는 Url만 허용 합니다. 정규화 된 Url이 거부 됩니다.
- **유효성 검사를 먼저 호출 하는 ModelState.IsValid 메서드 이제 필요**합니다. 새 입력된 유효성 검사 메서드를 사용 하도록 응용 프로그램을 변환 하는 호출 하는 경우는 *ModelState.IsValid* 메서드를 호출 해야 합니다 이제 *Validation.Validate* 미리 합니다. 예를 들어 이러한 패턴을 따르는 이제 해야 합니다. 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample2.cs)]

  하지만 새 입력된 유효성 검사 메서드를 사용 하는 경우 사용 하지 않아 권장 *ModelState.IsValid*합니다. 대신, 다음과 같은 코드를 구조 지정 합니다. 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample3.cs)]
- **Internet Explorer 7 및 Internet Explorer 8에서 클라이언트 쪽 유효성 검사 작동 하지 않습니다**합니다. 클라이언트 쪽 유효성 검사 작동 하지 않습니다 1.6.2, jQuery 호환 되지 않기 때문에 기본 프로젝트 템플릿이 포함 되어 있는. (서버 쪽 유효성 검사 작동합니다.).

#### <a id="_Toc303701289"></a>  Disclaimer

© 2011 Microsoft Corporation. All rights reserved. 이 설명서는 제공 "로-됩니다." URL 및 기타 인터넷 웹 사이트 참조를 포함 한이 문서의 내용과 관점은 예 고 없이 변경 될 수 있습니다. 정보의 사용으로 발생하는 위험은 귀하의 책임입니다.
