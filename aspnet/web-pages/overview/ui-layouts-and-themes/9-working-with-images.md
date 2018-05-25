---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: ASP.NET 웹 페이지 (Razor) 사이트에 이미지 작업 | Microsoft Docs
author: tfitzmac
description: 이 장에서 추가, 표시 및 이미지를 조작 하는 방법을 보여줍니다. (크기 조정, 대칭 이동, 및 워터 마크 추가할) 웹 사이트에 있습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 74838dd364a43f3f4c966c1417d0f0b2cc242f28
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 이미지 작업
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 추가, 표시 및 이미지를 조작 하는 방법을 보여 줍니다 (크기 조정, 대칭 이동, 및 워터 마크 추가할) ASP.NET 웹 페이지 (Razor) 웹 사이트에서.
> 
> 학습 내용:
> 
> - 페이지에 이미지를 동적으로 추가 하는 방법.
> - 사용자가 이미지를 업로드 하는 방법.
> - 이미지 크기를 조정 하는 방법.
> - 대칭 이동 또는 이미지를 회전 하는 방법.
> - 워터 마크 이미지에 추가 하는 방법.
> - 워터 마크로 이미지를 사용 하는 방법.
> 
> 다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.
> 
> - `WebImage` 도우미입니다.
> - `Path` 경로 파일 이름을 조작할 수 있도록 하는 메서드를 제공 하는 개체입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동합니다.


<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>웹 페이지에 이미지를 동적으로 추가

추가할 수 있습니다 이미지 웹 사이트를 개별 페이지를 웹 사이트를 개발 하는 동안. 이러한 프로필 사진 추가 등의 작업에 유용할 수 있는 이미지를 업로드 하는 사용자가 하도록 허용할 수도 있습니다.

HTML을 사용 하 여 이미지는 사이트에서 이미 사용할 수 있는 페이지에 표시 하려는 경우 `<img>` 다음과 같이 요소:

[!code-html[Main](9-working-with-images/samples/sample1.html)]

이미지를 동적으로 표시 하려면 필요 하지만, 경우에 따라 & #8212; 즉, 어떤 표시할 이미지를 페이지 될 때까지 실행에 대해 모릅니다.

이 섹션의 절차에는 사용자가 이미지 이름 목록에서 이미지 파일 이름을 지정 하는 위치에서 바로 이미지를 표시 하는 방법을 보여 줍니다. 드롭 다운 목록에서 이미지의 이름을 선택 하 고 페이지를 전송 하는 경우 선택한 이미지가 표시 됩니다.

![[image] ] (9-working-with-images/_static/image1.jpg "ch9images 1.jpg")

1. WebMatrix에서 새 웹 사이트를 만듭니다.
2. 명명 된 새 페이지 추가 *DynamicImage.cshtml*합니다.
3. 웹 사이트의 루트 폴더에 새 폴더를 추가 하 고 이름을 *이미지*합니다.
4. 에 이미지를 4 개의 추가 *이미지* 방금 만든 폴더입니다. (모든 이미지를 편리 합니다 있지만 페이지에 맞아야 합니다.) 이미지 이름 바꾸기 *Photo1.jpg*, *Photo2.jpg*, *Photo3.jpg*, 및 *Photo4.jpg*합니다. (사용 하지 않고 기존 *Photo4.jpg* 이 있지만 프로시저를 사용 하 여이 문서의 뒷부분에 있습니다.)
5. 4 개의 이미지 읽기 전용으로 표시 되지 않은 것을 확인 합니다.
6. 다음 페이지에서 기존 내용을 바꿉니다.

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    페이지의 본문에 드롭 다운 목록 (한 `<select>` 요소) 라는 `photoChoice`합니다. 목록에는 세 가지 옵션 및 `value` 각 목록 옵션의 특성에 저장 된 이미지 중 하나의 이름이 고 *이미지* 폴더입니다. 기본적으로, 목록을 선택할 수 있도록와 같은 친숙 한 이름을 &quot;사진 1&quot;, 다음 전달는 *.jpg* 전송 될 때 파일 이름입니다.

    코드를 가져올 수 있습니다 (즉, 이미지 파일 이름) 사용자의 선택 목록에서 참조 하 여 `Request["photoChoice"]`합니다. 먼저 경우 선택 내용이 없는 전혀 표시 됩니다. 없을 경우, 이미지에 대 한 폴더의 이름 및 사용자의 이미지 파일 이름으로 구성 된 이미지에 대 한 경로 생성 합니다. (경우 경로 생성 하려고 했지만의 경우 nothing `Request["photoChoice"]`, 오류가 발생 합니다.) 이 인해 다음과 같은 상대 경로:

    *이미지/Photo1.jpg*

    경로 이라는 변수에 저장 됩니다 `imagePath` 페이지의 뒷부분에 나오는 넣어야 합니다.

    본문에서 이기도 한 `<img>` 사용자 선택 하는 이미지를 표시 하는 데 사용 되는 요소입니다. `src` 특성 같이 정적 요소를 표시 하는 파일 이름 또는 URL을으로 설정 합니다. 로 설정 하는 대신, `@imagePath`, 코드에 설정 된 경로에서 값을 가져오는 것을 의미 합니다.

    페이지를 실행 하는 처음으로 하지만, 이미지가 없는 표시 하려면는 사용자의 아무 것도 선택 하지 않았습니다. 구성이 정상적으로이 `src` 특성 비게 되 고 이미지 빨간색으로 표시 됩니다 &quot;x&quot; (또는 어떤 브라우저에서 렌더링 이미지를 찾을 수 없는 경우). 이 방지 하려면 삽입는 `<img>` 요소에는 `if` 를 테스트 하는 블록 여부는 `imagePath` 변수에는 아무 것도 합니다. 사용자 선택 항목을 만들 경우 `imagePath` 경로 포함 합니다. 처음으로이 페이지가 표시 됩니다, 또는 사용자 이미지를 선택 하지 않은 경우는 `<img>` 요소가 렌더링 되지 않습니다.
7. 파일을 저장 하 고 브라우저에서 페이지를 실행 합니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)
8. 드롭다운 목록에서 이미지를 선택한 다음 클릭 **샘플 이미지**합니다. 다른 선택 항목에 대 한 서로 다른 이미지에 표시 되는지 확인 합니다.

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>이미지를 업로드 하는 중

이전 예제에서는 이미지를 동적으로 표시 하는 방법을 보여 주었습니다. 하지만 웹 사이트에 이미 있던 이미지에만 작동 합니다. 이 절차에서는 사용자가 다음 페이지에 표시 되는 이미지를 업로드 하는 방법을 설명 합니다. Asp.net에서 사용 하 여 즉시에서 이미지를 조작할 수 있습니다는 `WebImage` 도우미에는 만들기, 조작 및 이미지를 저장할 수 있는 방법입니다. `WebImage` 도우미 원하는 모든 공통 웹 이미지 파일 형식에 포함 하 여 *.jpg*, *.png*, 및 *.bmp*합니다. 이 문서 전체에서 사용 하 여 *.jpg* 이미지 형식 중 하나는 이미지, 하지만 있습니다 사용할 수 있습니다.

![[image] ] (9-working-with-images/_static/image2.jpg "ch9images 2.jpg")

1. 새 페이지를 추가 하 고 이름을 *UploadImage.cshtml*합니다.
2. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    텍스트의 본문에는 `<input type="file">` 요소를 사용자가 업로드할 파일을 선택할 수 있습니다. 클릭할 때 **전송**, 온 파일 양식과 함께 전송 됩니다.

    업로드 된 이미지를 얻기 위해 사용 하는 `WebImage` 도우미에는 이미지 작업에 대 한 유용한 메서드의 모든 종류입니다. 특히 사용할 `WebImage.GetImageFromRequest` (있는 경우)에 업로드 된 이미지를 얻은 이라는 변수에 저장 하도록 `photo`합니다.

    많은이 예에서 작업을 가져오고 파일 및 경로 이름을 설정 해야 합니다. 문제는 것인지는 사용자가 업로드 되는 이미지의 이름 (및 이름만)를 가져오고 다음 이미지를 저장 하려는 대 한 새 경로 만듭니다. 사용자가 동일한 이름을 가진 여러 이미지를 업로드 잠재적으로 수 때문에 고유한 이름을 만들 사용자가 기존 그림을 덮어쓰지 마십시오 선택 되어 있는지 확인 하십시오 약간의 추가 코드를 사용 합니다.

    이미지 실제로 업로드 한 경우 (테스트 `if (photo != null)`)에서 이미지의 이미지 이름을 가져오는 `FileName` 속성입니다. 사용자 이미지를 업로드 하는 경우 `FileName` 사용자의 컴퓨터에서 경로 포함 하는 사용자의 원래 이름을 포함 합니다. 그는 다음과 같이 표시 될 수 있습니다.

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    그러나 해당 경로 정보가 되지 않도록 하려면 & #8212; 려는 실제 파일 이름 (*SamplePhoto1.jpg*). 사용 하 여 경로에서 파일만 제거할 수 있습니다는 `Path.GetFileName` 다음과 같이 메서드:

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    그런 다음 새 고유한 파일 이름을 원래 이름으로 GUID를 추가 하 여 만듭니다. (Guid에 대 한 자세한 내용은 [에 대 한 Guid](#SB_AboutGUIDs) 이 문서의 뒷부분에 나오는.) 다음 이미지를 저장 하는 데 사용할 수 있는 전체 경로 작성 합니다. 저장 경로 새 파일 이름, 폴더 (이미지) 및 현재 웹 사이트 위치에 구성 된 합니다.

    > [!NOTE]
    > 파일을 저장할 코드에 대 한 순서 대로 *이미지* 폴더, 응용 프로그램이 필요한 읽기 / 쓰기 해당 폴더에 대 한 권한. 개발 컴퓨터에서이 발생 하지 않습니다 일반적으로 합니다. 그러나 호스팅 공급자의 웹 서버에 사이트를 게시 하는 경우에 해당 권한을 명시적으로 설정 해야 합니다. 호스팅 공급자의 서버에서이 코드를 실행 하 고 오류가 발생 하는 경우에 이러한 권한을 설정 하는 방법을 알아보려면 호스팅 공급자와 함께 확인 합니다.

    저장을 전달 하는 마지막으로,에 대 한 경로 `Save` 의 메서드는 `WebImage` 도우미입니다. 새 이름으로 업로드 된 이미지를 저장합니다. 저장 메서드는 다음과 같습니다: `photo.Save(@"~\" + imagePath)`합니다. 전체 경로에 추가 됩니다 `@"~\"`는 현재 웹 사이트 위치입니다. (에 대 한 내용은 `~` 연산자 참조 [ASP.NET 웹 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)

    페이지의 본문에 포함 되어 앞의 예와 `<img>` 요소 이미지를 표시 합니다. 경우 `imagePath` 설정 되어는 `<img>` 요소가 렌더링 및 해당 `src` 특성이로 설정 된는 `imagePath` 값입니다.
3. 브라우저에서 페이지를 실행 합니다.
4. 이미지를 업로드 하 고 페이지에 표시 되는지 확인 합니다.
5. 사이트를 열고는 *이미지* 폴더입니다. 새 파일의 이름은 다음과 같은 모양의 추가 된 참조:: 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*

    이름에 접두어로 추가 되는 GUID와 함께 업로드 하는 이미지입니다. (파일을 직접 다른 guid이 고 아마도 이름이 다른 값 *MyPhoto.png*.)

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>Guid에 대 한
> 
> GUID (globally unique ID)는 일반적으로 다음과 같은 형식으로 렌더링 되는 식별자: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`합니다. 숫자와 문자 (A-F)에서 각 GUID에 대 한 다르지만, 모든 8-4-4-4-12 문자 그룹을 사용 하 여 패턴을 따릅니다. (기술적으로 GUID는 16 바이트/128 비트 숫자입니다.) GUID를 해야 하는 경우 사용자에 대 한 GUID를 생성 하는 특수화 된 코드를 호출할 수 있습니다. Guid의 기본 개념은 숫자의 엄청난 크기 간의 (3.4 x 10<sup>38</sup>) 및 생성에 대 한 알고리즘을 결과 수는 거의 항상 종류 중 하나입니다. Guid에는 따라서 이름이 같은 두 번 사용 하지 않도록 해야 하는 경우 작업의 이름을 생성 하는 좋은 방법입니다. 단점은는 물론, Guid는 이름이 코드에만 사용 될 때 사용할 경향이 있으므로 특히 사용 하기 편리해 되지 해당입니다.


<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>이미지 크기 조정

웹 사이트에서 사용자 로부터 이미지를 표시 하거나 저장 하기 전에 이미지 크기를 조정 하는 것이 좋습니다. 다시 사용할 수 있습니다는 `WebImage` 이 대 한 도우미입니다.

이 절차에서는 미리 보기를 만들고 웹 사이트의 축소판 그림 및 원본 이미지 저장에 업로드 된 이미지의 크기를 조정 하는 방법을 보여 줍니다. 미리 보기 페이지에 표시 하 고 하이퍼링크를 사용 하 여 큰 이미지를 사용자가 리디렉션할 합니다.

![[image] ] (9-working-with-images/_static/image3.jpg "ch9images 3.jpg")

1. 명명 된 새 페이지 추가 *Thumbnail.cshtml*합니다.
2. 에 *이미지* 폴더 라는 하위 폴더를 만들 *엄지*합니다.
3. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    이 코드는 이전 예제에서 코드와 비슷합니다. 차이점은 두 번, 일반적으로 한 번이 코드는 이미지를 저장 하는 이미지의 축소판 그림 복사본을 만든 후 한 번입니다. 먼저 업로드 된 이미지 될를에 저장 된 *이미지* 폴더입니다. 다음 미리 보기 이미지에 대 한 새 경로 작성 합니다. 호출 하면 미리 보기를 만들려면 실제로 `WebImage` 도우미의 `Resize` 60-픽셀 60 픽셀 이미지를 만드는 메서드. (경우에 새 크기는 실제로 커질 이미지) 확장 되는지에서 이미지를 방지 하는 방법 및 가로 세로 비율을 유지 하는 방법을 보여 줍니다. 크기 조정된 된 이미지에 저장 한 다음 됩니다는 *엄지* 하위 폴더입니다.

    끝 태그에 사용 하면 동일한 `<img>` 동적 인 요소 `src` 특성 조건에 따라 이미지를 표시 하도록 이전 예제에 나와 있는 것입니다. 이 경우 미리 보기를 표시 합니다. 또한 사용는 `<a>` 큰 이미지의 버전에 대 한 하이퍼링크를 만들 요소입니다. 와 마찬가지로 `src` 특성의는 `<img>` 요소를 설정한는 `href` 특성에는 `<a>` 요소에서 무엇이를 동적으로 `imagePath`합니다. 를 경로 URL로 사용할 수 있는지 확인 하려면 전달 `imagePath` 에 `Html.AttributeEncode` 경로에 예약 된 문자를 URL에 확인 된 문자를 변환 하는 메서드.
4. 브라우저에서 페이지를 실행 합니다.
5. 사진 업로드 및 축소판 그림 표시 되는지 확인 하십시오.
6. 큰 이미지를 참조 하도록 미리 보기를 클릭 합니다.
7. 에 *이미지* 및 *이미지/엄지*, 추가 된 새 파일을 확인 합니다.

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>이미지 대칭 이동 및 회전

`WebImage` 도우미 수도 있습니다 대칭 이동 및 회전 이미지입니다. 이 절차에서는 서버에서 이미지를 가져올 상하로 대칭 이동 이미지 180도 회전 () 저장 하 고 다음 페이지에 대칭 이동한 이미지를 표시 하는 방법을 보여 줍니다. 이 예제에서는 방금 사용 하는 서버에 이미 있는 파일 (*Photo2.jpg*). 아마도 실제 응용 프로그램에서 이미지 이름이 이전 예제에서와 같이 동적으로 가져올 대칭 이동할 것 있습니다.

![[image] ] (9-working-with-images/_static/image4.jpg "ch9images 4.jpg")

1. 명명 된 새 페이지 추가 *FlipImage.cshtml*합니다.
2. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    코드를 사용 하 여는 `WebImage` 도우미는 서버에서 이미지를 가져올 수 있습니다. 이미지를 저장 하는 것에 대 한 이전 예제에서 사용 된 동일한 기법을 사용 하 여 이미지의 경로를 만들고 사용 하 여 이미지를 만들 때 해당 경로 전달 `WebImage`:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    이미지 발견 되 면 하는 경우 새 경로 파일 이름을 이전 예제에서와 같이 구성 합니다. 이미지 대칭 이동, 호출 된 `FlipVertical` 메서드를 다음 이미지를 다시 저장 합니다.

    이미지는 다시 사용 하 여 페이지에 표시 됩니다는 `<img>` 인 요소는 `src` 특성이로 설정 `imagePath`합니다.
3. 브라우저에서 페이지를 실행 합니다. 이미지를 *Photo2.jpg* 거꾸로 표시 됩니다.
4. 페이지를 새로 고칩니다 받거나 페이지 이미지 대칭 이동 된 오른쪽 프로그램이 다시 활성화 되는 참조를 다시 요청 하십시오.

이미지를 회전 하려면 호출 하는 대신 점을 제외 하 고 동일한 코드를 사용 하는 `FlipVertical` 또는 `FlipHorizontal`를 호출 하면 `RotateLeft` 또는 `RotateRight`합니다.

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>워터 마크 이미지에 추가

웹 사이트에 이미지를 추가할 때에 페이지에 표시 하거나 저장 하기 전에 워터 마크 이미지를 추가 하는 것이 좋습니다. 사용자는 종종를 이미지에 저작권 정보를 추가 하거나 비즈니스 이름 광고할 워터 마크를 사용 합니다.

![[image] ] (9-working-with-images/_static/image5.jpg "ch9images 5.jpg")

1. 명명 된 새 페이지 추가 *Watermark.cshtml*합니다.
2. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    이 코드의 코드와는 *FlipImage.cshtml* 앞에서 페이지 (사용 하 여 시간이 있지만 *Photo3.jpg* 파일). 호출 워터 마크를 추가 하려면는 `WebImage` 도우미의 `AddTextWatermark` 메서드 전에 이미지를 저장 합니다. 에 대 한 호출에서 `AddTextWatermark`, 텍스트를 전달 &quot;내 워터 마크&quot;, 노랑, 글꼴 색을 설정 및 Arial 글꼴 패밀리를 설정 합니다. (여기 표시 되지 않지만 `WebImage` 도우미도 불투명도, 글꼴 패밀리 및 글꼴 크기 및 워터 마크 텍스트의 위치를 지정할 수 있습니다.) 이미지를 저장 하는 경우 읽기 전용 이어서는 안 됩니다.

    사용 하 여 이미지가 페이지에 표시 하기 전에 지금까지 살펴본 대로 `<img>` src 특성을 가진 요소 설정 `@imagePath`합니다.
3. 브라우저에서 페이지를 실행 합니다. 이미지의 오른쪽 아래 모서리에서 "My 워터 마크" 텍스트를 확인 합니다.

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>이미지를 사용 하 여 워터 마크로

워터 마크에 대 한 텍스트를 사용 하는 대신 다른 이미지를 사용할 수 있습니다. 경우에 따라 사용자를 워터의 회사 로고와 같은 이미지를 사용 하거나 저작권 정보에 대 한 텍스트 대신 워터 마크 이미지를 사용 합니다.

![[image] ] (9-working-with-images/_static/image6.jpg "ch9images 6.jpg")

1. 명명 된 새 페이지 추가 *ImageWatermark.cshtml*합니다.
2. 이미지를 추가할는 *이미지* 로고로 사용할 수 있으며 이미지의 이름을 바꿀 폴더 *MyCompanyLogo.jpg*합니다. 이 이미지에 표시 될 수 있는 명확 하 게 80 픽셀 너비 및 높이 20 픽셀으로 설정 되 면 이미지 여야 합니다.
3. 다음 페이지에서 기존 내용을 바꿉니다. 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    이 이전 예제에서 코드에 다른 종류입니다. 호출 하는 경우에 `AddImageWatermark` 워터 마크 이미지 대상 이미지를 추가 하려면 (*Photo3.jpg*) 이미지를 저장 하기 전에. 호출 하는 경우 `AddImageWatermark`, 80 및 20 픽셀 높이에 너비를 설정 합니다. *MyCompanyLogo.jpg* 이미지 가로로 가운데에 정렬 이며 대상 이미지의 아래쪽에 세로 방향으로 정렬 합니다. 불투명도 100%로 설정 된 및 안쪽 여백 10 픽셀로 설정 됩니다. 워터 마크 이미지 대상 이미지 보다 큰 경우 아무것도 나타나지 않습니다. 워터 마크 이미지가 대상 이미지 보다 크면 0 이미지 워터 마크의 안쪽 여백을 설정 하는 경우 워터 마크는 무시 됩니다.

    사용 하 여 이미지를 표시 하기 전에,는 `<img>` 요소 및 동적 `src` 특성입니다.
4. 브라우저에서 페이지를 실행 합니다. 워터 마크 이미지의 기본 이미지 아래에 나타나는지 확인 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지 사이트에 대 한 파일 작업](https://go.microsoft.com/fwlink/?LinkId=202896)

[ASP.NET 웹 페이지 Razor 구문을 사용 하 여 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)
