---
title: "이미지 태그 도우미 | Microsoft Docs"
author: pkellner
description: "이미지 태그 도우미를 사용 하는 방법을 보여 줍니다."
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: d0857e1926c341b2357bc824fa379c4fc30affbc
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="imagetaghelper"></a><span data-ttu-id="878eb-103">ImageTagHelper</span><span class="sxs-lookup"><span data-stu-id="878eb-103">ImageTagHelper</span></span>

<span data-ttu-id="878eb-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="878eb-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="878eb-105">향상 된 이미지 태그 도우미의 `img` (`<img>`) 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-105">The Image Tag Helper enhances the `img` (`<img>`) tag.</span></span> <span data-ttu-id="878eb-106">필요한는 `src` 태그도 `boolean` 특성 `asp-append-version`합니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-106">It requires a `src` tag as well as the `boolean` attribute `asp-append-version`.</span></span>

<span data-ttu-id="878eb-107">경우 이미지 원본은 (`src`) 정적 파일은 호스트 웹 서버에서 문자열 busting 고유한 캐시 이미지 원본에 쿼리 매개 변수로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-107">If the image source (`src`) is a static file on the host web server, a unique cache busting string is appended as a query parameter to the image source.</span></span> <span data-ttu-id="878eb-108">이렇게 하면 있는지 호스트 웹 서버의 파일이 변경 되 면 고유한 요청 URL이 생성 업데이트 요청 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-108">This ensures that if the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span> <span data-ttu-id="878eb-109">Busting 문자열 캐시는 정적 이미지 파일의 해시를 나타내는 고유 값입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-109">The cache busting string is a unique value representing the hash of the static image file.</span></span>

<span data-ttu-id="878eb-110">경우 이미지 원본은 (`src`) 정적 파일 (예를 들어 원격 URL 또는 파일에 존재 하지 서버) 되지 않습니다는 `<img>` 태그의 `src` 쿼리 문자열 매개 변수를 busting 캐시가 없는 특성이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-110">If the image source (`src`) isn't a static file (for example a remote URL or the file doesn't exist on the server), the `<img>` tag's `src` attribute is generated with no cache busting query string parameter.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="878eb-111">이미지 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="878eb-111">Image Tag Helper Attributes</span></span>


### <a name="asp-append-version"></a><span data-ttu-id="878eb-112">asp 추가 버전</span><span class="sxs-lookup"><span data-stu-id="878eb-112">asp-append-version</span></span>

<span data-ttu-id="878eb-113">와 함께 지정 된 경우는 `src` 이미지 태그 도우미 특성 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-113">When specified along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="878eb-114">유효한의 예로 `img` 태그 도우미는:</span><span class="sxs-lookup"><span data-stu-id="878eb-114">An example of a valid `img` tag helper is:</span></span>

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

<span data-ttu-id="878eb-115">정적 파일이 디렉터리에 있는 경우 *... wwwroot/images/asplogo.png* (해시 다를 수는) 다음 생성 된 html 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-115">If the static file exists in the directory *..wwwroot/images/asplogo.png* the generated html is similar to the following (the hash will be different):</span></span>

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

<span data-ttu-id="878eb-116">매개 변수에 할당 된 값 `v` 디스크에 있는 파일의 해시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-116">The value assigned to the parameter `v` is the hash value of the file on disk.</span></span> <span data-ttu-id="878eb-117">웹 서버에 대 한 읽기 액세스를 얻을 수 없는 경우 정적 참조 하는 파일이, 아니요 `v` 에 매개 변수 추가 되는 `src` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-117">If the web server is unable to obtain read access to the static file referenced,  no `v` parameters is added to the `src` attribute.</span></span>

- - -

### <a name="src"></a><span data-ttu-id="878eb-118">src</span><span class="sxs-lookup"><span data-stu-id="878eb-118">src</span></span>

<span data-ttu-id="878eb-119">이미지 태그 도우미를 활성화 하려면 src 특성에 필요는 `<img>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-119">To activate the Image Tag Helper, the src attribute is required on the `<img>` element.</span></span> 

> [!NOTE]
> <span data-ttu-id="878eb-120">이미지 태그 도우미를 사용 하 여는 `Cache` 저장할 계산 된 로컬 웹 서버에 공급자 `Sha512` 제공 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-120">The Image Tag Helper uses the `Cache` provider on the local web server to store the calculated `Sha512` of a given file.</span></span> <span data-ttu-id="878eb-121">파일을 다시 요청 하는 경우는 `Sha512` 계산 해야 하는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-121">If the file is requested again the `Sha512` doesn't need to be recalculated.</span></span> <span data-ttu-id="878eb-122">파일에 연결 된 파일 감시자에서 캐시를 무효화 하는 경우 파일의 `Sha512` 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="878eb-122">The Cache is invalidated by a file watcher that's attached to the file when the file's `Sha512` is calculated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="878eb-123">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="878eb-123">Additional resources</span></span>

* <xref:performance/caching/memory>
