---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작을 사용자 지정 | Microsoft Docs
author: tfitzmac
description: 이 장의 페이지 뿐 아니라 전체 웹 사이트 또는 전체 폴더를 설정 하는 방법에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: 4457318bcf1d2886eb8ed68fdd795eea7905368b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작을 사용자 지정
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 페이지에 대 한 사이트 측 설정을 만드는 방법에 설명 합니다.
> 
> 학습 내용:
> 
> - 코드를 실행할 수 있도록 하는 방법 집합 (전역 값 또는 설정 도우미)는 사이트의 모든 페이지에 대 한 값.
> - 폴더의 모든 페이지에 대 한 값을 설정할 수 있는 코드를 실행 하는 방법입니다.
> - 이전 및 이후 페이지 코드를 실행 하는 방법에 로드 합니다.
> - 중앙 오류 페이지를 오류를 보내는 방법입니다.
> - 폴더의 모든 페이지에 인증을 추가 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3
> - ASP.NET Web Helpers Library (NuGet 패키지)
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 3으로도 작동 하 고 Visual Studio 2013 (또는 Visual Studio Express 2013 for Web) 온다는 점만 다릅니다 ASP.NET Web Helpers Library를 사용할 수 없습니다.


<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>ASP.NET 웹 페이지에 대 한 웹 사이트 시작 코드 추가

ASP.NET 웹 페이지에서 작성 하는 코드의 대부분에 대 한 개별 페이지는 해당 페이지에 대해 필요한 모든 코드를 포함할 수 있습니다. 예를 들어 페이지에 전자 메일 메시지를 보내면 경우 단일 페이지에 해당 작업에 대 한 모든 코드를 저장할 수는 있습니다. 이 전자 메일에 대 한 설정을 초기화 하는 코드를 포함할 수 있습니다 (즉, SMTP 서버에 대 한) 및 전자 메일 메시지를 보내기 위한 합니다.

그러나 경우에 따라 사이트에서 모든 페이지를 실행 하기 전에 일부 코드를 실행 수 있습니다. 이 사이트의 어디서 나 사용할 수 있는 값을 설정 하는 데 유용 (라고 *전역 값*.) 예를 들어 일부 도우미에 전자 메일 설정 또는 계정 키와 같은 값을 제공 해야 합니다. 전역 값에서 이러한 설정을 사용 하려면 유용할 수 있습니다.

명명 된 페이지를 만들어 이렇게 하려면  *\_AppStart.cshtml* 사이트의 루트에 있습니다. 이 페이지에 있는 경우 요청 된 모든 페이지는 사이트에 처음으로 실행 됩니다. 따라서 것이 전역 값을 설정 하는 코드를 실행 하는 것이 좋습니다. (때문에  *\_AppStart.cshtml* 밑줄 전위는 사용자가 직접 요청 하는 경우에 ASP.NET 브라우저에 페이지 보내지 않습니다.)

다음 다이어그램에서는 방법을  *\_AppStart.cshtml* 페이지 작동 합니다. 요청 된 페이지 들어오고 경우 이것이 첫 번째 요청에 대 한 페이지 ASP.NET 사이트의 첫 번째 확인 여부는  *\_AppStart.cshtml* 페이지가 있습니다. 이 경우 코드에서  *\_AppStart.cshtml* 페이지가 실행, 한 다음 요청된 된 페이지 실행 합니다.

![[image]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>웹 사이트에 대 한 전역 값을 설정합니다.

1. WebMatrix 웹 사이트의 루트 폴더에 라는 파일을 만듭니다  *\_AppStart.cshtml*합니다. 파일은 사이트의 루트에 있어야 합니다.
2. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    에 값을 저장 하는이 코드는 `AppState` 사이트의 모든 페이지에 자동으로 사용할 수 있는 사전입니다. 에  *\_AppStart.cshtml* 파일에 모든 태그가 들어 있지 않습니다. 페이지가 됩니다 코드를 실행 하 고 원래 요청 된 페이지로 리디렉션합니다.

    > [!NOTE]
    > 에 코드를 배치할 때 주의 해야는  *\_AppStart.cshtml* 파일입니다. 코드에서 오류가 발생 한 경우는  *\_AppStart.cshtml* 파일을 웹 사이트 시작 되지 않습니다.
3. 루트 폴더에 명명 된 새 페이지를 만듭니다 *AppName.cshtml*합니다.
4. 기본 태그 및 코드를 다음으로 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    이 코드의 값을 추출는 `AppState` 개체에서 설정 하는  *\_AppStart.cshtml* 페이지.
5. 실행 된 *AppName.cshtml* 브라우저에서 페이지입니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 페이지는 전역 값을 표시합니다. 

    ![[image]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>도우미에 대 한 값을 설정합니다.

에 대 한 적절 하 게 사용은  *\_AppStart.cshtml* 파일은 사이트에서 사용 하 고 초기화 해야 하는 도우미에 대 한 값을 설정 하는 것입니다. 일반적인 예로 전자 메일 설정에 대 한는 `WebMail` 도우미와에 대 한 개인 및 공개 키의 `ReCaptcha` 도우미입니다. 이와 같은 경우에 한 번으로 값을 설정할 수는  *\_AppStart.cshtml* 로 있습니다 하는 이미 설정한 모든 페이지에 대 한 사이트에 있습니다.

이 절차에서는 설정 하는 방법을 보여 줍니다 `WebMail` 설정을 전역적으로 합니다. (사용 하는 방법에 대 한 자세한 내용은 `WebMail` 도우미, 참조 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](../getting-started/11-adding-email-to-your-web-site.md).)

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.
2. 아직 없는 경우는  *\_AppStart.cshtml* 파일, 웹 사이트의 루트 폴더에 라는 파일을 만들어  *\_AppStart.cshtml*합니다.
3. 다음 추가 `WebMail` 설정을  *\_AppStart.cshtml* 파일: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    수정 다음 전자 메일의 코드에서 관련된 설정:

   - 설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버의 이름입니다.
   - 설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.
   - 설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.
   - 설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다. 메시지에서 보내는 전자 메일 주소입니다. (다른 지정할 수는 일부 전자 메일 공급자 주저 하지 마시기 바랍니다 `From` 주소 및 사용자 이름으로 사용 합니다는 `From` 주소입니다.)

     SMTP 설정에 대 한 자세한 내용은 참조 [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) 문서의 [ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기](https://go.microsoft.com/fwlink/?LinkID=202899) 및 [보내는전자메일문제](https://go.microsoft.com/fwlink/?LinkId=253001#email)에 [ASP.NET 웹 페이지 (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)합니다.
4. 저장 된  *\_AppStart.cshtml* 파일을 닫습니다.
5. 웹 사이트의 루트 폴더에 명명 된 새 페이지를 만들 *TestEmail.cshtml*합니다.
6. 기존 콘텐츠를 다음으로 바꿉니다. 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. 실행 된 *TestEmail.cshtml* 브라우저에서 페이지입니다.
8. 전자 메일 메시지를 보내봅니다 누른 다음 필드에 **보낼**합니다.
9. 메시지 참조 되도록 전자 메일을 확인 합니다.

이 예제에서 중요 한 부분은 일반적으로 변경 하지 않는 설정을-SMTP 서버와 전자 메일 자격 증명의 이름이 마음에-에 설정 된는  *\_AppStart.cshtml* 파일입니다. 이런 방식으로 다시 설정 각 페이지에서 전자 메일을 전송 하는 위치 필요가 없습니다. (몇 가지 이유로 이러한 설정을 변경 해야 하는 경우 설정할 수 있지만 개별적으로 페이지에 있습니다.) 페이지에서 일반적으로 받는 사람 및 전자 메일 메시지의 본문 같이 각 시간을 변경 하는 값만 설정 합니다.

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>폴더의 파일 전후 코드를 실행합니다.

사용할 수 있습니다 하는 것 처럼  *\_AppStart.cshtml* 코드를 작성 하는 사이트의에서 페이지를 실행 하기 전에, 이전 (및 이후)를 실행 하는 코드를 작성할 수 있습니다 실행 하는 특정 폴더의 모든 페이지입니다. 동일한 레이아웃 페이지 설정 폴더의 모든 페이지에 대 한 또는 검사에 대 한 폴더에는 페이지를 실행 하기 전에 사용자가 로그인 하는 등의 작업에 유용 합니다.

페이지에 대 한 특히 폴더를 만들 수 있습니다 코드 라는 파일에  *\_PageStart.cshtml*합니다. 다음 다이어그램에서는 방법을  *\_PageStart.cshtml* 페이지 작동 합니다. 에 대 한 ASP.NET 페이지에 대 한 요청이 들어올 경우 먼저 확인 한  *\_AppStart.cshtml* 페이지 및를 실행 합니다. ASP.NET 있는지 여부를 확인 한 다음는  *\_PageStart.cshtml* 페이지 및 그렇다면를 실행 합니다. 요청된 된 페이지를 실행합니다.

내에서  *\_PageStart.cshtml* 페이지에서 요청 된 페이지를 포함 하 여 실행를 처리 하는 동안 위치를 지정할 수는 `RunPage` 메서드. 이렇게 하면 요청 된 페이지를 실행 하기 전에 코드를 실행 한 후 다시 다음 합니다. 포함 하지 않으면 `RunPage`, 모든 코드에  *\_PageStart.cshtml* 실행 되 고 요청된 된 페이지 자동으로 실행 합니다.

![[image]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET를 사용 하면 계층 구조를 만들  *\_PageStart.cshtml* 파일입니다. 넣을 수는  *\_PageStart.cshtml* 사이트의 루트에 있는 파일과 하위 폴더에 있습니다. 페이지 요청 될 때는  *\_PageStart.cshtml* 파일 이어서 최상위 수준 (가장 가까운 사이트 루트) 실행에는  *\_PageStart.cshtml* 다음에서 파일 하위 폴더를 요청에 요청된 된 페이지를 포함 하는 폴더에 도달할 때까지 하위 폴더 구조가 아래의 합니다. 모든 적용 가능한 후  *\_PageStart.cshtml* 파일 실행, 요청 된 페이지를 실행 합니다.

예를 들어 다음과 같은 조합을 해야할  *\_PageStart.cshtml* 파일 및 *Default.cshtml* 파일:

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

실행 하는 경우 */myfolder/default.cshtml*, 다음에 표시 됩니다.

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>폴더의 모든 페이지에 대 한 초기화 코드를 실행합니다.

에 대 한 적절 하 게 사용  *\_PageStart.cshtml* 파일 단일 폴더에 모든 파일에 대해 동일한 레이아웃 페이지를 초기화 하는 것입니다.

1. 루트 폴더에서 라는 새 폴더를 만듭니다 *InitPages*합니다.
2. 에 *InitPages* 라는 파일을 만들어 웹 사이트의 폴더  *\_PageStart.cshtml* 기본 태그 및 코드는 다음과 같이 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. 웹 사이트의 루트에서 라는 폴더를 만듭니다 *Shared*합니다.
4. 에 *Shared* 폴더를 라는 파일을 만들어  *\_Layout1.cshtml* 기본 태그 및 코드는 다음과 같이 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. *InitPages* 폴더를 라는 파일을 만들어 *Content1.cshtml* 기존 콘텐츠는 다음과 같이 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. 에 *InitPages* 폴더를 명명 된 다른 파일을 만들 *Content2.cshtml* 기본 태그는 다음과 같이 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. 실행 *Content1.cshtml* 브라우저에서 합니다. 

    ![[image]](18-customizing-site-wide-behavior/_static/image4.jpg)

    경우는 *Content1.cshtml* 실행 페이지는  *\_PageStart.cshtml* 파일 집합 `Layout` 설정 `PageData["MyBackground"]` 색입니다. *Content1.cshtml*, 레이아웃 및 색이 적용 됩니다.
8. 디스플레이 *Content2.cshtml* 브라우저에서 합니다. 

    초기화 페이지를 둘 다 동일한 페이지 레이아웃 및 색 사용 하기 때문에 레이아웃은 동일  *\_PageStart.cshtml*합니다.

## <a name="using-pagestartcshtml-to-handle-errors"></a>사용 하 여 \_PageStart.cshtml 오류 처리

에 사용 된 다른는  *\_PageStart.cshtml* 파일 하나에서 발생할 수 있는 프로그래밍 오류 (예외)를 처리 하는 방법을 만드는 것 *.cshtml* 폴더에는 페이지입니다. 이 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.

1. 루트 폴더에 라는 폴더를 만듭니다 *InitCatch*합니다.
2. 에 *InitCatch* 라는 파일을 만들어 웹 사이트의 폴더  *\_PageStart.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    요청된 된 페이지를 명시적으로 호출 하 여 실행 하면이 코드는 `RunPage` 내에서 메서드는 `try` 블록입니다. 요청 된에서 프로그래밍 오류가 발생 한 경우 페이지 내의 코드는 `catch` 블록이 실행 됩니다. 코드는 페이지로 리디렉션합니다.이 경우 (*Error.cshtml*) 오류는 URL의 일부로 발생 하는 파일의 이름을 전달 합니다. (만듭니다 페이지 곧.)
3. 에 *InitCatch* 라는 파일을 만들어 웹 사이트의 폴더 *Exception.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    이 예제에 대 한 일이 페이지에 의도적으로 만들어지고 오류가 존재 하지 않는 데이터베이스 파일을 열려고 시도 하 여 있습니다.
4. 루트 폴더에 라는 파일을 만듭니다 *Error.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다. 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    이 페이지에서는 식에서에서 `@Request["source"]` url 값을 가져오고 표시 합니다.
5. 도구 모음에서 클릭 **저장**합니다.
6. 실행 *Exception.cshtml* 브라우저에서 합니다. 

    ![[image]](18-customizing-site-wide-behavior/_static/image5.jpg)

    오류가 발생 하기 때문에 *Exception.cshtml*,  *\_PageStart.cshtml* 페이지 리디렉션하는 *Error.cshtml* 메시지를 표시 하는 파일입니다.

    예외에 대 한 자세한 내용은 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkID=251587)합니다.

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-pagestartcshtml-to-restrict-folder-access"></a>사용 하 여 \_PageStart.cshtml 폴더 액세스를 제한 하려면

사용할 수도 있습니다는  *\_PageStart.cshtml* 파일을 폴더에 있는 모든 파일에 대 한 액세스를 제한 합니다.

1. WebMatrix를 사용 하 여 새 웹 사이트를 만들어는 **템플릿에서 사이트** 옵션입니다.
2. 사용 가능한 템플릿에서 선택 **시작 사이트**합니다.
3. 루트 폴더에 라는 폴더를 만듭니다 *AuthenticatedContent*합니다.
4. 에 *AuthenticatedContent* 폴더를 라는 파일을 만들어  *\_PageStart.cshtml* 는 기존 태그와 코드는 다음과 같이 바꿉니다. 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    코드는 폴더의 모든 파일에 캐시 되는 것을 방지 하 여 시작 합니다. (이 같은 공용 컴퓨터, 한 사용자의 캐시 된 페이지는 다음 사용자에 사용할 수 있도록 않도록 하려는 시나리오에 필요 합니다.) 다음으로 코드 여부는 사용자가 로그인 사이트에 폴더의 모든 페이지를 볼 수 있도록 하려면 결정 합니다. 사용자가 로그인 되지 않은 경우 코드 로그인 페이지로 리디렉션합니다. 로그인 페이지 라는 쿼리 문자열 값을 포함 하는 경우 원래 요청 된 페이지에 사용자를 반환할 수 `ReturnUrl`합니다.
5. 새 페이지를 만들고는 *AuthenticatedContent* 라는 폴더 *Page.cshtml*합니다.
6. 기본 태그를 다음 코드로 바꿉니다.  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. 실행 *Page.cshtml* 브라우저에서 합니다. 코드는 로그인 페이지로 리디렉션됩니다. 로그인 하기 전에 등록 해야 합니다. 등록 로그인 한 후 페이지를 탐색 하 고 해당 내용을 볼 수 있습니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료

[ASP.NET 웹 페이지 Razor 구문을 사용 하 여 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)
