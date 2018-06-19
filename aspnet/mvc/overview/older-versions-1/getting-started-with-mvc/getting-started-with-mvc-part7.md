---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 78dd6bdd81fcb51a3a21a8f1ee12b4b2bfc37db5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871950"
---
<a name="adding-validation-to-the-model"></a>모델에 유효성 검사 추가
====================
으로 [Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다. 방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.


이 섹션에서는 하겠습니다 응용 프로그램 내에서 입력된 유효성 검사를 사용 하는 데 필요한 지원을 구현 합니다. म 합니다 확인 데이터베이스 콘텐츠 올바른지 항상 시도 하 고 잘못 된 동영상 데이터를 입력할 때 최종 사용자에 게 유용한 오류 메시지를 제공 합니다. 영화 클래스에 유효성 검사 논리를 약간 추가 시작 합니다.

모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다. 영화 클래스를 이름을 지정 합니다.

앞, 동영상 엔터티 모델에서 만든 동영상 클래스를 IDE 만들어집니다. 사실, 영화 클래스의 일부는 한 파일의 다른 파트에 수 있습니다. 이 Partial 클래스 라고 합니다. 다른 파일에서 영화 클래스를 확장 하려고 합니다.

시스템에 유효성 검사 힌트를 제공 하는 일부 특성을 가진 "버디 클래스"를 가리키는 부분 영화 클래스를 만들어 보겠습니다. 또한 책정할 특정 범위 내 되도록 요구 알아보고 제목과 가격 필수로 표시 하겠습니다. 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 클래스를 선택 합니다. 영화 클래스 이름을 지정 하 고 확인 단추를 클릭 합니다. 이 부분 영화 클래스의 모양은 다음과 같습니다.

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

다시 응용 프로그램을 실행 하 고 가격이 100 초과 동영상을 입력 하려고 합니다. 오류가 폼을 제출 했습니다. 오류는 서버 쪽에서 발생 하 고는 폼이 게시 한 후 발생 합니다. ASP.NET MVC의 기본 제공 HTML 도우미 된 오류 메시지를 표시 하 여 textbox 요소 내에서 us에 대 한 값을 유지 관리 방법을 확인 합니다.

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

이 방식은 효과적, 이지만 그 좋을 것을 확인할 수 사용자 클라이언트 쪽에서 즉시 전에 서버 관련 됩니다.

JavaScript 일부 클라이언트 쪽 유효성 검사가 가능 보겠습니다.

## <a name="adding-client-side-validation"></a>클라이언트 쪽 유효성 검사 추가

영화 클래스에는 일부 유효성 검사 특성에 이미 있으므로 방금 해야 우리의 Create.aspx 보기 서식 파일에 몇 개의 JavaScript 파일을 추가 하 고 수행 되려면 클라이언트 쪽 유효성 검사를 사용 하는 코드 줄을 추가 합니다.

내에서 VWD 우리의 동영상 보기/폴더를 이동 하 고 Create.aspx를 엽니다.

솔루션 탐색기에서 스크립트 폴더를 열고 내에서 다음 세 가지 스크립트를 끌어는 &lt;h e a d&gt; 태그입니다.

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

원하는이 순서로 표시 되도록이 스크립트 파일입니다.

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

또한는 Html.BeginForm 위에이 한 줄을 추가 합니다.

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

IDE 내에서 표시 된 코드는 다음과 같습니다.

[![동영상-Microsoft Visual 웹 Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

응용 프로그램을 실행 하 고 /Movies/Create 다시 방문 하 고 데이터를 입력 하지 않고 만들기를 클릭 합니다. 오류 메시지가 즉시 표시 데이터 보내기 연관 플래시 페이지 없이 거슬러 올라갑니다 서버에 있습니다. 이 ASP.NET MVC는 이제 한 입력 유효성 검사 둘 다에서 (JavaScript를 사용 하 여) 클라이언트 때문에 서버에 있습니다.

[![만들기-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

좋은 볼 됩니다! 데이터베이스에 추가 열 하나를 지금 추가 해 보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part6.md)
> [다음](getting-started-with-mvc-part8.md)
