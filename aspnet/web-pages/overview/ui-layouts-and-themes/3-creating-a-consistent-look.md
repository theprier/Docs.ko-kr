---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 일관적인 레이아웃 만들기 | Microsoft Docs
author: Rick-Anderson
description: '보다 효과적으로 만들 웹 페이지 사이트에 대 한 확인을 다시 사용할 수 있는 콘텐츠의 블록입니다 (예: 머리글 및 바닥글) 웹 사이트 및 있습니다 c를 만들 수 있습니다...'
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 83aef41c0baaeca6a25e09b4ea797ce9ee963a85
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021549"
---
<a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 일관적인 레이아웃 만들기
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 사용 하는 방법을 레이아웃 페이지는 ASP.NET Web Pages (Razor) 웹 사이트에서 다시 사용할 수 있는 콘텐츠의 블록입니다 (예: 머리글 및 바닥글)를 만들고 사이트의 모든 페이지에 일관 된 모양을 만들려면 설명 합니다.
> 
> **학습할 내용:** 
> 
> - 머리글 및 바닥글 같은 콘텐츠 재사용 가능한 블록을 만드는 방법입니다.
> - 레이아웃을 사용 하 여 사이트에서 모든 페이지에 일관 된 모양을 만드는 방법입니다.
> - 레이아웃 페이지에 런타임 시 데이터를 전달 하는 방법입니다.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - 여러 페이지에 삽입할 HTML 형식의 콘텐츠를 포함 하는 파일에는 콘텐츠 블록입니다.
> - 레이아웃 페이지는 웹 사이트의 페이지에서 공유할 수 있는 HTML 형식의 콘텐츠를 포함 하는 페이지입니다.
> - `RenderPage`, `RenderBody`, 및 `RenderSection` ASP.NET 페이지 요소를 삽입할 위치를 알 수 있는 방법입니다.
> - `PageData` 콘텐츠 블록 및 페이지 레이아웃 간에 데이터를 공유할 수 있는 사전입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


## <a name="about-layout-pages"></a>레이아웃 페이지에 대 한

많은 웹 사이트에는 머리글 및 바닥글 또는 로그인는 사용자가 지시 하는 상자와 같은 모든 페이지에 표시 되는 내용이 있습니다. ASP.NET을 통해 텍스트, 태그 및 일반 웹 페이지와 마찬가지로 코드를 포함할 수 있는 콘텐츠 블록을 사용 하 여 별도 파일을 만들 수 있습니다. 다음 정보를 표시 하려는 사이트의 다른 페이지에서 콘텐츠 블록을 삽입할 수 있습니다. 이렇게 복사한 모든 페이지에 동일한 콘텐츠를 붙여넣이 필요가 없습니다. 다음과 같은 일반적인 콘텐츠 만들기도 쉽게 사이트를 업데이트 합니다. 콘텐츠를 변경 해야 하 고 단일 파일을 업데이트 하는 다음 변경 내용이 everywhere 반영 하는 경우 콘텐츠 삽입 되었습니다.

다음 다이어그램은 콘텐츠 작업을 차단 하는 방법을 보여 줍니다. ASP.NET 지점에 콘텐츠 블록을 삽입 웹 서버에서 페이지를 요청 하는 브라우저, 여기서는 `RenderPage` 기본 페이지에서 호출 됩니다. 완료 (병합된) 페이지를 브라우저로 전송 됩니다.

![현재 페이지에 RenderPage 메서드 참조 페이지를 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image1.jpg)

이 절차에서는 별도 파일에 있는 두 개의 콘텐츠 블록 (헤더 및 바닥글)를 참조 하는 페이지를 만들어야 합니다. 사이트의 모든 페이지에 이러한 동일한 콘텐츠 블록을 사용할 수 있습니다. 완료 되 면 다음과 같은 페이지가 표시 됩니다.

![RenderPage 메서드에 대 한 호출을 포함 하는 페이지 실행 결과로 생성 되는 브라우저에서 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image2.jpg)

1. 웹 사이트의 루트 폴더에서 이라는 파일을 만듭니다 *Index.cshtml*합니다.
2. 기존 태그를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 루트 폴더에서 라는 폴더를 만듭니다 *공유*합니다.

    > [!NOTE]
    > 라는 폴더에 웹 페이지 간에 공유 되는 파일을 저장 하는 일반적인 방법은 것 *공유*합니다.
4. 에 *공유* 폴더에 라는 파일을 만듭니다  *\_Header.cshtml*합니다.
5. 모든 기존 내용을 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    파일 이름은 되었다는  *\_Header.cshtml*를 밑줄로 (\_) 접두사로 합니다. 해당 이름이 밑줄로 시작 하는 경우 ASP.NET 브라우저 페이지를 보내지 않습니다. 이 페이지를 요청 (실수로 또는 그렇지 않은 경우) 이러한 직접에서 사용자를 방지 합니다. 이러한 페이지를 요청할 수 있도록 사용자가 실제로 않으려고 하기 때문에 콘텐츠 블록에 있는 페이지 이름에 밑줄을 사용 하는 것이 좋습니다 &#8212; 다른 페이지에 삽입할 엄격 하 게 존재 합니다.
6. *공유* 폴더를 라는 파일을 만듭니다  *\_Footer.cshtml* 및 콘텐츠를 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. 에 *Index.cshtml* 페이지에서 두 개의 호출을 추가 합니다 `RenderPage` 메서드를 다음과 같이:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    이 웹 페이지에는 콘텐츠 블록을 삽입 하는 방법을 보여 줍니다. 호출 된 `RenderPage` 메서드 이때 삽입 하려는 내용이 파일의 이름을 전달 합니다. 콘텐츠를 삽입 하는 여기에  *\_Header.cshtml* 및  *\_Footer.cshtml* 파일에 *Index.cshtml* 파일입니다.
8. 실행 합니다 *Index.cshtml* 브라우저에서 페이지입니다. (WebMatrix에서에 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 하 고 선택한 **브라우저에서 시작**.)
9. 브라우저에서 페이지 소스를 봅니다. (예를 들어, Internet Explorer에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **소스 보기**.)

    이 콘텐츠 블록을 사용 하 여 인덱스 페이지 태그를 결합 하는 브라우저로 전송 되는 웹 페이지 태그를 볼 수 있습니다. 다음 예제에 대 한 렌더링 되는 페이지 소스를 보여 줍니다 *Index.cshtml*합니다. 에 대 한 호출 `RenderPage` 에 삽입 *Index.cshtml* 머리글 및 바닥글 파일의 실제 내용으로 대체 되었습니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>레이아웃 페이지를 사용 하 여 일관적인 모양 만들기

지금까지 여러 페이지에 동일한 콘텐츠를 포함 하도록 쉽습니다 살펴보았습니다. 사이트에 대 한 일관적인 모양 만들기를 더 구조화 된 접근 방식은 레이아웃 페이지를 사용 하는 것입니다. 레이아웃 페이지는 웹 페이지의 구조를 정의 하지만 실제 콘텐츠를 포함 하지 않습니다. 레이아웃 페이지를 만든 후에 콘텐츠를 포함 하 고 레이아웃 페이지에 연결 하는 웹 페이지를 만들 수 있습니다. 이러한 페이지에 표시 되는 경우 레이아웃 페이지에 따라 포맷 됩니다. (이러한 관점에서 레이아웃 페이지는 역할을 일종의 다른 페이지에 정의 된 콘텐츠에 대 한 템플릿입니다.)

레이아웃 페이지는 모든 HTML 페이지와 마찬가지로 제외에 대 한 호출을 포함 하는 `RenderBody` 메서드. 위치는 `RenderBody` 메서드 레이아웃 페이지의 콘텐츠 페이지에서 정보를 포함 될 위치를 결정 합니다.

다음 다이어그램에서는 콘텐츠 페이지 및 레이아웃 페이지 완성된 된 웹 페이지를 생성 하기 위해 런타임에 결합 됩니다. 브라우저는 콘텐츠 페이지를 요청합니다. 콘텐츠 페이지에는 코드 페이지의 구조에 사용할 레이아웃 페이지를 지정 하는 합니다. 레이아웃 페이지에서 콘텐츠는 지점에 삽입 위치를 `RenderBody` 메서드가 호출 됩니다. 블록도 삽입할 수 레이아웃 페이지를 호출 하 여 콘텐츠를 `RenderPage` 메서드, 이전 섹션에서 수행한 방식입니다. 웹 페이지를 완료 하는 경우 브라우저에 전송 됩니다.

![RenderBody 메서드에 대 한 호출을 포함 하는 페이지 실행 결과로 생성 되는 브라우저에서 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image3.jpg)

다음 절차에는 레이아웃 페이지 및 링크 콘텐츠 페이지를 만드는 방법을 보여 줍니다.

1. 에 *Shared* 웹 사이트의 폴더 라는 파일을 만듭니다  *\_Layout1.cshtml*합니다.
2. 모든 기존 내용을 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    사용 된 `RenderPage` 콘텐츠 블록을 삽입할 레이아웃 페이지에는 메서드. 레이아웃 페이지에는 한 번만 호출 포함 될 수 있습니다는 `RenderBody` 메서드.
3. 에 *공유* 폴더를 이라는 파일을 만듭니다  *\_Header2.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 루트 폴더에 새 폴더를 만들고 이름을 *스타일*합니다.
5. 에 *스타일* 폴더에 라는 파일을 만듭니다 *Site.css* 다음 스타일 정의 추가 하 고:

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    이러한 스타일을 정의 하려는 여기만 레이아웃 페이지를 사용 하 여 스타일 시트를 사용할 수 있는 방법을 보여 줍니다. 원하는 경우 이러한 요소에 대 한 사용자 고유의 스타일을 정의할 수 있습니다.
6. 루트 폴더에서 이라는 파일을 만듭니다 *Content1.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    레이아웃 페이지를 사용 하는 페이지입니다. 페이지의 맨 위에 있는 코드 블록은이 콘텐츠 형식을 지정 하는 데는 레이아웃 페이지를 나타냅니다.
7. 실행할 *Content1.cshtml* 브라우저에서 합니다. 렌더링된 된 페이지 형식을 사용 및 스타일 시트에 정의 된  *\_Layout1.cshtml* 에 정의 된 텍스트 (콘텐츠)와 *Content1.cshtml*합니다.

    ![[이미지]](3-creating-a-consistent-look/_static/image4.jpg)

    그런 다음 동일한 레이아웃 페이지를 공유할 수 있는 추가 콘텐츠 페이지를 만들려면 6 단계를 반복할 수 있습니다.

    > [!NOTE]
    > 폴더에 있는 모든 콘텐츠 페이지에 대 한 동일한 레이아웃 페이지를 자동으로 사용할 수 있도록 사이트를 설정할 수 있습니다. 자세한 내용은 참조 하세요 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)합니다.

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>여러 콘텐츠 섹션이 포함 된 레이아웃 페이지 디자인

콘텐츠 페이지를 대체할 수 있는 콘텐츠를 사용 하 여 여러 영역에 있는 레이아웃을 사용 하려는 경우 유용한 섹션이 여러 개 있을 수 있습니다. 콘텐츠 페이지에서 각 섹션 이름은 고유를 제공합니다. (기본 섹션 그대로 명명 되지 않은.) 레이아웃 페이지에서 추가 `RenderBody` 명명 되지 않은 (기본) 섹션은 표시할 위치를 지정 하는 방법입니다. 그런 다음 별도 추가 `RenderSection` 개별적으로 명명 된 섹션을 렌더링 하기 위해 메서드.

다음 다이어그램에서는 ASP.NET에서 여러 섹션으로 구분 되는 콘텐츠를 처리 하는 방법을 보여 줍니다. 각 명명 된 섹션은 섹션 블록 콘텐츠 페이지에 포함 되어 있습니다. (이름을 `Header` 고 `List` 예제에서입니다.) 프레임 워크 시점 레이아웃 페이지에 콘텐츠 섹션을 삽입 위치를 `RenderSection` 메서드가 호출 됩니다. 명명 되지 않은 (기본) 섹션의 지점에 삽입 됩니다 여기서는 `RenderBody` 앞서 살펴본 메서드가 호출 됩니다.

![RenderSection 메서드 참조 섹션에서는 현재 페이지에 삽입 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image5.jpg)

이 절차에는 여러 콘텐츠 섹션에 있는 콘텐츠 페이지를 만드는 방법 및 여러 콘텐츠 섹션을 지 원하는 레이아웃 페이지를 사용 하 여 렌더링 하는 방법을 보여 줍니다.

1. 에 *공유* 폴더에 라는 파일을 만듭니다  *\_Layout2.cshtml*합니다.
2. 모든 기존 내용을 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    사용 된 `RenderSection` 헤더와 목록 섹션을 렌더링 하는 방법입니다.
3. 루트 폴더에서 이라는 파일을 만듭니다 *Content2.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    이 콘텐츠 페이지는 페이지의 맨 위에 있는 코드 블록을 포함합니다. 각 명명 된 섹션은 섹션 블록에 포함 됩니다. 페이지의 나머지 기본 (명명 되지 않은) 콘텐츠 섹션을 포함 합니다.
4. 실행할 *Content2.cshtml* 브라우저에서 합니다.

    ![RenderSection 메서드에 대 한 호출을 포함 하는 페이지 실행 결과로 생성 되는 브라우저에서 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image6.jpg)

## <a name="making-content-sections-optional"></a>선택적 콘텐츠 섹션 만들기

일반적으로 콘텐츠 페이지에서 만든 섹션 레이아웃 페이지에 정의 된 섹션을 일치 해야 합니다. 다음 중 하나가 발생할 경우 오류를 가져올 수 있습니다.

- 콘텐츠 페이지 레이아웃 페이지에서 해당 섹션이 포함 된 섹션에 포함 되어 있습니다.
- 레이아웃 페이지에 콘텐츠가 없는 섹션을 포함 합니다.
- 레이아웃 페이지 같은 섹션을 두 번 이상 렌더링 하려고 하는 메서드 호출을 포함 합니다.

그러나 레이아웃 페이지에서 선택적 섹션을 선언 하 여 명명된 된 섹션에 대 한이 동작을 재정의할 수 있습니다. 이 레이아웃 페이지를 공유할 수는 있지만 수도 특정 섹션에 대 한 콘텐츠 없을 수 있는 여러 콘텐츠 페이지를 정의할 수 있습니다.

1. 오픈 *Content2.cshtml* 및 다음 섹션을 제거 합니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 페이지를 저장 하 고 브라우저에서 실행 합니다. 콘텐츠 페이지 레이아웃 페이지, 즉 헤더 섹션에에서 정의 된 섹션에 대 한 콘텐츠를 제공 하지 않습니다 오류 메시지가 표시 됩니다.

    ![RenderSection 메서드를 호출 하는 페이지를 실행 하는 경우 발생 하는 오류를 보여 주는 스크린샷 하 하지만 해당 섹션이 제공 되지 않았습니다.](3-creating-a-consistent-look/_static/image7.jpg)
3. 에 *Shared* 폴더를 열고 합니다  *\_Layout2.cshtml* 이 줄을 바꾸고 페이지:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    다음 코드를 사용 하 여

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    대신 동일한 결과 생성 하는 다음 코드 블록을 사용 하 여 이전 코드 줄을 대체할 수 있습니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 실행 합니다 *Content2.cshtml* 다시 브라우저에서 페이지입니다. (아직이 페이지를 브라우저에서 연 경우 있습니다만 새로 고칠 수 있습니다.) 이 이번에 머리글이 있는 경우에 페이지 오류 없이 표시 됩니다.

## <a name="passing-data-to-layout-pages"></a>레이아웃 페이지에 데이터 전달

레이아웃 페이지를 참조 해야 하는 콘텐츠 페이지에 정의 된 데이터를 할 수도 있습니다. 그렇다면, 레이아웃 페이지에 콘텐츠 페이지에서 데이터를 전달 해야 합니다. 예를 들어, 사용자의 로그인 상태를 표시 하려는 경우 또는 사용자 입력을 기반으로 하는 콘텐츠 영역을 표시할지 하려는 될 수 있습니다.

레이아웃 페이지에 콘텐츠 페이지 로부터 데이터를 전달,에 값을 삽입할 수는 `PageData` 콘텐츠 페이지의 속성입니다. `PageData` 속성은 페이지 사이 전달 하려는 데이터를 저장 하는 이름/값 쌍의 컬렉션입니다. 레이아웃 페이지에서 다음의 값을 읽을 수는 `PageData` 속성입니다.

다른 다이어그램 다음과 같습니다. ASP.NET을 사용 하는 방법을 보여 줍니다 이와 `PageData` 레이아웃 페이지에 콘텐츠 페이지 로부터 값을 전달할 속성입니다. ASP.NET 웹 페이지 작성을 시작 하는 경우 생성 된 `PageData` 컬렉션입니다. 콘텐츠 페이지 데이터를 배치 하는 코드를 작성 합니다 `PageData` 컬렉션입니다. 값은 `PageData` 컬렉션 콘텐츠 블록을 추가 하거나 콘텐츠 페이지의 다른 섹션에서 액세스할 수도 있습니다.

![콘텐츠 페이지 수 PageData 사전을 채우는 하 고 레이아웃 페이지에 해당 정보를 전달 하는 방법을 보여 주는 개념 다이어그램입니다.](3-creating-a-consistent-look/_static/image8.jpg)

다음 절차에는 레이아웃 페이지에 콘텐츠 페이지 로부터 데이터를 전달 하는 방법을 보여 줍니다. 페이지를 실행 하는 경우 사용자가 레이아웃 페이지에 정의 된 목록을 표시 하거나 숨길 수 있는 단추를 표시 합니다. 사용자가 단추를 클릭 하는 경우에 true/false (부울) 값 설정 된 `PageData` 속성입니다. 레이아웃 페이지 해당 값을 읽고 false 인 경우 목록을 숨깁니다. 값도는 콘텐츠 페이지를 표시할지 여부를 결정 하는 **숨기기 목록** 단추 또는 **목록 표시** 단추입니다.

![[이미지]](3-creating-a-consistent-look/_static/image9.jpg)

1. 루트 폴더에서 이라는 파일을 만듭니다 *Content3.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    두 가지에 대 한 데이터를 저장 하는 코드를 `PageData` 속성 &#8212; 웹 페이지 및 true 또는 false를 목록을 표시할지 여부를 지정 하는 제목입니다.

    ASP.NET을 사용 조건에 따라 코드 블록을 사용 하 여 페이지에 HTML 태그를 추가할 수 있습니다를 확인 합니다. 예를 들어 합니다 `if/else` 여부에 따라 표시할 형태를 결정 하는 페이지의 본문에는 블록 `PageData["ShowList"]` 설정 된 true로 합니다.
2. 에 *공유* 폴더를 이라는 파일을 만듭니다  *\_Layout3.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    레이아웃 페이지에는 식을 포함 합니다 `<title>` 요소에서 title 값을 가져오는 `PageData` 속성입니다. 또한 사용 하 여는 `ShowList` 의 값을 `PageData` 목록 콘텐츠 블록을 표시할지 여부를 결정 하는 속성입니다.
3. 에 *공유* 폴더를 이라는 파일을 만듭니다  *\_List.cshtml* 기존 내용을 다음으로 바꿉니다.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 실행 합니다 *Content3.cshtml* 브라우저에서 페이지입니다. 페이지의 왼쪽에 표시 된 목록을 사용 하 여 페이지가 표시 됩니다 및 **숨기기 목록** 아래쪽 단추입니다.

    ![목록 및 목록 숨기기 ' 라는 단추를 포함 하는 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image10.jpg)
5. 클릭 **목록 숨기기**합니다. 목록 사라지고 단추가로 바뀝니다 **표시 목록**합니다.

    ![목록 및 목록 표시 ' 라는 단추를 포함 하지 않는 페이지를 보여주는 스크린샷.](3-creating-a-consistent-look/_static/image11.jpg)
6. 클릭 합니다 **표시 목록** 단추 및 목록을 다시 표시 됩니다.

## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
