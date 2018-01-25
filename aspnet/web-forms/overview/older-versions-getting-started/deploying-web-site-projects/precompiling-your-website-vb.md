---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
title: "웹 사이트 (VB) 미리 컴파일 | Microsoft Docs"
author: rick-anderson
description: "Visual Studio에서는 ASP.NET 개발자에 게 두 가지 프로젝트 유형의: 웹 응용 프로그램 프로젝트 (Wap) 및 웹 사이트 프로젝트 (WSPs). 주요 차이점 betwe 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: c285dc6f-a1c6-46e6-ac03-3830947f57e3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
msc.type: authoredcontent
ms.openlocfilehash: 7cc487aa5276c601fed632e82d7b6d32d1b53b58
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="precompiling-your-website-vb"></a>웹 사이트 (VB) 미리 컴파일
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_vb.pdf)

> Visual Studio에서는 ASP.NET 개발자에 게 두 가지 프로젝트 유형의: 웹 응용 프로그램 프로젝트 (Wap) 및 웹 사이트 프로젝트 (WSPs). 두 가지 프로젝트 형식 간의 주요 차이점 중 하나는 Wap WSP의 코드를 웹 서버에서 자동으로 컴파일할 수 있지만 배포 하기 전에 명시적으로 컴파일된 코드를 갖도록입니다. 그러나를 배포 하기 전에 WSP 미리 컴파일하는 것이 같습니다. 이 자습서 미리 컴파일 혜택을 탐색 하 고 웹 사이트에서 Visual Studio 내에서 명령줄에서를 미리 컴파일하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

Visual Studio에서는 ASP.NET 개발자에 게 두 개의 서로 다른 프로젝트 형식: 응용 프로그램 프로젝트 WAP (웹) 및 웹 사이트 프로젝트 (WSP). 이러한 프로젝트 형식 간의 주요 차이점 중 하나는 Wap 필요 함을 *명시적 컴파일을* 반면 WSPs 사용 하 여 *자동 컴파일을*, 기본적으로 합니다. Wap를와 웹 사이트에서 생성 된 단일 어셈블리에 웹 응용 프로그램의 코드를 컴파일할 `Bin` 폴더입니다. 태그 콘텐츠를 복사 하는 배포 작업이 포함 됩니다 (는 `.aspx.ascx`, 및 `.master` 파일)에 있는 어셈블리와 함께 프로젝트에는 `Bin` 폴더; 코드 숨김 클래스 파일 자체를 배포할 필요가 없습니다. 반면에 프로덕션 환경으로 태그 페이지와 해당 하는 코드 숨김 클래스를 복사 하 여 WSPs를 배포 합니다. 코드 숨김 클래스는 웹 서버에서 필요할 때 컴파일됩니다.

> [!NOTE]
> "Explicit 컴파일 대 자동 컴파일을" 섹션을 다시 참조는 [ *결정 어떤 파일 배포 해야 할* 자습서](determining-what-files-need-to-be-deployed-vb.md) 프로젝트 간의 차이점에 자세한 배경을 알고 싶으면 모델, 자동 및 명시적 컴파일 및 컴파일 모델 배포에 미치는 영향


자동 컴파일 옵션은 쉽게 사용할 수 있습니다. 명시적 컴파일을 단계의 및 된 파일만 수정 필요 명시적 컴파일을 변경 된 태그 페이지와 마찬가지로 컴파일된 어셈블리를 배포 해야 하는 반면 배포 해야 합니다. 그러나 자동 배포에는 두 가지 잠재적인 단점이 있습니다.

- 먼저 방문 되는 경우 페이지가 자동으로 컴파일해야, 때문에 있을 수 있습니다 짧지만 현저한 지연이 배포 후 처음으로 요청 되는 ASP.NET 페이지.
- 자동 컴파일을 선언적 태그 코드와 소스 코드를 웹 서버에 없는 된다는 필요 합니다. 이 옵션을 사용 하려는 웹 서버에 설치 하는 고객에 게 웹 응용 프로그램을 판매 중인 경우 이상한 옵션 수 있습니다.

경우 단점 위의 두 거래 분리기가, WAP 모델 전환 하거나 수 중 하나 또는 *미리 컴파일할* 배포 하기 전에 WSP 합니다. 이 자습서를 호스팅되는 웹 사이트에 대 한 가장 적합 한 미리 컴파일 옵션을 검사 하 고 미리 컴파일 프로세스 및 미리 컴파일된 웹 사이트의 배포를 안내 합니다.

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>ASP.NET 코드 생성 및 컴파일의 개요

사용 가능한 미리 컴파일 옵션을 보기 전에 먼저에 대해 살펴보기 코드 생성 및 컴파일을 ASP.NET 페이지 생성 또는 마지막으로 업데이트 된 이후 처음 요청 될 때 발생 하 합니다. ASP.NET 페이지 두 부분으로 구성 되며, 아시다시피:에 선언적 태그는 `.aspx` 파일 및 소스 코드의 부분에는 별도 코드 숨김 클래스 파일에서 일반적으로 (`.aspx.vb`). ASP.NET 페이지를 요청할 때 런타임에 의해 수행 되는 단계는 응용 프로그램의 컴파일 모델에 따라 달라 집니다.

Wap를와 페이지의 소스 코드 컴파일해야 합니다. 명시적으로 배포 하기 전에 단일 어셈블리에 있습니다. 배포 하는 동안이 어셈블리 및 다양 한 태그 페이지는 프로덕션 환경에 복사 됩니다. ASP.NET 페이지에 대 한 웹 서버에 요청이 도착 하는 경우 런타임에서 페이지의 코드 숨김 클래스의 인스턴스를 만들고 고이 호출 하는 해당 `ProcessRequest` 페이지 수명 주기를 시작 하 고 궁극적으로, 반환 되는 페이지의 콘텐츠를 생성 하는 메서드 요청자입니다. 코드 숨김 클래스를 배포 하기 전에 어셈블리에 이미 컴파일된 때문에 런타임에서 ASP.NET 페이지의 코드 숨김 클래스 작업할 수 있습니다.

WSPs 및 자동 컴파일을 배포 하기 전에 명시적 컴파일을 단계가 없습니다. 대신, 배포 과정 프로덕션 환경으로 선언적 및 소스 코드 콘텐츠를 복사 합니다. 요청이 도착 하면 ASP.NET 페이지에 대 한 웹 서버에 처음으로 페이지 생성 또는 마지막으로 업데이트 된 이후, 런타임에 해야 먼저 코드 숨김 클래스를 어셈블리로 컴파일해야 합니다. 컴파일된 어셈블리에이 폴더에 저장 됩니다 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`이 폴더의 위치를 통해 사용자 지정할 수 있지만는 `<pages>` 요소 `Web.config`합니다. 어셈블리가 디스크에 저장 하지 않아도 동일한 페이지에 대 한 후속 요청에 다시 컴파일할 수 있습니다.

> [!NOTE]
> 예상한 사업이 약간의 지연 시간이 걸리는 페이지의 코드를 컴파일하고 결과 어셈블리를 저장 하는 서버에 대 한 현재 자동 컴파일을 사용 하는 사이트에 처음으로 (또는 변경 된 후 처음으로) 페이지를 요청할 때 디스크입니다.


즉, 명시적 컴파일을 사용 해야 배포 하기 전에 웹 사이트의 소스 코드를 컴파일하려고 런타임에 해당 단계를 수행 하지 않아도 저장 합니다. 자동 컴파일을 런타임에 생성 되거나 마지막으로 업데이트 된 이후 페이지를 처음 방문할에 대 한 약간의 초기화 비용은 하지만 페이지의 소스 코드의 컴파일을 처리 합니다.

하지만 ASP.NET 페이지의 선언적 일부 (의 `.aspx` 파일)? 간의 관계 임을 명확는 `.aspx` 파일과 선언적 태그에 정의 된 웹 컨트롤로 자신의 코드 숨김 클래스의 코드는 코드에 액세스할 수 있습니다. 또한 하의 콘텐츠는 `.aspx` 파일 페이지에서 생성 된 렌더링 된 태그 상당한 영향을 줍니다. 런타임에 된 텍스트, HTML, 작업 및 웹 컨트롤 구문에 정의 된 어떻게는 `.aspx` 요청한 페이지를 생성 하는 파일의 콘텐츠를 렌더링 된?

Wap 및 WSPs 달라질 하위 수준의 구현 세부 사항에 너무 sidetracked 가져올 하지 않으려는 경우 하지만 런타임은로 보호 된 멤버와 메서드는 다양 한 웹 컨트롤을 포함 하는 클래스 파일 자동으로 생성 되는 간단히 말해 합니다. 이 생성 된 파일으로 구현 됩니다는 *partial 클래스* 에 해당 하는 코드 숨김 클래스입니다. ([Partial 클래스](http://www.dotnet-guide.com/partialclasses.html) 단일 클래스의 내용에 대 한 여러 파일에 분산 될를 허용 합니다.) 두 위치에서 코드 숨김 클래스가 정의 되어 있는 따라서:에서 `.aspx.vb` 생성 및이 자동으로 생성 된 클래스에서 런타임에 생성 된 파일입니다. 이 자동으로 생성 된 클래스에 저장 됩니다는 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` 폴더입니다.

중요 한 소모할 여기은 런타임에 의해 렌더링 해야 하는 ASP.NET 페이지에 대 한 선언적 해당 어셈블리로 컴파일해야 합니다. 소스 코드 부분 및 합니다. Wap, 소스 코드에 명시적으로 배포 하기 전에 어셈블리에 컴파일됩니다 있지만 선언 태그 해야 계속 코드로 변환 하 고 웹 서버에서 런타임에 의해 컴파일됩니다. WSPs 자동 컴파일을 사용 하 여, 소스 코드와 선언 태그를 모두 웹 서버에서 컴파일할 필요 합니다.

WSP 모델을 사용 하 여 명시적 컴파일을 사용 하는 것이 불가능 합니다. WAP 모델로 같은 소스 코드 부분을 명시적으로 컴파일할 수 있습니다. 게다가 선언적 태그를 컴파일할 수 있습니다.

## <a name="precompilation-options"></a>미리 컴파일 옵션

.NET Framework와 함께 제공 되는 [ASP.NET 컴파일 도구 (`aspnet_compiler.exe`)](https://msdn.microsoft.com/library/ms229863.aspx) WSP 모델을 사용 하 여 만든 ASP.NET 응용 프로그램의 소스 코드 (및 콘텐츠도) 컴파일할 수 있습니다. 이 도구는.NET Framework 버전 2.0과 함께 출시 된 및에 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727` 폴더; 명령줄에서 사용 되거나 빌드 메뉴의 웹 사이트 게시 옵션을 통해 Visual Studio 내에서 시작 될 수 있습니다.

컴파일 도구에서는 두 가지 일반적인 형태의 컴파일: 내부 미리 컴파일 및 배포용입니다. 실행 하면 전체 미리 컴파일에서 `aspnet_compiler.exe` 명령줄에서 도구를 컴퓨터에 가상 디렉터리 또는 상주 하는 웹 사이트의 실제 경로에 대 한 경로 지정 합니다. 컴파일 도구에는 다음 각 ASP.NET 페이지의 컴파일된 버전을 저장할 프로젝트를 컴파일합니다는 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` 폴더 경우 페이지에 각 방문한 처음으로 브라우저에서와 동일 하 게 합니다. 내부 미리 컴파일에이 단계를 수행 하지 않아도 런타임 줄어들어 사이트에 새로 배포 된 ASP.NET 페이지에 대 한 첫 번째 요청 속도가 수 있습니다. 그러나 프로그램을 실행 하는 웹 서버에서 명령줄 수 있어야 하기 때문에 내부에서 미리 컴파일 호스팅된 웹 사이트의 대부분에 유용 하지 않습니다. 공유 호스팅 환경에서 이러한 액세스 수준을 허용 되지 않습니다.

> [!NOTE]
> 내부 미리 컴파일에 대 한 자세한 내용은 체크 아웃 [방법: ASP.NET 웹 사이트를 미리 컴파일하](https://msdn.microsoft.com/library/ms227972.aspx) 및 [ASP.NET 2.0에서 미리 컴파일](http://www.odetocode.com/Articles/417.aspx)합니다.


웹 사이트의 페이지를 컴파일하는 대신는 `Temporary ASP.NET Files` 폴더 배포용 디렉터리를 선택 해 및 프로덕션 환경에 배포할 수 있는 형식에서 페이지를 컴파일합니다.

이 자습서에서는 탐색 배포용의 두 종류가 있습니다:을 업데이트할 수 있는 사용자 인터페이스를 미리 컴파일 및 업데이트할 수 없는 사용자 인터페이스와 미리 컴파일입니다. 미리 컴파일을 업데이트할 수 있는 사용자 인터페이스에서 선언 태그 유지는 `.aspx`, `.ascx`, 및 `.master` 파일, 되므로 개발자를 확인 하 고 필요한 경우 프로덕션 서버에 대 한 선언적 태그를 수정 합니다. 업데이트할 수 없는 사용자 인터페이스를 미리 생성 `.aspx` 페이지의 모든 콘텐츠 및 제거 void를 `.ascx` 및 `.master` 함으로써 선언적 태그를 숨기 거 나 개발자가에서 변경 금지 파일은 프로덕션 환경입니다.

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>업데이트할 수 있는 사용자 인터페이스를 사용 하는 배포를 위한 미리 컴파일

배포용을 이해 하는 가장 좋은 방법은 작업의 예제를 확인 하는 것입니다. 업데이트할 수 있는 사용자 인터페이스를 사용 하 여 배포에 대 한 책 검토 WSP 미리 컴파일할 보겠습니다. ASP.NET 컴파일 도구는 Visual Studio의 빌드 메뉴에서 또는 명령줄에서 호출할 수 있습니다. 이 섹션에서는 Visual Studio; 내에서 도구를 사용 하 여 검사 "미리 컴파일 명령줄에서" 섹션 컴파일러 도구는 명령줄에서 실행 살펴 봅니다.

Visual Studio에서 책 검토 WSP 열고 빌드 메뉴에서 웹 사이트 게시 메뉴 옵션을 선택 합니다. 이 웹 사이트 게시 대화 상자를 엽니다 (참조 **그림 1**) 대상 위치, 미리 컴파일된이 사이트의 사용자 인터페이스는 업데이트할 수 있는, 여부 및 기타 컴파일러 도구 옵션을 지정할 수 있습니다. 대상 위치 원격 웹 서버나 FTP 서버 수는 있지만 현재 컴퓨터의 하드 드라이브에 폴더를 선택 합니다. 업데이트할 수 있는 사용자 인터페이스를 사용 하 여 사이트를 미리 컴파일하 하고자 하기 때문에 "미리 컴파일된이 사이트를 업데이트할 수 허용" 확인란을 선택 하 고 확인을 클릭 합니다.

[![](precompiling-your-website-vb/_static/image2.png)](precompiling-your-website-vb/_static/image1.png)

**그림 1**: ASP.NET Compilation Tool 지정한 대상 위치에 웹 사이트를 미리 컴파일하는  
 ([전체 크기 이미지를 보려면 클릭](precompiling-your-website-vb/_static/image3.png))

> [!NOTE]
> 빌드 메뉴에서 웹 사이트 게시 옵션 Visual Web Developer에서 사용할 수 없는 경우 Visual Web Developer를 사용 하는 경우에 "미리 컴파일 명령줄에서" 섹션에서 설명 되는 ASP.NET 컴파일 도구의 명령줄 버전을 사용 해야 합니다.


웹 사이트를 미리 컴파일한 후 웹 사이트 게시 대화 상자에 입력 한 대상 위치로 이동 합니다. 웹 사이트의 내용으로이 폴더의 내용을 비교 보십시오. **그림 2** 책 검토 웹 사이트 폴더를 표시 합니다. 모두 포함 되어 참고 `.aspx` 및 `.aspx.cs` 파일입니다. 또한는 `Bin` 디렉터리에 파일을 하나만 포함 됩니다. `Elmah.dll`에 추가 하는 [이전 자습서](logging-error-details-with-elmah-vb.md)

[![](precompiling-your-website-vb/_static/image5.png)](precompiling-your-website-vb/_static/image4.png)

**그림 2**: 프로젝트 디렉터리에 `.aspx` 및 `.aspx.cs` ; 파일의 `Bin` 폴더에만 포함 되어`Elmah.dll`  
 ([전체 크기 이미지를 보려면 클릭](precompiling-your-website-vb/_static/image6.png))

**그림 3** 내용이 ASP.NET 컴파일 도구에서 생성 된 대상 위치 폴더를 표시 합니다. 이 폴더에는 코드 숨김 파일이 없습니다. 또한이 폴더의 `Bin` 디렉터리에 여러 어셈블리 및 두 개의 `.compiled` 외에 파일의 `Elmah.dll` 어셈블리입니다.

[![](precompiling-your-website-vb/_static/image8.png)](precompiling-your-website-vb/_static/image7.png)

**그림 3**: 배포에 대 한 포함 된 파일은 대상 위치 폴더  
 ([전체 크기 이미지를 보려면 클릭](precompiling-your-website-vb/_static/image9.png))

Wap의 명시적 컴파일을 달리 배포 프로세스에 대 한 미리 컴파일 전체 사이트에 대해 하나의 어셈블리를 만들지 않습니다. 대신, 해당 일괄 처리 함께 여러 페이지에 각 어셈블리. 또한 컴파일합니다는 `Global.asax` (있는 경우)의 모든 클래스 뿐 아니라 자체 어셈블리 파일의 `App_Code` 폴더입니다. ASP.NET에 대 한 선언적 태그를 포함 하는 파일 웹 페이지, 사용자 정의 컨트롤 및 마스터 페이지 (`.aspx`, `.ascx`, 및 `.master` 파일 각각)으로 복사 됩니다-대상 위치 디렉터리 하는 것입니다. 마찬가지로,는 `Web.config` 오버, 예: 이미지, CSS 및 PDF 파일의 모든 정적 파일 뿐만 아니라 파일은 복사 합니다. 에 대 한 보다 공식적인 설명은 어떻게 컴파일 처리 다양 한 파일 형식, 참조 [파일을 처리 하는 동안 ASP.NET 미리 컴파일](https://msdn.microsoft.com/library/e22s60h9.aspx)합니다.

> [!NOTE]
> 컴파일 도구 웹 사이트 게시 대화 상자에서 "고정 된 이름을 사용 하 고 페이지당 하나의 어셈블리만" 확인란을 선택 하 여 ASP.NET 페이지, 사용자 정의 컨트롤 또는 마스터 페이지 당 하나의 어셈블리를 만들를 지시할 수 있습니다. 각 ASP.NET 페이징하지 자체 어셈블리로 컴파일된 배포 보다 세부적으로 제어를 허용 합니다. 예를 들어 배포한 경우, 단일 ASP.NET 웹 페이지를 업데이트 하 고 해당 변경 내용을 배포 하는 데 필요한 필요만 해당 페이지의 `.aspx` 파일과 프로덕션 환경에 연결 된 어셈블리입니다. 참조 [방법: ASP.NET Compilation Tool와 고정 된 이름을 생성](https://msdn.microsoft.com/library/ms228040.aspx) 자세한 정보에 대 한 합니다.


대상 위치 디렉터리도 파일이 포함 된 미리 컴파일된 웹 프로젝트의 일부를 즉 였던 `PrecompiledApp.config`합니다. 이 파일에는 ASP.NET 응용 프로그램이 미리 컴파일 되었는지 런타임과 미리 여부는 업데이트할 수 있는 또는 정오를 업데이트할 수 있는 UI를 사용한 컴파일 되었는지 알립니다.

마지막으로, 잠시 중 하나를 열려면는 `.aspx` Visual Studio 또는 원하는 텍스트 편집기를 사용 하 여 대상 위치에 있는 파일입니다. 업데이트할 수 있는 사용자 인터페이스와 함께 배포를 위한 미리 컴파일 대상 위치 디렉터리의 ASP.NET 페이지 웹 사이트에서 해당 파일과 정확히 동일한 태그를 포함 합니다.

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>업데이트할 수 없는 사용자 인터페이스를 사용 하는 배포를 위한 미리 컴파일

업데이트할 수 없는 UI 사용 하는 배포에 대 한 사이트를 미리 컴파일하는 ASP.NET 컴파일러 도구를 사용할 수도 있습니다. 업데이트할 수 없는 UI 사용 하 여 사이트를 미리 컴파일하기 태그의 ASP.NET 페이지, 사용자 정의 컨트롤 및 대상 디렉터리의 마스터 페이지는 제거 되는 업데이트할 수 있는 UI 중요 한 차이점으로 미리 컴파일 하는 것과 마찬가지로 작동 합니다. 업데이트할 수 없는 UI 사용 하는 배포에 대 한 웹 사이트를 미리 컴파일할 빌드 메뉴에서 웹 사이트 게시 옵션을 선택 합니다. 하지만 "미리 컴파일된이 사이트를 업데이트할 수 허용" 옵션을 선택 취소 (참조 **그림 4**).

[![](precompiling-your-website-vb/_static/image11.png)](precompiling-your-website-vb/_static/image10.png)

**그림 4**: "미리 컴파일된이 사이트를 업데이트할 수 허용" 옵션을 미리 컴파일할와 정도 업데이트가 불가능 UI의 선택을 취소  
 ([전체 크기 이미지를 보려면 클릭](precompiling-your-website-vb/_static/image12.png))

**그림 5** 업데이트할 수 없는 사용자 인터페이스를 미리 컴파일한 후 대상 위치 폴더를 표시 합니다.

[![](precompiling-your-website-vb/_static/image14.png)](precompiling-your-website-vb/_static/image13.png)

**그림 5**: 업데이트할 수 없는 UI 사용 하는 배포에 대 한 대상 위치 폴더  
 ([전체 크기 이미지를 보려면 클릭](precompiling-your-website-vb/_static/image15.png))

비교 **그림 3** 를 **그림 5**합니다. 두 폴더는 동일 하 게 보일 수, 하는 동안에 업데이트할 수 없는 UI 폴더 마스터 페이지에는 유의 `Site.master`합니다. 반면 **그림 5** 는 되었습니다 선언적 태그 제거 되었으며 개체 틀 텍스트 아래 템플릿으로 바뀝니다 표시 됩니다이 파일의 내용을 보는 경우 다양 한 ASP.NET 페이지에 포함 됩니다: "이 마커 파일은에 의해 생성 된 미리 컴파일 도구를 삭제 해야 합니다! "

[![](precompiling-your-website-vb/_static/image17.png)](precompiling-your-website-vb/_static/image16.png)

**그림 5**: 선언적 태그 ASP.NET 페이지에서 제거 되었습니다

`Bin` 폴더에 **그림 3** 및 **5** 더 크게 다릅니다. 어셈블리, 외에 `Bin` 폴더에 **그림 5** 포함는 `.compiled` 각 ASP.NET 페이지, 사용자 정의 컨트롤 및 마스터 페이지에 대 한 파일입니다.

업데이트할 수 없는 UI 사용 하 여 사이트를 미리 컴파일하기를 원하지 않는 ASP.NET 페이지의 내용을 한 사용자나 회사를 설치 하거나 프로덕션 환경에서 웹 사이트를 관리 하 여 수정할 경우에 유용 합니다. 직접 편집 하 여 사이트의 모양과 느낌을 수정 하지 않습니다는 되도록 할 수 자신의 웹 서버에 설치 하는 고객에 게 판매 하는 ASP.NET 웹 응용 프로그램을 작성 하는 경우는 `.aspx` 페이지 배송 합니다. 자리 표시자 업데이트할 수 없는 UI 사용한 웹 사이트를 컴파일하여 배송 `.aspx` 고객 검사 하거나 콘텐츠를 수정할 것을 방지 하는 설치의 일부로 페이지입니다.

### <a name="precompiling-from-the-command-line"></a>명령줄에서 미리 컴파일

Visual Studio의 웹 사이트 게시 대화 상자를 내부적으로 ASP.NET 컴파일 도구 호출 (`aspnet_compiler.exe`) 웹 사이트를 미리 컴파일할 수 있습니다. 또는 명령줄에서이 도구를 호출할 수 있습니다. 사실, Visual Web Developer를 사용 하는 경우 다음 해야 합니다는 명령줄에서 컴파일러 도구를 실행: Visual Web Developer의 빌드 메뉴에 포함 된 웹 사이트 게시 옵션입니다.

명령줄에서 컴파일러 도구를 사용 하려면 명령줄에 삭제 하 고 있는 프레임 워크 디렉터리로 이동 하 여 시작 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727`합니다. 명령줄에 다음 문을 다음으로 입력 합니다.

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

위의 명령은 ASP.NET 컴파일러 도구를 시작 (`aspnet_compiler.exe`) 및 via는 `-p` 에서 시작 하는 웹 사이트를 미리 컴파일하 하도록 지시를 바꾸거나 *물리적\_경로\_를\_앱*; 이 값과 같이 설정 해야 합니다 `C:\MySites\BookReviews`, 인용 부호 구분 해야 합니다.

`-v` 스위치는 사이트의 가상 디렉터리를 지정 합니다. 사이트의 기본 웹 사이트는 IIS 메타 베이스로 등록 되어 있으면 생략할 수 있습니다는 `-p` 전환 하 고 방금 응용 프로그램의 가상 디렉터리를 지정 합니다. 사용 하는 경우는 `-p` 값 계속 스위치는 `-v` 스위치는 웹 사이트의 루트를 나타내며 응용 프로그램 루트 참조를 확인 하는 데 사용 됩니다. 예를 들어, 값을 지정 하는 경우 `-v /MySite` 응용 프로그램에 다음 참조 `~/path/file` 로 확인 될 `~/MySite/path/file`합니다. 교환기를 사용 하려면 책 검토 사이트는 웹 호스팅 회사 내에서 루트 디렉터리에 있으므로 `-v /`합니다.

`-f` 스위치, 있는 경우를 지정 하면 덮어쓸지 컴파일 도구는 *대상\_위치\_폴더* 이미 있는 경우에 디렉터리입니다. 생략 하면는 `-f` 스위치와 대상 위치 폴더가 이미 있습니다., 컴파일 도구 오류와 함께 종료 됩니다: "ASPRUNTIME 오류: 대상 디렉터리가 비어 있지 않습니다. 하십시오 수동으로 삭제 하거나 다른 대상을 선택 합니다. "

`-u` 스위치에 있는 경우 알립니다 업데이트할 수 있는 사용자 인터페이스를 만드는 도구입니다. 이 스위치를 업데이트할 수 없는 사용자 인터페이스를 사용 하 여 사이트를 미리 컴파일하를 생략 합니다.

마지막으로,는 *대상\_위치\_폴더* 대상 위치 디렉터리;에 실제 경로이 값이 다음과 같이 됩니다 `C:\MySites\Output\BookReviews`, 인용 부호 구분 해야 합니다.

## <a name="deploying-the-precompiled-website"></a>미리 컴파일된 웹 사이트를 배포합니다.

이 시점에서 업데이트 가능 하 고 업데이트할 수 없는 사용자 인터페이스 옵션에 모두 사용 하 여 웹 사이트를 미리 컴파일하 ASP.NET 컴파일 도구를 사용 하는 방법을 살펴보았습니다. 그러나 예제의 지금까지 미리 컴파일한 프로덕션 환경 아닌 로컬 폴더에 웹 사이트입니다. 다행 스럽게는 미리 컴파일된 웹 사이트 배포를 쉽게 수행할 수 있습니다 Visual Studio 또는 다른 파일 복사 메커니즘을 통해와 같은 독립 실행형 FTP 클라이언트에서입니다.

웹 사이트 게시 대화 상자 (에 처음 표시 된 **그림 1**)를 나타내는 미리 컴파일된 웹 사이트 파일을 복사할 대상 위치 옵션을 했습니다. 이 위치는 원격 웹 서버나 FTP 서버 수 있습니다. 이 텍스트 상자에 원격 서버를 입력 합니다. 미리 컴파일하고 및 한 번에 지정된 된 서버에 웹 사이트를 배포 합니다. 또는 로컬 폴더에 웹 사이트를 미리 컴파일하 수 있으며 그런 다음 FTP 또는 다른 방법을 통해 프로덕션 환경으로 해당 폴더의 내용을 수동으로 복사할 수 있습니다.

Visual Studio의 웹 사이트 게시 대화 상자를 통해 자동으로 배포 하는 미리 컴파일된 웹 사이트 도움이 됩니다 간단한 사이트에 대 한 경우 개발 및 프로덕션 환경 간에 구성 차이가 있습니다. 그러나 설명한 것 처럼는 [ *일반적인 구성 차이점 간의 개발 및 프로덕션* 자습서](common-configuration-differences-between-development-and-production-vb.md) 유지 하려면 이러한 차이점에 대 한도 드물지 않습니다. 예를 들어, 책 검토 웹 응용 프로그램 개발 환경에서 보다 프로덕션 환경에서 다른 데이터베이스를 사용합니다. Visual Studio에서 원격 서버에 웹 사이트를 게시할 때 맹목적으로 개발 환경에서 구성 파일 정보를 복사 합니다.

개발 및 프로덕션 환경 간의 차이점은 있지만 구성 사이트에 대 한 사이트의 로컬 디렉터리를 컴파일하고 프로덕션 관련 구성 파일을 복사 후에 미리 컴파일된 출력의 내용을 복사 하는 최선의 수 있습니다. 프로덕션 합니다.

프로덕션 환경으로 개발 환경에서 파일을 복사 하는 방법에 대 한 세부 정보에 대 한 참조는 [ *FTP 클라이언트를 사용 하 여 웹 사이트 배포* ](deploying-your-site-using-an-ftp-client-vb.md) 및 [  *배포 사용자 웹 사이트를 사용 하 여 Visual Studio 포함* ](determining-what-files-need-to-be-deployed-vb.md) 자습서입니다.

## <a name="summary"></a>요약

ASP.NET 컴파일 두 모드를 지원: 자동 및 명시적입니다. 이전 자습서에서 설명 했 듯이 웹 응용 프로그램 프로젝트 (Wap) 웹 사이트 프로젝트 (WSPs)는 기본적으로 자동 컴파일을 사용 하는 반면 명시적 컴파일을 사용 합니다. 그러나, 명시적으로 배포 하기 전에 WSP ASP.NET 컴파일 도구를 사용 하 여 컴파일할 수는 있습니다.

이 자습서 배포 지원에 대 한 미리 컴파일 도구에 집중 합니다. 배포를 위한 미리 컴파일 때 컴파일 도구 대상 위치 폴더, 지정 된 웹 응용 프로그램의 소스 코드를 컴파일하 만들고 복사 이러한 컴파일된 어셈블리 및 콘텐츠 파일을 대상 위치 폴더에 있습니다. 업데이트할 수 있는 또는 업데이트할 수 없는 사용자 인터페이스를 만들려면 컴파일 도구를 구성할 수 있습니다. 업데이트할 수 없는 사용자 인터페이스 옵션으로 미리 컴파일, 콘텐츠 파일에 있는 선언적 태그 제거 됩니다. 간단히 말해서 미리 컴파일 허용 원하는 경우 모든 소스 코드 파일을 포함 하지 않고 및 제거 하는 선언적 태그가 포함 된 웹 사이트 프로젝트 기반 응용 프로그램을 배포할 수 있습니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 웹 사이트를 미리 컴파일](https://msdn.microsoft.com/library/ms228015.aspx)
- [코드 숨김 및 ASP.NET 2.0에서 컴파일](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [ASP.NET에서 미리 컴파일](http://www.odetocode.com/Articles/417.aspx)
- [ASP.NET에서 미리 컴파일된 사이트가 옵션](http://www.dotnetperls.com/precompiled)

>[!div class="step-by-step"]
[이전](logging-error-details-with-elmah-vb.md)
[다음](users-and-roles-on-the-production-website-vb.md)
