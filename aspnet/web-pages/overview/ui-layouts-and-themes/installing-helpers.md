---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: (Razor) 사이트 페이지는 ASP.NET 웹 도우미 설치 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다. 도우미는 코드 및 당 태그를 포함 하는 재사용 가능한 구성 하는 중...
ms.author: aspnetcontent
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: db3dff9f2d70577bb0618335c0100b9899e87727
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838616"
---
<a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 설치
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다. A *도우미* 코드와 길거나 복잡 한 않을 수 있는 작업을 수행 하는 태그를 포함 하는 재사용 가능한 구성 요소입니다.
> 
> 학습할 내용:
> 
> - WebMatrix 3를 사용 하 여 만든 웹 사이트에서 도우미를 설치 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - WebMatrix 3


## <a name="overview-of-helpers"></a>도우미의 개요

일부 작업을 사용자 웹 페이지에서 작업을 수행 하려는 경우가 많습니다 많은 코드가 필요 하거나 추가 정보가 필요 합니다. 예를 들어 데이터에 대 한 차트를 표시 합니다. 페이지에 Twitter "팔 로우" 단추를 넣는 웹 사이트에서 보내는 전자 메일 자르기 또는 이미지 크기 조정 PayPal을 사용 하 여 사이트에 대 한 합니다. 이러한 유형의 작업을 위해 쉽게 ASP.NET 웹 페이지를 사용 하면 *도우미*합니다. 도우미, 줄 또는 Razor 코드의 두 개를 사용 하 여 일반적인 작업을 수행 하는 구성 요소 설치 하는 데 사용할 수 있는 사이트에 있습니다.

ASP.NET 웹 페이지에 기본 제공 하는 몇 가지 도우미 그러나 많은 도우미 NuGet 패키지 관리자를 사용 하 여 제공 되는 패키지 (추가 기능)에서 사용할 수 있습니다. NuGet 패키지 설치를 선택 하면 및 설치의 모든 세부 정보 처리 합니다.

## <a name="installing-a-helper-in-webmatrix-3"></a>WebMatrix 3에서에서 도우미 설치

1. WebMatrix 3에서을 클릭 합니다 **NuGet** 단추입니다.

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image1.png)
2. 이 NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. 검색 상자에서 설치 하려는 도우미에 대 한 키워드를 입력 합니다.

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image2.png)
3. 패키지를 선택 하 고 클릭 **설치**합니다. 클릭 **예** 패키지를 설치 하 고 약관을 수락 함을 나타내려면 하려는 경우 메시지가 표시 되 면 합니다.

     처음으로 도우미를 설치한 경우 NuGet 도우미를 구성 하는 코드에 대 한 웹 사이트의 폴더를 만듭니다.
4. 도우미를 제거 하려면 클릭 합니다 **갤러리** 단추를 클릭 하는 **설치 된** 탭을 제거 하려는 패키지를 선택 합니다.

## <a name="installing-the-twitter-helper"></a>Twitter 도우미를 설치합니다.

Twitter API의 최신 NuGet을 통해 설치 된 Twitter 도우미를 사용 하 여 호환 되지 않습니다. 대신 참조를 [WebMatrix 사용 하 여 Twitter 도우미](twitter-helper.md) Twitter 도우미 프로젝트를 설정 하는 방법에 대 한 정보에 대 한 항목입니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[소개 ASP.NET 웹 페이지 2-프로그래밍 기본 사항](../getting-started/introducing-razor-syntax-c.md)

[WebMatrix 사용 하 여 twitter 도우미](twitter-helper.md)
