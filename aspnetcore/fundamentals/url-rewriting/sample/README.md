# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="a1970-101">ASP.NET Core URL 다시 작성 샘플(ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="a1970-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="a1970-102">이 샘플은 ASP.NET Core 2.x URL 다시 작성 미들웨어의 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="a1970-103">응용 프로그램은 URL 리디렉션 및 URL 다시 작성 옵션을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-103">The application demonstrates URL redirect and URL rewriting options.</span></span> <span data-ttu-id="a1970-104">ASP.NET Core 1.x 샘플의 경우, [ASP.NET Core URL 다시 작성 샘플(ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/1.x)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-104">For the ASP.NET Core 1.x sample, see [ASP.NET Core URL Rewriting Sample (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/1.x).</span></span>

<span data-ttu-id="a1970-105">샘플을 실행하면 규칙 중 하나가 요청 URL에 적용될 때 다시 작성되거나 리디렉션된 URL을 보여주는 응답이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-105">When running the sample, a response will be served that shows the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="a1970-106">이 샘플의 예</span><span class="sxs-lookup"><span data-stu-id="a1970-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="a1970-107">성공 상태 코드: 302(Found)</span><span class="sxs-lookup"><span data-stu-id="a1970-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="a1970-108">예(리디렉션): **/redirect-rule/{capture_group}** 을 **/redirected/{capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="a1970-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="a1970-109">성공 상태 코드: 200(OK)</span><span class="sxs-lookup"><span data-stu-id="a1970-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="a1970-110">예(다시 작성): **/rewrite-rule/{capture_group_1}/{capture_group_2}** 를 **/rewrtten?var1={capture_group_1}&var2={capture_group_2}** 로</span><span class="sxs-lookup"><span data-stu-id="a1970-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="a1970-111">성공 상태 코드: 302(Found)</span><span class="sxs-lookup"><span data-stu-id="a1970-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="a1970-112">예(리디렉션): **/apache-mod-rules-redirect/{capture_group}** 을 **/redirected?id={capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="a1970-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="a1970-113">성공 상태 코드: 200(OK)</span><span class="sxs-lookup"><span data-stu-id="a1970-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="a1970-114">예(다시 작성): **/iis-rules-rewrite/{capture_group}** 을 **/rewritten?id={capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="a1970-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXMLRequests)`
  - <span data-ttu-id="a1970-115">성공 상태 코드: 301(영구적 이동)</span><span class="sxs-lookup"><span data-stu-id="a1970-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="a1970-116">예(리디렉션): **/file.xml**을 **/xmlfiles/file.xml**로</span><span class="sxs-lookup"><span data-stu-id="a1970-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(new RedirectPNGRequests(".png", "/png-images")))`<br>`Add(new RedirectPNGRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="a1970-117">성공 상태 코드: 301(영구적 이동)</span><span class="sxs-lookup"><span data-stu-id="a1970-117">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="a1970-118">예(리디렉션): **/image.png**를 **/png-images/image.png**로</span><span class="sxs-lookup"><span data-stu-id="a1970-118">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="a1970-119">예(리디렉션): **/image.jpg**를 **/jpg-images/image.jpg**로</span><span class="sxs-lookup"><span data-stu-id="a1970-119">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="using-a-physicalfileprovider"></a><span data-ttu-id="a1970-120">`PhysicalFileProvider` 사용</span><span class="sxs-lookup"><span data-stu-id="a1970-120">Using a `PhysicalFileProvider`</span></span>
<span data-ttu-id="a1970-121">또한 `PhysicalFileProvider`를 만들어 `IFileProvider`를 얻은 후 `AddApacheModRewrite()` 및 `AddIISUrlRewrite()` 메서드로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-121">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>
```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```
## <a name="secure-redirection-extensions"></a><span data-ttu-id="a1970-122">보안 리디렉션 확장</span><span class="sxs-lookup"><span data-stu-id="a1970-122">Secure redirection extensions</span></span>
<span data-ttu-id="a1970-123">이 샘플에는 URL(**https://localhost:5001**, **https://localhost**)을 사용하는 데 필요한 앱에 대한 `WebHostBuilder` 구성 및 이러한 리디렉션 메서드를 살펴보는 데 도움이 되는 테스트 인증서(**testCert.pfx**)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-123">This sample includes `WebHostBuilder` configuration for the app to use URLs (**https://localhost:5001**, **https://localhost**) and a test certificate (**testCert.pfx**) to assist you in exploring these redirect methods.</span></span> <span data-ttu-id="a1970-124">**Startup.cs**의 `RewriteOptions()`에 이 중 하나를 추가하여 동작을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1970-124">Add any of them to the `RewriteOptions()` in **Startup.cs** to study their behavior.</span></span>


|              <span data-ttu-id="a1970-125">메서드</span><span class="sxs-lookup"><span data-stu-id="a1970-125">Method</span></span>              | <span data-ttu-id="a1970-126">상태 코드</span><span class="sxs-lookup"><span data-stu-id="a1970-126">Status Code</span></span> |    <span data-ttu-id="a1970-127">포트</span><span class="sxs-lookup"><span data-stu-id="a1970-127">Port</span></span>    |
|----------------------------------|:-----------:|:----------:|
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="a1970-128">301</span><span class="sxs-lookup"><span data-stu-id="a1970-128">301</span></span>     | <span data-ttu-id="a1970-129">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="a1970-129">null (465)</span></span> |
|     `.AddRedirectToHttps()`      |     <span data-ttu-id="a1970-130">302</span><span class="sxs-lookup"><span data-stu-id="a1970-130">302</span></span>     | <span data-ttu-id="a1970-131">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="a1970-131">null (465)</span></span> |
|    `.AddRedirectToHttps(301)`    |     <span data-ttu-id="a1970-132">301</span><span class="sxs-lookup"><span data-stu-id="a1970-132">301</span></span>     | <span data-ttu-id="a1970-133">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="a1970-133">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="a1970-134">301</span><span class="sxs-lookup"><span data-stu-id="a1970-134">301</span></span>     |    <span data-ttu-id="a1970-135">5001</span><span class="sxs-lookup"><span data-stu-id="a1970-135">5001</span></span>    |

