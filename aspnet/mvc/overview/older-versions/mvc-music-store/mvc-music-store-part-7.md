---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7 단계: 멤버 자격 및 권한 부여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2010
ms.topic: article
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a0f599da4691c5bb7c8e6f01625fc0e94ce0eac8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879506"
---
<a name="part-7-membership-and-authorization"></a>7 단계: 멤버 자격 및 권한 부여
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여에 설명 합니다.


이 저장소 관리자 컨트롤러는 사이트를 방문 하는 모든를 현재 액세스할 수 없습니다. 사이트 관리자에 게 사용 권한을 제한 하려면이 옵션을 변경해 보겠습니다.

## <a name="adding-the-accountcontroller-and-views"></a>AccountController 및 뷰 추가

전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿 및 ASP.NET MVC 3 빈 웹 응용 프로그램 템플릿은 간의 한 가지 차이점은 빈 템플릿 계정 컨트롤러를 포함 하지 않습니다. 계정 컨트롤러 전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿에서 만들어진 새 ASP.NET MVC 응용 프로그램에서 일부 파일을 복사 하 여 추가 합니다.

전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들고 다음 파일을 프로젝트에 동일한 디렉터리에 복사 합니다.

1. AccountController.cs 컨트롤러 디렉터리에 복사
2. AccountModels 모델 디렉터리에 복사
3. Views 디렉터리 내에 계정 디렉터리를 만들고의 네 가지 보기를 모두 복사

MvcMusicStore로 시작 하도록 컨트롤러와 모델 클래스에 대 한 네임 스페이스를 변경 합니다. AccountController 클래스 MvcMusicStore.Controllers 네임 스페이스를 사용 해야 하 고 AccountModels 클래스 MvcMusicStore.Models 네임 스페이스를 사용 해야 합니다.

*참고: 이러한 파일 우리 복사해 올 사이트 디자인 파일 자습서의 시작 부분에서 MvcMusicStore Assets.zip 다운로드에 사용할 수도 있습니다. 멤버 자격 파일은 코드 디렉터리에 있습니다.*

업데이트 된 솔루션은 다음과 같이 표시 됩니다.

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>ASP.NET 구성 사이트와 관리 사용자를 추가합니다.

웹 사이트에서 권한 부여를 요구에서는 먼저 사용자를 만들려면 액세스할 수 있는 해야 합니다. 사용자를 만드는 가장 쉬운 방법은 기본 제공 ASP.NET 구성 웹 사이트를 사용 하는 것입니다.

다음 솔루션 탐색기에서 아이콘을 클릭 하 여 ASP.NET 구성 웹 사이트를 시작 합니다.

![](mvc-music-store-part-7/_static/image2.png)

그러면 웹 사이트 구성 됩니다. 보안 탭의 홈 화면을 클릭 한 다음 화면 가운데의 "역할을 사용 하도록" 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image3.png)

"역할 만들기 또는 관리" 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image4.png)

역할 이름으로 "Administrator"를 입력 하 고 역할 추가 단추를 누릅니다.

![](mvc-music-store-part-7/_static/image5.png)

뒤로 단추를 클릭 한 다음 왼쪽에서 사용자 만들기 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image6.png)

다음 정보를 사용 하 여 왼쪽에 사용자 정보 필드를 입력 합니다.

| **필드** | **값** |
| --- | --- |
| **사용자 이름** | 관리자 |
| **암호** | password123! |
| **암호 확인** | password123! |
| **전자 메일** | (모든 전자 메일 주소는 동작) |
| **보안 질문** | (원하는) |
| **보안 대답** | (원하는) |

*참고: 원하는 모든 암호를 물론 사용할 수 있습니다. 기본 암호 보안 설정에는 7 자 이며 하나의 영숫자가 아닌 문자를 포함 하는 암호가 필요 합니다.*

이 사용자에 대 한 관리자 역할을 선택 하 고 사용자 만들기 단추를 클릭 합니다.

![](mvc-music-store-part-7/_static/image7.png)

이 시점에서 사용자를 성공적으로 만들어졌는지 없다는 메시지가 나타납니다.

![](mvc-music-store-part-7/_static/image8.png)

이제 브라우저 창을 닫을 수 있습니다.

## <a name="role-based-authorization"></a>역할 기반 권한 부여

이제 사용자 클래스에 있는 컨트롤러 작업에 액세스 하려면 관리자 역할에 되어야 함을 지정 하는 [Authorize] 특성을 사용 하 여 StoreManagerController에 액세스를 제한할 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*참고: 특정 작업 메서드에 적용 뿐만 아니라 컨트롤러 클래스 수준에서 [Authorize] 특성에 배치할 수 있습니다.*

로그온에 대화 상자를 불러오는 이제 /StoreManager로 이동 합니다.

![](mvc-music-store-part-7/_static/image9.png)

이 새 관리자 계정으로 로그온 한 후 we 're 전으로 앨범 편집 화면으로 이동할 수 있습니다.

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-6.md)
> [다음](mvc-music-store-part-8.md)
