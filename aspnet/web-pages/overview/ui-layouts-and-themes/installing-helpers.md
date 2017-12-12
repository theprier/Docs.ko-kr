---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: "(Razor) 사이트 페이지에 ASP.NET 웹 도우미를 설치 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 한 도우미를 설치 하는 방법을 설명 합니다. 도우미는 코드와 당 태그를 포함 하는 재사용 가능한 구성 요소 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2014
ms.topic: article
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 842c5a56d14314217c1e6ad6d48ded28d3cc5b4e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 도우미를 설치합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 한 도우미를 설치 하는 방법을 설명 합니다. A *도우미* 코드와 길거나 복잡 한 될 수 있는 작업을 수행 하는 태그를 포함 하는 재사용 가능한 구성 요소입니다.
> 
> 학습 내용:
> 
> - WebMatrix 3을 사용 하 여 만든 웹 사이트의 도우미를 설치 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - WebMatrix 3


## <a name="overview-of-helpers"></a>도우미의 개요

사용자 웹 페이지에서 작업을 수행 하고자 하는 몇 가지 작업 코드 많이 필요 하거나 추가 정보가 필요 합니다. 예로 데이터에 대 한 차트를 표시 합니다. Twitter "Follow" 단추 페이지;의 게시 웹 사이트에서 메일을 보내는 중 자르기 또는; 이미지 크기 조정 PayPal을 사용 하 여 사이트에 대 한 합니다. 이러한 종류의 작업을 수행 하기 쉽도록 ASP.NET 웹 페이지 사용 하면 사용 하 여 *도우미*합니다. 도우미는 구성 요소 설치 하는 데 사용할 수 있는 및 사이트에 대 한 하면 줄만 또는 Razor 코드의 두 개 사용 하 여 일반적인 작업을 수행 합니다.

ASP.NET 웹 페이지에서 기본적으로 제공 하는 몇 가지 도우미에 있습니다. 그러나 많은 도우미는 NuGet 패키지 관리자를 사용 하 여 제공 되는 (추가 기능) 패키지에서 사용할 수 있습니다. 설치의 모든 세부 정보는 담당 다음 및 NuGet 패키지를 설치 하도록 선택할 수 있습니다.

## <a name="installing-a-helper-in-webmatrix-3"></a>도우미는 WebMatrix 3에서 설치

1. WebMatrix 3에서 클릭 하 고 **NuGet** 단추입니다.

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image1.png)
2. 이 NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. 검색 상자에를 설치 하려면 도우미에 대 한 키워드를 입력 합니다.

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image2.png)
- 패키지를 선택한 다음 클릭 **설치**합니다. 클릭 **예** 패키지를 설치 하 고 약관을 수락 함을 나타내려면 것인지 묻는 메시지가 나타나면 합니다.

    처음으로 도우미를 설치한 경우 NuGet 도우미를 구성 하는 코드에 대 한 웹 사이트의 폴더를 만듭니다.
- 도우미 메서드를 제거 하려면 클릭는 **갤러리** 단추를 클릭 하 여는 **설치 됨** 탭을 제거 하려는 패키지를 선택 합니다.

## <a name="installing-the-twitter-helper"></a>Twitter 도우미를 설치합니다.

최신 버전의 Twitter API NuGet을 통해 설치 된 Twitter 도우미와 호환 되지 않습니다. 대신, 참조는 [Twitter 도우미를 WebMatrix로](twitter-helper.md) Twitter 도우미 프로젝트를 설정 하는 방법에 대 한 정보에 대 한 항목입니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[소개 ASP.NET 웹 페이지 2-프로그래밍 기본 사항](../getting-started/introducing-razor-syntax-c.md)

[WebMatrix로 twitter 도우미](twitter-helper.md)
