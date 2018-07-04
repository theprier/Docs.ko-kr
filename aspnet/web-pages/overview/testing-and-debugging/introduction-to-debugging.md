---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: ASP.NET 웹 디버깅 소개 페이지 (Razor) 사이트 | Microsoft Docs
author: tfitzmac
description: 디버깅은 찾기 및 코드 페이지에 오류를 수정 하는 과정입니다. 이 장에서 몇 가지 도구 및 기술을 디버그 하는 데 사용할 수 및 분석 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: 0d189eb8640346ca7850d9013961cbf45aaefd6f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375864"
---
<a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 디버깅 소개 페이지 (Razor) 사이트
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 페이지를 디버깅 하는 다양 한 방법에 설명 합니다. 디버깅은 찾기 및 코드 페이지에 오류를 수정 하는 과정입니다.
> 
> **학습할 내용:** 
> 
> - 도움이 되는 정보를 표시 하는 방법 분석 및 페이지를 디버깅 합니다.
> - Visual Studio에서 디버깅을 사용 하는 방법 도구입니다.
>   
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `ServerInfo` 도우미입니다.
> - `ObjectInfo` 도우미입니다.
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
> - Visual Studio 2013
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다. WebMatrix 3를 사용할 수 있지만 통합된 된 디버거 지원 되지 않습니다.


오류 및 코드의 문제를 해결 하는 중요 한 부분은 애초에 대처 하는 것입니다. 오류를 일으킬 수 있는 코드의 섹션을 배치 하 여 이렇게 `try/catch` 블록입니다. 오류 처리에 대 한 내용은 섹션을 참조 [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkId=202890)합니다.

`ServerInfo` 도우미는 페이지를 호스팅하는 웹 서버 환경에 대 한 정보의 개요를 제공 하는 진단 도구입니다. 또한, 브라우저 페이지를 요청할 때 전송 되는 HTTP 요청 정보를 보여줍니다. `ServerInfo` 형식 요청을 수행 하는 브라우저의 현재 사용자 id를 표시 하는 도우미 등입니다. 이러한 종류의 정보는 일반적인 문제를 해결 하면 도움이 됩니다.

1. 라는 새 웹 페이지를 만듭니다 *ServerInfo.cshtml*합니다.
2. 페이지의 끝을 닫기 전에 방금 `</body>` 태그를 추가 `@ServerInfo.GetHtml()`:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    추가할 수는 `ServerInfo` 페이지의 코드입니다. 하지만 끝에 추가 됩니다 출력 별도로 유지 하 여 다른 페이지 콘텐츠를 쉽게 읽을 수 있습니다.

    > [!NOTE] 
    > 
    > **중요 한** 프로덕션 서버에 웹 페이지를 이동 하기 전에 웹 페이지에서 모든 진단 코드를 제거 해야 합니다. 이 적용 됩니다는 `ServerInfo` 도우미 뿐만 아니라 다른 진단이 문서는 기술 페이지로 코드를 추가 합니다. 이러한 종류의 정보는 악의적인 의도 가진 사용자에 게 유용할 수 있으므로 비슷한 세부 정보를 확인 하 고 서버에서 서버 이름, 사용자 이름, 경로 대 한 내용은 웹 사이트 방문자가 하지 않으려고 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다.

    ![디버깅-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` 도우미 페이지에 네 개의 테이블 정보를 표시 합니다.

   - 서버 구성입니다. 이 섹션에서는 호스팅 웹 서버 컴퓨터 이름, 버전을 실행 하는 ASP.NET, 도메인 이름 및 서버 시간을 포함 하는 방법에 대 한 정보를 제공 합니다.
   - ASP.NET 서버 변수입니다. 이 섹션에서는 여러 HTTP 프로토콜 세부 정보 (라는 HTTP 변수)에 대 한 세부 정보를 제공 하 고 값을 각 웹 페이지 요청에 포함 됩니다.
   - HTTP 런타임 정보입니다. 이 섹션에서는 버전 웹 페이지에서 실행 되는 Microsoft.NET Framework, 경로, 캐시, 등에 대 한 세부 정보는에 대 한 정보를 제공 합니다. (에서 설명한 대로 [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkId=202890), Razor 구문을 기반으로 하는 광범위 한 소프트웨어는 Microsoft의 ASP.NET 웹 서버 기술에 기반을 사용 하 여 ASP.NET 웹 페이지 개발 라이브러리는.NET Framework를 호출 합니다.)
   - 환경 변수입니다. 이 섹션에서는 웹 서버의 모든 로컬 환경 변수 및 해당 값의 목록을 제공 합니다.

     모든 서버 및 요청 정보에 대 한 자세한 내용은이 문서의 범위를 벗어납니다. 하지만 볼 수 있습니다는 `ServerInfo` 도우미 많은 진단 정보를 반환 합니다. 값에 대 한 자세한 내용은 `ServerInfo` 반환 되는 경우 참조 [환경 변수 인식](https://technet.microsoft.com/library/dd560744(WS.10).aspx) Microsoft TechNet 웹 사이트 및 [IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) MSDN 웹 사이트입니다.

## <a name="embedding-output-expressions-to-display-page-values"></a>페이지 값을 표시 하려면 출력 식 포함

페이지 출력 식 포함 방법은 하는 또 다른 방법은 코드에서 발생 한 것입니다. 변수의 값 같은 추가 하 여 직접 출력할 수 했 듯이 `@myVariable` 또는 `@(subTotal * 12)` 페이지입니다. 디버깅을 위해 코드에서 전략적 지점에 해당 출력 식을 배치할 수 있습니다. 이 페이지에 실행 될 때 키 변수 또는 계산의 결과의 값을 확인할 수 있습니다. 완료 되 면 디버깅, 식 제거 하거나 주석입니다. 이 절차에서는 페이지를 디버깅 하는 데 포함된 식을 사용 하는 일반적인 방법을 보여 줍니다.

1. 라는 새 WebMatrix 페이지를 만듭니다 *OutputExpression.cshtml*합니다.
2. 페이지를 내용을 다음으로 바꿉니다.

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    이 예제에서는 사용을 `switch` 의 값을 확인 하는 문이 `weekday` 변수와 것이 어떤 요일에 따라 서로 다른 출력 메시지를 한 다음 표시 합니다. 예에서를 `if` 블록 첫 번째 코드 블록 내에서 현재 요일 값으로 1 일을 추가 하 여 주의 요일을 임의로 변경 합니다. 이해를 돕기 위해 도입 하는 오류입니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다.

    페이지에 잘못 된 요일에 대 한 메시지가 표시 됩니다. 모든 요일 실제로 인 있습니다 하루 나중에 대 한 메시지가 표시 됩니다. 이 경우 이유 메시지 이므로 해제 (코드는 의도적으로 잘못 된 날짜 값을 설정) 알 수 있지만, 여기서 진행 코드에서 잘못 된 알기 어려운 경우가 실제로 합니다. 와 같은 주요 개체 및 변수 값으로 일어나 알아보려면 해야를 디버깅 하려면 `weekday`합니다.
4. 삽입 하 여 출력 식을 추가할 `@weekday` 코드의 주석으로 표시 하는 두 곳에 표시 된 대로 합니다. 이러한 출력 식 코드 실행에 해당 지점에서 변수 값 표시 됩니다.

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. 저장 하 고 브라우저에서 페이지를 실행 합니다.

    페이지 실제 요일을 먼저 표시 한 다음 업데이트 된 요일 결과에서 나온 하루 및 다음 결과 메시지를 추가 합니다 `switch` 문입니다. 두 변수 식의 출력 (`@weekday`)은 HTML을 추가 하지 않은 때문에 날짜 사이 공백이 없어야 `<p>` 출력; 태그 식만 사용할 테스트 합니다.

    ![디버깅-2](introduction-to-debugging/_static/image2.jpg)

    이제 오류가 볼 수 있습니다. 처음 표시 하면는 `weekday` 올바른 날짜 표시는 코드에서 변수를 합니다. 표시할 때는 두 번째로 후는 `if` 코드 블록, 하루 하나에서 해제 되어 있습니다. 요일 변수의 첫 번째 및 두 번째 모양을 간에 발생 하는 것을 알 수 있습니다. 실제 버그 인 것으로 확인 되 이러한 유형의 접근 방식 문제의 원인이 되는 코드의 위치를 좁힐는 데 도움이 됩니다.
6. 라는 두 개의 출력 식 추가, 제거 및 주의 요일을 변경 하는 코드를 제거 하 여 페이지에서 코드를 수정 합니다. 나머지, 완전 한 코드 블록을 다음 예제에서는 다음과 같습니다.

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. 브라우저에서 페이지를 실행 합니다. 이 이번 실제 요일에 대해 표시 하는 올바른 메시지가 표시 됩니다.

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>ObjectInfo 도우미를 사용 하 여 개체 값을 표시 하려면

`ObjectInfo` 도우미 종류와을 전달 하는 각 개체의 값을 표시 합니다. 코드 (예: 이전 예제의 출력 식을 사용 하 여 수행한)에서 변수 및 개체의 값을 보는 데 사용할 뿐만 아니라 개체에 대 한 정보를 입력 하는 데이터를 볼 수 있습니다.

1. 라는 파일을 엽니다 *OutputExpression.cshtml* 앞서 만든 합니다.
2. 다음 코드 블록을 사용 하 여 페이지에서 모든 코드를 바꿉니다.

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. 저장 하 고 브라우저에서 페이지를 실행 합니다.

    ![디버깅-4](introduction-to-debugging/_static/image3.jpg)

    이 예제에서는 `ObjectInfo` 도우미에는 두 개의 항목이 표시 됩니다.

   - 형식입니다. 첫 번째 형식은 `DayOfWeek`합니다. 형식이 두 번째 변수에 `String`합니다.
   - 값입니다. 이 경우 이미 인사말 변수 값 페이지를 표시, 값을 다시 표시 됩니다 변수를 전달 하는 경우 `ObjectInfo`합니다.

     더 복잡 한 개체에 대 한 합니다 `ObjectInfo` 도우미 자세한 정보를 표시할 수 &#8212; 기본적으로, 형식 및 모든 개체의 속성의 값을 표시할 수 있습니다.

## <a name="using-debugging-tools-in-visual-studio"></a>Visual Studio에서 디버깅 도구를 사용 하 여

보다 포괄적인 디버깅 환경을 사용 하 여 Visual Studio 2013 또는 무료 [Visual Studio Express 2013 for Web](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-2013-express)합니다. Visual Studio를 사용 하 여 조사 하려는 줄에서 코드에 중단점을 설정할 수 있습니다.

![중단점 설정](introduction-to-debugging/_static/image1.png)

웹 사이트를 테스트할 때 코드 실행이 중단점에서 중단 합니다.

![중단점 도달](introduction-to-debugging/_static/image2.png)

변수 및 단계에서의 코드에서 줄의 현재 값을 검사할 수 있습니다.

![값을 참조 하세요.](introduction-to-debugging/_static/image3.png)

ASP.NET Razor 페이지를 디버깅 하려면 Visual Studio에서 통합된 된 디버거를 사용 하는 방법에 대 한 내용은 [프로그래밍 ASP.NET Web Pages (Razor)를 사용 하 여 Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854)합니다.

## <a name="additional-resources"></a>추가 리소스

- [Visual Studio를 사용 하 여 ASP.NET 웹 페이지 (Razor) 프로그래밍](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS 서버 변수](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)
- [환경 변수를 인식](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)
