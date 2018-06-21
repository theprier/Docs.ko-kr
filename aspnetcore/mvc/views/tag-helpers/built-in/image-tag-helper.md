---
title: ASP.NET Core의 이미지 태그 도우미
author: pkellner
description: 이미지 태그 도우미의 사용 방법을 알아봅니다.
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
# <a name="image-tag-helper-in-aspnet-core"></a><span data-ttu-id="cce3c-103">ASP.NET Core의 이미지 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="cce3c-103">Image Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="cce3c-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="cce3c-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="cce3c-105">이미지 태그 도우미는 `img`(`<img>`) 태그의 기능을 향상시기며.</span><span class="sxs-lookup"><span data-stu-id="cce3c-105">The Image Tag Helper enhances the `img` (`<img>`) tag.</span></span> <span data-ttu-id="cce3c-106">`boolean` 특성인 `asp-append-version`뿐 아니라 `src` 태그가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-106">It requires a `src` tag as well as the `boolean` attribute `asp-append-version`.</span></span>

<span data-ttu-id="cce3c-107">이미지 원본(`src`)이 호스트 웹 서버에 존재하는 정적 파일인 경우 이미지 원본에 대한 고유한 캐시 버스팅 문자열이 쿼리 매개 변수로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-107">If the image source (`src`) is a static file on the host web server, a unique cache busting string is appended as a query parameter to the image source.</span></span> <span data-ttu-id="cce3c-108">그러면 호스트 웹 서버에 위치한 파일이 변경될 경우 갱신된 요청 매개 변수를 포함하는 고유한 요청 URL이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-108">This ensures that if the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span> <span data-ttu-id="cce3c-109">캐시 버스팅 문자열은 정적 이미지 파일의 해시를 나타내는 고유한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-109">The cache busting string is a unique value representing the hash of the static image file.</span></span>

<span data-ttu-id="cce3c-110">이미지 원본(`src`)이 정적 파일이 아닌 경우(예: 원격 URL 또는 파일이 서버에 존재하지 않을 경우), 캐시 버스팅 쿼리 문자열 매개 변수가 포함되지 않은 `<img>` 태그의 `src` 특성이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-110">If the image source (`src`) isn't a static file (for example a remote URL or the file doesn't exist on the server), the `<img>` tag's `src` attribute is generated with no cache busting query string parameter.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="cce3c-111">이미지 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="cce3c-111">Image Tag Helper Attributes</span></span>


### <a name="asp-append-version"></a><span data-ttu-id="cce3c-112">asp-append-version</span><span class="sxs-lookup"><span data-stu-id="cce3c-112">asp-append-version</span></span>

<span data-ttu-id="cce3c-113">`src` 특성과 함께 지정되면 이미지 태그 도우미가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-113">When specified along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="cce3c-114">유효한 `img` 태그 도우미의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-114">An example of a valid `img` tag helper is:</span></span>

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

<span data-ttu-id="cce3c-115">정적 파일이 *..wwwroot/images/asplogo.png* 디렉터리에 있을 경우, 생성되는 HTML은 다음과 비슷합니다(해시는 다름).</span><span class="sxs-lookup"><span data-stu-id="cce3c-115">If the static file exists in the directory *..wwwroot/images/asplogo.png* the generated html is similar to the following (the hash will be different):</span></span>

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

<span data-ttu-id="cce3c-116">매개 변수 `v`에 할당된 값은 디스크에 존재하는 파일의 해시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-116">The value assigned to the parameter `v` is the hash value of the file on disk.</span></span> <span data-ttu-id="cce3c-117">웹 서버가 참조된 정적 파일에 대한 읽기 접근 권한을 얻을 수 없으면 `src` 특성에 `v` 매개 변수가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-117">If the web server is unable to obtain read access to the static file referenced,  no `v` parameters is added to the `src` attribute.</span></span>

- - -

### <a name="src"></a><span data-ttu-id="cce3c-118">src</span><span class="sxs-lookup"><span data-stu-id="cce3c-118">src</span></span>

<span data-ttu-id="cce3c-119">이미지 태그 도우미를 활성화하려면 `<img>` 요소에 src 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-119">To activate the Image Tag Helper, the src attribute is required on the `<img>` element.</span></span> 

> [!NOTE]
> <span data-ttu-id="cce3c-120">이미지 태그 도우미는 로컬 웹 서버에서 `Cache` 공급자를 사용해서 해당 파일의 계산된 `Sha512`를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-120">The Image Tag Helper uses the `Cache` provider on the local web server to store the calculated `Sha512` of a given file.</span></span> <span data-ttu-id="cce3c-121">파일을 다시 요청하는 경우 `Sha512`를 다시 계산하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-121">If the file is requested again the `Sha512` doesn't need to be recalculated.</span></span> <span data-ttu-id="cce3c-122">캐시는 파일의 `Sha512`가 계산될 때 파일에 첨부된 파일 감시자에 의해 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce3c-122">The Cache is invalidated by a file watcher that's attached to the file when the file's `Sha512` is calculated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cce3c-123">추가 자료</span><span class="sxs-lookup"><span data-stu-id="cce3c-123">Additional resources</span></span>

* <xref:performance/caching/memory>
