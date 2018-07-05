---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: (Razor) 사이트 성능 향상을 위해 페이지는 ASP.NET 웹에서 데이터 캐싱 | Microsoft Docs
author: tfitzmac
description: 속도가 빨라질 수 있습니다 웹 사이트-즉, 저장 하 여 캐시에서 검색 하거나 처리 하려면 상당한 시간이 걸리는 일반적으로 데이터의 결과 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2014
ms.topic: article
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 4134c80d7eed4752c90a06aab796a0fd8c2a9782
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383411"
---
<a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>성능 향상을 위해 ASP.NET 웹 페이지 (Razor) 사이트에서 데이터 캐싱
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 성능 향상에 대 한 정보를 캐시 하는 도우미를 사용 하는 방법을 설명 합니다. 저장 하 여 웹 사이트 속도 높일 수 있습니다 &#8212; 즉, 캐시 &#8212; 는 일반적으로 상당한 시간이 걸립니다 받거나 처리 하 고 자주 변경 되지 않는 데이터의 결과입니다.
> 
> **학습할 내용:** 
> 
> - 웹 사이트의 응답성을 개선 하기 위해 캐싱을 사용 하는 방법입니다.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `WebCache` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


사이트에서 페이지를 요청이 있을 때마다 웹 서버 요청을 처리 하기 위해 일부 작업을 수행 해야 합니다. 페이지의 일부 서버 (비교적) 시간이 오래 걸릴, 데이터베이스에서 데이터를 검색 하는 작업을 수행 해야 할 수도 있습니다. 이러한 작업은 사이트 많은 트래픽이 발생 하는 경우 절대 용어로 장기 사용 하지, 경우에 복잡 하거나 느린 작업을 수행 하려면 웹 서버는 개별 요청에 대 한 전체 계열을 많은 작업을 추가할 수 있습니다. 이 사이트의 성능을 궁극적으로 영향을 수 있습니다.

다음과 같은 상황에서 웹 사이트의 성능을 향상 시키는 한 가지 방법은 데이터를 캐시 하는 경우 사이트 가져옵니다 반복된은 같은 정보를 요청 하 고 정보를 각 사용자에 대 한 수정할 필요가 없습니다 시간이 없는 다시 인출 하거나, 다시 계산 하는 대신 중요 한 데이터를 한 번 인출할를 다음 결과 저장 합니다. 다음에는 요청이 들어오면 내용은 수만 가져올 캐시에서.

일반적으로 자주 변경 되지 않는 정보를 캐시 합니다. 캐시에 정보를 배치 하면 웹 서버의 메모리에 저장 됩니다. 기간 캐시 않아야, 일 시간 (초)에서 지정할 수 있습니다. 캐싱 기간 만료 되 면 캐시에서 정보를 자동으로 제거 됩니다.

> [!NOTE]
> 캐시의 항목이 제거 될 수 있습니다 이유로 이외의 만료 되었습니다. 예를 들어, 웹 서버를 일시적으로 발생할 낮은 메모리가 이며 메모리를 회수할 수는 한 가지 방법은 캐시에서 항목을 throw 하 여 합니다. 알 수 있듯이, 캐시에 정보를 배치한 경우에, 이것은 필요할 때 되도록 확인 해야 합니다.


웹 사이트에 현재 온도 및 일기 예보를 표시 하는 페이지가 한다고 가정 합니다. 이러한 종류의 정보를 가져오려면 외부 서비스에 요청을 보낼 수 있습니다. 있으므로이 정보 (예를 들어 두 시간 기간) 내 대부분 변경 되지 않습니다 및 외부 호출 시간 및 대역폭이 필요 하므로 캐싱에 적합 한지 합니다.

## <a name="adding-caching-to-a-page"></a>페이지에 캐싱 추가

ASP.NET에 포함 되어는 `WebCache` 쉽게 사이트에 캐싱을 추가 하 고 캐시에 데이터를 추가 하는 도우미입니다. 이 절차에서는 현재 시간을 캐시 하는 페이지를 만들어야 합니다. 현재는 종종 변하지와 또한 이것이 계산 하기 복잡 하므로 실제 예에서 아닙니다. 그러나 실행 중인 캐싱을 설명 하기 좋은 방법입니다.

1. 명명 된 새 페이지 추가 *WebCache.cshtml* 웹 사이트에 있습니다.
2. 페이지에 다음 코드와 태그를 추가 합니다.

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    데이터를 캐시 하는 경우에 넣기는 이름을 사용 하 여 캐시가는 웹 사이트에서 고유 합니다. 이 경우 명명 된 캐시 엔트리를 사용할지 `CachedTime`합니다. 이 `cacheItemKey` 코드 예제에 표시 합니다.

    코드를 먼저 읽습니다.는 `CachedTime` 항목을 캐시 합니다. (즉, 캐시 항목에 없는 경우 null) 값을 반환 되 면 코드 캐시 데이터를 시간 변수 값만 설정 합니다.

    그러나 캐시 항목이 존재 하지 않는 경우 (즉, 인 null) 코드 시간 값을 설정, 캐시에 추가 하 고 만료 값을 1 분으로 설정 합니다. 1 분 후 캐시 항목 삭제 됩니다. (캐시에서 항목에 대 한 만료 기본값은 20 분입니다.) 이 명령은 `WebCache.Set(cacheItemKey, time, 1, false)` 캐시에 현재 시간 값을 추가 하 고 만료 되기 1 분으로 설정 하는 방법을 보여 줍니다. 설정 된 *slidingExpiration* 매개 변수를 `false` 만료 시간을 요청할 때마다 갱신 하지 않으면 의미 합니다. 원래 캐시에 추가 된 후 정확 하 게 1 분 후 만료 됩니다. 이 값을 설정 하는 경우 `true` 1 분의 만료 시간에는 캐시에서 값을 요청할 때마다 다시 설정 됩니다.

    이 코드에서는 데이터를 캐시 하는 경우 항상 사용 해야 하는 패턴을 보여 줍니다. 캐시에서 항목을 가져오기 전에 항상 먼저 확인 여부는 `WebCache.Get` 메서드가 null을 반환 합니다. 캐시 항목 만료 또는 제거 되었거나 다른 이유로, 지정 된 항목은 캐시 된다는 보장이 없으므로 하므로 기억 합니다.
3. 실행할 *WebCache.cshtml* 브라우저에서 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 처음 페이지를 요청할 때는 데이터를 캐시에 없는 및 코드는 시간 값을 캐시에 추가 합니다.

    ![캐시-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. 새로 고침 *WebCache.cshtml* 브라우저에서 합니다. 이 시간은 데이터를 캐시 되어 있습니다. 에 마지막 페이지를 볼 이후 변경 되지 않은 확인 합니다.

    ![캐시-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. 캐시를 비울 수에 대 일 분 정도 기다린 다음 페이지를 새로 고칩니다. 페이지에는 다시 캐시에 데이터를 찾을 수 없습니다 하 고 업데이트 된 시간이 캐시에 추가 됩니다 나타냅니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


- [차트에 데이터 표시](https://go.microsoft.com/fwlink/?LinkId=202895)
- [WebCache API 참조](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)
