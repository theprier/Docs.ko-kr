---
uid: whitepapers/side-by-side-with-10
title: .NET Framework 1.0 및 1.1의 ASP.NET-Side-by-side 실행 | Microsoft Docs
author: rick-anderson
description: 이 백서는 타이밍의 버전 중 하나에서 실행 되도록 ASP.NET 웹 응용 프로그램 수 있도록 컴퓨터에.NET 1.0와.NET 1.1을 설치 하는 방법에 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
ms.technology: ''
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: 1b8bcebd59a900e54c759509fd4fc5ad1f4f8576
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391162"
---
<a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>.NET Framework 1.0 및 1.1의 ASP.NET-Side-by-side 실행
====================
> 이 백서에는 ASP.NET 웹 응용 프로그램 프레임 워크의 버전 중 하나에서 실행할 수 있도록 컴퓨터에.NET 1.0와.NET 1.1을 설치 하는 방법을 설명 합니다.
> 
> ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.


ASP.NET에서 실행 되 고 함께 동일한 컴퓨터에 설치 되어 있지만 다른 버전의.NET Framework를 사용 하는 경우 응용 프로그램 이라고 합니다. 다음 항목에서는-병렬 실행에 대 한 ASP.NET 응용 프로그램을 구성 하는 방법에 설명 하 고 하는 자세한 단계를 제공 합니다.

- [.NET Framework 버전 1.0 설치 하는 동안 웹 응용 프로그램의 매핑을 유지 관리](#1)
- [특정 버전.NET Framework의 웹 응용 프로그램 맵](#2)
- [웹 사이트를 사용 하는.NET Framework의 버전을 확인](#3)

일반적으로 구성 요소 또는 응용 프로그램을 컴퓨터에 업데이트 되 면 이전 버전은 제거 되 고 최신 버전으로 대체 됩니다. 새 버전이 이전 버전과 호환 되지 않으면 일반적으로 응용 프로그램 구성 요소 또는 응용 프로그램 사용 중단 됩니다. .NET Framework 어셈블리 또는 동시에 동일한 컴퓨터에 설치할 응용 프로그램의 여러 버전을 허용 하는-병렬 실행에 대 한 지원을 제공 합니다. 여러 버전이 동시에 설치할 수 있으므로 관리 되는 응용 프로그램 다른 버전을 사용 하는 응용 프로그램에 영향을 주지 않고 사용할 버전을 선택할 수 있습니다.

기본적으로.NET Framework 버전 1.1 설치 하는 동안 기존 ASP.NET 응용 프로그램 모두 자동으로 재구성 됩니다.NET Framework의 최신 버전을 사용 하도록 합니다. ASP.NET 응용 프로그램을.NET Framework 1.1을 기본값으로 하지 않으려면 클릭 [여기](#1) 를 설치 하는 동안이 방지 하는 방법을 알아봅니다.

.NET Framework 1.1로 웹 서버를 업데이트 하 고 하나 이상의 웹 응용 프로그램에.NET Framework 1.0을 실행 하는 경우 인터넷 정보 서비스 (IIS) 스크립트 맵을 업데이트 해야 합니다. 스크립트 매핑은 특정 웹 응용 프로그램을.NET Framework의 버전에 대 한.aspx 파일 확장명을 매핑하려 메커니즘입니다. 클릭 [여기](#2) 에 특정 버전.NET Framework의 웹 응용 프로그램을 매핑하는 방법에 알아봅니다.

인터넷 정보 관리자 또는 ASP.NET IIS 등록 도구를 사용할 수 있습니다 (Aspnet\_regiis.exe) 특정 웹 응용 프로그램을 실행 중인.NET Framework 버전을 찾을 수 있습니다. 클릭 [여기](#3) 에 웹 사이트를 사용 하는.NET Framework의 버전을 확인 하는 방법을 알아봅니다.

각 버전의.NET Framework는 자체의 Machine.config 파일은.NET Framework 1.1로 마이그레이션하는 경우 하나의 가져오기 고려 합니다. 결과적으로, 웹 관리자가 변경할 경우 Machine.config 파일,.NET Framework 1.1 Machine.config 파일에 이러한 변경 내용은 마이그레이션해야 합니다.

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>.NET Framework 1.0을 설치 하는 동안 웹 응용 프로그램의 매핑을 유지 관리

기본적으로 모든 기존 ASP.NET 응용 프로그램 설치 중.NET Framework의 최신 버전을 사용 하기 위해 자동으로 재구성 됩니다. .NET Framework의 최신 버전을 사용 하 여 응용 프로그램 개선 사항과 새 버전에 포함 된 새로운 기능을 완전히 활용을 걸릴 수 있습니다. 동시에 응용 프로그램을 세부적으로 제어 하려는 웹 관리자는 업데이트, 자동 다시 매핑할 모든 기존 ASP.NET 응용 프로그램의.NET Framework를 설치 하는 동안 방지할 수 있습니다.

.NET Framework의 최신 버전으로 전체 ASP.NET 응용 프로그램의 자동 다시 매핑을 사용 하지 않으려면 웹 관리자 Dotnetfx.exe 설치 프로그램을 사용 하 여 /noaspupgrade 명령줄 옵션을 사용 수 있습니다.

**ASP.NET 응용 프로그램을 최신 버전의 전체 다시 매핑을 방지 하기 위해**

1. 로 이동 **시작**합니다.
2. 클릭할 **실행**합니다.
3. **cmd**를 입력합니다.
4. **확인**을 클릭합니다.  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. 명령 프롬프트에서.NET Framework의 설치를 시작 하려면 다음 줄을 입력 합니다. **Dotnetfx.exe /c: "/noaspupgrade 설치?** 합니다.  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. 클릭 **예** Microsoft.NET Framework 1.1 설치에서 합니다. 이.NET Framework 1.1의 설치 프로세스를 시작 됩니다.  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>특정 버전.NET Framework의 웹 응용 프로그램 맵

ASP.NET IIS Registration Tool의 버전을 포함 하는 각 버전의.NET Framework (Aspnet\_regiis.exe). 이 도구에는 관리자를 웹 응용 프로그램을.NET Framework의 특정 버전에서 실행 되도록 지정할 수 있습니다. 이 웹 응용 프로그램을.NET Framework의 버전 매핑 이라고 합니다. 관리자를 선택 하 여 Aspnet 해야\_regiis.exe 웹 응용 프로그램과 관련 된.NET Framework의 버전에 해당 합니다. 예를 들어, 웹 사이트를.NET Framework 1.1을 사용 하도록 지정 하려는 관리자 Aspnet를 사용 해야\_regiis.exe.NET Framework 1.1을 사용 하 여 제공 되는 합니다.

Aspnet\_regiis.exe 버전 1.0에 대 한 위치는:

- C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis

Aspnet\_regiis.exe 버전 1, 1에 대 한 위치는:

- C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis

Aspnet\_regiis.exe 스크립트 매핑 웹 응용 프로그램에 대 한 두 가지 옵션을 제공 합니다.

- **-s** 설정 스크립트 맵을 경로 및 해당 하위 디렉터리입니다.
- **-sn** 만 경로에 스크립트 맵을 설정 합니다.

W3SVC/루트 형식에 정의 되어 있는 웹 응용 프로그램 IIS 메타 데이터 경로 정의 하는 경로 / {WebSiteNumber} / {응용 프로그램\_이름}. 예를 들어 기본 웹 사이트 아래에 있는 포털 이라는 웹 응용 프로그램, 메타 베이스 경로 W3SVC/1/루트/포털입니다.

![](side-by-side-with-10/_static/image4.gif)

메타 베이스 경로를 가져오는 메타 베이스 편집기 라는 도구를 사용할 수도 있습니다 note 합니다. Microsoft 지원 사이트에서이 도구를 다운로드할 수 있습니다 [ https://support.microsoft.com/default.aspx?scid=kb; en-우리; 232068 합니다.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)

- Aspnet 실행\_맵과 해당 subapplication regiis.exe-s W3SVC/1/루트/포털 IIS 포털 업데이트를 스크립팅 합니다.  
  
    ![](side-by-side-with-10/_static/image5.gif)

- Aspnet 실행\_regiis.exe-sn W3SVC/1/루트/포털 포털 IIS 스크립트를 업데이트 하에 매핑하는 포털에서 응용 프로그램에 영향을 주지 않고? s 하위 디렉터리입니다.  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>웹 응용 프로그램을 사용 하는.NET Framework 버전 확인

관리자로는 인터넷 서비스 관리자를 사용 하 여 웹 사이트를 실행 하는.NET Framework의 버전을 찾을 수 있습니다. 다른 운영 체제 버전 다르게 인터넷 서비스 관리자를 시작합니다. 서비스 관리자를 시작 하려면 아래에 나열 된 단계를 수행 합니다.

**인터넷 서비스 관리자를 시작 하려면**

1. 로 이동 **시작**합니다.
2. 클릭할 **실행**합니다.
3. 형식 **inetmgr**합니다.  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. 인터넷 서비스 관리자에서 웹 응용 프로그램 확인 하려는.NET Framework의 버전을 선택 합니다.  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성입니다.**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. 속성 창에서 선택 **구성 합니다.**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. 응용 프로그램 매핑 테이블에서 선택 **.aspx**, 클릭 **편집**합니다.  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. **실행 파일** 텍스트 상자를 스크롤하여 버전 디렉터리를 살펴봅니다. 버전 디렉터리 v.1.1.4322 인 경우 응용 프로그램이.NET Framework 1.1에 매핑됩니다. 반대로, 버전 디렉터리 v1.0.3705 인 경우 응용 프로그램이.NET Framework 1.0에 매핑됩니다.  
  
    ![](side-by-side-with-10/_static/image12.gif)
