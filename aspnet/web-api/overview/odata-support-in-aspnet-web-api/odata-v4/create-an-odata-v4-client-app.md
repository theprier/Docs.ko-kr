---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: "OData v4 클라이언트 앱 (C#) 만들기 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: daa39fbbb4ff17d61f71bf2a642a9c2260b353e4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-an-odata-v4-client-app-c"></a>OData v4 클라이언트 앱 (C#) 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이전 자습서에서 CRUD 작업을 지 원하는 기본 OData 서비스를 만들었습니다. 이제 서비스에 대 한 클라이언트를 만들어 보겠습니다.

Visual Studio의 새 인스턴스를 시작 하 고 새 콘솔 응용 프로그램 프로젝트를 만듭니다. 에 **새 프로젝트** 대화 상자에서 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **Windows 바탕 화면**, 선택는 **콘솔 응용 프로그램** 템플릿. 프로젝트 이름을 &quot;ProductsApp&quot;합니다.

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> OData 서비스가 포함 된 Visual Studio 솔루션에 콘솔 응용 프로그램을 추가할 수도 있습니다.


## <a name="install-the-odata-client-code-generator"></a>OData 클라이언트 코드 생성기를 설치 합니다.

**도구** 메뉴 선택 **확장명 및 업데이트**합니다. 선택 **온라인** &gt; **Visual Studio 갤러리**합니다. 검색 상자에 검색 &quot;OData 클라이언트 코드 생성기&quot;합니다. 클릭 **다운로드** VSIX를 설치 합니다. Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>OData 서비스를 로컬로 실행

Visual Studio에서 ProductService 프로젝트를 실행 합니다. 기본적으로 Visual Studio 응용 프로그램 루트에 대 한 브라우저를 시작 합니다. 참고 URI입니다. 다음 단계에서이 필요 합니다. 응용 프로그램을 실행 상태로 둡니다.

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> 동일한 솔루션의 두 프로젝트를 설정 하는 경우에 디버깅 하지 않고 ProductService 프로젝트를 실행 해야 합니다. 다음 단계에서 콘솔 응용 프로그램 프로젝트를 수정 하는 동안 실행 되는 서비스를 유지 해야 합니다.


## <a name="generate-the-service-proxy"></a>서비스 프록시를 생성 합니다.

서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는.NET 클래스입니다. 프록시는 HTTP 요청에 대 한 메서드 호출으로 변환합니다. 실행 하 여 프록시 클래스를 만듭니다는 [T4 템플릿](https://msdn.microsoft.com/en-us/library/bb126445.aspx)합니다.

프로젝트를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가** &gt; **새 항목**합니다.

![](create-an-odata-v4-client-app/_static/image5.png)

에 **새 항목 추가** 대화 상자에서 **Visual C# 항목** &gt; **코드** &gt; **OData 클라이언트**합니다. 템플릿에 이름을 &quot;ProductClient.tt&quot;합니다. 클릭 **추가** 보안 경고를 클릭 합니다.

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

이 시점에서 무시할 수 있는 오류를 얻게 됩니다. Visual Studio는 자동으로 서식 파일을 실행 하지만 서식 파일에 일부 구성 설정이 필요한 첫 번째입니다.

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

ProductClient.odata.config 파일을 엽니다. 에 `Parameter` 요소인 ProductService 프로젝트 (이전 단계)에서 URI에 붙여 넣습니다. 예:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

서식 파일을 다시 실행 합니다. 솔루션 탐색기에서 ProductClient.tt 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 지정 도구 실행**합니다.

템플릿은 라는 ProductClient.cs 프록시를 정의 하는 코드 파일을 만듭니다. OData 끝점을 변경 하면 응용 프로그램을 개발 하는 경우 프록시 업데이트 서식 파일을 실행 합니다.

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>OData 서비스를 호출 하 여 서비스 프록시를 사용 하 여

Program.cs 파일을 열고 상용구 코드를 다음과 같이 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

값을 바꿉니다 *serviceUri* 앞에서 서비스 URI와 합니다.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

응용 프로그램을 실행 하면 다음 출력 해야 합니다.

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
