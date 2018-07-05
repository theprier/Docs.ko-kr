---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7 부: 멤버 자격 및 권한 부여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여를 설명합니다.
ms.author: aspnetcontent
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: 1f2ad9de3a21366931efe6ca2466f4efc23a6192
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802541"
---
<a name="part-7-membership-and-authorization"></a>7 부: 멤버 자격 및 권한 부여
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여를 설명합니다.


저장소 관리자 컨트롤러 사이트를 방문 하는 모든 현재 액세스할 수 있습니다. 사이트 관리자에 게 사용 권한을 제한 하려면이 옵션을 변경해 보겠습니다.

## <a name="adding-the-accountcontroller-and-views"></a>AccountController 및 뷰를 추가합니다.

전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿 및 ASP.NET MVC 3 빈 웹 응용 프로그램 템플릿 간의 차이점 중 하나는 빈 템플릿에 계정 컨트롤러를 포함 하지 않습니다. 전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿에서 만든 새 ASP.NET MVC 응용 프로그램에서 일부 파일을 복사 하 여 계정 컨트롤러를 추가 하겠습니다.

전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들고 프로젝트에서 동일한 디렉터리에 다음 파일을 복사 합니다.

1. AccountController.cs 컨트롤러 디렉터리에 복사
2. AccountModels 모델 디렉터리에 복사
3. Views 디렉터리 내에서 계정 디렉터리를 만들고의 네 가지 보기를 모두 복사

MvcMusicStore를 사용 하 여 시작 하도록 컨트롤러 및 모델 클래스에 대 한 네임 스페이스를 변경 합니다. AccountController 클래스 MvcMusicStore.Controllers 네임 스페이스를 사용 해야 하 고 AccountModels 클래스 MvcMusicStore.Models 네임 스페이스를 사용 해야 합니다.

*참고: 이러한 파일은 자습서의 시작 부분에 사이트 디자인 파일이 복사한 MvcMusicStore Assets.zip 다운로드에 사용할 수 있습니다. 멤버 자격 파일의 코드 디렉터리에 있습니다.*

업데이트 된 솔루션은 다음과 같아야 합니다.

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>ASP.NET 구성 사이트를 사용 하 여 관리 사용자를 추가합니다.

웹 사이트에서 권한 부여 필요, 전에 액세스가 있는 사용자를 만들려면 해야 합니다. 사용자를 만드는 가장 쉬운 방법은 기본 제공 ASP.NET 구성 웹 사이트를 사용 하는 것입니다.

다음 솔루션 탐색기에서 아이콘을 클릭 하 여 ASP.NET 구성 웹 사이트를 시작 합니다.

![](mvc-music-store-part-7/_static/image2.png)

그러면 웹 사이트를 구성 합니다. 홈 화면에서 보안 탭을 클릭 한 다음 화면 중앙에 "역할을 사용 하도록 설정" 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image3.png)

"역할 만들기 또는 관리" 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image4.png)

역할 이름으로 "관리자"를 입력 하 고 역할 추가 단추를 누릅니다.

![](mvc-music-store-part-7/_static/image5.png)

뒤로 단추를 클릭 한 다음 왼쪽에서 만들기 사용자 링크를 클릭 합니다.

![](mvc-music-store-part-7/_static/image6.png)

다음 정보를 사용 하 여 왼쪽에서 사용자 정보 필드에 입력 합니다.

| **필드** | **값** |
| --- | --- |
| **사용자 이름** | 관리자 |
| **암호** | password123! |
| **암호 확인** | password123! |
| **전자 메일** | (모든 전자 메일 주소는 동작) |
| **보안 질문** | (원하는) |
| **보안 대답** | (원하는) |

*참고: 원하는 모든 암호를 이외에 사용할 수 있습니다. 기본 암호 보안 설정에는 7 자 이상의 영숫자 이외의 문자를 포함 하는 암호가 필요 합니다.*

이 사용자에 대 한 관리자 역할을 선택 하 고 사용자 만들기 단추를 클릭 합니다.

![](mvc-music-store-part-7/_static/image7.png)

이 시점에서 사용자를 성공적으로 만들어졌는지 나타내는 메시지가 표시 됩니다.

![](mvc-music-store-part-7/_static/image8.png)

이제 브라우저 창을 닫을 수 있습니다.

## <a name="role-based-authorization"></a>역할 기반 권한 부여

이제 [Authorize] 특성을 사용 하 여 StoreManagerController 클래스의 모든 컨트롤러 작업에 액세스 하려면 관리자 역할에 사용자 되도록 지정 하려면 액세스를 제한할 수 했습니다.

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*참고: 컨트롤러 클래스 수준에서 뿐만 아니라 특정 작업 메서드에 [Authorize] 특성에 배치할 수 있습니다.*

이제 /StoreManager 이동 로그온 대화 상자가 나타납니다.

![](mvc-music-store-part-7/_static/image9.png)

이 새 관리자 계정으로 로그온 한 후 우리 전 앨범 편집 화면으로 이동할 수 있습니다.

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-6.md)
> [다음](mvc-music-store-part-8.md)
