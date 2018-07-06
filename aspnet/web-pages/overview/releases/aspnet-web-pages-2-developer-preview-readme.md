---
uid: web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
title: ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 09/14/2011
ms.assetid: 159a92e2-e011-4da7-b61d-2edde2a967da
msc.legacyurl: /web-pages/overview/releases/aspnet-web-pages-2-developer-preview-readme
msc.type: authoredcontent
ms.openlocfilehash: 0a89216c0f65d49d00c96a27a5ab33e3872f9bc5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818348"
---
<a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보
====================
[Microsoft](https://github.com/microsoft)

## <a name="aspnet-web-pages-2-developer-preview-readme"></a>ASP.NET 웹 페이지 2 개발자 미리 보기 추가 정보

2011 년 9 월 14 일

### <a name="contents"></a>목차

#### <a id="_Toc303701284"></a>  설치 참고 사항

웹 페이지 2 개발자 미리 보기를 설치 하려면 다음이 옵션 해야 합니다.

- WebMatrix 2 베타 사용 하 여 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=226883)합니다. WebMatrix는 ASP.NET 웹 페이지를 포함 하는 무료 웹 개발 도구 집합입니다. 자세한 내용은의 설치 섹션을 참조 하세요 [ASP.NET 웹 페이지 2 개발자 미리 보기의 주요 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

- 웹 페이지 2 개발자 미리 보기를 사용 하 여 직접 설치 합니다 [다운로드 링크](https://go.microsoft.com/fwlink/?LinkID=226335)합니다. 웹 페이지 응용 프로그램 텍스트를 사용 하 여 메모장과 같은 편집기를 만들려는 경우이 방법을 사용 합니다. 웹 페이지 2 응용 프로그램을 실행 하기 위해 IIS 7.5 Express 있어야 합니다. (이 경우 WebMatrix를 사용 하 여 자동으로 포함) IIS Express를 사용 하 여 웹 페이지의 페이지를 테스트 하는 방법에 대 한 팁에서 "만들기 및 테스트 ASP.NET 페이지를 사용 하 여 사용자 고유의 텍스트 편집기" 보충 기사를 참조 하세요 [WebMatrix 및 ASP.NET Web Pages 시작](https://go.microsoft.com/fwlink/?LinkId=202889)합니다.

ASP.NET 웹 페이지 2 개발자 미리 보기를 설치할 수-나란히 실행할 수 있는 ASP.NET 웹 페이지 1입니다. <a id="a"></a>자세한 내용은의 "실행 웹 페이지 응용 프로그램-Side-by-side" 섹션을 참조 [웹 페이지 2 개발자 미리 보기의 주요 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

#### <a id="_Toc303701285"></a>  설명서

자습서 및 기타 정보에 대 한 ASP.NET Web Pages는 ASP.NET 웹 사이트의 웹 페이지에서 사용할 수 있습니다 ([https://www.asp.net/web-pages/](../../index.md)). 새로운 기능 및 웹 페이지 2의 향상 된 기능에 대 한 정보를 참조 하세요 [웹 페이지 2 개발자 미리 보기의 주요 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.

#### <a id="_Toc303701286"></a>  지원

<a id="_Toc209852135"></a><a id="_Toc255833657"></a> 이 미리 보기 버전 이며 공식적으로 지원 되지 않습니다. 이 릴리스를 사용 하는 방법에 대 한 질문이 있으면 ASP.NET Web Pages 포럼에 게시 ([ https://forums.asp.net/1224.aspx/1?WebMatrix ](https://forums.asp.net/1224.aspx/1?WebMatrix) ) ASP.NET 커뮤니티 회원이 비공식적인 지원을 제공 하기 위해 자주 수 있는, 합니다.

#### <a id="_Toc303701287"></a>  소프트웨어 요구 사항

ASP.NET 웹 페이지 2에는.NET Framework 4에 필요 합니다. 또한.NET Framework 4.5 개발자 미리 보기 릴리스를 사용 하 여 작동합니다.

<a id="_Toc303701288"></a><a id="_Breaking_Changes"></a>

#### <a name="fixes-known-issues-and-breaking-changes"></a>수정, 알려진된 문제 및 주요 변경 내용

<a id="_Toc224729061"></a><a id="_Toc238051347"></a>

- **\* 메서드 (예를 들어 IsDateTime) 이제 올바른 값을 반환 하는 모든 culture에 대 한 합니다.** 와 같은 일부 메서드 *IsDateTime* 이전에 반환 된 *false* 경우는 반환 되기 *true* 이전에 culture 별 검사 수행 하 고 있던 때문입니다. 이러한 메서드는 이제 culture를 고려해 야 할 수정 되었습니다. 이 주요 변경 내용입니다. 응용 프로그램이 이전 동작에 의존 하는 경우 중단 됩니다.
- **Href 메서드의 동작이 변경 되었습니다.** 이전에 호출 Href("~/SomeFile") 현재 실행 중인 파일을 기준으로 URL을 반환 합니다. 이제 Href("~/SomeFile") 응용 프로그램의 루트에서 절대 경로 항상 반환합니다. 대부분의 경우이 동작 반환 값의 차이 확인 하지 않습니다. 특정 Ajax 시나리오를 해결 하려면이 변경 되었습니다. 예를 들어, 다음 예제 코드를 것이 좋습니다. 

    [!code-cshtml[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample1.cshtml)]

    이 코드 이전에 확인 Images/Logo.jpg, 해당 페이지에 Ajax 요청에 대 한 올바른 것입니다. 루트에 확인 이제 되는 (/ MySite/Images/Logo.jpg).
- **HttpContext.RedirectLocal 방법이 변경**합니다. 이 메서드는 이제 현재 응용 프로그램에 상대적인 Url만 허용 합니다. 정규화 된 Url이 거부 됩니다.
- **유효성 검사를 먼저 호출 하는 ModelState.IsValid 메서드 이제 필요**합니다. 새 입력된 유효성 검사 메서드를 사용 하도록 응용 프로그램을 변환 하는 호출 하는 경우는 *ModelState.IsValid* 메서드를 호출 해야 합니다 이제 *Validation.Validate* 사전입니다. 예를 들어이 패턴은 지금 수행 해야 합니다. 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample2.cs)]

  그러나는 새 입력된 유효성 검사 메서드를 사용 하는 경우 사용 하지 좋습니다 *ModelState.IsValid*합니다. 다음과 같은 코드 대신 구조체입니다. 

    [!code-csharp[Main](aspnet-web-pages-2-developer-preview-readme/samples/sample3.cs)]
- **Internet Explorer 7 및 Internet Explorer 8에서 클라이언트 쪽 유효성 검사 작동 하지 않습니다**합니다. 클라이언트 쪽 유효성 검사 작동 하지 않습니다 1.6.2, jQuery 사용한 비 호환성으로 인해 기본 프로젝트 템플릿을 사용 하 여 포함 된. (서버 쪽 유효성 검사 작동합니다.).

#### <a id="_Toc303701289"></a>  Disclaimer

© 2011 Microsoft Corporation. All rights reserved. 이 문서는 제공 "으로-됩니다." 정보 및 견해 URL 및 기타 인터넷 웹 사이트 참조를 포함 하 여이 문서의 예 고 없이 변경 될 수 있습니다. 정보의 사용으로 발생하는 위험은 귀하의 책임입니다.
