---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: ASP.NET 웹 페이지 (Razor) 사이트에서 이미지 작업 | Microsoft Docs
author: tfitzmac
description: 이 장에서 추가, 표시 및 이미지를 조작 하는 방법 (크기 조정, 대칭 이동 및 워터 마크 추가) 웹 사이트의.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: e609cd1c6ab74b5b40d28bde353501dbacb5d544
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837591"
---
<a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 이미지 작업
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 추가, 표시 및 이미지를 조작 하는 방법을 보여 줍니다 (크기 조정, 대칭 이동 및 워터 마크 추가)를 ASP.NET Web Pages (Razor) 웹 사이트에 있습니다.
> 
> 학습할 내용:
> 
> - 페이지에 이미지를 동적으로 추가 하는 방법입니다.
> - 사용자가 이미지를 업로드 하는 방법.
> - 이미지 크기를 조정 하는 방법.
> - 대칭 이동 이미지를 회전 하는 방법입니다.
> - 워터 마크 이미지에 추가 하는 방법.
> - 워터 마크로 이미지를 사용 하는 방법입니다.
> 
> ASP.NET 문서에 도입 된 기능을 프로그래밍은 다음과 같습니다.
> 
> - `WebImage` 도우미입니다.
> - `Path` 경로 파일 이름을 조작할 수 있는 메서드를 제공 하는 개체입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서 에서도 WebMatrix 3를 사용 하 여 작동합니다.


<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>웹 페이지에 이미지를 동적으로 추가

추가할 수 있습니다 이미지 개별 페이지에 웹 사이트를 웹 사이트를 개발 하는 동안. 사용자 프로필 사진을 추가할 수 있도록 하는 등의 작업에 유용할 수 있는 이미지를 업로드 할 수도 있습니다.

HTML 페이지에 표시 하려는 이미지에서 이미 사용 가능한 사이트를 사용 하 여 `<img>` 다음과 같은 요소:

[!code-html[Main](9-working-with-images/samples/sample1.html)]

이미지를 동적으로 표시할 수 있게 되기가 필요 하지만 경우에 따라 &#8212; 즉, 알 수 없는 내용 페이지 실행 될 때까지 표시할 이미지입니다.

이 섹션의 절차에는 사용자가 이미지 이름 목록에서 이미지 파일 이름을 지정 하는 위치를 즉석에서 이미지를 표시 하는 방법을 보여 줍니다. 드롭다운 목록에서 이미지의 이름을 선택 하 고 페이지를 전송 하는 경우 선택한 이미지가 표시 됩니다.

![[image]](9-working-with-images/_static/image1.jpg "ch9images 1.jpg")

1. WebMatrix에서 새 웹 사이트를 만듭니다.
2. 명명 된 새 페이지 추가 *DynamicImage.cshtml*합니다.
3. 웹 사이트의 루트 폴더에 새 폴더를 추가 하 고 이름을 *이미지*합니다.
4. 4 개의 이미지를 추가 합니다 *이미지* 방금 만든 폴더입니다. (모든 이미지를 수행 하는 편리한는 있지만 이러한 페이지에 맞아야 합니다.) 이미지 이름 바꾸기 *Photo1.jpg*를 *Photo2.jpg*합니다 *Photo3.jpg*, 및 *Photo4.jpg*합니다. (사용 하지 않는 *Photo4.jpg* 이 있지만 프로시저에서는 문서의 뒷부분에 있습니다.)
5. 읽기 전용으로 이미지 4 개가 표시 되지 않도록 확인 합니다.
6. 다음 페이지에서 기존 콘텐츠를 바꿉니다.

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    페이지의 본문에는 드롭다운 목록 (한 `<select>` 요소) 라는 `photoChoice`. 목록에 세 가지 옵션 및 `value` 각 목록 옵션 특성에 저장 된 이미지 중 하나의 이름이 합니다 *이미지* 폴더입니다. 기본적으로 목록을 선택할 수 있도록와 같은 친숙 한 이름을 &quot;사진 1&quot;, 다음 전달 된 *.jpg* 페이지가 제출 되 면 파일 이름.

    코드를 가져올 수 있습니다 (즉, 이미지 파일 이름) 사용자의 선택 목록에서 참조 하 여 `Request["photoChoice"]`입니다. 먼저 있는지 여부를 선택 영역에 표시 됩니다. 경우에 이미지에 대 한 폴더의 이름 및 사용자의 이미지 파일 이름으로 구성 된 이미지에 대 한 경로 생성 합니다. (경우 경로 생성 하려고 했지만의 경우 nothing `Request["photoChoice"]`, 오류가 표시 됩니다.) 이 인해 다음과 같은 상대 경로:

    *이미지/Photo1.jpg*

    라는 변수에 저장 됩니다 `imagePath` 페이지의 뒷부분에 나오는 해야 합니다.

    본문에서 이기도 한 `<img>` 사용자 선택 하는 이미지를 표시 하는 데 사용 되는 요소입니다. `src` 정적 요소를 표시 하는 것 처럼 특성이 파일 이름 또는 URL로 설정 되지 않습니다. 로 설정 하는 대신 `@imagePath`, 코드에 설정 된 경로에서 값을 가져오는 것을 의미 합니다.

    처음 페이지를 실행 하지만 이미지가 없는 표시할 하므로 사용자는 아무 항목도 선택 되지 않았습니다. 이 일반적으로 구성이 합니다 `src` 특성 비게 되 고 이미지 빨간색으로 표시 됩니다 &quot;x&quot; (또는 모든 브라우저에서 렌더링 이미지를 찾을 수 없는 경우). 이 방지 하려면 배치를 `<img>` 요소에는 `if` 있는지 테스트 하는 블록 여부를 `imagePath` 변수에는 아무 것도 합니다. 사용자 선택 했다면 `imagePath` 경로 포함 합니다. 사용자 이미지를 선택 하지 않은 경우 처음에는이 페이지가 표시 됩니다는 `<img>` 요소도 렌더링 되지 않습니다.
7. 파일을 저장 하 고 브라우저에서 페이지를 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)
8. 드롭다운 목록에서 이미지를 선택한 다음 클릭 **샘플 이미지**합니다. 다양 한 옵션에 대 한 서로 다른 이미지가 표시 되는지 확인 합니다.

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>이미지 업로드

이전 예제에서는 이미지를 동적으로 표시 하는 방법을 보여 주었습니다. 하지만 웹 사이트에 이미 있던 이미지에만 작동 합니다. 이 절차에는 사용자가 다음 페이지에 표시 되는 이미지를 업로드 하는 방법을 보여 줍니다. ASP.NET에서 사용 하 여 즉석에서 이미지를 조작할 수 있습니다는 `WebImage` 만들기, 조작 및 이미지를 저장할 수 있는 방법에 있는 도우미입니다. 합니다 `WebImage` 도우미는 모든 공용 웹 이미지 파일 형식에 포함 하 여 지원 *.jpg*를 *.png*, 및 *.bmp*합니다. 이 기사에서는 사용할지 *.jpg* 이미지를 사용할 수 있습니다 이미지 형식 중 하나입니다.

![[image]](9-working-with-images/_static/image2.jpg "ch9images 2.jpg")

1. 새 페이지를 추가 하 고 이름을 *UploadImage.cshtml*합니다.
2. 다음 페이지에서 기존 콘텐츠를 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    텍스트의 본문에는 `<input type="file">` 사용자가 업로드할 파일을 선택할 수 있는 요소입니다. 클릭 하면 **제출**, 온 파일 폼과 함께 제출 합니다.

    업로드 된 이미지를 가져오려면, 사용 된 `WebImage` 도우미에는 모든 종류의 이미지 작업에 대 한 유용한 메서드는 합니다. 사용 하는 특히 `WebImage.GetImageFromRequest` 를 (있는 경우)에 업로드 된 이미지를 가져오고 라는 변수에 저장 `photo`합니다.

    많은이 예제에서 작업을 가져오고 파일 이름과 경로 설정 해야 합니다. 문제는 되도록 사용자 업로드 한 이미지의 이름 (및 이름)를 가져오고 다음 이미지를 저장 하려는 위치에 대 한 새 경로 만듭니다. 사용자가 동일한 이름을 가진 여러 이미지를 업로드 잠재적으로 수 때문에 약간의 추가 코드를 사용 하 여 고유한 이름을 만들을 사용자가 기존 그림을 덮어쓰지 마십시오 있는지 확인 합니다.

    이미지를 실제로 업로드 된 경우 (테스트 `if (photo != null)`), 이미지의 이미지 이름을 가져올 `FileName` 속성입니다. 사용자 이미지를 업로드 하는 경우 `FileName` 사용자의 컴퓨터에서 경로 포함 하는 사용자의 원래 이름을 포함 합니다. 것 같이 보일 수 있습니다.

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    하지만 해당 경로 정보가 되지 않도록 하려면 &#8212; 원하는 실제 파일 이름 (*SamplePhoto1.jpg*). 사용 하 여 파일 경로에서 제거할 수 있습니다는 `Path.GetFileName` 메서드를 다음과 같이 합니다.

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    그런 다음 원래 이름으로 GUID를 추가 하 여 새 고유한 파일 이름을 만듭니다. (Guid에 대 한 자세한 내용은 참조 하세요 [에 대 한 Guid](#SB_AboutGUIDs) 이 문서의 뒷부분에 나오는.) 다음 이미지를 저장 하는 데 사용할 수 있는 전체 경로 생성 합니다. 저장 경로 새 파일 이름, 폴더 (이미지) 및 현재 웹 사이트 위치를 구성 합니다.

    > [!NOTE]
    > 파일을 저장 하도록 코드를 *이미지* 폴더, 응용 프로그램 해야 읽기 / 쓰기 권한 해당 폴더에 대 한 합니다. 개발 컴퓨터에서이 아닌 경우 일반적으로 문제 그러나 호스팅 공급자의 웹 서버에 사이트를 게시할 때에 해당 권한을 명시적으로 설정 해야 합니다. 호스팅 공급자의 서버에서이 코드를 실행 하 고 오류가 발생 하는 경우 이러한 권한을 설정 하는 방법을 알아보려면 호스팅 공급자를 사용 하 여 확인 합니다.

    저장을 전달 하는 마지막으로 경로 `Save` 메서드를 `WebImage` 도우미입니다. 새 이름으로 업로드 한 이미지를 저장합니다. 저장 메서드는 다음과 같습니다: `photo.Save(@"~\" + imagePath)`합니다. 전체 경로에 추가 됩니다 `@"~\"`의 현재 웹 사이트 위치입니다. (에 대 한 자세한 합니다 `~` 연산자를 참조 하세요 [로 ASP.NET 웹 프로그래밍 Razor 구문 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)

    이전 예에서 같이 페이지의 본문에 포함 된 `<img>` 이미지를 표시 하는 요소입니다. 경우 `imagePath` 설정한 합니다 `<img>` 요소가 렌더링 됩니다 및 해당 `src` 특성이로 설정 된는 `imagePath` 값입니다.
3. 브라우저에서 페이지를 실행 합니다.
4. 이미지를 업로드 하 고 페이지에 표시 되는지 확인 합니다.
5. 사이트에서 엽니다는 *이미지* 폴더입니다. 파일 이름이 다음과 같은 새 파일이 추가 되는 것이 표시: 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*

    이름에 접두사로 지정 하는 GUID를 사용 하 여 업로드 한 이미지입니다. (사용자 고유의 파일에는 다른 GUID를 있고 아마도 이름은 다르게 *MyPhoto.png*.)

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>Guid에 대 한
> 
> GUID (globally unique ID)는 일반적으로 다음과 같은 형식으로 렌더링 되는 식별자: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`합니다. 숫자와 문자 A-f) (에서 각 guid 다르지만 모두 8-4-4-4-12 문자의 그룹을 사용 하 여 패턴을 따릅니다. (기술적으로 GUID는 16 바이트/128 비트 숫자입니다.) GUID를 해야 하는 경우에 GUID를 생성 하는 특수 한 코드를 호출할 수 있습니다. Guid의 기본 개념을 사용 하면 숫자의 엄청난 크기 간에 (3.4 x 10<sup>38</sup>)이 고 생성에 대 한 알고리즘은 결과 수를 거의 라고 보장 종류 중 하나일 수 있습니다. 따라서 Guid이 동일한 이름을 두 번 사용 되지 않습니다 보장 해야 하는 경우 작업의 이름을 생성 하는 것이 좋습니다. 물론 단점은 이름이 코드에만 사용 됩니다 때 사용 되는 경향이 있으므로 Guid 사용자에 게 친숙 한 특히는 되지 않습니다.


<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>이미지 크기 조정

웹 사이트에서 사용자 로부터 이미지를 수락할 경우에 표시 하거나 저장 하기 전에 이미지 크기를 조정 하는 것이 좋습니다. 다시 사용할 수 있습니다는 `WebImage` 이 대 한 도우미입니다.

이 절차에는 미리 보기를 만들고 웹 사이트에서 미리 보기와 원래 이미지를 저장 하려면 업로드 된 이미지 크기를 조정 하는 방법을 보여 줍니다. 페이지의 축소판 그림을 표시 하 고 하이퍼링크를 사용 하 여 큰 이미지에 사용자를 리디렉션할 합니다.

![[image]](9-working-with-images/_static/image3.jpg "ch9images 3.jpg")

1. 명명 된 새 페이지 추가 *Thumbnail.cshtml*합니다.
2. 에 *이미지* 폴더를 라는 하위 폴더를 만듭니다 *thumbs*합니다.
3. 다음 페이지에서 기존 콘텐츠를 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    이 코드는 이전 예제의 코드와 비슷합니다. 차이점은 두 번, 일반적으로 한 번이 코드는 이미지를 저장 하 고 이미지의 축소판 그림 복사본을 만든 후에 한 번입니다. 먼저 업로드 된 이미지를에 저장 합니다 *이미지* 폴더입니다. 그런 다음 미리 보기 이미지에 대 한 새 경로 생성합니다. 미리 보기를 만들려면 실제로 호출 하는 `WebImage` 도우미의 `Resize` 60-60-픽셀 이미지를 만드는 방법. 예제에는 가로 세로 비율을 유지 하는 방법 및 (하는 경우 새 크기는 실제로 크게 이미지) 확대 되 고에서 이미지를 방지 하는 방법을 보여 줍니다. 크기가 조정 된 이미지에 저장 됩니다는 *thumbs* 하위 폴더입니다.

    끝 태그를 사용 하면 동일한 `<img>` 동적 요소 `src` 조건에 따라 이미지를 표시 하려면 앞의 예에서 볼 수 있는 특성입니다. 이 경우 미리 보기를 표시 합니다. 또한 사용 하 여는 `<a>` 이미지의 큰 버전에 대 한 하이퍼링크를 만들려면 요소입니다. 와 마찬가지로 `src` 특성을 `<img>` 요소를 설정한를 `href` 특성을 `<a>` 요소에 따라 동적으로 `imagePath`. 전달 되도록 경로 URL로 작업할 수 있는지, `imagePath` 에 `Html.AttributeEncode` URL에서 확인 된 문자를 경로에 예약 된 문자를 변환 하는 메서드.
4. 브라우저에서 페이지를 실행 합니다.
5. 사진을 업로드 하 고 미리 보기 표시 되는지 확인 합니다.
6. 큰 이미지를 보려면 축소판 그림을 클릭 합니다.
7. 에 *이미지* 하 고 *이미지/엄지 손가락*, 새 파일을 추가한 적이 있는지 확인 합니다.

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>이미지 대칭 이동 및 회전

`WebImage` 도우미 있습니다 대칭 이동 및 회전 이미지입니다. 이 절차에는 서버에서 이미지를 가져오려면, 상하 대칭 이동 이미지를 상하 대칭 (), 저장 한 후 페이지의 대칭 이동 된 이미지를 표시 하는 방법을 보여 줍니다. 이 예제에서는 수만 사용 하는 서버에 이미 있는 파일 (*Photo2.jpg*). 아마도 실제 응용 프로그램에서는 이전 예제에서와 같이 동적으로 가져올 이름이 이미지 대칭 이동할는 있습니다.

![[image]](9-working-with-images/_static/image4.jpg "ch9images 4.jpg")

1. 명명 된 새 페이지 추가 *FlipImage.cshtml*합니다.
2. 다음 페이지에서 기존 콘텐츠를 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    코드를 사용 하는 `WebImage` 서버에서 이미지를 가져오려면 도우미입니다. 이미지를 저장 하는 것에 대 한 이전 예제에서 사용한 동일한 기법을 사용 하 여 이미지의 경로를 만들고 사용 하 여 이미지를 만들 때 해당 경로 전달 하면 `WebImage`:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    이미지 없으면 새 경로 및 파일 이름 앞의 예제에서와 같이 생성 합니다. 이미지 대칭 이동, 호출 하는 `FlipVertical` 메서드를 다음 이미지를 다시 저장 합니다.

    이미지는 다시 사용 하 여 페이지에 표시 됩니다는 `<img>` 요소를 `src` 특성이로 설정 `imagePath`합니다.
3. 브라우저에서 페이지를 실행 합니다. 이미지 *Photo2.jpg* 거꾸로 표시 됩니다.
4. 페이지 새로 고침 또는 다시 확인 하기 위해 이미지 대칭 이동 된 오른쪽 위로 다시 페이지를 요청 합니다.

이미지를 회전 하려면 호출 하는 대신는 점을 제외 하면 동일한 코드를 사용할 합니다 `FlipVertical` 또는 `FlipHorizontal`를 호출 하면 `RotateLeft` 또는 `RotateRight`합니다.

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>워터 마크 이미지 추가

웹 사이트에 이미지를 추가 하면 페이지에 표시 하거나 저장 하기 전에 이미지에 워터 마크를 추가 하는 것이 좋습니다. 사용자는 이미지에 저작권 정보를 추가 하거나 비즈니스 이름별 보급 하려면 종종 워터 마크를 사용 합니다.

![[image]](9-working-with-images/_static/image5.jpg "ch9images 5.jpg")

1. 명명 된 새 페이지 추가 *Watermark.cshtml*합니다.
2. 다음 페이지에서 기존 콘텐츠를 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    이 코드는 코드와는 *FlipImage.cshtml* 앞에서 페이지 (사용 시간이 있지만 합니다 *Photo3.jpg* 파일). 워터 마크를 추가 하려면 호출을 `WebImage` 도우미의 `AddTextWatermark` 이미지를 저장 하기 전에 메서드. 호출에서 `AddTextWatermark`, 텍스트를 전달 &quot;내 워터 마크&quot;, 노랑, 글꼴 색을 설정 하 고 글꼴 패밀리 Arial로 설정 합니다. (여기에 표시 되지 않지만 `WebImage` 도우미 또한 불투명도, 글꼴 패밀리 및 글꼴 크기 및 워터 마크 텍스트의 위치를 지정할 수 있습니다.) 이미지를 저장 하는 경우 읽기 전용 것이 아니어야 합니다.

    사용 하 여 이미지를 페이지에 표시 하기 전에 지금까지 살펴본 대로 합니다 `<img>` src 특성을 가진 요소로 `@imagePath`합니다.
3. 브라우저에서 페이지를 실행 합니다. 이미지의 오른쪽 아래 모서리에 있는 텍스트 "내 워터 마크"를 확인 합니다.

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>워터 마크로 이미지를 사용 하 여

텍스트에 워터 마크를 사용 하는 대신 다른 이미지를 사용할 수 있습니다. 사용자 경우에 따라 회사 로고와 같은 이미지는 워터 마크 또는 사용 하 여 워터 마크 이미지를 텍스트 대신 저작권 정보에 대 한 합니다.

![[image]](9-working-with-images/_static/image6.jpg "ch9images 6.jpg")

1. 명명 된 새 페이지 추가 *ImageWatermark.cshtml*합니다.
2. 이미지를 추가 합니다 *이미지* 로고로 사용 하 고 이미지 이름을 바꿀 수 있는 폴더 *MyCompanyLogo.jpg*합니다. 이 이미지를 볼 수 있는 명확 하 게 80 픽셀에서 20 픽셀 높이를 설정 하면 이미지 있어야 합니다.
3. 다음 페이지에서 기존 콘텐츠를 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    이전 예제에서 코드의 다른 변형입니다. 호출 하는 예에서 `AddImageWatermark` 워터 마크 이미지를 대상 이미지를 추가할 (*Photo3.jpg*) 이미지를 저장 하기 전에 합니다. 호출 하는 경우 `AddImageWatermark`, 80 픽셀에서 20 픽셀 높이를 너비를 설정 합니다. 합니다 *MyCompanyLogo.jpg* 이미지를 가로 방향으로 가운데에 정렬 이며 대상 이미지의 아래쪽에 세로 방향으로 정렬 합니다. 불투명도 100%로 설정 하 고 안쪽 여백 10 픽셀로 설정 됩니다. 워터 마크 이미지 대상 이미지 보다 큰 경우 아무 작업도 수행 합니다. 워터 마크 이미지 대상 이미지 보다 큽니다. 안쪽 여백을 0으로 이미지 워터 마크를 설정 하는 경우 워터 마크는 무시 됩니다.

    사용 하 여 이미지를 표시 하기 전에, 합니다 `<img>` 요소 및 동적 `src` 특성입니다.
4. 브라우저에서 페이지를 실행 합니다. 워터 마크 이미지가 기본 이미지의 맨 아래에 나타나는지 확인 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지 사이트에서 파일 사용](https://go.microsoft.com/fwlink/?LinkId=202896)

[ASP.NET 웹 페이지 Razor 구문을 사용 하 여 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)
