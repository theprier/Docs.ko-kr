---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 일관 된 레이아웃 만들기 | Microsoft Docs
author: tfitzmac
description: '사이트에 대 한 웹 페이지를 보다 효율적으로 만들, 콘텐츠 (예: 머리글 및 바닥글) 웹 사이트를 가리키고 있습니다 c에 대 한 다시 사용할 수 있는 블록을 만들 수 있습니다...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/10/2014
ms.topic: article
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 2c7631017f7c0fb31f43320c2ab78baddd87b516
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530242"
---
<a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 사용 하는 방법을 레이아웃 페이지에서 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 다시 사용할 수 있는 블록 콘텐츠 (예: 머리글 및 바닥글)으로 하 고 사이트에 있는 모든 페이지에 일관 된 모양을 만들 수에 대해 설명 합니다.
> 
> **학습 내용:** 
> 
> - 다시 사용할 수 있는 블록의 머리글 및 바닥글와 같은 콘텐츠를 만드는 방법.
> - 레이아웃을 사용 하 여 사이트에서 모든 페이지에 일관 된 모양을 만들 하는 방법.
> - 레이아웃 페이지에 실행 시 데이터를 전달 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - 여러 페이지에 삽입할 HTML 형식의 콘텐츠를 포함 하는 파일인 콘텐츠 차단 됩니다.
> - 레이아웃 페이지는 웹 사이트에서 페이지에서 공유할 수 있는 HTML 형식의 콘텐츠를 포함 하는 페이지입니다.
> - `RenderPage`, `RenderBody`, 및 `RenderSection` ASP.NET을 페이지 요소를 삽입할 위치를 알 수 있는 방법입니다.
> - `PageData` 콘텐츠 블록 및 레이아웃 페이지 간에 데이터를 공유할 수 있는 사전입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="about-layout-pages"></a>레이아웃 페이지 정보

대부분의 웹 사이트에는 머리글 및 바닥글 또는 변경 내용이에 기록 하는 사용자가 알려 주는 상자와 같은 모든 페이지에 표시 되는 내용이 있습니다. ASP.NET은 텍스트, 태그 및 일반 웹 페이지와 마찬가지로 코드를 포함할 수 있는 콘텐츠 블록이 있는 별도 파일을 만들 수 있습니다. 다음 정보를 표시 하려는 사이트의 다른 페이지에서 콘텐츠 블록을 삽입할 수 있습니다. 이렇게 복사한 모든 페이지에 동일한 콘텐츠를 붙여 넣습니다. 필요가 없습니다. 다음과 같은 일반적인 콘텐츠 만들기도 쉽게 사이트 업데이트할 수 있습니다. 콘텐츠를 변경 해야 하 고 방금 단일 파일을 업데이트할 수 있습니다 다음 변경 내용이 everywhere 반영 콘텐츠 삽입 되었습니다.

다음 다이어그램에서는 콘텐츠 작업을 차단 하는 방법을 보여 줍니다. ASP.NET 지점에 콘텐츠 블록을 삽입 브라우저에서 페이지는 웹 서버에서를 요청 하는 경우 여기서는 `RenderPage` 메서드는 기본 페이지에서입니다. 완료 (병합된) 페이지를 브라우저에 전송 됩니다.

![RenderPage 메서드를 현재 페이지에 참조 된 페이지를 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image1.jpg)

이 절차에서는 별도 파일에 있는 두 개의 콘텐츠 블록 (머리글과 바닥글이)를 참조 하는 페이지를 만듭니다. 사이트의 모든 페이지에서 이러한 동일한 콘텐츠 블록을 사용할 수 있습니다. 완료 되 면 다음과 같이 페이지 수 있게 됩니다.

![스크린 샷 RenderPage 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image2.jpg)

1. 웹 사이트의 루트 폴더에 라는 파일을 만듭니다 *Index.cshtml*합니다.
2. 기존 태그를 다음 코드로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 루트 폴더에 라는 폴더를 만듭니다 *Shared*합니다.

    > [!NOTE]
    > 것이 일반적 라는 폴더의 웹 페이지 간에 공유 되는 파일을 저장할 *Shared*합니다.
4. 에 *Shared* 폴더 라는 파일을 만들어  *\_Header.cshtml*합니다.
5. 다음 기존 내용을 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    파일 이름으로  *\_Header.cshtml*, 밑줄로 (\_) 접두사입니다. 이름이 밑줄로 시작 하는 경우 ASP.NET 브라우저에 페이지를 보내지 않습니다. 이렇게 하면이 페이지를 요청 (실수로 또는 기타) 이러한 직접에서 합니다. 실제로 이러한 페이지 &#8212; 요청할 수 있도록 하려면 사용자가 받지 않도록 하기 때문에 밑줄 이름 페이지에는 콘텐츠 블록을 사용 하는 것이 좋습니다. 다른 페이지에 삽입할 엄격 하 게 존재 합니다.
6. *Shared* 폴더를 라는 파일을 만들어  *\_Footer.cshtml* 콘텐츠는 다음과 같이 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. 에 *Index.cshtml* 페이지에 대 한 두 호출을 추가 합니다는 `RenderPage` 메서드를 다음과 같이 합니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    이 웹 페이지에는 콘텐츠 블록을 삽입 하는 방법을 보여 줍니다. 호출 하 여 `RenderPage` 메서드 하 고 해당 시점에 삽입할 내용을 파일의 이름을 전달 합니다. 콘텐츠를 삽입 하는 여기에서  *\_Header.cshtml* 및  *\_Footer.cshtml* 로 파일은 *Index.cshtml* 파일입니다.
8. 실행 된 *Index.cshtml* 브라우저에서 페이지입니다. (WebMatrix에서에서 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **브라우저에서 시작**.)
9. 브라우저에서 페이지 소스를 봅니다. (예를 들어 Internet Explorer에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **소스 보기**.)

    이렇게 하면 인덱스 페이지 태그는 콘텐츠 블록으로 결합 하는 브라우저로 전송 되는 웹 페이지 태그를 볼 수 있습니다. 다음 예제에 대 한 렌더링 되는 페이지 소스 *Index.cshtml*합니다. 에 대 한 호출 `RenderPage` 에 삽입 된 *Index.cshtml* 머리글 및 바닥글 파일의 실제 내용이로 대체 되었습니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>레이아웃 페이지를 사용 하 여 일관 된 모양을

지금까지 여러 페이지에 동일한 콘텐츠를 포함 하도록 쉽도록 살펴보았습니다. 사이트에 대 한 일관 된 모양을 하는 보다 구조적인된 방법을 레이아웃 페이지를 사용 하는 것입니다. 레이아웃 페이지, 웹 페이지의 구조를 정의 하지만 실제 콘텐츠를 포함 되어 있지 않습니다. 페이지 레이아웃을 만든 후에 콘텐츠를 포함 하는 레이아웃 페이지에 연결 하는 웹 페이지를 만들 수 있습니다. 이러한 페이지에 표시 되는 페이지 레이아웃에 따라 포맷 됩니다. (이러한 관점에서 레이아웃 페이지 역할을 다른 페이지에 정의 된 콘텐츠에 대 한 서식 파일의 종류 합니다.)

레이아웃 페이지 것과 HTML 페이지를 제외 하 고 포함에 대 한 호출에서 `RenderBody` 메서드. 위치는 `RenderBody` 레이아웃 페이지의 메서드 콘텐츠 페이지의 정보를 포함 될 위치를 결정 합니다.

다음 다이어그램은 어떻게 콘텐츠 페이지를 보여주며, 레이아웃 페이지의 최종된 웹 페이지를 생성 하기 위해 런타임 시 결합 됩니다. 브라우저에서 콘텐츠 페이지를 요청 합니다. 콘텐츠 페이지에 페이지의 구조에 사용할 레이아웃 페이지를 지정 하는 코드가 있습니다. 레이아웃 페이지에서 콘텐츠가 지점에 삽입 됩니다 위치는 `RenderBody` 메서드를 호출 합니다. 블록도 삽입할 수 레이아웃 페이지를 호출 하 여 콘텐츠는 `RenderPage` 메서드, 이전 섹션에서 수행한 방식으로 합니다. 웹 페이지 완료 되 면 브라우저에 전송 됩니다.

![스크린 샷 RenderBody 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image3.jpg)

다음 절차를 레이아웃 페이지 및 링크 콘텐츠 페이지를 만드는 방법을 보여 줍니다.

1. 에 *Shared* 라는 파일을 만들어 웹 사이트의 폴더  *\_Layout1.cshtml*합니다.
2. 다음 기존 내용을 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    사용 된 `RenderPage` 콘텐츠 블록을 삽입 하려면 레이아웃 페이지에서 메서드. 레이아웃 페이지를 한 번만 호출을 포함할 수 있습니다는 `RenderBody` 메서드.
3. 에 *Shared* 폴더를 라는 파일을 만듭니다  *\_Header2.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 루트 폴더에 새 폴더를 만들고 이름을 *스타일*합니다.
5. 에 *스타일* 폴더 라는 파일을 만들어 *Site.css* 다음과 같은 스타일 정의 추가 하 고:

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    이러한 스타일 정의를 레이아웃 페이지와 스타일 시트를 사용할 수 있는 방법을 보여주기 여기 됩니다. 원하는 경우 이러한 요소에 대 한 사용자 고유의 스타일을 정의할 수 있습니다.
6. 루트 폴더에 라는 파일을 만듭니다 *Content1.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    레이아웃 페이지를 사용 하는 페이지입니다. 페이지 맨 위에 있는 코드 블록이이 콘텐츠 서식 지정 하는 데 어떤 레이아웃 페이지를 나타냅니다.
7. 실행 *Content1.cshtml* 브라우저에서 합니다. 렌더링된 된 페이지 형식을 사용 및 스타일 시트에 정의 된  *\_Layout1.cshtml* 및에 정의 된 텍스트 (콘텐츠) *Content1.cshtml*합니다.

    ![[image]](3-creating-a-consistent-look/_static/image4.jpg)

    그러면 동일한 레이아웃 페이지를 공유할 수 있는 추가 콘텐츠 페이지를 만들려면 6 단계를 반복할 수 있습니다.

    > [!NOTE]
    > 폴더의 모든 콘텐츠 페이지에 대 한 동일한 레이아웃 페이지를 자동으로 사용할 수 있도록 사이트를 설정할 수 있습니다. 자세한 내용은 참조 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkId=202906)합니다.

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>여러 콘텐츠 섹션에 있는 레이아웃 페이지 디자인

콘텐츠 페이지에 여러 영역 대체 가능한 콘텐츠가 있는 레이아웃을 사용 하려는 경우 유용한 섹션이 여러 개 있을 수 있습니다. 콘텐츠 페이지에서 각 섹션 된 고유 이름을 지정 합니다. (기본 섹션을 두면 명명 되지 않은.) 레이아웃 페이지에서 추가 된 `RenderBody` 명명 되지 않은 (기본값) 섹션의 표시 위치를 지정 하는 메서드. 그런 다음 별도 추가 `RenderSection` 개별적으로 명명 된 섹션을 렌더링 하는 데 메서드.

다음 다이어그램에서는 ASP.NET에서 여러 섹션으로 구분 하는 콘텐츠를 처리 하는 방법을 보여 줍니다. 각 명명 된 섹션은 콘텐츠 페이지에 있는 섹션 블록에 포함 됩니다. (이름을 `Header` 및 `List` 예제에서입니다.) 프레임 워크는 시점의 레이아웃 페이지에 콘텐츠 섹션을 삽입 위치는 `RenderSection` 메서드를 호출 합니다. 명명 되지 않은 (기본값) 섹션의 지점에 삽입 됩니다 위치는 `RenderBody` 했 듯이 메서드가 호출 됩니다.

![RenderSection 메서드를 현재 페이지에 대 한 참조 섹션을 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image5.jpg)

이 절차에서는 여러 콘텐츠 섹션에 있는 콘텐츠 페이지를 만드는 방법과 여러 콘텐츠 섹션을 지 원하는 레이아웃 페이지를 사용 하 여 렌더링 하는 방법을 보여 줍니다.

1. 에 *Shared* 폴더 라는 파일을 만들어  *\_Layout2.cshtml*합니다.
2. 다음 기존 내용을 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    사용 된 `RenderSection` 헤더와 목록 섹션을 렌더링 하는 메서드.
3. 루트 폴더에 라는 파일을 만듭니다 *Content2.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    이 콘텐츠 페이지의 페이지 맨 위에 있는 코드 블록을 포함합니다. 각 명명 된 섹션 섹션 블록에 포함 됩니다. 페이지의 나머지 기본 (명명 되지 않은) 콘텐츠 섹션을 포함합니다.
4. 실행 *Content2.cshtml* 브라우저에서 합니다.

    ![스크린 샷 RenderSection 메서드에 대 한 호출을 포함 하는 페이지 실행 으로부터 만들어지는 브라우저에서 페이지를 표시 합니다.](3-creating-a-consistent-look/_static/image6.jpg)

## <a name="making-content-sections-optional"></a>선택적 콘텐츠 섹션 만들기

일반적으로 콘텐츠 페이지에서 만드는 섹션 페이지 레이아웃 페이지에 정의 된 섹션을 일치 해야 합니다. 다음 중 하나가 발생 하는 경우 오류가 발생할 수 있습니다.

- 콘텐츠 페이지 레이아웃 페이지에서 해당 섹션이 없습니다. 포함 된 섹션에 포함 되어 있습니다.
- 레이아웃 페이지에 콘텐츠가 없는 섹션이 포함 되어 있습니다.
- 레이아웃 페이지 같은 섹션을 두 번 이상 렌더링 하려고 하는 메서드 호출을 포함 합니다.

그러나, 레이아웃 페이지에서 선택적 섹션을 선언 하 여 명명된 된 섹션에 대 한이 동작을 재정의할 수 있습니다. 이 레이아웃 페이지를 공유할 수는 있지만 수 또는 특정 섹션에 대 한 콘텐츠가 없을 수도 있는 여러 콘텐츠 페이지를 정의할 수 있습니다.

1. 열기 *Content2.cshtml* 하 고 다음 섹션을 제거 합니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 페이지를 저장 하 고 브라우저에서 실행 합니다. 콘텐츠 페이지 레이아웃 페이지, 즉 헤더 섹션에에서 정의 된 섹션에 대 한 콘텐츠를 제공 하지 않습니다 오류 메시지가 표시 됩니다.

    ![RenderSection 메서드를 호출 하는 페이지를 실행 하는 경우 발생 하는 오류를 보여 주는 스크린 샷 하지만 해당 섹션에 제공 되지 않습니다.](3-creating-a-consistent-look/_static/image7.jpg)
3. 에 *Shared* 폴더를 엽니다는  *\_Layout2.cshtml* 페이지 하 고이 줄을 바꿉니다.

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    다음 코드로:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    대신 다음 코드 블록 동일한 결과 생성 된 코드의 이전 줄을 바꿀 수 있습니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 실행 된 *Content2.cshtml* 다시 브라우저에서 페이지. (이 페이지를 브라우저에서 엽니다. 여전히 있으면 있습니다 방금 새로 고치면 됩니다.) 이 현재 페이지에 머리글이 있는 경우에 오류 없이 표시 됩니다.

## <a name="passing-data-to-layout-pages"></a>레이아웃 페이지에 대 한 데이터 전달

레이아웃 페이지에서를 참조 해야 하는 콘텐츠 페이지에 정의 된 데이터를 할 수 있습니다. 그렇다면 콘텐츠 페이지의 페이지 레이아웃에 데이터를 전달 해야 합니다. 예를 들어 사용자의 로그인 상태를 표시 하는 것이 좋습니다 또는를 사용자 입력에 따라 콘텐츠 영역을 표시할지는 것이 좋습니다.

데이터를 콘텐츠 페이지에서 페이지 레이아웃을 전달 하려면에 값을 정렬할 수 있습니다는 `PageData` 콘텐츠 페이지의 속성입니다. `PageData` 속성은 페이지 사이 전달 하려면 데이터를 보유 하는 이름/값 쌍의 컬렉션입니다. 레이아웃 페이지에서 다음의 값을 읽을 수는 `PageData` 속성입니다.

다른 다이어그램 다음과 같습니다. ASP.NET 사용 하는 방법을 보여 줍니다이 중 하나는 `PageData` 속성 값을 전달 하는 콘텐츠 페이지 레이아웃 페이지에 있습니다. ASP.NET 웹 페이지를 작성을 시작 하는 경우 생성 된 `PageData` 컬렉션입니다. 콘텐츠 페이지에 데이터를 저장 하는 코드를 작성 하는 `PageData` 컬렉션입니다. 값에 `PageData` 컬렉션 콘텐츠 페이지의 다른 섹션 하거나 콘텐츠 블록을 추가 하 여 액세스할 수도 있습니다.

![콘텐츠 페이지 수는 PageData 사전을 채우는 하 고 페이지 레이아웃 페이지에 해당 정보를 전달 하는 방법을 보여 주는 개념 다이어그램](3-creating-a-consistent-look/_static/image8.jpg)

다음 절차에는 레이아웃 페이지에 콘텐츠 페이지에서 데이터를 전달 하는 방법을 보여 줍니다. 페이지를 실행 하는 경우에 사용자가 페이지 레이아웃 페이지에 정의 된 목록을 표시 하거나 숨길 수 있는 단추가 표시 됩니다. 사용자가 단추를 클릭 하는 경우에 true/false (부울) 값 설정 된 `PageData` 속성입니다. 레이아웃 페이지 그 값을 읽고 false 인 경우 목록을 숨깁니다. 콘텐츠 페이지에도 값은 사용을 표시할지 여부를 결정 하는 **숨길 목록** 단추 또는 **목록 표시** 단추입니다.

![[image]](3-creating-a-consistent-look/_static/image9.jpg)

1. 루트 폴더에 라는 파일을 만듭니다 *Content3.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    라는 두 가지의 데이터를 저장 하는 코드는 `PageData` 속성 &#8212; 제목 웹 페이지 및 true 또는 false 목록을 표시할 것인지 지정할 수 있습니다.

    ASP.NET 코드 블록을 사용 하 여 조건에 따라 페이지에 HTML 태그를 설정할 수 있는지 확인 합니다. 예를 들어는 `if/else` 페이지의 본문에는 블록 폼을 표시 하는지 여부에 따라 결정 `PageData["ShowList"]` 설정을 true로 합니다.
2. 에 *Shared* 폴더를 라는 파일을 만듭니다  *\_Layout3.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    레이아웃 페이지에 식이 포함 되어는 `<title>` 에서 제목 값을 가져오는 요소는 `PageData` 속성입니다. 또한 사용 하 여는 `ShowList` 의 값은 `PageData` 속성을 목록 콘텐츠 블록을 표시할지 여부를 결정 합니다.
3. 에 *Shared* 폴더를 라는 파일을 만듭니다  *\_List.cshtml* 다음 기존 내용을 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 실행 된 *Content3.cshtml* 브라우저에서 페이지입니다. 페이지는 페이지의 왼쪽에 표시 목록에는 및 **숨길 목록** 아래쪽 단추입니다.

    ![목록 및 목록 숨기기 ' 라는 단추를 포함 하는 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image10.jpg)
5. 클릭 **목록 숨기기**합니다. 목록 사라지고 단추가으로 변경 **목록 표시**합니다.

    ![목록과 목록 표시 ' 라는 단추를 포함 하지 않는 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image11.jpg)
6. 클릭는 **목록 표시** 단추 및 목록을 다시 표시 됩니다.

## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
