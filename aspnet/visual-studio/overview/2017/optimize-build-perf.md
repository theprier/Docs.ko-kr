---
uid: visual-studio/overview/2017/optimize-build-perf
title: 솔루션에 대 한 빌드 성능 최적화
author: tfitzmac
description: 솔루션에 대 한 빌드 성능 최적화
ms.author: riande
ms.date: 08/22/2018
msc.type: authoredcontent
ms.openlocfilehash: 19f190835e7477e69db470b74edac9e211fd9158
ms.sourcegitcommit: 5a2456cbf429069dc48aaa2823cde14100e4c438
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2018
ms.locfileid: "41909888"
---
# <a name="optimize-build-performance-for-solution"></a>솔루션에 대 한 빌드 성능 최적화
Visual Studio 2017 15.8 나중에 아래에 새 메뉴 항목을 추가 하 고 **빌드 > ASP.NET 컴파일 > 솔루션에 대 한 빌드 성능 최적화**합니다.

![새 메뉴 항목의 스크린샷](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET에서는 ASP.NET 프로젝트에는 저마다 컴파일러의 복사본 즉 런타임에 해당 뷰를 컴파일합니다. 그러나 개발자 컴퓨터에서 경우 컴파일러의 복사본에는 Visual Studio의 복사본과 일치 하지 않습니다 빌드 성능이 저하 됩니다 증분 빌드 1 ~ 3 초 순서입니다. 이 기능은 Visual Studio의 증분 빌드 속도 일치 하는 컴파일러의 프로젝트의 복사본을 업데이트 됩니다.

이 ASP.NET 프레임 워크 프로젝트에만 적용 됩니다, 그리고 ASP.NET Core에 적용 되지 않습니다.
