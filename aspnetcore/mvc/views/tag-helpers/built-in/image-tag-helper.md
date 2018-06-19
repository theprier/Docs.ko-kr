---
title: ASP.NET Core의 이미지 태그 도우미
author: pkellner
description: 이미지 태그 도우미 사용 방법 소개
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: 6aa9175f873c4ea62e0319c812e5312cd3331141
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30072264"
---
# <a name="image-tag-helper-in-aspnet-core"></a>ASP.NET Core의 이미지 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 

이미지 태그 도우미는 `img`(`<img>`) 태그 기능을 향상시킵니다. `boolean` 특성 `asp-append-version`뿐만 아니라 `src` 태그도 필요합니다.

이미지 원본(`src`)이 호스트 웹 서버에 있는 고정 파일인 경우 문자열을 버스팅하는 고유한 캐시는 이미지 원본에 쿼리 매개 변수로 추가됩니다. 이렇게 하면 호스트 웹 서버에 있는 파일이 변경되는 경우 업데이트된 요청 매개 변수를 포함하는 고유한 요청 URL이 생성됩니다. 문자열을 버스팅하는 캐시는 고정 이미지 파일의 해시를 나타내는 고유 값입니다.

이미지 원본(`src`)이 고정 파일이 아닌 경우(예: 원격 URL 또는 파일이 서버에 존재하지 않음) 쿼리 문자열 매개 변수를 버스팅하는 캐시를 포함하지 않는 `<img>` 태그의 `src` 특성이 생성됩니다.

## <a name="image-tag-helper-attributes"></a>이미지 태그 도우미 특성


### <a name="asp-append-version"></a>asp-append-version

`src` 특성과 함께 지정된 경우 이미지 태그 도우미가 호출됩니다.

유효한 `img` 태그 도우미의 예는 다음과 같습니다.

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

고정 파일이 *..wwwroot/images/asplogo.png* 디렉터리에 있는 경우 생성된 html은 다음과 비슷합니다(해시는 다름).

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

매개 변수 `v`에 할당된 값은 디스크에 있는 파일의 해시 값입니다. 웹 서버가 참조된 고정 파일에 대한 읽기 액세스 권한을 얻을 수 없는 경우 `v` 매개 변수가 `src` 특성에 추가되지 않습니다.

- - -

### <a name="src"></a>src

이미지 태그 도우미를 활성화하려면 `<img>` 요소에 src 특성이 필요합니다. 

> [!NOTE]
> 이미지 태그 도우미는 로컬 웹 서버에서 `Cache` 공급자를 사용하여 지정된 파일의 계산된 `Sha512`를 저장합니다. 파일을 다시 요청하는 경우 `Sha512`를 다시 계산하지 않아도 됩니다. 파일의 `Sha512`를 계산하는 경우 파일에 연결된 파일 감시자에서 캐시를 무효화합니다.

## <a name="additional-resources"></a>추가 자료

* <xref:performance/caching/memory>
