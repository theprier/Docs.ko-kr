---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6 부: 모델 유효성 검사에 대 한 데이터 주석 사용 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부에서는 V 모델에 대 한 데이터 주석 사용을 설명 하는 중...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: b666c3cef0b09c6d68cee581a3c27c08e3357cca
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837558"
---
<a name="part-6-using-data-annotations-for-model-validation"></a>6 부: 모델 유효성 검사에 대 한 데이터 주석 사용
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 6 부 모델 유효성 검사에 대 한 데이터 주석을 사용 하 여 설명 합니다.


만들기 및 편집 폼을 사용 하 여 중요 한 문제가 있다고: 유효성 검사를 수행 중인 합니다. 가격 필드에 필수 필드를 빈 또는 형식 문자를 유지 하는 등 수행할 수 있습니다이 고 데이터베이스에서 살펴보겠습니다 첫 번째 오류가 발생 합니다.

데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 쉽게 추가할 수 것입니다. 데이터 주석 허락 하는 모델 속성에 적용 되는 원하는 규칙에 설명 하 고 ASP.NET MVC 해 줄 것으로 강제 적용 하 고 사용자에 게 적절 한 메시지를 표시 합니다.

## <a name="adding-validation-to-our-album-forms"></a>앨범은 폼에 유효성 검사 추가

다음 데이터 주석 특성을 사용 합니다.

- **필요한** – 속성이 필수 필드 임을 나타냅니다.
- **DisplayName** – 양식 필드 유효성 검사 메시지에 사용 되는 대상 텍스트를 정의 합니다.
- **StringLength** – 문자열 필드에 대 한 최대 길이 정의 합니다.
- **범위** – 숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.
- **바인딩** – 모델 속성을 매개 변수 또는 형식 값을 바인딩하는 경우를 포함 하거나 제외 하도록 필드를 나열 합니다.
- **ScaffoldColumn** – 편집기 폼에서 필드를 숨기면 허용

*참고: 데이터 주석 특성을 사용 하 여 모델 유효성 검사에 대 한 자세한 내용은 참조는 MSDN 설명서*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

앨범 클래스를 열고 다음을 추가 합니다 *를 사용 하 여* 문을 맨 위에 있습니다.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

그런 다음 아래와 같이 표시 및 유효성 검사 특성을 추가 하는 속성을 업데이트 합니다.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

그곳에서 있는 동안 변경 했습니다 장르 및 음악가 가상 속성입니다. 이렇게 하면 지연 로드 고 필요에 따라 Entity Framework.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

앨범 모델에 이러한 특성을 추가 하지, 후 우리의 만들기 및 편집 화면에 즉시 보내기 시작 필드 유효성 검사 및 표시 이름을 사용 하 여 (예: 앨범 아트 Url AlbumArtUrl 대신)를 선택 했습니다. 응용 프로그램을 실행 하 고 /StoreManager/Create 찾습니다.

![](mvc-music-store-part-6/_static/image1.png)

다음으로, 일부 유효성 검사 규칙 중단 하 게 됩니다. 0의 가격을 입력 하 고 제목을 비워 둡니다. 만들기 단추를 클릭 하는 경우에 유효성 검사 오류 메시지와 함께 필드 유효성 검사 규칙을 충족 하지 않은 표시를 정의 했으며 표시 된 양식을 살펴보겠습니다.

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>클라이언트 쪽 유효성 검사 테스트

서버 쪽 유효성 검사 응용 프로그램 관점에서 매우 중요 한 이므로 사용자가 클라이언트 쪽 유효성 검사를 피할 수 있습니다. 그러나 웹 페이지 forms만 서버 쪽 유효성 검사를 구현 하는 세 가지 중요 한 문제를 일으킵니다.

1. 사용자가 브라우저에 전송할 응답에 대 한 폼 게시, 서버의 유효성을 검사할 수에서 기다린 후 해야 합니다.
2. 사용자는 이제 유효성 검사 규칙을 통과할 수 있도록 필드를 수정 하는 경우 즉각적인 피드백을 받게 하지 않습니다.
3. 사용자의 브라우저를 활용 하는 대신 유효성 검사 논리를 수행 하는 서버 리소스를 낭비 하 했습니다.

다행 스럽게도 ASP.NET MVC 3 스 캐 폴드 템플릿 모두 클라이언트 쪽 유효성 검사에는 기본적으로 추가 작업이 필요 합니다.

유효성 검사 메시지를 즉시 제거 됩니다 있도록 유효성 검사 요구 사항을 충족 제목 필드에서 문자 하나를 입력 합니다.

![](mvc-music-store-part-6/_static/image3.png)


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-5.md)
> [다음](mvc-music-store-part-7.md)
